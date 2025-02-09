**Link:** https://www.kaggle.com/c/bengaliai-speech/overview

**Problem Type:** [[transcription]]

**Input:** mp3 files

**Output:** the transcribed Bengali text

**Eval Metric:** [[Word Error Rate]]
## Summary

Bengali dialects (especially those spoken by Muslim religious sermons) aren't transcribed well.
- There are no robust open-source speech recognition models for Bengali
- (the Google Speech API for Bengali has a Word Error Rate of 74% for Bengali religious sermons).
## Important notebooks/discussions
- explaining the competition
	- https://www.kaggle.com/code/sujaykapadnis/bengali-speech-recognition-for-everyone
	- the test set has 18 different dialects
		- the train set only has 1 dialect
	- each training sample is either a "train or valid" sample
		- valid samples have been manually reviewed and corrected
		- train samples have only been algorithmically labelled
		- both are **drawn from the same distribution**.
## Solutions
- ### (1st) - openai whisper, custom whisper tokenizer, speech to text (SST) model, punctuation model
	- https://www.kaggle.com/competitions/bengaliai-speech/discussion/447961
	- cool tricks
		- [[Spectrogram dithering]]
		- Resampling 16khz->8khz->16khz as augmentation [[downscale upscale examples]]
	- they realized that whisper's tokenizer was slow on Bengali audios [[identifying slow feature generation]]
		- so they retrained it using a 12k vocabulary on Bengali texts.
		- "How did you initialize the word embeddings after changing the tokenizer?"
			- they probably didn't and just finetuned the model on those new tokens
				- I guess it's hard to set initial word embeddings (so your model converges faster - see kaparthy's tips for ml) after working in such high dimentional space
			- The original Whisper tokenizer employs character-level tokens for low-resource languages, which can be time-consuming. So we trained a [[BPE tokenizer]] with 12,000 tokens specifically for Bengali text. We then replaced some tokens in the Whisper tokenizer with these. We carefully replaced tokens after the 10,000th position of the original Whisper's tokens.
				- so their tokenizer has a vocab of 22,000 tokens?
					- I guess they removed it after the 10,000th position since the tokens past those are super rare?
			- I should look into how to modify tokenizers. too bad they don't have training code
	- augmented the speech using Libsonic
	- downloaded many youtube videos and pseudolabelled them
		- I think he used a previous version of his model to do the labelling for hte next version of his model
		- How did you handle the alignment between audio and transcription?
			- Long youtube audios are splitted using with VAD. Reject too short or too long audio segments and let's say use only segments between 5 and 22 seconds.
		- used webrtcvad for the [[voice activity detection (VAD)]] library
	- many ppl didn't succeed finetuning with whisper cause they didn't remove wrong annotations from the dataset
		- "Because the competition dataset was not validated, the initial model was trained on OpenSLR datasets"
			- yeah they really didn't trust the trainin data, which is why their score was so much better than everyone else's
- ### (2nd) - SST, language, and punctuation model
	- https://www.kaggle.com/competitions/bengaliai-speech/discussion/447976
	- apply heavy augmentation for read speech and lighter augmentation for spontaneous speech
		- probably because when someone is reading, it's more fake
		- he noticed that spontaneous speech
			- has a much more diverse range of speed (much faster)
			- contains more background noise
	- augmentations he did:
		- time stretch, room simulator, add background noise, add gaussian noise, gain
	- The idea is that after he got the text from the SST and language model, he would use the punctuation model to fill in punctuation
	- **Language model**
		- used a 6-gram kenLM model
		- I'm not sure how this model was with the STT model. maybe it was used to generate extra features for the STT?
	- **punctuation model**
		- it's a token classification model to add the following punctuation set: `।,?!`
			- my prediction is that for each token, it will classify it as "no punctuation," or "add a I, , ?, or ! punctuation right after it"
		- [[GRU head (neck) after the backbone layer]]
			- used an LSTM head, then the classification outputs
			- [[Masked Language Modeling (MLM)]] on 15% of the tokens
			- used [[beam search decoding]]
	- Note: he gave dot and hyphen for ASR model to learn because they are the most problematic punctuations in the annotations.
		- NOTE: adding hyphens is crucial to do well with the [[Word Error Rate]] because if you don't have a hyphen, a word would be broken up into two by the STT model
			- but word error rate considers hyphenated words to be one word
		- this makes sense, cause you can easily identify pauses in speech
		- he needed to find external data that have dot annotations to do this well
	- the final full train took ~5days. Training punctuation models are relatively quick though, only a few hours.
		- used v100s
	- I am still very confused. why are they using three models. shouldn't it just be 2?
		- 1 model for sound to text (STT)
		- 1 model to insert punctuation?
		- why is there a random kenlm model?
		- **Answer:**
		- the STT model just outputs characters or subwords ƒrom the audio
		- we need to piece together these into actual words
		- [[kenlm]] is the model that generates the final sentence (with the highest probabilities from the given subwords / sounds)
			- this is why [[beam search decoding]] is used, to quickly find a string transcription
- ### (3rd) [[Connectionist temporal classification (CTC)]], [[KenLM]], xlm-roberta-large, denoised using Demucs
	- https://www.kaggle.com/competitions/bengaliai-speech/discussion/447957
	- [[text data cleaning]]
		-  consecutive `[।!?]` in the train data were replaced by a single character
		- We also removed sentences containing consecutive `[,-]` from the train data
	- During inference, we sorted data based on audio_length in ascending order and set the dataloader's variable shuffle=False.
	- [[Connectionist temporal classification (CTC)]]
		- we fine-tuned a model only with the human reviewed & corrected data (split=”valid”), which improved CV
			- cause finetuning on all data decreased CV
	- used [[kenlm]]
		- Because there are many out-of-vocabulary in OOD data, we thought training strong LM with large external text data is important. So we downloaded text data and script of ASR datasets(Competition data, indicCorp v2, common voice, fleurs, openslr, openslr37, and oscar) and trained 5-gram LM.
	- used [[Demucs]] to denoise audios
		- note: demucs sometimes makes the audio worse
			- so if it's worse, they don't use it
			- how to detect if it makes it worse?
				- 1) make two predictions one with and one without demucs
					- use mean_width=10 (during bean search) to speed up the inference
				- 2) we compared the number of tokens in two predictions. If the number of tokens in the prediction with Demucs is longer, then use Demucs, else, don't use it
	- post processing: the punctuation model (xlm-roberta-large)
		- their punctuation model will look at the spaces in between words. and it'll decide to insert a punctuation in those spaces if needed
		- As a tip for training, the CV score was better improved by setting the loss weight of "PAD" to 0.0.
- ### (4th) similar solution to (3rd). not much new
	- https://www.kaggle.com/competitions/bengaliai-speech/discussion/447995
	- trained a spelling error correction model (but didn't work)
## Takeaways
- use good training data.  if you are given bad training data, don't make a cake out of garbage. find better ingredients!
- a good approach to data augmentation:
	- (2nd) "most of the augmentations are there because logically it makes sense for them to be there and not the results of some grid search experiments. I try to take the same approach in CV comps too"
- when dealing with audio, train a punctuation model to input punctuation afterwards.
	- but make sure hypthens and periods are trained with the original model (so it can pick up on pauses)
	- only the top competitors UNDERSTOOD THE IMPORTANCE OF A PUNCTUATION MODEL
	- people tried ot use a seq2seq model to generate the punctuation (probably given the predicted sentence with no punctuation, generate one that did have it)
		- however, a classification model worked much better
	- Since there is no good end-to-end [[speech to Text (STT)]] model to convert the audio into sentences, ppl in this competition hacked a pipeline of three models (mp3 -> subword / character tokens -> constructed sentences -> sentences w/ punctuation) to get the transcriptions.
		- this probably won't be required in a few years
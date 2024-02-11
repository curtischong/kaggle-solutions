**Link:** https://www.kaggle.com/competitions/vesuvius-challenge-ink-detection

**Problem Type:** [[semantic segmentation]]

**Input:** 3D scans of the papyrus
- it's hard cause ink may penetrate different depths of the paper
- Since it's 3D and high res, the dataset is also massive

**Output:** 
- The output should be binary, with 0 indicating "no ink" and 1 indicating "ink".

**Eval Metric:**
- [[F-score | F0.5 Score]]
	- This weights precision higher than recall, which improves the ability to form coherent characters out of detected ink areas.
## Summary
- There are 2000-year-old scrolls left from Pompei (carbonized from the Vesuvius eruption)
	- we can't read them without breaking them
	- so ppl 3D Xray-scanned the scrolls
- The goal is to detect the ink in the 3D Xray scans.
- the training data are (3D scans from the Herculaneum Papyri)
	- The ground truth are the ink in these scrolls (found via infrared light)
	- "We also provide hand-labeled binary masks indicating the presence of ink in the photographs."
## Solutions

- ### (1st - youtube vid) [[Stochastic Weights Averaging]], [[remove easy examples]]
	- https://www.youtube.com/watch?v=IWySc8s00P0
		- discarded earlier layers of the papyrus when training (since it was blank) [[remove easy examples]]
			- it also decreases bias in the model
		- used [[BCELoss]] + [[DiceLoss]]
			- BCE since it's smooth. Dice since that is the evaluation for the competition
		- used [[Stochastic Weights Averaging]] since the loss is noisy
		- Used [[hold-out cross validation]] rather than [[kfold]]
			- fragment 1 was their validation set
			- if it was better, then retrain on all the data and submit to the leaderboard
			- If it improved on fragment 1 AND the public LB, they would keep that improvement
			- [[cosine annealing LR]] (didn't do too much iteration here. it worked well)
			- for each image of the scroll, they cropped it and fed each crop to the model
				- found that large crops of the image is better
				- this is the SAME amount of compute, even though the cropped img is larger, there are fewer crops of the scroll img
			- used many [[segformer]] and [[unet]] models
		- [[remove stray pixels]]
		- they didn't really try to do multiclass classification until the end
			- multiclass as in: predict what is air, papyrus, and ink?
				- training it was comparative to training the binary-based target network
		- used [[vast.ai]] to train
		- they were using small batch sizes (4,6) even across multiple GPUs
		- thing they didn't try yet:
			- transform the data into the frequency domain. if some frequencies have no signal, the model will just assign 0 weight to it!
- ### (2nd) Focused more resources on training the encoder than the decoder.
	- https://www.kaggle.com/competitions/vesuvius-challenge-ink-detection/discussion/417255
	- tattaka & mipypf's part
		- used 1/32 resolution [[reduce resolution]]
			- this allows them to have more resources for training the encoder (more layers)
			- using [[bilinear interpolation]]
		- The normalized each image [[normalize features]]
			```python
			  # img: (bs, layers, h, w)
			  mean = img.mean(dim=(1, 2, 3), keepdim=True)
			  std = img.std(dim=(1, 2, 3), keepdim=True) + 1e-6
			  img = (img - mean) / std
			```
			- This normalization is per batch size it seems? not normalized against the entire dataset?
		- [[GroupKFold]]
			- 3 groups: ink_id=0, 1, 2
				- not sure what 2 is?
	- 

## Important notebooks/discussions

## Takeaways
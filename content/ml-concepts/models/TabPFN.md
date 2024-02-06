- "A Transformer That Solves Small Tabular Classification Problems in a Second"
- https://arxiv.org/abs/2207.01848
- https://medium.com/chat-gpt-now-writes-all-my-articles/tabpfn-the-new-xgboost-easy-models-for-efficient-high-performance-machine-learning-1327de095b4f
	- "The training is computationally expensive, requiring significant time and computational resources. However, it is a one-time offline step done during algorithm development."
- it uses a transformer which encodes each feature vector and label as a token
	- each each incoming feature vector a word vector? I guess you skip the tokenizer part
	- but how do you turn a feature (e.g. age) into a 512 dim vector (for example)
- github: https://github.com/automl/TabPFN
- https://www.youtube.com/watch?v=9cE8lqQiLyM
	- a video by one of the authors
	- limitations:
		- up to 1000 data points, 100 features, 10 classes
	- this video isn't very good

### Gotchas
- Do not power transform your data before feeding into TabPFN. 
- "We do not have special nan handling built into our model. We replace nan values with zero at test time"

### Limitations
- "We also focused the development of TabPFN to purely numerical datasets without missing values, and while they can be applied to datasets with categorical features and/or missing values, their performance is generally worse."
- "we did not consider the existence of many uninformative features in our prior, leading to performance degradation when such features are added"
- since TabPFN does training AND inference at the same time, inference is slower
- it works much better for categorization than regression
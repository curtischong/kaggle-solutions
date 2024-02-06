- "A Transformer That Solves Small Tabular Classification Problems in a Second"
- https://arxiv.org/abs/2207.01848
- https://medium.com/chat-gpt-now-writes-all-my-articles/tabpfn-the-new-xgboost-easy-models-for-efficient-high-performance-machine-learning-1327de095b4f
	- "The training is computationally expensive, requiring significant time and computational resources. However, it is a one-time offline step done during algorithm development."
- it uses a transformer which encodes each feature vector and label as a token
	- each each incoming feature vector a word vector? I guess you skip the tokenizer part
	- but how do you turn a feature (e.g. age) into a 512 dim vector (for example)
- github:
	- usage:
		```python
		from sklearn.metrics import accuracy_score
		from sklearn.datasets import load_breast_cancer
		from sklearn.model_selection import train_test_split
		from tabpfn import TabPFNClassifier
		
		X, y = load_breast_cancer(return_X_y=True)
		X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=42)
		
		# N_ensemble_configurations controls the number of model predictions that are ensembled with feature and class rotations (See our work for details).
		# When N_ensemble_configurations > #features * #classes, no further averaging is applied.
		
		classifier = TabPFNClassifier(device='cpu', N_ensemble_configurations=32)
		
		classifier.fit(X_train, y_train)
		y_eval, p_eval = classifier.predict(X_test, return_winning_probability=True)
		
		print('Accuracy', accuracy_score(y_test, y_eval))
```
- https://www.youtube.com/watch?v=9cE8lqQiLyM
	- a video by one of the authors
	- limitations:
		- up to 1000 data points, 100 features, 10 classes
	- this video isn't very good

### Limitations
- "We also focused the development of TabPFN to purely numerical datasets without missing values, and while they can be applied to datasets with categorical features and/or missing values, their performance is generally worse."
- "we did not consider the existence of many uninformative features in our prior, leading to performance degradation when such features are added"
- since TabPFN does training AND inference at the same time, inference is slower
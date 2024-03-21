https://blmoistawinde.github.io/ml_equations_latex/#cross-entropy
### Summary
- aka [[log loss]] / binary cross entropy loss
- It measures the performance of a classification model whose 
- why is it called "cross-entropy"?
	- since the [[entropy]] of a random variable X is:
		$$H = - \sum_i{p_i * \log(p_i)}$$
		- the summation is over each class (i.e. distribution for each class)
		- for 2 classes, we get the BCE loss below
output is a probability value between 0 and 1.

In binary classification (one target) [[BCELoss]]:

$$-{(y\log(\hat{y}) + (1 - y)\log(1 - \hat{y}))}$$


- derivation:
	- 1) the likelihood for a binomial distribution is:
		- $\binom{n}{k}\theta^k(1-\theta)^{n-k}$
			- for n samples, k positive class, and theta, probability of the positive class
		- since $\binom{n}{k}$ is a constant, we drop it when optimizing for the likelihood function of the binomial distribution
	- 2) we take the log of the likelihood:
		- $\log(\theta^k(1-\theta)^{n-k})$
		- = $k\log(\theta) + (n - k)\log(1 - \theta)$
	- 2.5) Change the variables:
		- Let $\theta = \hat{y}$
			$k\log(\theta) + (n - k)\log(1 - \theta)$
			$k\log(\hat{y}) + (n - k)\log(1 - \hat{y})$
			- this makes sense since yhat is our model's estimation of the theta parameter
		- divide everything by n
			- $k\log(\hat{y}) + (n - k)\log(1 - \hat{y})$
			- $\frac{k}{n}\log(\hat{y}) + \frac{n - k}{n}\log(1 - \hat{y})$
			- $\frac{k}{n}\log(\hat{y}) + (1 - \frac{k}{n})\log(1 - \hat{y})$
		- replace $\frac{k}{n}$ with y
			- if you think about it, y is the probability of TRUE positive examples in the dataset, so this replacement makes sense
			- $\frac{k}{n}\log(\hat{y}) + (1 - \frac{k}{n})\log(1 - \hat{y})$
			- $y\log(\hat{y}) + (1 - y)\log(1 - \hat{y})$
	- 3) Define the loss as the negative of the likelihood
		- This is because minimizing the negative likelihood is performing [[Maximum Likelihood Estimation]]
			- cause the likelihood that the distribution fits the model is larger!
[[categorical cross entropy]] In multiclass classification (multiple targets: M > 2):

$$-\sum_{c=1}^My_{o,c}\log(p_{o,c})$$

- M: number of classes
- log: the natural log
- y: binary indicator (0 or 1) if class label c is the correct classification for observation o
- p: predicted probability observation o is of class c


https://www.quora.com/What-are-some-advantages-and-disadvantages-of-using-cross-entropy-as-an-error-measure-when-training-neural-networks
#### pros
- It penalizes the model more strongly for incorrect predictions that are confident, which can lead to better-calibrated models that are less overconfident in their predictions.
#### cons
- Is sensitive to class imbalance, will be biased to the majority class
- Is sensitive to outliers and noise
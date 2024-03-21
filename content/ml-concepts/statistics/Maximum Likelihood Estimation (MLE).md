link: https://en.wikipedia.org/wiki/S%C3%B8rensen%E2%80%93Dice_coefficient
range: 
### summary
- Recall that [[likelihood]] is "given data that I know, what is the likelihood it came from this distribution"
- the goal of MLE is to plug in different distributions and find the params that fit the data's distribution
### How to find the MLE?
- **The way we're taught in school**
	1) Identify the type of distribution the data comes from (e.g. normal/geometric/binomial)
	2) Calculate the [[likelihood]] function for that distribution type
		- visit [[likelihood]] to learn how to calculate it
	1) set the derivative of the likelihood function, set it to 0, and solve for the parameters that maximizes the likelihood function
		- this is a standard grade 9 optimization problem
- **The way ppl do it IRL**
	- We typically don't know the distribution of the data we're modelling over
	- So we try to minimize loss functions for our model instead.
		- if the mean squared error is low enough, then our model's weights is good enough approximation of the MLE
### Other notes:
- There are an infinite number of distributions that can fit any data.
	- Why? Cause datapoints are noisy. We only see the sampled data, not where it came from
		- e.g. a student's T distribution looks like a normal distribution
	- so there isn't a single way that will always optimally get you a distribution

link: https://en.wikipedia.org/wiki/S%C3%B8rensen%E2%80%93Dice_coefficient
range: 
### summary
- Recall that [[likelihood]] is "given data that I know, what is the likelihood it came from this distribution"
- the goal of MLE is to plug in different distributions and find the params that fit a distribution
- There are many different ways to find this distribution. it's not a single algorithm
- There are a few questions:
	- 1) we don't know which distribution type the data came from:
		- normal? exponential? erlang?
		- **Note: In ML, we don't know the distribution type of our data. It doesn't even have a name**
			- e.g. What is the distribution of dog photos? We need to know this distribution so we can sample new dog photos from it and generate new dog images.
	- 2) we also don't know the parameters.
		- what is the mean / variance of the distribution/ k value / lambda?
- Note: there are an infinite number of distributions that can fit any data.
	- Why? Cause datapoints are noisy. We only see the sampled data, not where it came from
		- e.g. a student's T distribution looks like a normal distribution
	- so there isn't a single way that will always optimally get you a distribution
	- Thus, for most MLE methods, you have to select the distribution first before optimizing. the method will get you the params to the model
- If you think the data comes from a normal/geometric/binomial distribution, you'll use the corresponding [[likelihood]] function to find the MLE
	- This is an example of finding the MLE for data that fits a normal distribution: [Maximum Likelihood For the Normal Distribution, step-by-step!!! (youtube.com)](https://www.youtube.com/watch?v=Dn6b9fCIUpM)

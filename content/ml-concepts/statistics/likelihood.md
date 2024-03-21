[(136) Probability is not Likelihood. Find out why!!! - YouTube](https://www.youtube.com/watch?v=pYxNSUDSFH4)
	![[Pasted image 20240321132152.png]]
- This is NOT bayes rule. It's completely different
	- **probability is:** given a distribution, what is the the probability I'll see this data?
	- **likelihood is:** given data that I know, what is the likelihood it came from this distribution?
- note that likelihood and probability have different conditionals (priors)
	- in probability, the distribution is fixed
	- in likelihood, the distribution is fixed
**The definition**
- The likelihood function is the joint probability of observing the given data points, assuming that they are independent and identically distributed (i.i.d.)
- For a set of observations {x₁, x₂, ..., xₙ}, the likelihood function is given by:
$$L(X | \theta) = f(x_1, x_2, \ldots, x_n | \theta) = f(x_1 | \theta) \cdot f(x_1 | \theta) \cdot \ldots \cdot f(x_n | \theta)$$
- Where: 
	- L(θ) is the likelihood function
	- f(xᵢ | θ) is the probability density function - PDF (or PMF) of the i-th observation, given the parameter(s) θ
	- θ represents the parameter(s) of the distribution
- Note: calculating the log of the likelihood function is typically easier

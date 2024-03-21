Likelihood =  P(observing your sample as a function of the unknown parameter)
- though a likelihood function might look just like a probability density function, it’s fundamentally different.
	- A probability density function is a function of x, your data point, and it will tell you how likely it is that certain data points appear.
	- A likelihood function, on the other hand, takes the data set as a given, and represents the likeliness of different parameters for your distribution.



- Think of it as the probability, but the condition and observed values are flipped.
	- e.g. in a coin flip for 2 heads in a row:
		- $P(HH | p_H = 0.5) = 0.5^2 = 0.25$
	- but the likelihood function is:
		- $L(p_H = 0.5 | HH) = 0.25$

$$p(X | Z) = \frac{p(Z|X)p(X)}{p(Z)}$$
- [(137) Evidence Lower Bound (ELBO) - CLEARLY EXPLAINED! - YouTube](https://www.youtube.com/watch?v=IXsA5Rpp25w)
	- You can think of the P(Z) term as the normalizing constant
		- this is VERY hard to calculate in high dimensions since it's an intractable integral:
		- $\int p(z | x)p(x) dx$
- scratchpad (not sure if correct):
	- If Z is the hidden/latent variable, and X is observed variable
	- e.g. Z = the img is a cat
	- X = the pixels of the img
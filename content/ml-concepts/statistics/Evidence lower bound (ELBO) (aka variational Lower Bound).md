- https://blog.evjang.com/2016/08/variational-bayes.html
	- Assume we have a hidden variable that dictates the observed variable
	- ![[Pasted image 20240321171705.png]]
	- e.g.
		- X is the "raw pixel values of an image"
		- Z = 1 means: "the img is a cat"

	- We care about P(Z|X) (the _posterior inference_):
		- _Given this surveillance footage X, did the suspect show up in it?_
		- _Given historical stock prices $X_{1:t}$, what will $X_{t+1}$ be?_
	- We want to train models that match P(Z|X) as close as possible
		- We could try to use sampling-based approaches like [MCMC](https://en.wikipedia.org/wiki/Markov_chain_Monte_Carlo), but these are slow to converge.
	- In variational inference, the goal is to approximate a complex posterior distribution p(z|x) over latent variables z given observed data x. This is often intractable to compute directly.
	- Instead, a simpler variational distribution q(z) is introduced to approximate the true posterior distribution. The variational distribution is chosen from a family of distributions that are easier to work with, such as Gaussian distributions.
	- The log-likelihood of the observed data can be decomposed into two terms: `log p(x) = L(q) + KL(q || p)` where `L(q)` is the variational lower bound and `KL(q || p)` is the [[KLDivergenceLoss]]
	- The KL divergence is always non-negative, which means that L(q) is always less than or equal to the true log-likelihood log p(x). Hence, L(q) serves as a lower bound on the log-likelihood.
	- The goal of variational inference is to maximize the variational lower bound L(q) with respect to the parameters of the variational distribution q(z). **By maximizing the lower bound, we indirectly minimize the KL divergence between q(z) and p(z|x)**
		- so our model's distribution **q(Z)** is brought closer to **P(Z|X)** (and thus makes better predictions)
	- The term "variational" in "variational lower bound" comes from the fact that the approximation is based on variational calculus, which involves optimizing over a family of functions (in this case, the variational distributions).
- since `log p(x) = L(q) + KL(q || p)`
	- rearranging, we get:
		`L(q) = log p(x) - KL(q || p)`
	- since maximizing L(q) makes the model better, we can also minimize -L(q) to make the model better
	- Therefore, loss functions look like this:
		`Loss_vb = KL(q || p) - log p(x)`
### Scratchpad
- It's the lower bound on the log-likelihood of some observed data
- https://xyang35.github.io/2017/04/14/variational-lower-bound/
		- The definition is:
$$L = E_q[\log p(X,Z)] + H[Z]$$
- Where
	- Z is the hidden / latent variable
	- X is the observed variable
		- There is an unknown relationship about how the distribution of Z affects the distribution of X
	- H is [[entropy]]
- The derivation
	- ![[Pasted image 20240321164319.png]]
		- the first line comes from the law of total probability
		- The last line is L (variational Lower Bound)
- Why do we care about L?
	- cause if we want our model's outputs (Z) to match the distribution of the training data(X), we want P(Z | X) to be very close to 1
- Since we are dealing with logs multiplied by probabilities, it looks like [[KLDivergenceLoss]]
	- so another way to express L is:
		- $$L = \log p(X) - KL[q(Z) || p(Z|X)]$$
- [Evidence Lower Bound (ELBO) - CLEARLY EXPLAINED! (youtube.com)](https://www.youtube.com/watch?v=IXsA5Rpp25w)
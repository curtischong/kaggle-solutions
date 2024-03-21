link: https://en.wikipedia.org/wiki/S%C3%B8rensen%E2%80%93Dice_coefficient
range: 
### summary
- it is the log of the [[likelihood]] function
- If we take the negative of the log likelihood, we get the negative log-likelihood (NLL) loss
	- note: since the likelihood function changes depending on the distribution, there is no single NLL formula
	- e.g. if we are doing a binary classification problem, we use [[BCELoss]]

- Why use log likelihood instead of the pure likelihood function?
	- https://math.stackexchange.com/questions/892832/why-we-consider-log-likelihood-instead-of-likelihood-in-gaussian-distribution
	- since ln(a\*b) = ln(a) + ln(b), many equations simplify significantly
	- so we use the log likelihood over the likelihood
### pros

### Cons

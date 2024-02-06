Temporal Fusion Transformers for Interpretable Multi-horizon Time Series Forecastin
[1912.09363.pdf (arxiv.org)](https://arxiv.org/pdf/1912.09363.pdf)
- ![[Pasted image 20240206005227.png]]
- the main thing is that this model tries to predict for more than one time horizon
	- rather than predicting only the next timestep, it predicts further ahead
- it uses GRN layers (Gated Residual network) to perform nonlinear operations
	- it's just a small layer that is used everywhere to sprinkle nonlinearity
	- ![[Pasted image 20240206005140.png]]
- it does selection of features to use automatically via the Variable selection networks
	- it removes unimportant / noisy features so the model can predict easier
	- Here's how the Variable Selection Network / Layer works:
		- all of the features go into individual GRN layers (left side)
		- but all of the features are ALSO concatenated into one giant feature vector and go into another GRN (the right one, with the softmax)
		- we finally multiply the output of the softmax by the feature outputs of the GRN
			- so the GRN of the concatenated features selects which features to propagate. (kinda like the sigmoid in an LSTM)
		- ![[Pasted image 20240206004651.png]]
- after the features have been selected, each of these outputs are fed into a LSTM layer so the model can pick up time-dependent features
- static covariate encoder
	- As an example, taking ζ to be the output of the static variable selection network, contexts for temporal variable selection would be encoded according to $c_s$ = $GRN_{c_s}$ (ζ).
- The attention mechanism is used to "learn long-term relationships across different time steps"

### Takeaways
- When designing this model, they placed the attention mechanism later in the network. The first "preprocessed" information with many different layers
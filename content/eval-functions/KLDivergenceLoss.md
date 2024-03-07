
link: 
range: 
### summary
-  KLDivergence evaluates how one probability distribution aligns or diverges from a second, expected probability distribution.
- This video explains it intuitively: https://www.youtube.com/watch?v=SxGYPqCgJWM
	- if two distributions assign similar probabilities to the same sequence, then the distributions are similar
		- and vice versa
	- it's a natural measurement of distance between probability distributions motivated by looking at how likely the second distribution would be able to generate samples from the first distribution
- you can use it:
	- as a model loss
	- to determine feature drift from your training data and real data, but  [population stability index](https://arize.com/blog-course/population-stability-index-psi/) (PSI) is preferred (since it's symmetric)

L(y_pred, y_true) = y_true * (log y_true - log y_pred)


- I'm not sure if KLDivergence is the same as adding [[label smoothing]]
	- I do see people doing KLDivergence AND label smoothing together
- I think we just need to test.

- [Is label smoothing equivalent to adding a KL divergence term or a cross entropy term?](https://stats.stackexchange.com/questions/521006/is-label-smoothing-equivalent-to-adding-a-kl-divergence-term-or-a-cross-entropy)

- KL divergence is not technically a measure of distance, since it's not symmetric ( Dlk(P||Q) != Dlk(Q||P) ).
### pros

### Cons


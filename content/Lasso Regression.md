- https://www.youtube.com/watch?v=NGf0voTMlcs
	- very similar to [[ridge regression]] except instead of the loss being:

$$(\hat{y} - y)^2 + \lambda m^2$$

we have

$$(\hat{y} - y)^2 + \lambda |m|$$

- like ridge regression, the fit will have more bias than least squares (makes our prediction less sensitive to tiny datasets)
- it also shrinks parameters (when compared to just using least squares)
- Since we're using absolute value, weights for dimensions with large slope latter **less**
	- so **the main reason to use** lasso regression is because it can exclude useless features from equations
		- since it cares about the slope less
	- This also means that: ridge regression does a bit better when most features are useful
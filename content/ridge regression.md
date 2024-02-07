- https://www.youtube.com/watch?v=Q81RR3yKn30&t=0s
	- This is the same as linear regression, but instead of the loss being the least squares (i.e. the sum of the squared residuals):
	
	$$(\hat{y} - y)^2$$
	
	- the less is instead the least squared + $\lambda \cdot$ the slope$^2$:
	
	$$(\hat{y} - y)^2 + \lambda m^2$$
	- lambda determines how severe the regularization penalty is
		- it's a value from $[0, \infty)$
		- we tune the proper value of lambda using [[cross validation]]
	- The steeper the slope, the worse the loss
		- so ridge regression **shrinks the the model weights** like l1 / l2 loss
	- Note: we can apply this to logistic regression as well. we just add the lambda * slope ^2 term
	- we can also add all of the other model weights (not just slope) into the ridge regression loss function
		- the only weight we don't add is the y-intercept
	- advanced: ridge regression can help us fit an 200 dimensional model with only 100 training examples because the lambda * slope ^2 term helps us evaluate different fits better
		- least squares can't optimize this solution since it can't find a single line that will optimize all 200 dimensions with only 100 training examples
		- this means that ridge regression has more bias than linear regression since it's solution may not directly intersect all 100 training examples. but it will have better variance cause it's CV will be lower
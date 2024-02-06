### Use as a feature dimension reduction tool
- after performing SVD, you get the most significant singular values and vectors:
	- https://medium.com/nerd-for-tech/dimensionality-reduction-techniques-pca-lca-and-svd-f2a56b097f7c#:~:text=SVD%20allows%20for%20dimensionality%20reduction,significant%20singular%20values%20and%20vectors.&text=SVD%20is%20used%20in%20data,storage%20requirements%20of%20a%20matrix.&text=By%20using%20only%20the%20most,of%20noise%20in%20the%20data.
- If you use a technique to automate feature generation (e.g. [[tf-idf]] vectors), you should use this to reduce the dimensionality of those generated features

### Use as a denoiser:
- It's a technique to denoise target variables
	- https://www.kaggle.com/code/ambrosm/scp-quickstart?scriptVersionId=144293041&cellId=8
	- kinda like log transforming y in linear regression to make the target variable have constant variance
		- except this is for matrices of values
- Since SVD is applied to a matrix, only use this when you are predicting on multiple target variables
- PLEASE REMEMBER TO INVERSE TRANSFORM YHAT WHEN INFERENCING

e.g.
```python
svd = TruncatedSVD(n_components=n_components, random_state=1)

# fit the svd and your model
z_tr = svd.fit_transform(train[genes])
model.fit(train[features], z_tr)

# look! we're inverse transforming before returning the preds!
y_pred = svd.inverse_transform(model.predict(val[features]))
```
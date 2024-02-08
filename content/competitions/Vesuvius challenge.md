**Link:** 

**Problem Type:** 

**Input:** 3D scans of the papyrus
- it's hard cause ink may penetrate different depths of the paper

**Output:** 

**Eval Metric:** 
## Summary
## Solutions

https://www.youtube.com/watch?v=IWySc8s00P0
- discarded earlier layers of the papyrus when training (since it was blank)
- used [[BCELoss]] + [[DiceLoss]]
	- BCE since it's smooth. Dice since that is the evaluation for the competition
- used [[Stochastic Weights Averaging]] since the loss is noisy
- Used [[hold-out cross validation]] rather than [[kfold]]
	- fragment 1 was their validation set
	- if it was better, then retrain on all the data and submit to the leaderboard
	- If it improved on fragment 1 AND the public LB, they would keep that improvement
	- [[cosine annealing LR]] (didn't do too much iteration here. it worked well)
	- for each image of the scroll, they cropped it and fed each crop to the model
		- found that large crops of the image is better
		- this is the SAME amount of compute, even though the cropped img is larger, there are fewer crops of the scroll img
	- used many [[segformer]] and [[unet]] models
- [[remove stray pixels]]
- they didn't really try to do multiclass classification until the end
	- multiclass as in: predict what is air, papyrus, and ink?
		- training it was comparative to training the binary-based target network
- used [[vast.ai]] to train
- they were using small batch sizes (4,6) even across multiple GPUs
- thing they didn't try yet:
	- transform the data into the frequency domain. if some frequencies have no signal, the model will just assign 0 weight to it!

## Important notebooks/discussions

## Takeaways
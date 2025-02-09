- These are problems where you tell a computer to rank a list of n items (based on relevance)
- You want a model that scores items (like pagerank), so you can just sort each item by their score
- three approaches:
	- https://notesonai.com/Learning+to+Rank
	- Pointwise Approach
	    - Predict the relevance per item, simple but very naive.
	    - Ignores that ordering of items is what matters.
	- Pairwise Approach
	    - Loss based on document pairs, minimize the number of incorrect inversions.
	    - Ignores that not all document pairs have the same impact.
	    - Often used in the industry.
	- Listwise Approach
	    - Tries to optimize for IR metrics, but they are not differentiable.
		    - what is an IR matrix?
	    - Approximations by heuristics, bounding or probabilistic approaches to ranking.
- Check out these [[ranking loss functions]]
- Do not confuse learning to rank with [[ordering objects in list]] (doesn't have a query vector)
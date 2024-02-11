link: https://en.wikipedia.org/wiki/S%C3%B8rensen%E2%80%93Dice_coefficient
range: (not similar at all) [0, 1] (the two sets are the same)
### summary

`Dice Loss = 1 - 2 * (intersection of predicted and true) / (sum of predicted + sum of true)`

This based on the **Dice similarity coefficient:**
$$
DSC = \frac{2|X \cap Y|}{|X| + |Y|}
$$

- Where X and Y are two sets
- This loss is typically used for image segmentation problems
- this looks similar to the [[F-score]]: ````
- `F1 = 2 * (Precision * Recall) / (Precision + Recall)`

### pros

### Cons

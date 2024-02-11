https://en.wikipedia.org/wiki/F-score
There are several versions of F-score:
**F1 score:**

$$F_1 = 2\frac{\text{precision} \cdot \text{recall}}{\text{precision}+\text{recall}}$$

where:
$$
\text{precision} = \frac{\text{|true positive|}}{\text{|true positive| + |false positive|}}
$$

$$
\text{recall} = \frac{\text{|true positive|}}{\text{|true positive| + |false negative|}}
$$


$F_\beta$ **Score**
- Used when recall is considered $\beta$ times as important as precision
$$F_\beta = (1+\beta^2)\frac{\text{precision} \cdot \text{recall}}{(\beta^2 \cdot \text{precision})+\text{recall}}$$

**F0.5 Score**
 - $$
F_{0.5} = (1 + 0.5^2)\frac{\text{precision} \cdot \text{recall}}{(0.5^2 \cdot \text{precision})+\text{recall}}
$$ ^babo2y
- The F0.5 score weights precision higher than recall,
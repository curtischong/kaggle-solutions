- https://www.mdpi.com/2079-9292/11/4/540
$$f(x)=x \cdot \tanh[\ln(1+sigmoid(𝑥))]$$
- It's similar to Mish:
$$f(x)=x \cdot\tanh[\ln(1+e^x)]$$
![[Pasted image 20240207113352.png]]
- green is mish
- purple is [[Sigmoid Linear Unit (Swish)]]
	- Note: it converges with Mish as $x \rightarrow \infty$
- red is smish
	- Note: Smish doesn't converge with Swish as $x \rightarrow \infty$
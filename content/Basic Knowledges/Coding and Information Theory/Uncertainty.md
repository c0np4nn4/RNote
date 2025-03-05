Let $X$ be a random variable taking on a finite number $M$ of different values.
$$
x_1, \dots, x_m
$$
$X$ could be thought as the result of coin tossing, etc.

The probability of **random variable** $X$ for alphabet $\mathcal{X}$ is defined as below.

> [!Important] For discrete RV
> probability mass function (pmf) is defined as
> $$
> 	p(x) = \text{Pr} \{ X = x \} \;\; \text{ where } \;\; \Sigma_{x \in \mathcal{X}} \; p(x) = 1 
> $$

> [!Important] For continuous RV
> probability density function (pdf) is defined as
> $$
> 	f(x) \;\; \text{ where } \;\; \int_{-\infty}^{\infty} \; f(x) dx = 1 
> $$
> Cumulative distribution function $F(x) = \text{Pr}(X \le x)$ and $f(x) = F'(x)$

Uncertainty and probability are inversely proportional.
- "Low probability" means "High uncertainty"
- e.g., Biased coin tossing Head/Tail with probability as below (The uncertainty should be **zero**.)
  
 <center>
 
  $$\begin{cases}p(x=H)&=1 \\p(x=T) &=0\end{cases}$$
  
  </center>
  
  

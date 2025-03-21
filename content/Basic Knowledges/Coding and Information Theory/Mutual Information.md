상호 정보(mutual information)는 한 확률 변수가 다른 확률 변수에 대한 정보를 얼마나 포함하고 있는지를 나타내는 값입니다. 즉, 다른 확률 변수에 대한 정보를 알고 있음을 의미하기 때문에 '불확실성(uncertainty)'의 감소로도 생각할 수 있습니다.

## Definition
두 확률 변수 $X, Y$와 결합 확률 질량 함수(Joint probability mass function) $p(x, y)$, 주변확률 질량함수(marginal probability mass function) $p(x), q(x)$ 에 대하여, 상호 정보(mutual information) $I(X;Y)$ 는 아래와 같이 $p(x, y)$ 와 $p(x)p(y)$ 간의 상대 엔트로피([[Relative Entropy]])로 정의됩니다.

$$
\begin{aligned}
I(X;Y) &= \sum_{x \in \mathcal{X}}\sum_{y \in \mathcal{Y}} p(x, y) \log \frac{p(x, y)}{p(x)p(y)} \\
&=D\big(\, (p(x, y) \; || \; p(x)\,p(y)\, \big) \\
&= E_{p(x, y)} \log \frac{p(X, Y)}{p(X)p(Y)}
\end{aligned}
$$
## Theorem
[[Entropy]]와 [[Mutual Information]]간의 관계를 아래 정리와 같이 표현할 수 있습니다.
$$
I(X;Y) = H(X) - H(X|Y)
$$
### Proof
$$
\begin{aligned}
I(X;Y) &= \sum_{x, y} p(x, y) \log \frac{p(x, y)}{p(x)p(y)} \\
&= \sum_{x, y}p(x, y) \log \frac{p(x|y)}{p(x)} \;\; (\because \frac{p(x, y)}{p(y)} = p(x|y)\;\text{ (Bayes' rule)}) \\
&= -\sum_{x, y} p(x, y) \log p(x) + \sum_{x, y}p(x, y) \log p(x|y) \\
&= -\sum_{x} p(x) \log p(x) - \left( - \sum_{x, y} p(x, y) \log p(x|y) \right) \\
&= H(X) - H(X|Y)
\end{aligned}
$$
즉, 위 식을 해석하면 $I(X;Y)$란 $X$에 대한 불확실성(uncertainty)을 $Y$에 대한 지식($p(X|Y)$)을 통해 감소시키는 것으로 볼 수 있습니다.

Bayes' rule을 통해 $\log \frac{p(x, y)}{p(x)p(y)}$ 에서 분모에 남은 pmf가 첫 번째 항이 되므로, 대칭적으로 아래 식도 성립합니다.

$$
I(X;Y) = H(Y) - H(Y|X)
$$
[[Chain Rule]]을 이용해 아래와 같이 적을 수 있습니다.

$$
\begin{aligned}
I(X;Y) &= H(X) - H(X|Y) \\
&= H(X) - \left(H(X, Y) - H(Y)\right) &(\because \text{체인룰} H(X, Y) = H(Y) +H(Y|X)) \\
&= H(X) + H(Y) - H(X, Y)
\end{aligned}
$$
또, $I(X;X)$ 와 같은 형태도 생각해볼 수 있습니다.
$$
I(X;X) = H(X) - H(X|X) = H(X)
$$
$H(X|X)$는 '주어진 $X$에 대해 $X$의 불확실성'을 구하는 것이므로 '불확실성이 없다'로 해석되어 $0$ 이 됨을 알 수 있습니다.

[[Mutual Information]]과 [[Chain Rule]]의 관계를 아래 그림과 같이 벤 다이어그램으로 나타내면 보다 직관적으로 이해할 수 있습니다.


<center>

![[Pasted image 20250321172325.png|400]]

</center>
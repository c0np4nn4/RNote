## Definition
두 개 이상의 확률변수가 함께 만들어내는 **총 불확실성(total uncertainty)** 을 측정하는 지표입니다.

쉽게 말해, 두 확률 변수 $X$, $Y$가 동시에 발생했을 때의 사건들의 복합적인 정보량을 의미합니다.

두 이산 확률 변수 $X$, $Y$에 대해 *결합 확률분포* $p(x, y)$ 가 존재할 때, 결합 엔트로피(joint entropy) $H(X, Y)$는 다음과 같이 정의됩니다.

$$
H(X, Y) = -E \log p(X, Y) = -\sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log p(x, y)
$$
이 때, $\mathcal{X}, \mathcal{Y}$ 는 각각 $X, Y$ 의 가능한 값들의 집합을 의미하고 $p(x, y)$ 는 $X=x, Y=y$ 가 동시에 발생할 확률을 의미합니다.

결합 엔트로피는 두 변수 전체를 "설명하기 위해 필요한" 총 비트 수를 의미한다고 볼 수도 있고, 특히 통신시스템에서는 두 신호 간의 총 정보량을 의미한다고도 볼 수 있습니다.

## Example
아래와 같은 표가 주어졌을 때, $H(X, Y)$ 를 계산할 수 있습니다.

<center>

| Y \ X |           1   |           2   |
| :---: | :-----------: | :-----------: |
|   1   | $\frac{1}{2}$ | $\frac{1}{4}$ |
|   2   | $\frac{1}{8}$ | $\frac{1}{8}$ |

</center>

$$
\begin{aligned}
&H(X, Y) \\
&= - \Sigma_{x \in \mathcal{X}} \Sigma_{y \in \mathcal{Y}} \; p(x, y) \log p(x, y) \\
&= - \Sigma_{x \in \{1, 2 \}} \Sigma_{y \in \{1, 2 \}} \; p(x, y) \log p(x, y) \\
&= -p(1, 1) \log p(1, 1) -p(1, 2) \log p(1, 2) -p(2, 1) \log p(2, 1) - p(2, 2) \log p(2, 2) \\
\end{aligned}
$$

이 문제는 곧 [[Entropy]]에서의 `Example 3`의 단일 확률 변수의 Entropy를 계산한 것과 동일한 값이 됩니다. 즉, 두 개 이상의 확률 변수의 확률 분포를 단일 확률 변수의 확률 분포로 생각해도 무방함을 알 수 있습니다.

$$
H(X, Y) = H(Z)
$$
이 경우 확률변수 $Z$의 확률 분포는 아래와 같습니다.
$$
H(Z) = 
\begin{cases}
(X=1, Y=1) \; \text{ with probability } 1/2 \\
(X=1, Y=2) \; \text{ with probability } 1/4 \\
(X=2, Y=1) \; \text{ with probability } 1/8 \\
(X=2, Y=2) \; \text{ with probability } 1/8 
\end{cases}
$$

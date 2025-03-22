확률 변수 $X$, $Y$, $Z$에 대한 조건부 상호 정보([[Conditional Mutual Information]])는 아래와 같이 정의됩니다.

$$
I(X;Y|Z) = H(X|Z) - H(X|Y, Z)
$$
이 때, $Z$를 '가리면' 정확히 상호 정보([[Mutual Information]])의 정의와 같음을 확인할 수 있습니다. 즉, $Z$라는 임의의 정보가 추가로 주어진 상황에서 확률 변수 $X$에 대한 불확실성([[Uncertainty]])이 $Y$라는 지식으로 인해 감소함을 의미합니다.

## Theorem
이러한 상호 정보에 대해서도 체인룰([[Chain Rule]])이 성립합니다.
확률 변수 $X_1, \dots, X_n, Y$ 에 대하여 아래와 같이 체인룰 식을 적을 수 있습니다.

$$
I(X_1, X_2, \dots, X_n; Y) = \sum_{i=1}^n I(X_i ; Y | X_{i-1}, X_{i-2}, \dots, X_1)
$$
$n$ 개의 확률 변수 $X_j (j\in [n])$ 와 $Y$가 나타내는 정보는 특정한 $X_i$를 제외한 나머지 확률 변수들이 주어졌을 때, $X_i$ 와 $Y$가 나타내는 상호 정보들의 총합과 같음을 의미합니다.

### Proof
$$
\begin{aligned}
&I(X_1, X_2, \dots, X_n; Y) \\
&= H(X_1, X_2, \dots, X_n) - H(X_1, X_2, \dots, X_n | Y) &(\because \text{Mutual Information 정의}) \\
&= \sum_{i=1}^nH(X_i | X_{i-1}, \dots, X_1) - \sum_{i=1}^nH(X_i | X_{i-1}, \dots, X_1, Y) &(\because \text{Chain rule for Entropy} ) \\
&=\sum_{i=1}^n I(X_i; Y | X_1, X_2, \dots, X_{i-1}) &(\because \text{Conditional Mutual Information 정의})
\end{aligned}
$$


[[Chain Rule For Entropy]] 와 [[Conditional Mutual Information]]의 정의를 이용해 위와 같이 증명할 수 있습니다.
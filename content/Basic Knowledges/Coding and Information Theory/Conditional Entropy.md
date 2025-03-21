## Conditional Probability
조건부 확률(Conditional Probability)은 어떤 사건 $B$가 **이미** 일어난 상황에서 사건 $A$가 일어날 확률을 의미합니다. 즉, 어떤 정보가 주어진 후 다른 사건이 일어날 확률을 측정하는 방법입니다.

결합 확률분포 $p(x, y)$와 사건 $Y$에 대한 확률 분포 $p(y)$에 대하여 아래와 같이 정의됩니다.
$$
p(x|y) = \frac{p(x, y)}{p(y)}
$$
이는 베이즈 룰(Bayes' rule)을 활용해 두 확률 변수 간의 결합 관계를 표현한 것으로도 볼 수 있습니다.

### Example
아래 표에 대하여,

<center>

| Y \ X |  1  |  2  |
| :---: | :-: | :-: |
|   1   | 1/2 | 1/4 |
|   2   | 1/8 | 1/8 |

</center>

$$
p(x = 1 | y = 1) = \frac{p(x=1, y=1)}{p(y=1)} = \frac{1/2}{1/2 + 1/4} = \frac{2}{3}
$$
## Definition
**Conditional Entropy**는 두 사건 $X, Y$ 가 확률 분포 $p(x, y)$를 따를 때, $H(Y|X)$로 표기하고 아래와 같이 정의할 수 있습니다.

$$
\begin{aligned}
H(Y|X) &= \sum_{x \in \mathcal{X}} p(x) H(Y|X=x) \\
&= - \sum_{x \in \mathcal{X}} p(x) \sum_{y \in \mathcal{Y}} p(y|x) \log p(y|x)  \;\;(\because X=x\text{일 때, } y \text{ 에 대한 엔트로피 정의}) \;\\
&= - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x) \cdot p(y|x) \log p(y|x) \\
&= - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log p(y|x) \; (\because\text{Bayes' Rule})\\
&= -E_{p(x, y)} \log p(Y | X)
\end{aligned}
$$
직관적으로 이를 해석하면, $X$가 주어졌을 때 $Y$를 맞히는데 필요한 정보의 양(i.e., bit 개수)을 의미한다고 볼 수 있습니다.

### Example
아래 표에 대하여,

<center>

| Y \ X |  1  |  2  |
| :---: | :-: | :-: |
|   1   | 1/4 | 1/4 |
|   2   | 1/4 | 1/4 |

</center>

$H(Y|X) = \Sigma_{x \in \mathcal{X}} p(x) \; H(Y | X = x)$ 이므로,

$$
\begin{aligned}
H(Y | X) &= p(X=1)H(Y|X=1) + p(X=2)H(Y|X=2) \\
&= (1/2) \cdot H(Y | X=1) + (1/2) \cdot H(Y|X=2) \\
&= (1/2) \cdot \left\{-\sum_y P(Y|X=1) \log P(Y|X=1) \right\} + (1/2) \cdot \left\{-\sum_y P(Y|X=2) \log P(Y|X=2) \right\} \\
&= (1/2) \cdot \left\{-\sum_y P(Y=1|X=1)\log P(Y=1|X=1) - \sum_y P(Y=2|X=1)\log P(Y=2|X=1) \right\} \\
&+ (1/2) \cdot \left\{-\sum_y P(Y=1|X=2)\log P(Y=1|X=2) - \sum_y P(Y=2|X=2)\log P(Y=2|X=2) \right\} \\
&= \frac{1}{2} \cdot \left\{-(1/4) \log \left(1/4 \right)-(1/4) \log \left(1/4 \right)\right\} \times 2 = \frac{1}{2} \cdot 1 \cdot 2 = 1
\end{aligned}
$$

## Example 2
아래 표에 대하여,

<center>

| Y \ X | 1    | 2    | 3    | 4    |
| :---: | :--: | :--: | :--: | :--: |
| 1     | 1/8  | 1/16 | 1/32 | 1/32 |
| 2     | 1/16 | 1/8  | 1/32 | 1/32 |
| 3     | 1/16 | 1/16 | 1/16 | 1/16 |
| 4     | 1/4  | 0    | 0    | 0    |

</center>

조건부 엔트로피 $H(X|Y)$ 를 구하는 식은 아래와 같습니다.

$$
\begin{aligned}
H(X|Y) &= \sum_{i=1}^4 p(Y=i) H(X|Y=i) \\
&= - \sum_x \sum_y p(x, y) \log p(y|x)
\end{aligned}
$$
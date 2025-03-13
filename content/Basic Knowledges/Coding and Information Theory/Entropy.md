**Entropy** is a measure of [[Uncertainty]] and can also be thought of as the "expected amount of information."

## Definition

$$
H(X) = - \sum_{x \in \mathcal{X}} p(x) \log p(x) = \sum_{x\in\mathcal{X}} p(x) \log \frac{1}{p(x)}
$$
Note that $H(X)$ can be written as $E_p\left(\log\frac{1}{p(x)}\right)$, where $E_p$ denotes the expectation with respect to the probability distribution $p(x)$.

The logarithm base is often omitted and is typically assumed to be 2, corresponding to "bits" in information theory.

Entropy can be considered a functional of $p(x)$.

Moreover, entropy provides a lower bound on the number of bits required to represent (or describe) a random variable, making it a fundamental limit in *data compression*.

---

## Examples
### 1. 편향된 동전 던지기
'머리'가 항상 나오는 *편향된 동전 던지기* 의 경우 아래와 같은 확률을 가집니다.
$$
\begin{cases}
p\, (x=H) &= &1 \\
p\, (x=T) &= &0
\end{cases}
$$
따라서, Entropy는 아래와 같이 계산됩니다.
$$
H(X) = -(1 \log 1) - (0\log 0) = 0
$$
이는 곧, '불확실성이 없는 확률변수는 $0$의 entropy를 갖는다'고 해석할 수 있습니다.

또한, 편향된 동전 던지기를 표현하기 위해 $0$ 개의 bit가 필요하다고도 해석할 수 있습니다.

### 2. 동전 던지기
이와 달리 편향되지 않은 이상적인 *동전 던지기* 는 아래와 같은 확률을 가집니다.
$$
\begin{cases}
p(x=H) &= 0.5 \\ 
p(x=T) &= 0.5
\end{cases}
$$
따라서, Entropy는 아래와 같이 계산됩니다.
$$
H(X) = -(\frac{1}{2} \log \frac{1}{2}) - (\frac{1}{2} \log \frac{1}{2}) = 1 \log 2 = 1
$$
즉, 동전 던지기를 표현하기 위해서는 $1$ 개의 bit가 필요합니다.

---

## Property

### Lemma. Non-negativity
> [!Note] Lemma. **Non-negativity**
> Entropy $H(X)$ 는 항상 $0$ 보다 크거나 같습니다.
> 
> $H(X)$는 정의에 따라 아래와 같습니다.
> $$
> \begin{aligned}
> H(x) &= \sum_{x \in \mathcal{X}}  - p(x) \log p(x) \\
> &= \sum_{x \in \mathcal{X}} p(x) \log \big(\frac{1}{p(x)}\big) \\
> \end{aligned}
> $$
> 이 때, $\log \big( \frac{1}{p(x)} \big) \ge 0$ 이므로 항상 영보다 크거나 같습니다.


### Lemma.
> [!Note] Lemma.
> $$
> H_b(X) = (\log_b a) H_a(X)
> $$
> 이는 로그에 관한 기본적인 정리를 통해 쉽게 알 수 있습니다. 즉,
> $$
> \log_b p = \frac{\log_a p}{\log_a b} = \log_b a \log_a p
> $$

## Example 2
### Bernoulli RV's entropy
베르누이 확률변수 $X$ 는 아래와 같습니다.
$$
X = 
\begin{cases}
1, & \text{ with probability } p \\
0, & \text{ with probability } 1 - p
\end{cases}
$$
이에 대한 `Entropy`는 아래와 같습니다.
$$
H(X) = -p \log p - (1-p) \log (1-p)
$$
위 식은 Binary entropy function $H(p)$로도 부릅니다. 

아래 그림과 같이 위로 볼록한 곡선 형태를 그리며, $p=\frac{1}{2}$ 에서 최대값 $1$을 갖습니다.

<center>

![Binary Entropy Function](https://upload.wikimedia.org/wikipedia/commons/thumb/2/22/Binary_entropy_plot.svg/300px-Binary_entropy_plot.svg.png)

</center>

## Example 3
아래와 같은 확률변수를 가정합니다.
$$
X = 
\begin{cases}
a & \text{ with probability 1/2} \\
b & \text{ with probability 1/4} \\
c & \text{ with probability 1/8} \\
d & \text{ with probability 1/8}
\end{cases}
$$
$$
\therefore H(X) = \frac{14}{8} = \frac{7}{4}
$$


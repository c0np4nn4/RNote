---
tags:
  - ClassNote
  - Coding
  - InformationTheory
---
# Uncertainty Measure

> What is the **information**?

"Information" 을 정의하는 문제에 대해 shannon 도 나름의 답을 내렸나봄

"uncertainty"는 information theory 에서 중요한 역할을 한다고 함.
**certain** 은 정보를 주지 않는다고 함(e.g., 내일 해가 뜨는지 안뜨는지)
(e.g., 6 Lottery numbers between 1 to 45)

Low probability $\rightarrow$ High uncertainty
High probability $\rightarrow$ Low uncertainty

- **Quantify of information**

$$
\log(\frac{1}{p})
$$
log의 밑(base)는 infromation을 quantify 하기 위해 무엇이든 올 수 있지만, 일반적으로 $2$ 를 사용한다고 함

> [!Note] Example
> 편향된 동전 던지기에서 $p(x=H) = \frac{1}{8}$ 라고 가정
> "정보"를 계산하는 방법은 위의 식을 사용하면 됨.
> $\log_2(\frac{1}{p}) = \log_2(8) = 3$

확률과 랜덤 변수에 대한 기본 개념을 활용

finite number $M$ 에 대하여, 확률 변수 $X$가 서로 다른 값 $x_1, \dots, x_M$ 을 가진다고 가정.
- discrete RV: probability mass function (pmf)
  $p(x) = \text{Pr}\{X=x\}\;\;$ where $\sum_{x \in \mathcal{X}} p(x) = 1$ 
- continuous RV, probability density function (pdf)
  $f(x)$ where $\Sigma^{\infty}_{\infty} f(x) dx = 1$
	- culmulative distribution function
	  $f(x) = F'(x)$

PDF 도 활용될 수 있다고 함

'알아서 공부 하면 된다고 함'

---

# Entropy
'expectation of information'

$H(X) = - \Sigma_{x \in \mathcal{X}} p(x) \log p(x) = \Sigma_{x \in \mathcal{X}} p(x) \log \frac{1}{p(x)}$
$\therefore H(X) = E_p ( \log \frac{1}{p(X)})$

compression의 lower bound이 될 수 있음
'representation'

> [!Note] Example
> - 극단적으로 편향된 동전 던지기에서 항상 $head$ 만 나온다고 하면
> $$H(X) = -1 \log 1 - 0\log 0 = 0$$
> 즉, 아무런 정보를 주지 않으므로 0 'bit' 만 써서도 정보를 전달할 수 있음
> 
> - Head, Tail 이 고르게 0.5 확률로 나오는 동전 던지기에서는
> $$H(X) = - \frac{1}{2} \log \frac{1}{2} - \frac{1}{2} \log \frac{1}{2} = 1$$ (bit)
> - 만약 $p(x=H) = 1/4, p(x=T) = 3/4$ 이라면
> $$H(X) = 1/4 \cdot 2 + 3/4 \cdot \log 3/4 < 1$$


## Properties of Entropy
- Lemma 2.1.1 (non-negativity of entropy)
$$H(X) \ge 0$$
증명은 $0 \le p(x) \le 1$ 일 때, $\log(\frac{1}{p(x)}) \ge 0$ 이기 때문임

- 다른 base 를 사용하는 경우
$$
H_b(X) = (\log_b a)H_a(X)
$$
증명은 $log_b p = log_b a\log_a p$ 임을 활용하면 됨 ($\log_b p = \frac{\log_a b}{\log_a p})$


> [!Warning] Bernouli RV's Entropy
> 랜덤변수 $X$가 두 가지 선택이 있을 때, "bernoulli RV's entropy" 로 $H(X) = H(p)$ 를 아래와 같이 정의할 수 있음
> 
> $$H(X) = -p \log p - (1-p) \log (1-p) = H(p)$$
> 
> 그리고 $p = \frac{1}{2}$ 일 때, $H(p)$ 가 최대치를 갖는다고 함 (그래프 직접 그려보기)

$H(X) = \Sigma \frac{1}{M} \log \frac{1}{1/M}$
$\therefore H(X) = \log M$

> [!Note] Example (Entropy), 4 possibilities
> $$X=\begin{cases}a,\;\; pr = 1/2 \\ b,\;\; pr = 1/4 \\ c,\;\; pr = 1/8 \\ d,\;\; pr = 1/8 \\\end{cases}$$
> $H(X) = \frac{7}{4} > 1$
> - 4개의 가능성 때문에 '1'보다 큰 값이 나옴
> - 'uniform' 이었으면 2가 나온다고 함

## Joint Entropy
한 쌍의 discrete random variable (X, Y) 에 대해서 
$$
H(X, Y) = -E \log p(X, Y) = \Sigma \Sigma
$$

expectation --> sigma p(x, y) (joint probability)

example 을 보며 이해하면 됨


# Conditional Probability
- $p(x | y) = \frac{p(x, y)}{p(y)}$ (**Bayes' rule**)
- joint probability table 을 보고 적절한 값을 이용해 계산할 수 있는 것 같다...

# Conditional Entropy
entropy는 expectation 이므로..
$$
\begin{aligned}
H(Y|X) &= \bigg(\Sigma p(x) \bigg) H(Y | X = x) \\
&= - \Sigma p(x) \cdot \Sigma p(y|x) \log p(y | x) \\
&= - \Sigma \Sigma p(x) p(y | x) \log p(y | x) \\
&= - \Sigma \Sigma p(x, y) \log p(y | x) \\
\end{aligned}
$$

> [!Note] Example
> 테이블..


| Y \ X | 1   | 2   |
| :---: | :-: | :-: |
|   1   | 1/4 | 1/4 |
|   2   | 1/4 | 1/4 |

$H(X, Y)$ 인 joint entropy 가 total entropy, $H(Y|X)$ 는 partial entropy.

> 중간고사 때 이런 계산 문제가 나올 수 있나봄

# Chain Rule
$H(X, Y) = H(X) + H(Y|X)$ 
앞서 살펴본 정의(bayes' rule, conditional entropy 등)를 이용하여 유도할 수 있음

chain rule을 이용해서 두 개의 확률 변수로 이루어진 join entropy에서 여러 개의 확률 변수를 이용한 entropy 계산으로 이어질 수 있다고 하시는 것 같음

- $H(X, Y | Z) = H(X | Z) + H(Y | X, Z)$ 
- 확률변수 $Z$ 를 없애면 앞선 정의와 동일함

---

***손을 써서 직접 계산해보는게 매우 중요하다고 하심***
머리만 써서 하면 안된다고 함...
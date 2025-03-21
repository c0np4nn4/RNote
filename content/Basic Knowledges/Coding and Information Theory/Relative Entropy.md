확률 변수(random variable)에 대한 엔트로피는 해당 확률변수의 불확실성(uncertainty)을 측정하는 방법입니다. 다시 말해, 확률 변수를 기술하기 위해 필요한 정보의 평균을 의미합니다.

상대 엔트로피(Relative entropy)는 쿨백-라이블러 발산(Kullback-Leibler divergence)이라고도 불리며, <u>두 분포 간의 거리를 측정</u>하는 방법 입니다. 아래와 같이 정의할 수 있습니다.

## Definition.
두 확률 질량 함수(probability mass function; pmf) $p(x) \text{ and } q(x)$에 대하여
$$
\begin{aligned}
D(p||q) &= \sum_{x\in\mathcal{X}} p(x) \log\frac{p(x)}{q(x)} \\
&= E_p \log \frac{p(X)}{q(X)}
\end{aligned}
$$
이는 실제 분포가 $p$ 일 때, 추정하는 분포가 $q$ 라고 두고 얼마만큼의 '비효율성(inefficiency)'을 보이는지 측정할 때 사용된다고 이해할 수 있습니다.

## Example
본 예시를 통해 상대 엔트로피가 비대칭적(asymmetric)임을 확인할 수 있습니다.

집합 $\mathcal{X} = \{0, 1\}$ 와 이에 대한 두 분포 $p, q$ 가 아래와 같이 정의되었다고 해보겠습니다.
$$
\begin{aligned}
p(x)\begin{cases}r &\text{if} &x = 1 \\ 1-r & \text{if} & x= 0\end{cases} \\
q(x)\begin{cases}s &\text{if} &x = 1 \\ 1-s & \text{if} & x= 0\end{cases}
\end{aligned}
$$

이에 대한상대 엔트로피를 아래와 같이 구할 수 있습니다.

$$
\begin{aligned}
D(p||q) = (1-r) \log \frac{1-r}{1-s} + r \log \frac{r}{s} \\
D(q||p) = (1-s) \log \frac{1-s}{1-r} + s \log \frac{s}{r}
\end{aligned}
$$
만약 $r=s$ 이면, $D(p||q) = D(q||p) = 0$ 을 만족합니다. (여기서 $0\log\frac{0}{0} = 0$ 등 여러 컨벤션을 활용합니다.)

이와 달리, $r=1/2, s=1/4$ 와 같은 $r \neq s$ 상황이면, 아래와 같이 서로 다른 값이 나옵니다.

$$
\begin{aligned}
D(p||q) = (1/2) \log \frac{1/2}{3/4} + (1/2) \log \frac{1/2}{1/4} = 0.2075 \\
D(q||p) = (3/4) \log \frac{3/4}{1/2} + (1/4) \log \frac{1/4}{1/2} = 0.1887
\end{aligned}
$$

따라서, $D(p||q) \neq D(q||p)$ 입니다. 직관적으로는 이상한 결과일 것입니다. 똑같은 두 분포 $p, q$ 에 대한 '상대 엔트로피'를 구했는데 서로 결과값이 다르기 때문입니다. 따라서, 엄밀하게 상대 엔트로피는 '거리'를 구하는 방법은 아니지만 '거리'로 간주하고 사용하는 것이 종종 유용하기 때문에 그렇게 사용된다고 합니다.
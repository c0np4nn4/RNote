>  ⚠ 초안입니다.

## Abstract
`Reed-Solomon (RS)code family`는 quasi-linear *probabilistically checkable proofs* (PCPs)와 *perfect zero knowledge* + *polylogarithmic verifier* 를 달성한 interactive oracle proofs (IOPs)를 설계하는데 매우 중요한 역할을 합니다.
이 때, RS code에 속하는지에 관한 문제(membership proving problem)이 ==큰 계산적 복잡도를 가진다는 점==이 이러한 PCP, IOP를 전개하는 데 있어 큰 장애물이 됩니다.

이 문제에서 나아가기 위해, 본 논문에서는 새로운 형태의 RS code에 대한 *interactive oracle proof of proximity* (IOPP)를 제시합니다. ***Fast RS IOPP (FRI)*** 라는 이름을 붙였는데, 그 이유는 아래와 같습니다.
1. Fast Fourier Transform (FFT)와 유사한 방식으로 설계되었습니다.
2. Prover의 계산 복잡도는 엄격하게 선형적이고 Verifier는 엄격하게 로그복잡도(logarithmic complexity)를 갖습니다.
**FRI** 이전의 IOPP들과 PCPs of proximity (PCPPs)는 *super-linear*의 증명 시간을 필요로 한 것에 비하면 이는 많은 발전으로 볼 수 있습니다.

블록 길이가 $N$인 코드에 대하여, (interactive) **FRI** prover의 산술 복잡도(arithmetic complexity)는 $6 \cdot N$ 보다 작습니다. 
**FRI** verifier의 산술 복잡도는 $\le 21 \cdot \log N$ 이며, 쿼리 복잡도(query complexity)는 $2 \cdot \log N$이고 *constant soundness*를 가집니다.
여기서 *constant soundness*란, code rate에 주로 의존하는 값인 양의 상수 $\delta_0$에 대하여, $\min \{ \delta \cdot (1 - o(1)), \delta_0 \}$ 의 확률로 $\delta-\text{far}$인 (code)word 는 Reject 함을 의미합니다.

특히 **FRI**를 통해 얻은 *query complexity* + *soundness* 조합은 이전에 제시된 *quasilinear PCPP* 나 심지어 더 엄밀한 *soundness analysis*보다 더 나음을 보입니다.
결론적으로, **FRI**를 이용하면 더 나은 ==zero knowledge proof==이나 ==argument system==을 만들 수 있을 것으로 보입니다.

**FRI** 이전의 효율적이라 논해진 PCPPs, IOPPs 들은 soundness에 있어 매 round에서의 "proof composition"에서 계속되는 *multiplicative factor loss* 때문에 최대 $O(\log \log N)$의 round를 거쳐야만 했습니다.
본 논문에서는 $\delta$가 코드의 unique decoding radius 보다 작을 때, **FRI**는 오직 무시할만한 수준의 *additive loss*만을 soundness에서 겪음을 보입니다.
이러한 관찰은 "proof composition" round를 $\Theta(\log N)$까지 증가시킬 수 있도록 해주고, 고정된 soundness에 대해 prover와 verifier의 running time을 줄이게 됩니다.

---

## Introduction
**Family of Reed-Solomon (RS) code**는 대수 부호 이론(algebraic coding theory)와 이론 컴퓨터 과학(theoritic computer science)연구 분야의 근본적인 개념입니다.

유한체 $\mathbb{F}$에 속하는 $N$개의 원소로 구성된 평가 집합(evaluation set) $S$와 *rate*에 관한 인자인 $\rho \in (0, 1]$에 대하여, RS code인 $\texttt{RS}[\mathbb{F}, S, \rho]$는 함수 $f: S \rightarrow \mathbb{F}$에 대한 평가(evaluations)들로 구성된 공간으로, 함수 $f$의 차수는 $d < \rho N$ 을 만족합니다.

> [!Tip] 예시
> 예를 들어, $S$의 원소 개수가 $N=4$이고, rate $\rho = 0.5$라고 하겠습니다.
> 
> $f: S \rightarrow \mathbb{F}$ 는 $S$의 원소가 유한체 $\mathbb{F}$ 상의 어떤 원소로 매핑됨을 의미합니다.
> 
> *rate*는 |원본 메세지| / |코드워드 길이| 이므로, 이 경우에는 원본 메세지의 길이가 $N=4$이고 코드워드의 길이가 $|C| = N / \rho = 4 \times 2 = 8$ 임을 알 수 있습니다.
> 
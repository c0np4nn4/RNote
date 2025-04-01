# Fundamentals on Probability space
Euclidean vector space가 **norm**, **inner product**가 정의된 벡터 공간($\mathbb{R}^n$)인 것과 유사하게 확률 공간(Probability space)은 ***Sample space*** $\Omega$, ***Event space*** $\mathcal{B}$, ***Probability function*** $P$ 로 구성되어 있고 나름의 성질들을 만족한다.

$$
(\Omega, \mathcal{B}, P)
$$
## 1. Sample space
Sample space $\Omega$는 실험(experiment or trial)의 가능한 모든 결과(outcome)의 집합을 의미한다.

즉, 동전 던지기의 경우 $\Omega=\{H, T\}$ 가 되고, 주사위 굴리기의 경우 $\Omega=\{1, 2, 3, 4, 5, 6\}$ 이 된다.

## 2. Event space
Event space $\mathcal{B}$는 Sample space의 부분집합 중 아래 세 성질을 만족하는 것들로 정의된다.

1. $\emptyset \in \mathcal{B}$
2. $A \in \mathcal{B} \rightarrow A^c \in \mathcal{B}$
3. $A_1, A_2, \cdots \in \mathcal{B} \rightarrow \cup_{j=1}^{\infty} A_j \in \mathcal{B}$

이 중 1, 2번 성질에 의해 가장 작은 Event space 는 아래와 같이 공집합(empty set)과 표본공간(sample space)를 모두 갖고 있는 부분집합이 됨을 쉽게 알 수 있다.

$$
\{\emptyset, \Omega\}
$$
또, 2, 3번 성질에 대해 아래를 생각해볼 수 있다.
3번 성질의 전제인 $A_1, A_2, \cdots \in \mathcal{B}$ 에 대해 2번 성질에 의해 $A_1^c, A_2^c, \cdots \in \mathcal{B}$ 임을 알 수 있다.
그럼 3번 성질에 따라 $A_1^c, A_2^c, \cdots \in \mathcal{B} \rightarrow \cup_{j=1}^{\infty} A_j^c \in \mathcal{B}$ 이다. 이를 풀어서 적으면

$$
\begin{aligned}
(A_1^c \cup A_2^c \cup \cdots ) \in \mathcal{B}
\end{aligned}
$$
다시 성질 2번에 따라 여집합이 $\mathcal{B}$ 에 있어야 하므로,

$$
\begin{aligned}
(A_1^c \cup A_2^c \cup \cdots )^c \in \mathcal{B}
\end{aligned}
$$
드모르간의 법칙으로 정리하면

$$
\begin{aligned}
(A_1 \cap A_2 \cap \cdots ) \in \mathcal{B} \\
\therefore \cap_{j=1}^{\infty} A_j \in \mathcal{B}
\end{aligned}
$$

즉, Event space의 원소간 합집합(union), 교집합(intersection), 여집합(complement)이 모두 원소가 되어야 함을 의미한다.
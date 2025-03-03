---
title: Constant-Size Commitments to Polynomials and Their Applications
tags:
  - cryptography
  - commitment
  - Paper
---
# 0. Abstract
본 논문에서는 **Polynomial Commitment**에 대해 정의하고, 두 가지 효율적인 구조를 제공합니다. **Polynomial Commitment**는 커밋하는 사람(`committer`)이 다항식에 대한 짧은 string ($\pi$)을 만들 수 있게 합니다. 검증하는 사람(`verifier`)은 커밋된 어떤 계산된(evaluated) 값이 커밋된 다항식 상에서 계산된 것이 맞는지 검증하는 과정에서 이 string을 사용하게 됩니다. 즉, 개념적으로는 아래 순서를 따르는 것으로 이해할 수 있습니다.

<center>

| **Committer**         | $\leftrightarrow$ | **Verifier**       |
| --------------------- | :---------------: | ------------------ |
| Define polynomial     |                   |                    |
| Commit to polynomial  |                   |                    |
| send short commitment | $\rightarrow$     | Receive commitment |
| Send evaluation proof | $\rightarrow$     | Receive proof      |
|                       |                   | Verify proof       |
|                       |                   | Confirm evaluation |

</center>

*homomorphic commitment* 스킴을 이용하면 이러한 과정을 수행할 수 있음이 알려져 있습니다. 하지만,  *homomorphic commitment* 스킴은 커밋의 대상이 되는 다항식의 차수(degree)에 따라 선형적으로 커밋먼트의 크기가 증가합니다.

본 논문에서 제시하는 방법은 이와달리 상수(constant)로 일정합니다. 커밋먼트에 대한 오프닝의 오버헤드도 마찬가지로 상수입니다.여러 개의 evaluation에 대한 opening도 constant한 양의 communication overhead만 필요로 합니다.

따라서, 암호학적 프로토콜들에 대해 본 논문이 제시하는 스킴을 사용하면 communication cost를 많이 낮출 수 있습니다. 이를 보여주기 위해 본 논문에서는 아래 네 종류의 Application을 제시합니다.

- Verifiable Secret Sharing
- Zero-Knowledge Sets
- Credentials
- Content Extraction Signatures

# 1. Introduction
[Commitment Scheme]은 여러 암호학적 프로토콜(cryptographic protocol)들의 주요 구성요소 입니다. ***Commitment Scheme***은 커밋하는 사람(*Committer*)이 `commitment`라 부르는 어떤 값을 공표할 수 있게 합니다. 이 커밋먼트(`commitment`)는 커밋의 대상이 되는 메세지와 연관(==binding==)되고 이 메세지 자체를 드러내지는 않는(==hiding==) 성질을 갖기도 합니다. 이후에 *Committer*는 *open* 단계에서 이 `commitment` 와 `committed message`를 검증하는 사람(*Verifier*)에게 공개할 수 있습니다. *Verifier*는 `committed message`가 `commitment`와 일관되는(consistent) 성질을 만족하는지 검증할 수 있습니다.

우선 *commit* 방법으로 잘 알려진 세 종류에 대해 살펴볼 수 있습니다. 아래 구조들에서 Prime order $p$ 인 Group $\mathbb{G}$에 대하여, 임의의 생성자(generator) $g, h \in \mathbb{G}$ 를 가정합니다. 

> [!Note] 이산로그문제(Discrete Logarithm Problem; DLP) 기반
> 
> *Committer*는 $\mathbb{Z}_p$ 상에서 무작위로 선택된 `message` $m \in_R \mathbb{Z}_p$ 에 대하여 아래와 같이 `commitment`를 얻을 수 있습니다.
> 
> $$
> \mathcal{C}_{<g>}(m)=g^m
> $$
> 	이 방식의 스킴은 무조건 *binding* 을 만족하고, $\mathbb{G}$ 에서 DLP의 가정을 기반으로 계산적으로 *hiding*을 만족합니다.

> [!Note] Pedersen Commitment 기반
> Crypto '91에서 발표된 [Pedersen commitment](https://link.springer.com/chapter/10.1007/3-540-46766-1_9)를 기반으로 하는 구조입니다. 아래와 같이 수식으로 표현됩니다. 이 때, $r \in_R \mathbb{Z}_p$ 인 무작위 값 $r$ 을 선택하여 활용합니다.
> 
> $$
> \mathcal{C}_{<g, h>}(m, r) = g^mh^r
> $$
> 이 방식의 스킴은 무조건 *hiding* 을 만족하고, DLP 가정을 기반으로 계산적으로 *binding* 을 만족합니다.

> [!Note] 해시 기반
> *Committer*는 일방향(one-way)함수인 $H$를 이용해 아래와 같은 방식으로 `commitment`를 publish 할 수 있습니다.
> 
> $$
> H(m) \;\;\text{ or }\;\; H(m ||r)
> $$
> 실제로 충돌 저항성이 있는(collision-resistant) 해시 함수가 종종 사용됩니다.

commitment schemes에 대한 자세한 내용은 Ivan Damgard의 [survey paper](https://cs.au.dk/~ivan/ComZK05.pdf)를 통해 더 자세히 살펴볼 수 있습니다.

---

이제 단순히 "`message`"가 아닌 임의의 다항식 $\phi(x) \in_R \mathbb{Z}_p[x]$ 에 대해 커밋하는 방법을 생각해볼 수 있습니다. 이 문제는 [verifiable secret sharing]과 밀접한 관련이 있습니다.

$\phi(x)$의 차수가 $t$이고 계수가 $\phi_0, \dots, \phi_t$ 라고 가정해보겠습니다. $\phi(x)$에 대해 `커밋`하는 방법으로 계수를 이어붙인 string $(\phi_0 | \phi_1 | \cdots | \phi_t)$ 또는 어떤 특정한 string representation으로 다항식 $\phi(x)$ 를 표현한 뒤 해당 string 값에 대해 커밋하는 방법을 생각할 수 있습니다. 그리고, 이 **커밋하는 방법**이 무엇이냐에 따라 $\phi(x)$로 unique하게 결정되는 **constant size**의 `commitment`를 publish 할 수도 있습니다.

하지만, 이는 `commitment`에 대한 opening에 제한을 가할 수 있는데, 바로 다항식 $\phi(x)$ 전체를 드러내야 한다는 점입니다. "다항식 전체를 드러낸다"라는 점은 *verifiable secret sharing*과 같은 application에는 적합하지 않은 구조입니다. *verifiable secret sharing*에서는 다항식의 평가점(evaluation)들이 서로 다른 주체(party)에게 공개가 되어야 합니다. 즉 $\phi(i) \text{ for } i \in \mathbb{Z}_p$ 만을 공개하는 것입니다.

"다항식 전체를 드러내는 문제"를 해소하는 방법으로 **계수에 대해 커밋**하는 방법이 있습니다. 즉, 아래와 같이 `commitment` $\mathcal{C}$ 를 생성하는 것입니다.

$$
e.g., \;\mathcal{C} = (g^{\phi_0}, g^{\phi_1}, \dots, g^{\phi_t})
$$
이를 이용하면 *Verifier*가 `polynomial evaluation`인 $\phi(i)$가 `commitment`와 *consistent* 한지 쉽게 확인할 수 있습니다.

하지만, 차수 $t$ 가 증가함에 따라 $t+1$ 개의 계수도 증가하기 때문에 `commitment size`가 선형적으로 증가한다는 문제가 존재합니다.

## Contribution in this Paper
본 논문의 주요 기여는 다항식 $\phi(x) \in \mathbb{Z}_p[x]$ 에 대하여 ***bilinear pairing group*** 상에서의 커밋 스킴인 $\texttt{PolyCommit}_{\text{DL}}$을 제시한 점입니다. 이 스킴은 `commitment`의 크기가 *single group element*로 상수이며, *Committer*가 다항식의 적법한 평가 $\phi(i)$에 대하여 $witness$라 불리는 원소와 함께 `Open` 과정을 수행할 수 있고, *Verifier*가 이 값들을 사용하여 $\phi(i)$가 실제로 다항식 $\phi(x)$의 $i$ 에서의 평가된 값임을 확인할 수 있게 합니다.

구조(construction)는 다항식 $\phi(x) \in \mathbb{Z}_p[x]$의 대수적 성질에 기반하는데, 이는 $\forall i \in \mathbb{Z}_p$인 $i$에 대하여, $(x-i)$가 다항식 $\phi(x) - \phi(i)$ 를 **완벽하게** 나눌 수 있다는 점을 활용합니다.

`hiding` 성질은 이산로그문제의 어려움에 기반합니다. 그리고, `binding` 성질은 SDH(strong diffie-hellman) 가정에 기반하여 증명되었습니다.

Pedersen commitment에서 사용한 기술을 활용하여, 더 강력한 커밋먼트 스킴으로 $\texttt{PolyCommit}_{\text{Ped}}$ 도 제시합니다. 이는 무조건 `hiding`을 만족하고, SDH 가정을 기반으로 하여 계산적으로 `binding` 성질을 가집니다.

Evaluation 값들의 집합 $\{\phi(i):i\in S \}$가 있을 때, 이들을 동시에 `open`하는 것을 생각해볼 수 있습니다. 이를 **batch opening**이라 부르고, 이 때의 오버헤드는 여전히 *single witness element*로 일정합니다. batch opening의 보안성(security)은 *bilinear* 버전의 SDH인 `BSDH` 문제가 어렵다는 것에 기반합니다. 더불어, 본 논문의 스킴은 homomorphic이고 쉽게 randomizable 합니다. *communication cost*를 줄이려는 다른 연구들에서와 마찬가지로 'global system parameter'는 다소 큽니다(이 경우에는 다항식의 차수 $t$에 따른 $O(t)$). '전송하는 비트 수를 줄인다'와 같은 *communication complexity* 를 줄이는 목표 달성을 보여주기 위해 본 논문에서는 아래 네 가지 Application에 $\texttt{PolyCommit}$ 을 적용하여 제시합니다. 

Feldman Verifiable secret sharing(VSS) protocol
프로토콜 참여자가 $n$ 명일 때, 브로드캐스트 하는 데이터 사이즈가 $O(n)$인 것이 가장 효율적이라 알려진 것에 반해 $\texttt{PolyCommit}$을 사용하면 $O(1)$으로 줄일 수 있음을 보입니다.

ZKS (relaxed type)
ZKS(zero-knowledge set)는 임의의 집합 $S$ 에 대하여, *Committer*가 어떤 값 $i$에 대하여 $i\in S, \;\;\text{ or }\;\; i \notin S$ 여부를 $S$ 에 대한 어떠한 정보도 드러내지 않으면서 증명하는 `commitment scheme`을 의미합니다. 본 논문에서는 *nearly zero-knowledge sets* 라는 이름으로, 커밋된 집합의 "크기"를 숨기려는 시도를 하지 않는 ZKS를 정의합니다. ==크기를 숨기지 않으려는 것==만으로도 대부분의 ZKS application에서는 충분하고, 기존에는 membership proof을 위한 cost로 non-constant communication을 수행해야 했던 것을 constant-size proofs로 대체 할 수 있음을 보입니다. 나아가 zero-knowledge elementary database(ZK-DEB)에서도 이를 적용할 수 있음을 보입니다.

Content Extraction Signature (CES) scheme
**batch opening**을 이용하는 방식입니다. CES 스킴은 signature를 갖고 있는 사람이 `signed message`의 일부를 추출할 수 있게 해주는 스킴입니다. 본 논문에서의 커밋먼트 스킴을 사용해서 CES 싐을 만들었을 때 가장 효율적으로 알려진 CES 스킴과 비슷하게 효율적인 스킴임을 보여줍니다.

# 2. Preliminaries
# 3. Polynomial Commitment
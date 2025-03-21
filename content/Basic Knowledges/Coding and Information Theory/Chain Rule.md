결합 엔트로피([[Joint Entropy]])와 조건부 엔트로피([[Conditional Entropy]])간에 체인룰([[Chain Rule]])이라는 이름의 아래 정리를 살펴볼 수 있습니다.

## Theorem. "Chain Rule"
$$
H(X, Y) = H(X) + H(Y|X)
$$
### Proof.
$$
\begin{aligned}
H(X, Y) &= - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}}p(x, y) \log p(x, y) \\
&= - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log p(x) p(y|x) \;\; (\because \text{Bayes' Rule}) \\
&= - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log p(x) - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log p(y|x) \\
&= - \sum_{x \in \mathcal{X}} p(x) \log p(x) - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log p(y|x) \\
&= H(X) + H(Y|X) \;\; (\because \text{엔트로피 정의})
\end{aligned}
$$
같은 의미지만, 위 식에서 $\log p$ 부분을 주목하여
$$
\log p(X, Y) = \log p(X) + \log p(Y|X)
$$
위 식에 기대값(Expectation)을 곱해 체인룰 식을 얻는 것도 가능합니다.

## Corollary
$$
H(X, Y | Z) = H(X|Z) + H(Y|X, Z)
$$
위 증명과 같은 방식으로 간단히 증명할 수 있습니다.
조금 더 직관적인 방법으로는, $Z$ 값이 이미 주어진 값임을 생각하면 체인룰 식과 동일한 형태임을 알 수 있습니다.

## Remarks
아래 식들은 체인룰에 관한 여러 사실들입니다.

(1)
$$
H(Y) - H(Y|X) = H(X) - H(X|Y)
$$
조건부 엔트로피를 각자 반대편으로 넘기면 $H(X, Y)$로 같아짐을 알 수 있습니다.

(2)
$$
H(X, Y) = H(X) + H(Y|X) = H(Y) + H(X|Y)
$$

(3)
$$
\text{If } H(X) \neq H(Y) \text{, then } H(Y|X) \neq H(X|Y) 
$$

---

(+) [[Conditional Entropy]]의 Example 2를 통해, 주변 분포(marginal distribution) 값을 알고, 조건부 엔트로피 값을 구할 수 있으면 결합 엔트로피 값을 쉽게 계산할 수 있음을 생각해볼 수 있습니다.
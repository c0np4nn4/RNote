조건부 상대 엔트로피([[Conditional Relative Entropy]])는 확률 질량함수 $p(x)$에 대한 조건부 확률 질량 함수인 $p(x|y)$ 그리고 $p(y|x)$ 간의 상대 엔트로피([[Relative Entropy]])의 평균을 의미합니다.

## Definition
결합 확률 질량 함수 (joint pmf) $p(x, y)$ 그리고 $q(x, y)$에 대하여 **조건부 상대 엔트로피**([[Conditional Relative Entropy]]) $D\big(\,p(y\,|\,x) \;|| \;q(y\,|\,x)\,\big)$ 는 아래와 같이 정의됩니다.

$$
\begin{aligned}
D\big(\,p(y\,|\,x) \;|| \;q(y\,|\,x)\,\big) &= \sum_x p(x) \sum_y p(y|x) \log \frac{p(y|x)}{q(y|x)} \\
&= \sum_x \sum_yp(x)p(y|x) \log \frac{p(y|x)}{q(y|x)}\\
&= \sum_x \sum_yp(x, y) \log \frac{p(y|x)}{q(y|x)} &(\because \text{ 조건부 확률})\\ 
&=E_{p(x, y)} \log \frac{p(Y|X)}{q(Y|X)}
\end{aligned}
$$

---
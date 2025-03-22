[[Conditional Relative Entropy]]에서의 정의를 이용해 [[Relative Entropy]]에 대한 [[Chain Rule]]을 적용할 수 있습니다.

## Theorem
$$
\begin{aligned}
D\big(\,p(x\,,\,y) \;|| \;q(x\,,\,y)\,\big) = D\big(\,p(x) \;|| \;q(x)\,\big)  + D\big(\,p(y\,|\,x) \;|| \;q(y\,|\,x)\,\big) 
\end{aligned}
$$
즉, 두 결합 확률 분포 $p(x, y), q(x, y)$ 간의 "거리"([[Relative Entropy]]에서도 밝혔듯이 실제 "거리"는 아니지만 그러한 의미로 사용)는 두 확률 분포 $p(x), q(x)$간의 "거리" 와 두 조건부 확률 분포 $p(y|x), q(y|x)$ 간의 "거리"를 더한 것이 됨을 의미합니다.

### Proof
$$
\begin{aligned}
D\big(\,p(x\,,\,y) \;|| \;q(x\,,\,y)\,\big) &= \sum_x\sum_y p(x, y) \log \frac{p(x, y)}{q(x, y)} \\
&= \sum_x\sum_yp(x, y)\log \frac{p(x)p(y|x)}{q(x)q(y|x)} &(\because \text{조건부 확률})\\ 
&= \sum_x\sum_y p(x, y) \log \frac{p(x)}{q(x)} + \sum_x\sum_yp(x, y) \log \frac{p(y|x)}{q(y|x)} \\
&= D\big(\,p(x) \;|| \;q(x)\,\big) + D\big(\,p(y\,|\,x) \;|| \;q(y\,|\,x)\,\big)
\end{aligned}
$$
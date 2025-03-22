[[Conditional Mutual Information]]으로부터 아래와 같이 [[Interaction Information]] 개념을 생각할 수 있습니다.

$$
I(X;Y;Z) = I(X;Y) - (X;Y|Z)
$$
[[Mutual Information]]의 정의와 [[Chain Rule]]을 이용해 식을 정리하면 아래와 같이도 적을 수 있습니다.

$$
I(X;Y;Z) = H(X) + H(Y) + H(Z) - \{H(X, Y) + H(X, Z) + H(Y, Z)\} +H(X, Y, Z)
$$

이를 벤 다이어그램으로 나타내면 좀 더 직관적으로 이해할 수 있습니다.

![[Pasted image 20250321203108.png]]
$$
| < \texttt{a}, \texttt{b} > | \le || \texttt{a} || || \texttt{b} ||
$$
- When $\texttt{a} \text{ and } \texttt{b} \neq 0$, $-1 \le \frac{<\texttt{a}, \texttt{b}>}{||\texttt{a}|| || \texttt{b} || } \le 1$
- $<\texttt{a}, \texttt{b}> = || \texttt{a} || \cdot || \texttt{b} || \cos \theta$

## Proof
$$
\begin{aligned}
0 &\le || \texttt{a} - \lambda \texttt{b}||^2, \text{ for any } \lambda \in \mathbb{R} \\
&= <\texttt{a} - \lambda \texttt{b}, \texttt{a} - \lambda\texttt{b}> \\
&= <\texttt{a}, \texttt{a}> -2 \lambda < \texttt{a}, \texttt{b}> + \lambda^2<\texttt{b}, \texttt{b}> \\
&= <\texttt{a}, \texttt{a}> - \frac{|< \texttt{a}, \texttt{b}>|^2}{<\texttt{b}, \texttt{b}>} \;\; (\text{ let } \lambda= \frac{<\texttt{a}, \texttt{b}>}{<\texttt{b}, \texttt{b}>}) \\

\therefore |<\texttt{a}, \texttt{b}>|^2 &\le || \texttt{a}||^2 ||\texttt{b}||^2
\end{aligned}
$$
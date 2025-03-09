## Definition

> [!Important] Def. **Euclidean Vector Space**
> A **Euclidean vector space** is a vector space, $\mathbb{R}^n$, equipped with the euclidean distance (**norm**) and **innder product**.
> Any element, $\texttt{x}$, in $\mathbb{R}^n$ is called a vector and is given by
> $$
> \texttt{x}=[x_1, x_2, \cdots, x_n]^T,
> $$
> where $x_j \in \mathbb{R}$

---


> [!Important] Def. **norm**
> $|| \cdot ||$ is called (standrad) **norm** in $\mathbb{R}^n$ and is given by,
> $$
> || \texttt{a} || = \sqrt{a_1^2 + a_2^2 + \cdots a_n^2},
> $$
> where $\texttt{a} \in \mathbb{R}^n$

The *norm* must satisfy the following properties:
1. $|| \texttt{a} || \ge 0$, then $|| \texttt{a} || = 0 \Leftrightarrow \texttt{a} = \texttt{0}$
2. $|| c \texttt{a} || = |c| \, \cdot || \texttt{a} ||$
3. $|| \texttt{a} + \texttt{b} || \le || \texttt{a} || + || \texttt{b} ||$ (*[[triangle inequality]]*)
where $\forall \texttt{a}, \texttt{b} \in \mathbb{R}^n \text{ and } c \in \mathbb{R}$

One can also define any norm, named $|| \cdot ||_{any}$, if it satisfies all of the above properties.

---

> [!Important] Def. **inner product**
> $<\cdot, \cdot>$ is called the (standrad) **inner product** (or dot product) and is defined by,
> $$
> < \texttt{a}, \texttt{b} > = \texttt{a}^T \texttt{b} = \sum_{j=1}^n a_j b_j,
> $$
> where $\texttt{a}, \texttt{b} \in \mathbb{R}^n$

The *inner product* must satisfy the following properties:
1. $<\texttt{a}, \texttt{a}> \ge 0$, then $<\texttt{a}, \texttt{a}> \Leftrightarrow \texttt{a} = \texttt{0}$
2. $< \texttt{a}, \texttt{b} > = <\texttt{b}, \texttt{a}>$
3. $<c \, \texttt{a}, \texttt{b}> = c<\texttt{a}, \texttt{b}>$
4. $<\texttt{a} + \texttt{b}, c> = <\texttt{a}, \texttt{c}> + <\texttt{b}, \texttt{c}>$
where $\forall \texttt{a}, \texttt{b} \in \mathbb{R}^n \text{ and } \texttt{c} \in \mathbb{R}^n$

One can also define any inner product $< \cdot, \cdot >_{any}$, if it satisfies all of the above properties.

## Properties
For arbitrary vectors $\texttt{a} \text{ and } \texttt{b} \in \mathbb{R}^n$,
1. **Inner product** induces the **norm**:
$$
\sqrt{<\texttt{a}, \texttt{a}} = || \texttt{a} ||
$$
2. ***[[Cauchy-Schwarz inequality]]***
$$
| < \texttt{a}, \texttt{b} > | \le || \texttt{a} || || \texttt{b} ||
$$
- When $\texttt{a} \text{ and } \texttt{b} \neq 0$, $-1 \le \frac{<\texttt{a}, \texttt{b}>}{||\texttt{a}|| || \texttt{b} || } \le 1$
- $<\texttt{a}, \texttt{b}> = || \texttt{a} || \cdot || \texttt{b} || \cos \theta$

3. $<\texttt{a}, \texttt{b}> = 0 \Leftrightarrow \texttt{a} \text{ and } \texttt{b} \text{ are } \textbf{orthogonal}$
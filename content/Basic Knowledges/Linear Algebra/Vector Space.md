## Definition

> [!Important] Def.
> A **Vector space** $\mathcal{V}$ is a set of elements (i.e., vectors) with two operations:
> Addition and scalar multiplication defined by,
> $$
> \begin{align*}
> c \texttt{x} &\in \mathcal{V} \\
> \texttt{x} + \texttt{y} &\in \mathcal{V}
> \end{align*}
> $$
> where $\texttt{x}, \texttt{y} \in \mathcal{V}$ and $c \in \text{Field}$.

### Notes
- The name "Vector" can have different meanings depending on the space on which it is defined. 
- The examples of the $\text{Field}$ are $\mathbb{R}$ (the set of real numbers) and $\mathbb{C}$ (the set of complex numbers).
- In most cases, we are interested in a vector space over a $\mathbb{R}$.

---

## Examples

- $\mathbb{R}^n$ is the ==vector space==, where a vector $\texttt{x} \in \mathbb{R}^n$ is given by,
$$
\texttt{x} = \begin{bmatrix}x_1 \\ x_2 \\ \vdots \\x_n\end{bmatrix}, \; \text{ where } x_j \in \mathbb{R}
$$
- $\mathbb{R}^{m \times n}$ is also the ==vector space==, where a vector $A \in \mathbb{R}^{m\times n}$ is given by,
$$
A = \begin{bmatrix}a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \cdots & a_{mm}\end{bmatrix} = \begin{bmatrix}| & | & & | \\ \texttt{a}_1 & \texttt{a}_2 & \cdots & \texttt{a}_n\\ | & | & & |\end{bmatrix} = \begin{bmatrix}- & \texttt{a}^1 & - \\ - & \texttt{a}^2 & - \\ & \vdots & \\ - & \texttt{a}^m & -\end{bmatrix},
$$
where $a_{ij} \in \mathbb{R}, \; \texttt{a}_j \in \mathbb{R}^m, \; \text{ and } (\texttt{a}^j)^T \in \mathbb{R}^n$ which means $\texttt{a}_j$ is the vector in $\mathbb{R}^m$ vector space and $(\texttt{a}^j)^T$ is the vector in $\mathbb{R}^n$.

- $\mathcal{C}[a, b]$ is the ==vector space==, which is the set of *continuous functions* on the interval $[a, b]$.

---
## Q & A

1. The interval $[0, 1]$ is a set. Is this the vector space?
ans) It is not the *vector space*. One can easily think that the elements in the set violates the condition of definition (e.g., $0.6 + 0.5 \notin [0, 1]$ and $2 \times 0.7 \notin [0, 1]$)

2. Describe the zero vector (i.e., $\texttt{0}$), for each examples above. 
	1. For $\mathbb{R}^n$, $\texttt{0} = \begin{bmatrix}0 \\ 0 \\ \vdots \\ 0\end{bmatrix}$
	2. For $\mathbb{R}^{m \times n}$, $\texttt{0} = \begin{bmatrix}0 & 0 & \cdots & 0 \\ 0 & 0 & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & 0 \\ \end{bmatrix}$
	3. For $\mathcal{C}[a, b]$, $\texttt{0} = 0$

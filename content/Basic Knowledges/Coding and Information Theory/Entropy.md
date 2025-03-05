**Entropy** is a measure of [[Uncertainty]] and can also be thought of as the "expected amount of information."

### Definition

$$
H(X) = - \sum_{x \in \mathcal{X}} p(x) \log p(x) = \sum_{x\in\mathcal{X}} p(x) \log \frac{1}{p(x)}
$$
Note that $H(X)$ can be written as $E_p\left(\log\frac{1}{p(x)}\right)$, where $E_p$ denotes the expectation with respect to the probability distribution $p(x)$.

The logarithm base is often omitted and is typically assumed to be 2, corresponding to "bits" in information theory.

Entropy can be considered a functional of $p(x)$.

Moreover, entropy provides a lower bound on the number of bits required to represent (or describe) a random variable, making it a fundamental limit in *data compression*.


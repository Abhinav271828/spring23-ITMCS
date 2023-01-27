---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 27 January, Tuesday (Lecture 7)
author: Taught by Prof. Prasad Krishnan
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Entropy
## Fano's Inequality
Suppose that we have a Markov chain $X \to Y \to \hat{X}$, where $\hat{X}$ is an estimate of $X$ taken from $Y$. We would also like to estimate the probability of error
$$P_\text{error} = \text{Pr}(\hat{X} \neq X) = \sum_{x \neq \hat{x}} P_{X\hat{X}}(x,\hat{x}).$$

Fano's inequality relates this quantity to the uncertainty remaining in $Y$ once we know $X$:
$$P_\text{error} \geq \frac{H(Y \mid X)-1}{\log_2(|\mathcal{X}|-1)}.$$

To prove this, we define a new r.v. $E$, which is an indicator of the error:
$$E = \begin{cases} 1 & X \neq \hat{X} \\ 0 & X = \hat{X}. \end{cases}$$

Now, we have
$$\begin{split}
H(E, X \mid \hat{X}) &= H(E \mid \hat{X}) + H(X \mid E, \hat{X}) \\
&= H(X \mid \hat{X}) + H(E \mid X, \hat{X}) \\
&= H(X \mid \hat{X}).
\end{split}$$

We know that
$$H(E \mid \hat{X}) \leq H(E)$$
and that
$$H(X \mid E, \hat{X}) = \sum_e p_E(e)H(X \mid E=e, \hat{X}).$$
The second factor reduces to
$$\begin{split}
p_E(E = 0)H(X \mid E=0, \hat{X}) &+ p_E(E = 1)H(X \mid E=1, \hat{X}) \\
&= P_\text{error}H(X \mid E=1, \hat{X}),
\end{split}$$

so now we can write
$$H(X \mid \hat{X}) \leq H(E) + P_\text{error}H(X \mid E = 1, \hat{X}).$$

Rearranging,
$$P_\text{error} \geq \frac{H(X\mid\hat{X})-H(E)}{H(X \mid E=1,\hat{X})}$$

In this, $H(X \mid \hat{X}) \geq H(X \mid Y)$ (by the data processing inequality), $H(E) \leq 1$ (entropy of a Bernoulli variable), and $H(X \mid E=1, \hat{X}) \leq \log_2(|\mathcal{X}|-1)$ ($X$ can only take values not equal to $\hat{X}$). Therefore,
$$P_\text{error} \geq \frac{H(X \mid Y) - 1}{\log_2(|\mathcal{X}|-1)}.$$

# Source Coding
Consider a sequence of $n$ independent r.vs. $X_i$, each drawn from a distribution $q$ over a finite set $\mathcal{X}$ (*independent identically distributed*, or i.i.d, random variables). Let $\mathcal{X} = \{a_1, \dots, a_{|\mathcal{X}|}\}.$

Define
$$N_\mathbf{x}(a) = |\{j : x_j = a\}|$$
as the number of occurrences (frequency) of $a_i$ in the tuple $\mathbf{x}$.  
We can say that, asymptotically, $\frac1n N_\mathbf{x}(a)$ tends to $q(a)$. This can be proved by the central limit theorem.

We would like to analyse the probability distribution of a random sequence of length $n$, for some large $n$. We expect this to be
$$\lim_{n \to \infty} P_\mathbf{X}(\mathbf{x}) = \prod_{i=1}^{|\mathcal{X}|} q(a_i)^{n \cdot q(a_i)}.$$
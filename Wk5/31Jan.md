---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 31 January, Tuesday (Lecture 8)
author: Taught by Prof. Prasad Krishnan
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Source Coding (contd.)
We have seen that
$$\lim_{n \to \infty} P_\mathbf{X}(\mathbf{x}) = \prod_{i=1}^{|\mathcal{X}|} q(a_i)^{n \cdot q(a_i)}.$$

We can now take the log on both sides
$$\lim_{n \to \infty} \frac1n \log P_\mathbf{X}(\mathbf{x}) = \sum_{i=1}^{|\mathcal{X}|} q(a_i) \log q(a_i) = -H(X).$$

Thus we have that
$$\lim_{n \to \infty} P_\mathbf{X}(\mathbf{x}) = 2^{-nH(X)}.$$

Suppose we wish to encode $\mathbf{X}$ (in terms of bits), in a manner that can be decoded to get $\mathbf{X}$ back as accurately as possible. We call the decoded output $\mathbf{\hat{X}}$ – thus we want to minimise $P(\mathbf{\hat{X}} \neq \mathbf{X}) = P_\text{error}$.

We know that if $P_\text{error} = 0$, then we need at least $n\lceil H(X) \rceil$ bits for typical (specifically, frequency typical) sequences; for all sequences, we would need $n\lceil \log |\mathcal{X}| \rceil$ bits.  
Typicality can be defined in two (non-equivalent) ways. A sequence $\mathbf{x}$ can be called typical if
$$N_\mathbf{x}(a_i) \approx nq(a_i)$$
for all $a_i \in \mathcal{X}$ (called *frequency typicality*), or if
$$P_\mathbf{X}(\mathbf{x}) \approx 2^{-nH(X)},$$
called *weak typicality*.

Note that a frequency typical distribution must be weakly typical, but the converse does not hold. For example, if the distribution is $\text{Bernoulli}(0.5)$, then a sequence with, say 900 zeroes and 100 ones will be weakly typical, but not frequency typical.
---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 03 January, Tuesday (Lecture 1)
author: Taught by Prof. Gowtham K
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Introduction
*Shannon's entropy*, or simply *entropy*, is a characteristic of discrete random variables.

Consider, for example, two r.vs. $X_1, X_2$ with PMFs defined as
$$\begin{split}
P_{X_1}(0) = \frac12 &; P_{X_1}(1) = \frac12 \\
P_{X_2}(0) = 0.01 &; P_{X_2}(1) = 0.99
\end{split}$$

We can see that it is, intuitively speaking, "harder" to guess the value of $X_1$ – it is more *uncertain*. This is the notion formalised by (binary) entropy, which is defined as
$$H(X) = -p \log p - (1-p) \log (1-p) := h(p),$$
where $p = P_X(1) = 1 - P_X(0)$. In other words, entropy is the expected value of the logarithm of the probability values.  
It is easy to check that $H(X_1) > H(X_2)$ – in general, uniform r.vs. have the highest entropy of all r.vs. over the same support.

The following questions can be answered by entropy:
* Consider $n$ points in $\mathbb{R}^3$. Suppose that these points form $n_1$, $n_2$ and $n_3$ distinct projections in the $xy$-, $yz$- and $zx$-planes respectively. Can we form an upper bound on $n$ in terms of $n_1, n_2, n_3$?
* What is an upper bound on the number of perfect matchings in a bipartite graph?
* Consider a fair coin $P$ that lands on heads or tails with equal probability, and a biased one $Q$ that lands on heads with probability $\frac12 - \varepsilon$ and tails with probability $\frac12 + \varepsilon$. Let the outcomes of $n$ coin tosses of these coins be $x^n = (x_1, \dots, x_n)$, and consider a function $x^n \to \{P, Q\}.$ What is a lower bound on $n$ such that
$$\operatorname*{Pr}_{x^n \sim p^n} [A(x^n) = 0] \geq 1 - \varepsilon$$
$$\operatorname*{Pr}_{x^n \sim q^n} [A(x^n) = 1] \geq 1 - \varepsilon$$
* Suppose we have $n$ r.vs. $X_1, \dots X_n$, drawn from an unknown distribution $P_X$. How can we create more samples $x_{i > n}$?
* Given a secret r.v. $X$ and an observed r.v. $Y$, how much information does $Y$ "leak" about $X$?
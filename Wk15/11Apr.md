---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 11 April, Tuesday (Lecture 22)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Information Leakage
The model we use to study information leakage posits a r.v. $X$, which represents some sensitive data, and an observation $Y$ of this data by an adversary. The two r.vs. are related by a distribution $P_{Y \mid X}$.

We now ask the question "how much information does the observed data $Y$ reveal about the correlated data $X$?" The information leakage is quantified by the difference between the uncertainty in $X$ and the uncertainty left in $X$ after observing $Y$. This corresponds to the mutual information
$$I(X;Y) = H(X) - H(X\mid Y).$$

## Conditions for Leakage Measures
Let us consider what an ideal measure of leakage $L(X \to Y)$ should satisfy.

* (R1) Axioms
    - Data processing inequality: If $X–Y–Z$ is a Markov chain, then $L(X \to Z) \leq L(X \to Y)$ *and* $L(X \to Z) \leq L(Y \to Z)$.
    - Independence: $X$ and $Y$ are independent iff $L(X \to Y) = 0$.
    - Additivity: If $(X_1, Y_1)$ and $(X_2, Y_2)$ are independent, then $L(X_1X_2 \to Y_1Y_2) = L(X_1 \to Y_1) + L(X_2 \to Y_2)$.
* (R2) $L(X \to Y)$ should have an operational interpretation.
* (R3) There should be minimal assumptions on the adversary.
* (R4) It should be in accordance with intuition.

MI satisfies R1-3, but not R4.

## Guessing Framework
Suppose that the adversary is trying to guess the realisation of a random variable $U$ with (known) probability distribution $P_U$. Its guess is represented by $\hat{U} \sim P_{\hat{U}}$.  
Thus $P_{\hat{U}}(u)$ represents the probability of correctly guessing $\hat{U} = u$ when $U = u$.

The adversary is seeking the optimal strategy, which is equivalent to solving the maximisation problem
$$\max_{P_{\hat U}} \mathbb{E}_U[P_{\hat U}(U)].$$

Let $U$ be binary, and define $p = P_U(1) = 1- P_U(0)$. Then we have
$$\begin{split}
\mathbb{E}_U[P_{\hat U}(U)] &= (1-p)P_{\hat U}(0) + pP_{\hat U}(1) \\
&\leq \max\{p,1-p\} \cdot (P_{\hat U}(0) + P_{\hat U}(1)) \\
&= \max\{p, 1-p\}.
\end{split}$$

This upper bound corresponds to the strategy of setting $P_{\hat U}(0) = 1$ if $p \leq \frac12$, and $P_{\hat U}(1) = 1$ otherwise.

We can, in fact, show that the above maximisation problem is solved by $\max_u P_U(u)$:
$$\begin{split}
\mathbb{E}[P_{\hat U}(U)] &= \sum_u P_{\hat U}(u) P_U(u) \\
&\leq \sum_u (\max_v P_U(v))P_{\hat U}(u) \\
&= (\max_u P_U(u)) \sum_u P_{\hat U}(u) \\
&= \max_u P_U(u).
\end{split}$$
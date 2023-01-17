---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 17 January, Tuesday (Lecture 5)
author: Taught by Prof. Prasad Krishnan
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Exercise
$$H(X) = \sum_x p_X(x) \log \frac1{p_X(x)}$$

$$H(X, Y \mid Z, R) = \sum_{(z,r)} p_{Z,R}(z, r)\sum_{(x,y)}p_{X,Y}(x,y \mid Z = z, R = r) \log \frac1{p(x,y \mid Z = z, R = r)}$$

$$\begin{split}
I(Z;R \mid X, Y) &= H(Z \mid X, Y) + H(R \mid X, Y) - H(Z, R \mid X, Y) \\
&= H(Z \mid X, Y) - H(Z \mid X, Y, R) \\
&= \sum_{(x,y)}p_{XY}(x, y) \sum_z p_Z(z \mid X = x, Y = y) \log \frac1{p_Z(z \mid X = x, Y = y)} \\
&+ \sum_{(x,y,r)} p_{XYR}(x, y, r) \sum_z p_Z(z \mid X = x, Y = y, R = r) \log\frac1{p_Z(z \mid X = x, Y= y, R =r)}
\end{split}$$


$$H(X, Y \mid Z, R) = H(X, Y, Z, R) - H(Z, R)$$

$$\begin{split}
I(Z; R \mid X, Y) &= H(Z \mid X, Y) + H(R \mid X, Y) - H(Z, R \mid X, Y) \\
&= H(Z \mid X, Y) + H(R, X, Y) - H(X, Y) - H(Z, R, X, Y) + H(X, Y) \\
&= H(Z \mid X, Y) + H(R, X, Y) - H(Z, R, X, Y) \\
&= H(Z, X, Y) + H(R, X, Y) - H(X, Y) - H(Z, R, X, Y)
\end{split}$$

**N.B.** $;$ has higher precedence than $\mid$.

# Entropy (contd.)
## Subadditivity
We know that
$$H(X,Y) = H(X) + H(Y \mid X).$$
Since $H(Y \mid X) \leq H(Y)$, we have that
$$H(X,Y) \leq H(X) + H(Y).$$

This can be extended to
$$H(X_1, \dots, X_n) \leq \sum_i H(X_i).$$

We can prove similarly that
$$I(X;Y \mid Z) \leq I(X;Y).$$

## Fano's Inequality
Consider two r.vs. $X$ and $Y$, which have some correlation between them. Suppose we wish to guess, or *estimate*, $X$ given $Y$. We denote the estimation of $X$ from $Y$ as $\hat{X}$.

We need a measure to capture the "goodness" of an estimate. One good way to do this is to compute the probability that $\hat{X} \neq X$. Given the joint distribution of $P_{\hat{X}, X}$, we can compute this as
$$\sum_{\hat{x} \neq x}p(\hat{x}, x).$$
We call this quantity $P_e$, or *probability of error*.

Fano's inequality links $P_e$ to $H(X \mid Y)$, the uncertainty remaining in $X$ once we have $Y$.
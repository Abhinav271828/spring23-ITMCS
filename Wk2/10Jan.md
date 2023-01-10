---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 10 January, Tuesday (Lecture 3)
author: Taught by Prof. Prasad Krishnan
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Entropy (contd.)
## Properties
The entropy is always nonnegative, *i.e.*, for any r.v. $X$,
$$H(X) \geq 0.$$

For a Bernoulli r.v. $X \sim \text{Bern}(p)$,
$$H(X) = -p\log p - (1-p)\log(1-p) = H_2(p).$$
This quantity is called *binary entropy*. It achieves a maximum value of 1 at $p = 0.5$, which tells us that this is the most "uncertain" distribution (the hardest to predict).

## Joint Entropy
We can generalise entropy to multivariate distributions. Consider the set of r.vs. $(X_1, \dots, X_n) \sim P_{X_1, \dots, X_n}$; the entropy of this joint distribution is
$$H(X_1, \dots, X_n) = \sum P_{\mathbf{X}}(\mathbf{x}) \log \frac1{P_{\mathbf{X}}(\mathbf{x})}.$$

A special case of this is $n = 2$:
$$H(X, Y) = \sum p(x,y) \log \frac1{p(x,y)}.$$

## Conditional Entropy
We can define the entropy of a conditional distribution given a single event in a straightforward way as
$$H(X \mid Y = y) = \sum p_{X \mid Y = y}(x) \log \frac1{p_{X \mid Y = y}(x)},$$
and then extend this to define
$$H(X \mid Y) = \sum p_Y(y) H(X \mid Y = y).$$

We can show that
$$\begin{split}
H(X,Y) &= H(X) + H(Y \mid X) \\
&= H(Y) + H(X \mid Y)
\end{split}$$

More generally,
$$H(X_1, \dots, X_n) = \sum_{i=1}^n H(X_i \mid X_1, \dots, X_{i-1}).$$
This is called the chain rule of joint entropy.

If $Y = X$, we can show that $H(X \mid Y) = 0$. Thus we have $H(X,X) = H(X)$.

## Mutual Information
The mutual information between two r.vs. $X, Y$ is defined as
$$\begin{split}
I(X;Y) &= H(Y) - H(Y \mid X) \\
&= H(X) - H(X \mid Y) \\
&= H(X) + H(Y) - H(X,Y)
\end{split}$$
We can therefore show that $I(X;X) = H(X)$.

Further, for independent $X, Y$, 
$$H(X,Y) = H(X) + H(Y),$$
and so
$$I(X;Y) = 0.$$

Mutual information also has a chain rule:
$$I(X_1, \dots, X_n; Y) = \sum_{i=1}^n I(X_i; Y \mid X_1, \dots, X_{i-1}).$$

## Relative Entropy (Kullback-Leibler Divergence)
Consider two distributions $p, q$, both over a ground set $\mathcal{X}$. We define the relative entropy between the distributions as
$$D(p \parallel q) = \sum p(x)\log\frac{p(x)}{q(x)}.$$
---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 06 January, Friday (Lecture 2)
author: Taught by Prof. Prasad Krishnan
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Basics of Probability Theory
## Random Variables
Let $X$ be a r.v. (taking any value in $\mathbb{R}$), and $x \in \mathbb{R}$ be some real number. We define the *cumulative distribution function* of $X$ as
$$F_X(x) = P(X \leq x).$$
Discrete r.vs. have step CDFs, while continuous ones have differentiable CDFs.

The actual probability is captured by the *probability mass function* $P_X$.  
In the case of discrete r.vs., the steps in the CDF correspond to spikes in the PMF.  
For a continuous r.v., the probability of any specific value is zero. We can instead consider the probability of a range
$$P\left(x - \frac\delta2 \leq X \leq x+\frac\delta2\right) = f_X(x) \cdot \delta,$$
where
$$f_X(x) = \frac{dF_X(x)}{dx}$$
is the *probability density function* of $X$.

## Joint Distributions
We define the joint CDF of $n$ r.vs. $X_1, \dots, X_n$ as
$$F_{X_1, \dots, X_n}(x_1, \dots, x_n) = P(X_1 \leq x_1, \dots, X_n \leq x_n)$$
or
$$F_\mathbf{X}(\mathbf{x}) = P(\mathbf{X} \leq \mathbf{x}).$$
The r.vs. $X_i$ are called *jointly distributed*.  
Analogously, we can define a joint PMF or joint PDF for the r.vs.

## Conditional Distributions
If $X$ and $Y$ are two jointly distributed r.vs. with PMF $P_{XY}$, then the *conditional distribution* of $X$ given $Y = y$ is
$$P_{X \mid Y = y}(x) = \frac{P_{XY}(x,y)}{P_Y(y)},$$
defined when $P_Y(y) > 0$.  
$X$ and $Y$ are said to be independent if $P_{X \mid Y = y}(x) = P_X(x)$ for all $y$. Equivalently,
$$P_{XY}(x,y) = P_X(x) \cdot P_Y(y),$$
for all $x$ and $y$.  
If we calculate $P_Y(y)$ from the joint distribution as
$$\sum_x P_{XY}(x,y),$$
then we call $P_Y$ the *marginal distribution* of $Y$.

For discrete r.vs., the sum of probabilities is 1; for continuous r.vs., the integral over the range is 1.

## Functions on R.Vs.
If we have a function $g$ from $n$ random variables $X_1, \dots, X_n$ to $\mathbb{R}$, it is also a random variable. We can calculate its PMF as
$$P(g(X_1, \dots, X_n) = y) = \sum_{g(\mathbf{x})=y} P_\mathbf X(\mathbf x).$$

## Expectation
The expected value of a r.v. is its mean value, weighted by the probabilities
$$\mathbb{E}[X] = \mu_x = \sum_x xP_X(x).$$
Note that if $Y = g(X_1, \dots, X_n)$, we can write
$$\mathbb{E}[Y] = \mathbf{E}[g(\mathbf{X})],$$
but the expression on the left side is over the distribution $P_Y$, while that on the right is over $P_{\mathbf X}$.

Expectation is linear:
$$\mathbb{E}[X_1 + \cdots + X_n] = \mathbb{E}[X_1] + \cdots + \mathbb{E}[X_n].$$

## Variance
Variance is a quantity that measures how much a r.v. fluctuates from its mean. It is defined as
$$\begin{split}
\text{var}(X) &= \mathbb{E}\left[(X - \mathbb{E}[X])^2\right] \\
&= \mathbb{E}[X^2] - \mathbb{E}[X]^2.
\end{split}$$

# Entropy
## Definition
Consider a function $g$ on the r.v. $X$, defined as
$$g(x) = \log\frac1{P_X(X = x)}.$$
The expectation of this function is
$$\mathbf{E}[g(X)] = \sum_x P_X(x)g(x) = \sum P_X(x)\log\frac1{P_X(x)}.$$
This is defined as the (Shannon's) entropy $H(X)$ of $X$.

Note that $x$ ranges over the *support* of $X$, *i.e.*, all values such that $P_X(x) \neq 0$.

The entropy formalises the notion of *uncertainty* in the value of the r.v., which corresponds to the amount of information available in its value.
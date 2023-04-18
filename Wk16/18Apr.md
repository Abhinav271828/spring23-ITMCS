---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 18 April, Tuesday (Lecture 24)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Information Leakage
## Maximal Leakage
We define the maximal leakage between $X$ and $Y$ as
$$L(X \to Y) = \sup_{U : U–X–Y} \left( \log\frac1{P_C(U)} - \log\frac1{P_C(U \mid Y)} \right),$$
or equivalently,
$$L(X \to Y) = \sup_{U : U–X–Y} \log\frac{\sum_y P_Y(y) \max_u P_{U \mid Y}(u 
\mid y)}{\max_u P_U(u)}.$$

This optimisation problem is intractable. However, it is possible to show that
$$L(X \to Y) = \log\sum_y\max_x P_{Y \mid X}(y \mid x).$$

First, consider $\sum_y P(y) \max_u P(u \mid y)$. Introducing the joint distribution and taking the marginal, we get
$$\begin{split}
\sum_y P(y) \max_u P(u \mid y) &= \sum_y P(y) \max_u \sum_x P(u,x \mid y) \\
&= \sum_y P(y) \max_u \sum_x P(x \mid y)P(u \mid x) \\
&= \sum_y \max_u \sum_x P(y \mid x) P(x) P(u \mid x) \\
&\leq \sum_y \left(\max_x P(y \mid x)\right) \max_u \sum_x P(u, x) \\
&= \left(\sum_y \max_x P(y \mid x) \right) \left(\max_u P_U(u)\right).
\end{split}$$
Therefore the term inside the supremum in $L(X \to Y)$ is upper-bounded by $\log\sum_y\max_x P_{Y \mid X}(y \mid x)$.

To prove equality, we only need to show that this bound can be achieved, *i.e.*, that this expression is indeed the supremum.  
Let $\mathcal{X} = \{x_1, x_2, \dots, x_n\}$. For each $x_i$, we define
$$\mathcal{U}_{x_i} = \{(x_i, 1), \dots, (x_i, k_{x_i})\},$$
where $k_{x_i} = \frac{P(x_i)}{\min_x P(x)}$ (assume that this is a natural number).  
Let $\mathcal{U} = \bigcup_{x \in \mathcal{X}} \mathcal{U}_x.$

Now, we define the distribution
$$P_{U \mid X}(u \mid x) = \begin{cases}
\frac1{k_x} & u \in \mathcal{U}_x \\
0 & \text{otherwise}.
\end{cases}$$
This means that $P_U(u)$ is $\frac{P_X(0)}{1}$ when $u \in \mathcal{U}_0$, and $\frac{P_X(1)}{3}$ when $u \in \mathcal{U}_1$.

It can be shown that this distribution achieves the upper bound.

### Axioms
As we have derived it, this measure of information leakage is operationally motivated. An upper bound on the value of $L(X \to Y)$ places a bound on the difference between being able to guess $U$ given $Y$ and being able to guess $U$ without any information.

We can also show that, in accordance with our intuition, it is nonnegative. This is because the term inside the log in the second formulation is lower-bounded by
$$\max_x\sum_y P_{Y \mid X}(y \mid x),$$
which is 1.

Furthermore, the independence property is satisfied:
$$L(X \to Y) \iff X \perp Y.$$
The backward implication is trivial. For the forward implication, if $L(X \to Y) = 0$, then
$$\begin{split}
\sum_y\max_x P(y \mid x) &= 1 \\
&= \sum_y P(y)
\end{split}$$
Since $\max_x P(y \mid x) \geq P_Y(y)$ for all $y$, this makes each term equal:
$$\max_x P(y \mid x) = P(y),$$
and so $X$ and $Y$ are independent.

So is the data processing inequality:
$$L(X \to Z) \leq L(X \to Y)$$
$$L(X \to Z) \leq L(Y \to Z)$$
for a Markov chain $X–Y–Z$.

Moreover, maximal leakage is additive. For independent $(X_1, Y_1)$ and $(X_2, Y_2)$, we have
$$L(X_1X_2 \to Y_1Y_2) = L(X_1 \to Y_1) + L(X_2 \to Y_2).$$

### Examples
If $P_{Y \mid X}$ is a piecewise Bernoulli r.v. of the form
$$\begin{bmatrix} 1-q & q \\ q & 1-q \end{bmatrix},$$
where $q \leq \frac12$, then
$$L(X \to Y) = \log 2(1-q).$$
Note that this is independent of $P_X$.
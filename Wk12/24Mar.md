---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 24 March, Friday (Lecture 19)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Total Variational Distance (contd.)
We have proven that for any two distributions $P_X, Q_X$,
$$\text{TVD}(P_X, Q_X) = \sup_{A \subseteq \mathcal{X}} |P_X(A) - Q_X(A)|.$$

Suppose we wish to distinguish, given a sample $x$, if it is drawn from $P_X$ or $Q_X$, *i.e.*, we need a test $T : \mathcal{X} \to \{0,1\}$ such that $T(x) = 0$ if $x$ is drawn from $P_X$ and $T(x) = 1$ if $x$ is drawn from $Q_X$.  
Note that $P_X$ and $Q_X$ should be such that $\Pr_{X \sim P}[T(X) = 0]$ is maximised and $\Pr_{X \sim Q}[T(X) = 0]$ is minimised.

Consider some $A$ s.t. $\mathcal{X} = A \cup A^c$; define $T$ based on membership in $A$. Then these quantities are respectively $P_X(A)$ and $Q_X(A)$. Thus we wish to maximise $P_X(A) - Q_X(A)$, which is accomplished by the TVD between $P_X$ and $Q_X$.  
Thus one interpretation of TVD is the maximum probability that a test distinguishes between $P_X$ and $Q_X$.

We can rewrite the previously proved lemma as
$$\left|\mathbb{E}_{X \sim P}[T(X)] - \mathbb{E}_{X \sim Q}[T(X)]\right| \leq \text{TVD}(P_X, Q_X).$$

## Pinsker's Inequality
Let $P_X$ and $Q_X$ be two distributions on $\mathcal{X}$. Then
$$D(P_X \mid\mid Q_X) \geq \frac{2\text{TVD}(P_X, Q_X)^2}{\ln 2}.$$

To prove this, assume that $\mathcal{X} = \{0,1\}$. Define $p = P_X(0)$ and $q = Q_X(0)$.  
Suppose $p \geq q$. Then let
$$g_p(q) = p\log\frac{p}{q} + (1-p)\log\frac{1-p}{1-q} - \frac{2(p-q)^2}{\ln2}.$$
Then we have $g_p(0) = \infty$, $g_p(p) = 0$.

We can also evaluate
$$g_p'(q) = \frac{p-q}{\ln2}\left[4-\frac1{q(1-q)}\right].$$
The factor outside the brackets is always nonnegative, and the bracketed term is always nonpositive. Thus this quantity is nonpositive, which means that $g_p(q)$ is always decreasing. Therefore,
$$\begin{split}
q \leq p &\implies g_p(q) \geq g_p(p) \\
&\implies g_p(q) \geq 0 \\
&\implies p\log\frac{p}{q} + (1-p)\log\frac{1-p}{1-q} \geq \frac{2(p-q)^2}{\ln2},
\end{split}$$
QED. This proves Pinker's Inequality in the case of binary variables.

## Chain Rule of Relative Entropy
For the general case, we will use the chain rule of relative entropy. This states that if we have two joint distributions $P_{XY}$ and $Q_{XY}$, distributed over $\mathcal{X} \times \mathcal{Y}$, then
$$D(P_{XY} \mid\mid Q_{XY}) = D(P_X \mid\mid Q_X) + \sum_{x \in \mathcal{X}} P_X(x)D(P_{Y \mid X = x} \mid\mid Q_{Y \mid X = x}).$$

To prove this, note first that
$$\begin{split}
D(P_{XY} \mid\mid Q_{XY}) &= \sum_{x,y} P(x,y) \log\frac{P(X,Y)}{Q(X,Y)} \\
&= \sum_{x,y} P(x)P(y \mid x) \log\frac{P(x)}{Q(x)} + \sum_{x,y} P(x)P(y \mid x) \log\frac{P(y \mid x)}{Q(y \mid x)} \\
&= D(P_X \mid\mid Q_X) + \sum_x P(x) \sum_y P(y \mid x) \log\frac{P(y \mid x)}{Q(y \mid x)} \\
&= D(P_X \mid\mid Q_X) + \sum_{x \in \mathcal{X}} P_X(x)D(P_{Y \mid X = x} \mid\mid Q_{Y \mid X = x}),
\end{split}$$
QED.

## Pinsker's Inequality (contd.)
Now let $P_X, Q_X$ be arbitrary distributions over $\mathcal{X}$. Then there exist distributions $P', Q'$ over $\{0,1\}$, such that
$$\text{TVD}(P_X, Q_X) = \text{TVD}(P', Q')$$
and
$$D(P_X \mid\mid Q_X) \geq D(P' \mid\mid Q').$$

To prove this, let $S = \{x : P_X(x) > Q_X(x)\}$ as before, and define a r.v. $Z = 1\{X \in S\}$. Then we have
$$P_Z(1) = 1 - P_Z(0) = P_X(S),$$
and
$$Q_Z(1) = 1 - Q_Z(0) = Q_X(S).$$
Therefore $\text{TVD}(P_Z, Q_Z) = P_X(S) - Q_X(S) = \text{TVD}(P_X, Q_X)$. This means that we can set $P' = P_Z$, $Q' = Q_Z$ to satisfy the condition on the TVD.

We only need to prove now that this can only decrease the KL-Divergence. This can be proved as follows.
$$\begin{split}
D(P_X \mid\mid Q_X) &= D(P_{XZ} \mid\mid Q_{XZ}) \\
&\geq D(P_Z \mid\mid Q_Z) \text{  [by the chain rule]} \\
&= D(P' \mid\mid Q'),
\end{split}$$
QED.

Thus, for any pair of distributions $P_X, Q_X$,
$$\begin{split}
D(P_X \mid\mid Q_X) &\geq D(P' \mid\mid Q') \\
&\geq \frac{2\text{TVD}(P', Q')^2}{\ln2} \\
&= \frac{2\text{TVD}(P_X, Q_X)^2}{\ln2},
\end{split}$$
which proved Pinsker's Inequality.
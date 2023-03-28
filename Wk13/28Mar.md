---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 28 March, Tuesday (Lecture 20)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Total Variational Distance
## Pinsker's Inequality (contd.)
In the binary case, we proved that
$$D(P_X \mid\mid Q_X) \geq \frac{2\text{TVD}(P_X, Q_X)^2}{\ln 2}$$
if $P_X(0) = p \geq q = Q_X(0)$. We now consider the other case, *i.e.*, $p \leq q$.

We defined $g_p(q)$ and noted that
$$g_p'(q) = \frac{p-q}{\ln2}\left[4-\frac1{q(1-q)}\right],$$
which is nonnegative if $p \leq q$. Thus $g_p(q)$ is decreasing in the range $[0,p]$ and increasing in the range $[p,1]$.

Since $g_p(p) = 0$, this means that $g_p(q) \geq 0$ for all $q$, QED. This completes the proof of Pinsker's Inequality.

By the chain rule for KL divergence,
$$D(P_{X_1X_2} \mid\mid Q_{X_1X_2}) = 2D(P_X \mid\mid Q_X),$$
where $P_{X_1X_2} = P_X \cdot P_X$, and similarly for $Q_{X_1X_2}$.  
We can prove that
$$\text{TVD}(P_{X_1X_2}, Q_{X_1X_2}) \leq 2\text{TVD}(P_X, Q_X)$$
by proceeding as follows
$$\begin{split}
\text{TVD}(P_{X_1X_2}, Q_{X_1X_2}) &= \frac12\sum_{x_1,x_2}|P_X(x_1)P_X(x_2) - Q_X(x_1)Q_X(x_2)| \\
&= \frac12\sum_{x_1,x_2}|P_X(x_1)P_X(x_2) - P_X(x_1)Q_X(x_2) \\
&+ P_X(x_1)Q_X(x_2) - Q_X(x_1)Q_X(x_2) \\
&\leq \frac12\left(\sum_{x_1}P_X(x_1)\right)\sum_{x_2}|P_X(x_2)-Q_X(x_2)| \\
&+ \frac12\left(\sum_{x_2}Q_X(x_2)\right)\sum_{x_1}|P_X(x_1) - Q_X(x_1)| \\
&= 2\text{TVD}(P_X, Q_X).
\end{split}$$

## Distinguishing Coins
Consider two coins defined by the distributions
$$P_X(x) = \begin{cases}
\frac12 & x = 1 \\
\frac12 & x = 0 \end{cases}$$
and
$$Q_X(x) = \begin{cases}
\frac12 + \varepsilon & x = 1 \\
\frac12 - \varepsilon & x = 0. \end{cases}$$

Given $n$ i.i.d. samples $x_1, x_n$, drawn from either $P_X$ or $Q_X$, we need to identify the distribution. This is operationalised as a function $T : \mathcal{X}^n \to \{0,1\}$, where $T(\mathbf{x}) = 0$ means that the samples are drawn from $P_X$ and $1$ means they are drawn from $Q_X$.  
We say that $T$ distinguishes the distributions *with high probability* (w.h.p) if
$$\Pr_{x^n \sim P_{x^n}}[T(x^n) = 0] \geq p$$
and
$$\Pr_{x^n \sim Q_{x^n}}[T(x^n) = 1] \geq p,$$
for some sufficiently large $p$, say $\frac9{10}$. We can ask what the minimum number of samples $n$ is to achieve this – this can, in fact, be answered without any further information about $T$.

To find this bound, note that the condition can be rewritten as
$$\Pr_{x^n \sim Q_{X^n}}[T(x^n)=1] \geq \frac9{10}$$
and
$$\Pr_{x^n \sim P_{X^n}}[T(x^n)=0] \leq \frac1{10},$$
so then
$$\Pr_{x^n \sim Q_{X^n}}[T(x^n) = 1] - \Pr_{x^n \sim P_{X^n}}[T(x^n) = 1] \geq \frac8{10}.$$
Therefore,
$$\operatorname*{\mathbb{E}}_{x^n \sim Q_{X^n}}[T(x^n)] - \operatorname*{\mathbb{E}}_{x^n \sim P_{X^n}}[T(x^n)] \geq \frac8{10},$$
and so
$$\text{TVD}(P_{X^n}, Q_{X^n}) \geq \frac8{10}.$$

From here, we proceed as follows
$$\begin{split}
\text{TVD}(P_{X^n}, Q_{X^n})^2 &\geq \left(\frac8{10}\right)^2 \\
\implies \frac{\ln2}2D(P_{X^n} \mid\mid Q_{X^n}) &\geq \left(\frac8{10}\right)^2 \\
\implies n &\geq \left(\frac8{10}\right)^2 \frac2{\ln2} \frac1{D(P_X \mid\mid Q_X)}.
\end{split}$$

We are only left now with proving an upper bound on $D(P_X \mid\mid Q_X)$ in terms of $\varepsilon$.
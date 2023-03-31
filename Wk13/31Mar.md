---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 31 March, Friday (Lecture 21)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Total Variational Distance
## Distinguishing Coins (contd.)
We have established that
$$n \geq \left(\frac8{10}\right)^2\frac2{\ln2} \frac1{D(P_X \mid\mid Q_X)}$$
and that an upper bound on $D(P_X \mid\mid Q_X)$ in terms of $\varepsilon$ is all we need now. Identifying this bound is straightforward:
$$\begin{split}
D(P_X \mid\mid Q_X) &= \frac12\log\frac1{1+2\varepsilon} + \frac12\log\frac1{1-2\varepsilon} \\
&= \frac12\log\frac1{1-4\varepsilon^2} \\
&= \frac12\log\left(1 + \frac{4\varepsilon^2}{1-4\varepsilon^2}\right) \\
&\leq \frac1{2\ln2}\left(\frac{4\varepsilon^2}{1-4\varepsilon^2}\right),
\end{split}$$
since $\ln(1+x) \leq x$.  
Furthermore, we know that $\varepsilon \leq \frac14$. This makes the denominator greater than $\frac34$, so we have
$$\begin{split}
D(P_X \mid\mid Q_X) &\leq \frac1{2\ln2}\cdot 4\varepsilon^2 \cdot \frac43 \\
&\leq \frac{8\varepsilon^2}{3\ln2}.
\end{split}$$

Substituting this in the inequality on $n$, we obtain
$$\begin{split}
n &\geq \left(\frac8{10}\right)^2 \frac2{\ln2} \frac{3\ln2}{8\varepsilon^2} \\
&= \frac34\left(\frac8{10}\right)^2\frac1{\varepsilon^2}.
\end{split}$$

### Optimality of Lower Bound
We can prove the achievability of this lower bound. We need to construct a test $T$ such that for all $n \geq \frac34\left(\frac8{10}\right)^2\frac1{\varepsilon^2}$, 
$$\Pr_{x^n \sim P_{X^n}} [T(x^n) = 0] \geq \frac9{10}$$
and
$$\Pr_{x^n \sim Q_{X^n}} [T(x^n) = 0] \geq \frac9{10}.$$

### Chernoff Bound
We can use the Chernoff bound, which states that for $n$ i.i.d. Bernoulli variables $X_1, \dots, X_n \sim \text{Bern}(p)$, and any $\varepsilon > 0$,
$$P\left(\frac{\sum_{i=1}^n x_i}{n} \geq p + \varepsilon \right) \leq e^{-2n\varepsilon^2}$$
and
$$P\left(\frac{\sum_{i=1}^n x_i}{n} \leq p - \varepsilon \right) \leq e^{-2n\varepsilon^2}.$$

First, we will prove this. Let $X = \sum_{i=1}^n X_i$, and $q = p + \varepsilon$; then
$$\begin{split}
P(X \geq nq) &= P(tx \geq nqt) \text{ for any } t > 0 \\
&= P(e^{tx} \geq e^{nqt}) \\
&\leq \frac{\mathbb{E}[e^{tx}]}{e^{nqt}} \text{ by Markov's Inequality}.
\end{split}$$
Therefore
$$P(X \geq nq) \leq \inf_{t > 0} \frac{\mathbb{E}[e^{tx}]}{e^{nqt}} = \inf_{t > 0} \left(\frac{\mathbb{E}[e^{t\overline{x}}]}{e^{tq}}\right)^n,$$
since $e^{tx}$ is the product of $n$ i.i.d. variables and can be decomposed. Note that $\overline{X} \sim P_X$.

We can calculate
$$\begin{split}
f(t) &= \frac{\mathbb{E}[e^{t\overline{x}}]}{e^{tq}} \\
&= \frac{pe^t + (1-p)}{e^{tq}}.
\end{split}$$

We leave it as an exercise to show that $\inf_{t > 0} f(t) = e^{-D_e(q \mid\mid p)}$. Then we have, by Pinsker's Inequality, that
$$e^{-D(q \mid\mid p)} \leq e^{-2\varepsilon^2},$$
which proves Chernoff's bound.

### Optimality of Lower Bound (contd.)
Consider the test $T$ such that
$$T(x^n) = \begin{cases}
0 & \frac{\sum_{i=1}^n x_i}{n} < \frac12 + \frac\varepsilon2 \\
1 & \frac{\sum_{i=1}^n x_i}{n} \geq \frac12 + \frac\varepsilon2.
\end{cases}$$

Then we have
$$\begin{split}
\Pr_{x^n \sim P_{X^n}}[T(x^n) = 0] &= P\left(\frac{X}n < \frac12 + \frac\varepsilon2\right) \\
&= 1 - P\left(\frac{X}n > \frac12 + \frac\varepsilon2 \right) \\
&\geq 1 - e^{-2n\frac{\varepsilon^2}{4}} \\
&= 1 - e^{-\frac12n\varepsilon^2} \\
&\geq \frac9{10},
\end{split}$$
QED.
We can show the other condition in an exactly similar way.
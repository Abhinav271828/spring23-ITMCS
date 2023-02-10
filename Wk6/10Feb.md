---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 10 February, Friday (Lecture 10)
author: Taught by Prof. Prasad Krishnan
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Connection between Entropy and Counting
## Binomial Coefficients (contd.)
Suppose we have $2n$ movies and $2^n$ people, each of whom watches at least $\frac9{10}2n$ movies. Can we prove that there are two people who have watched the same subset of movies?

We know that the number of subsets of movies of size at least $\frac9{10}2n$ is
$$\sum_{i=\frac9{10}2n}^{2n}{2n \choose i} = \sum_{i=0}^{\frac1{10}2n}{2n \choose i}$$
We want to show that this number is smaller than $2^n$.

We first claim that
$$\sum_{i=0}^k {m \choose i} \leq 2^{mH\left(\frac{k}{m}\right)}$$
for $k \leq \frac{m}{2}$.
Assuming this, we can say that
$$\begin{split}
\sum_{i=0}^{\frac1{10}2n}{2n \choose i} &= 2^{2nH\left(\frac{1}{10}\right)} \\
&< 2^{2n \cdot \frac12} \\
&= 2^n.
\end{split}$$

We now prove the claim. We first note that the set of subsets of $\{1, \dots, n\}$ is in bijection with the set of bitstrings of length $n$. Extending this, the set of subsets of $\{1, \dots, n\}$ of at most $k$ elements is in bijection with
$$c = \{x^n : \sum_{i=1}^n x_i \leq k\},$$
where $x_i \in \{0,1\}$.
Now $|c|$ is the LHS of the claim above.

Let us define a r.v. $X = (X_1, \dots, X_n) \sim \text{Unif}(c)$, where $X_i$ are identically distributed. Then we have that
$$P_X(a^n) = \frac1{|c|},$$
for any $a^n \in c$, and so $H(X) = \log |c|$.  
Now we consider the entropies of the constituent $X_i$:
$$\begin{split}
P(X_i = 1) &= \sum_{l=0}^k P\left(X_i = 1 \mid \sum_{j=1}^n X_j = l\right) P\left(\sum_{j=1}^n X_j = l\right)\\
&= \sum_{l=0}^k \frac{P\left(X_i = 1 \mid \sum_{j=1}^n X_j = l\right)}{P\left(\sum_{j=1}^n X_j = l\right)}\cdot P\left(\sum_{j=1}^n X_j = l\right) \\
&= \sum_{l=0}^k \frac{\frac{{n-1} \choose {l-1}}{|c|}}{\frac{n \choose l}{|c|}} \cdot P\left(\sum_{j=1}^n X_j = l\right) \\
&= \sum_{l=0}^k \frac{(n-1)!}{(l-1)!} \cdot \frac{l}{n} \cdot P\left(\sum_{j=1}^n X_j = l\right) \\
&= \sum_{l=0}^k \frac{l}{n} \cdot P\left(\sum_{j=1}^n X_j = l\right) \\
&\leq \sum_{l=0}^k \frac{k}{n} \cdot P\left(\sum_{j=1}^n X_j = l\right) \\
&\leq \frac{k}{n} \sum_{l=0}^k P\left(\sum_{j=1}^n X_j = l\right) \\
&= \frac{k}{n}.
\end{split}$$
We can also prove this by observing that since $\sum_{i=1}^n X_i \leq k$, $\sum_{i=1}^n \mathbb{E}[X_i] \leq k$, and so $\mathbb{E}[X_i] \leq \frac{k}{n}$ (since the $X_i$ are identically distributed).

From this, we get that $H(X_i) \leq H\left(\frac{k}{n}\right)$. Now, from the subadditivity of entropy,
$$H(X) \leq \sum_{i=1}^n H(X_i) \leq nH\left(\frac{k}{n}\right).$$
This shows that
$$|c| \leq 2^{nH\left(\frac{n}{k}\right)},$$
QED.

## Repetitions in Matrices
Consider an $n\times n$ matrix such that each column and each row has at most $t$ distinct entries. Then there exists an entry that appears at least $\frac{n^2}{t^2}$ times.

Consider two r.vs. $X, Y \sim \text{Unif}(\{1, \dots, n\})$, which represent a row and a column of the matrix $A$ respectively. Further, let $Z$ be the r.v. which determines an entry of the matrix given values of $X$ and $Y$, *i.e.*, $Z = A_{XY}$.

Now, we claim that $H(Z) \leq H(Z \mid X) + H(Z \mid Y)$. Furthermore,
$$\begin{split}
H(Z \mid X) &= \sum_{x=1}^n H(Z \mid X = x)P_X(x) \\
&= \sum_{x=1}^n H(A_{xY} \mid X = x) P_X(x) \\
&\leq \sum_{x=1}^n \log t \cdot P_X(x) \\
&\leq \log t.
\end{split}$$
Therefore, $H(Z) \leq 2\log t$.

We note that if $\sum_i a_ip_i \leq \alpha$, then there exists an $i$ such that $a_i \leq \alpha$. Applying this to the entropy we derived
$$\sum_Z P_Z(z) \log \frac1{P_Z(z)} \leq 2 \log t,$$
we get that there exists a $z^*$ such that
$P_Z(z^*) \geq \frac1{t^2}$.  
Now we know that
$$P_Z(z) = \frac{\text{no. of occurrences of } z}{n^2},$$
so this tells us that the number of occurrences of $z^*$ is at least $\frac{t^2}{n^2}$.
---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 14 February, Tuesday (Lecture 11)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Connection between Entropy and Counting
## Repetitions in Matrices (contd.)
We now need to prove that $H(Z) \leq H(Z \mid X) + H(Z \mid Y)$, as claimed. Note first that
$$\begin{split}
H(X,Y,Z) &= H(X,Y) + H(Z \mid X, Y) \\
&= H(X) + H(Y) + 0 = H(X) + H(Y)
\end{split}$$
and also
$$H(X,Y,Z) = H(Z) + H(X, Y \mid Z).$$

From these two identities, we see that
$$\begin{split}
H(Z) &= H(X) + H(Y) - H(X, Y \mid Z) \\
&= H(X) + H(Y) - H(X \mid Z) - H(Y \mid Z, X) \\
&\geq H(X) + H(Y) - H(X \mid Z) - H(Y \mid Z) \\
&= I(X;Z) + I(Y;Z) \\
&= H(Z) - H(Z \mid X) + H(Z) - H(Z \mid Y).
\end{split}$$

The claim follows directly from this.

## Shearer's Lemma
Let $S = \{(x_1, y_1), \dots, (x_n, y_n)\}$ be a set of $n$ distinct points in $\mathbb{R}^2$. Let $S_x = \{x_1, \dots, x_n\}$, and $S_y = \{y_1, \dots, y_n\}$.  
We define $n = |S|, n_1 = |S_x|, n_2 = |S_y|$. We can show that $n \leq n_1 n_2$.

To prove this, first let $A = (X,Y) \sim \text{Unif}(S)$ be a r.v. Then we have
$$P(A = (a,b)) = \frac1n$$
for any $(a,b) \in S$.  
Now we can apply the subadditivity of entropy as follows:
$$\begin{split}
H(A) &= H(X,Y) \\
&\leq H(X) + H(Y) \\
\implies \log n &\leq H(X) + H(Y) \\
&\leq \log n_1 + \log n_2,
\end{split}$$
QED.

## Loomis-Whitney Inequality
Consider the analogous case in three dimensions, where $S = \{(x_1, y_1, z_1), \dots, (x_n, y_n, z_n)\}$, and $n_1 = |S_{yz}|, n_2 = |S_{zx}|, n_3 = |S_{xy}|$. We can prove that $n^2 \leq n_1 n_2 n_3.$

Again, let $P = (X,Y,Z) \sim \text{Unif}(S)$ be a r.v. We have Shearer's lemma, which states that
$$2H(X,Y,Z) \leq H(X,Y) + H(Y,Z) + H(Z,X).$$
From here, noting that $H(X,Y,Z) = H(P) = \log n$, and that the summation is at most $\log n_1 + \log n_2 + \log n_3$, we complete the proof.
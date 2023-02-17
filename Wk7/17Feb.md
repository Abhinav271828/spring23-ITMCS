---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 17 February, Friday (Lecture 12)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Connection between Entropy and Counting
## Loomis-Whitney Inequality (contd.)
We now need to prove Shearer's Lemma, *i.e.*,
$$2H(X,Y,Z) \leq H(X,Y) + H(Y,Z) + H(Z,X).$$

To prove this, we note first that
$$\begin{split}
H(X,Y,Z) &= H(X) + H(Y \mid X) + H(Z \mid X, Y) \\
H(X,Y) &= H(X) + H(Y \mid X) \\
H(Y,Z) &= H(Y) + H(Z \mid Y) \\
H(Z,X) &= H(X) + H(Z \mid X)
\end{split}$$
Then we get
$$\begin{split}
H(X,Y) + H(Y,Z) + H(Z,X) &= H(X) + H(X) \\
&+ H(Y \mid X) + H(Y) \\
&+ H(Z \mid Y) + H(Z \mid Y) \\
&\geq 2[H(X) + H(Y \mid X) + H(Z \mid X, Y)] \\
&= 2H(X,Y,Z).
\end{split}$$

## Shearer's Lemma
The more general form of Shearer's Lemma states that if we have a family $\mathcal{F}$ of subsets of $[ n] = \{1, \dots, n\}$, such that each $i \in [n]$ appears in at least $k$ subsets, then we have
$$kH(X_1, \dots, X_n) \leq \sum_{F \in \mathcal{F}} H(X_F).$$

To prove this, consider some $F = \{i_1, \dots, i_t\}$ in $\mathcal{F}$. Then we have
$$\begin{split}
H(X_F) &= \sum_{i \in F} H(X_i \mid X_{F \cap [i-1]}) \\
&\geq \sum_{i \in F} H(X_i \mid X_{[i-1]}).
\end{split}$$

Taking the sum over all $F \in \mathcal{F}$, we get
$$\begin{split}
\sum_{F \in \mathcal{F}}H(X_F) &\geq \sum_{F \in \mathcal{F}} \sum_{i \in F} H(X_i \mid X_{[i-1]}) \\
&\geq k\left[\sum_{i=1}^n H(X_i \mid X_{[i-1]})\right] \\
&= k\sum_{i=1}^n H(X_i) \\
&\geq kH(X_1, \dots, X_n).
\end{split}$$

Substituting $n=3, k=2$ in this equality gives us the special case we used in the proof of the Loomis-Whitney inequality.

Shearer's Lemma also has a combinatorial form. Let us define the trace of a family $\mathcal{A}$ of subsets of $[n]$ w.r.t a subset $F \subseteq [n]$ as
$$\text{trace}_f(\mathcal{A}) = \{A \cap F \mid A \in \mathcal{A}\}.$$  
Now, if $\mathcal{F}$ is another family of subsets of $[n]$ such that each element in $[n]$ appears in at least $k$ subsets. Then for any family $\mathcal{A}$,
$$|\mathcal{A}| \leq \prod_{F \in \mathcal{F}} |\text{trace}_F(\mathcal{A})|^{\frac1k}.$$

To prove this, let $\mathbf{X} = (X_1, \dots, X_n) \in \mathbb{Z}_2^n$ be uniformly distributed on $\mathcal{A}$. Then we know that
$$H(X) = \log |\mathcal{A}|,$$
and $X_F$ takes at most $|\text{trace}_F(\mathcal{A})|$ values, so
$$H(X_F) \leq \log |\text{trace}_F(\mathcal{A})|.$$
Taking the summation over $\mathcal{F}$ gives us
$$k\log|\mathcal{A}| \leq \sum_{F \in \mathcal{F}} \log |\text{trace}_F(\mathcal{A})|,$$
QED.
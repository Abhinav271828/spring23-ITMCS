---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 21 February, Tuesday (Lecture 13)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Connection between Entropy and Counting (contd.)
Let
$$\mathcal{F} = \{\{1,2\}, \{3,4\}, \{1,3,4\}, \{1,2,4\}\}.$$
Show that, for jointly distributed r.vs. $X_1, \dots, X_4$,
$$\begin{split}
\sum_{F \in \mathcal{F}} H(X_F) &\geq 3[H(X_1) + H(X_4 \mid X_1, X_2, X_3)] \\
&+ 2[H(X_2 \mid X_1) + H(X_3 \mid X_1, X_2)].
\end{split}$$


$$\begin{split}
\sum_{F \in \mathcal{F}}H(X_F) &= \sum_{F \in \mathcal{F}} \sum_{i \in F} H(X_i \mid X_{[i-1]}) \\
&\geq [3H(X_1)] + [2H(X_2 \mid X_1)] \\
&+ [H(X_3) + H(X_3 \mid X_1)] \\
&+ [H(X_4 \mid X_2, X_1) + H(X_4 \mid X_1, X_3) + H(X_4 \mid X_3)] \\
&\geq 3H(X_1) + 3H(X_4 \mid X_1, X_2, X_3) \\
&+ 2H(X_2 \mid X_1) + 2H(X_3 \mid X_1, X_2),
\end{split}$$
QED.

# Connections between Entropy and Counting
## Shearer's Lemma (contd.)
We can write Shearer's Lemma in terms of distributions. Let $S$ be a r.v. distributed according to $P_S$ over a family $\mathcal{F}$ of subsets of $[n]$. We are given that, for all $i$, $P(i \in S) \geq \mu$.  
Then we can say that
$$\begin{split}
\mu H(X_1, \dots, X_n) &\leq \mathbb{E}_S[H(X_S)] \\
&= \sum_{s \in \mathcal{P}([n])} P_S(s)H(X_s)
\end{split}$$
implies that
$$kH(X_1, \dots, X_n) \leq \sum_{F \in \mathcal{F}} H(X_F),$$
where $k = \min_i \deg(i)$.

This can be proved by assuming that $P_S \sim \text{Unif}(\mathcal{F})$, which means that
$$P(i \in S) = \frac{\deg(i)}{|\mathcal{F}|} \geq \mu.$$

We can prove the premise as well, in the following manner:
$$\begin{split}
H(X_S) &= \sum_{i \in S} H(X_i \mid X_{S \cap [i-1]}) \\
&\geq \sum_{i \in S} H(X_i \mid X_{[i-1]}) \\
&= \sum_{i=1}^n \mathbb{1}(i \in S) H(X_i \mid X_{[i-1]}).
\end{split}$$
This gives us the result.

## Bregman's Theorem
Consider a matrix $A_{n \times n} = (a_{ij})$. Its *permanent* is defined as
$$\text{perm}(A) = \sum_{\sigma \in S_n} \prod_{i=1}^n a_{i\sigma(i)},$$
where $S_n$ is the set of all permutations of $[n]$.

Note that this is very similar to the determinant
$$\det(A) = \sum_{\sigma \in S_n} \text{sgn}(\sigma)\prod_{i=1}^na_{i\sigma(i)}.$$

The statement of the theorem is as follows. For any $A \in \mathbb{Z}_2^{n \times n}$, let $d_i$ be the number of ones in row $i$. Then,
$$\text{perm}(A) \leq \prod_{i=1}^n(d_i!)^{\frac1{d_i}}.$$

To prove this, consider a bipartite graph with two sets $V = \{v_1, \dots, v_n\}, W = \{w_1, \dots, w_n\}$ of $n$ vertices each. Let there be an edge between $v_i$ and $w_j$ iff $a_{ij} = 1$.

We know that a *matching* is a set of edges with no common vertices, and a *perfect matching* is one that covers all vertices. We can see that for a bipartite graph $G = (V,W,E)$ with a perfect matching $P \subseteq E$, we must have $|P| = n$.  
We note that for a fixed $\sigma \in S_n$,
$$\{a_{i\sigma(i)} \in E : i \in [n]\}$$
is a matching (it need not be perfect because not all vertices may be included).
---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 07 February, Tuesday (Lecture 9)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Connection between Entropy and Counting
We know that for any discrete r.v. $X$, with support $\mathcal{X}$, then
$$H(X) \leq \log|\mathcal{X}|,$$
where equality is achieved when $X \sim \text{Unif}(\mathcal{X})$.

## Sorting
Consider the problem of sorting. We know that if $t$ bits are required to represent a permutation of the input, then
$$n! \leq 2^t.$$
We also know that each comparison gives one bit of information. Thus we need at most $\log n!$ comparisons to reach $t$ bits.  
If we represent the outputs of the comparisons as r.vs. $Y_1, \dots, Y_t$, we can obtain the same inequality via an information-theoretic approach. We know that the permutation of the inputs is a deterministic function of $Y_1, \dots, Y_t$, and so we have that
$$\begin{split}
\log n! &\leq H(f(Y_1, \dots, Y_t)) \\
&\leq H(Y_1, \dots, Y_t) \\
&\leq H(Y_1) + \dots + H(Y_t) \\
&\leq t.
\end{split}$$

## Binomial Coefficients
We can easily show, by the PHP, that if there are $n$ movies and $2^n$ people who watch at least one movie each, then there must be at least two people who have seen the same subset of movies.

Consider the following problem, however – we have $2n$ movies and $2^n$ people, each of whom watches at least $\frac9{10}2n$ movies. Can we prove a similar claim?
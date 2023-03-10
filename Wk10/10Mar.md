---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 10 March, Friday (Lecture 16)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

**N.B.** I don't know how this ties in with the stuff that was there so far.

# Connections between Entropy and Counting
## Permutations
Consider a set of numbers $a_1, \dots, a_n$. We wish to find the number of permutations in which a fixed set $a_1, \dots, a_d$, where $d < n$, occur in that order. We can show that this is $\frac{n!}{d!}$.

We can show first that the number of permutations in which a certain $a_i$ occurs at the $j^\text{th}$ place, among $a_1, \dots, a_d$, is $\frac{n!}{d}$.  

Now consider a matrix $A \in \mathbb{Z}_2^{n \times n}$ and a perfect matching $\sigma$ in $A$.  
We have seen that
$$N_i(\sigma, \tau) = |D_i - \left\{\sigma(\tau(l)) \mid l < \tau^{-1}(i)\right\}|.$$
Note that if $\tau$  puts $i$ first among $\sigma^{-1}(D_i)$, then $N_i(\sigma, \tau) = d_i$ (where $d_i = |D_i|$).  
Similarly, if it appears second, then $N_i(\sigma, \tau) = d_i - 1$.

Using the proposition that we started with, among all $\tau \in S_n$, the number of permutations in which $i$ occurs first (or at any given position $j$) among $i, u_1, \dots, u_{d_i - 1}$, is
$$\frac{n!}{d_i}.$$
In other words
$$\sum_{\tau \in S_n}1\{N_i(\sigma,\tau)=j\} = \frac{n!}{d_i}.$$
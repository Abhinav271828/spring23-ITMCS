---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 14 April, Friday (Lecture 23)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Information Leakage
## Guessing Framework (contd.)
If $U$ and $Y$ are jointly distributed according to $P_{UY}$, and an adversary wishes to guess $U$ on observing $Y = y$. Then we define
$$u^* = \argmax_u P_{U \mid Y}(u \mid y),$$
and set $P_{\hat U \mid Y}(u^* \mid y) = 1$. This solves the optimisation problem
$$\max_{P_{\hat U \mid Y = y}} \mathbb{E}_{U \mid Y = y} [P_{\hat U \mid Y}(u \mid y)].$$

What if the adversary has not observed any single realisation of $Y$, but requires a strategy that would work well on average? This corresponds to the optimisation problem
$$\max_{P_{\hat U \mid Y}} \left[P_Y(0)\mathbb{E}_{U \mid Y = 0}[P_{\hat U \mid Y}(U \mid 0)] + P_Y(1)\mathbb{E}_{U \mid Y = 1}[P_{\hat U \mid Y}(U \mid 1)]\right].$$

We can take the $\max$ inside to get
$$P_Y(0) \cdot \max_{P_{\hat U \mid Y = 0}} \mathbb{E}_{U \mid Y = 0} [P_{\hat U \mid Y} (U \mid 0)] + P_Y(1) \cdot \max_{P_{\hat U \mid Y = 1}} \mathbb{E}_{U \mid Y = 1}[P_{\hat U \mid Y}(U \mid 1)].$$

Given this framework, let us define the probability $P_C(U)$ of correctly guessing $U$:
$$P_C(U) = \mathbb{E}_U[P_{\hat U}(U)] = \max_u P_U(u).$$

We now define the "uncertainty in $U$", instead of using entropy, as
$$\log\frac1{P_C(U)}.$$
Then we can define the information leakage between $U$ and $Y$ as
$$\log\frac1{P_C(U)} - \log\frac1{P_C(U \mid Y)} = \log\frac{P_C(U \mid Y)}{P_C(U)}.$$
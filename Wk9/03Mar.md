---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 03 March, Friday (Lecture 15)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Connections between Entropy and Counting
## Bregman's Theorem (contd.)
Let us define $N_i(\sigma, \tau)$ as the number of possibilities for $\sigma(i)$ given $\sigma(\tau(l < \tau^{-1}(i)))$. Thus
$$N_i(\sigma, \tau) = |D_i - \{\sigma(\tau(l)) \mid l < \tau^{-1}(i)\}|.$$

We will make use of the following lemma. For a fixed $\sigma \in \text{PF}$,
$$\sum_{\tau \in S_n} \frac{1\{N_i(\sigma, \tau) = j\}}{n!} = \frac1{d},$$
for all $j \in [d_i]$.  
Thus we can write that
$$\operatorname*{Pr}_{\tau \sim \text{Unif}(S_n)} (N_i(\sigma, \tau) = j) = \frac1{d_i}, \forall j \in [d_i].$$

Using the lemma discussed in [the previous class](../Wk8/24Feb.md), we can say that
$$\begin{split}
\sum_{\tau \in S_n} \frac1{n!} H(\sigma(i) \mid \sigma(\tau(l < \tau^{-1}(i)))) &\leq \sum_{\tau \in S_n} \frac1{n!}\sum_{j=i}^{d_i} P(N_i(\sigma, \tau) = j) \log(j) \\
&= \sum_{j=1}^{d_i} \frac{\sum_{\tau \in S_n} P_\sigma(N_i(\sigma, \tau) = j)}{n!} \log(j) \\
&= \sum_{j=1}^{d_i} \log(j) \left[\frac1{d_i}\right].
\end{split}$$
since $|N_i(\sigma, \tau)| < D_i$.


कभी तक़दीर का मातम
कभी दुनिया का गिला
मंज़िले-इश्क़ में हर गाम पे
रोना आया

ऐ मुहब्बत तेरे अंजाम पे
रोना आया
जाने क्यों आज तेरे नाम पे
रोना आया

यूँ तो हर शाम
उम्मीदों में गुज़र जाती थी
आज कुछ बात है जो शाम पे
रोना आया

जब हुआ ज़िक्र ज़माने में
मुहब्बत का शकील
मुझको अपने दिले-नाकाम पे
रोना आया
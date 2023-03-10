---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 24 February, Friday (Lecture 14)
author: Taught by Prof. Gowtham Kurri
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Connections between Entropy and Counting
## Bregman's Theorem (contd.)
Let $\sigma \in S_n$ be a permutation of $[n]$. Then we know that $\sigma$ is a perfect matching iff
$$\prod_{i=1}^n a_{i\sigma(i)} = 1.$$
Therefore $\text{perm}(A)$ is the number of perfect matches in the graph corresponding to $A$.

Now, let $\sigma \sim \text{Unif(PF)}$ be a r.v., where $\text{PF} = \{\alpha \in S_n : a_{i\alpha(i)} = 1, \forall i \in [n]\}$ is the set of all perfect matchings in $A$.

Then we can say that $\log|\text{PF}| = H(\sigma)$. Then,
$$\begin{split}
\log|\text{PF}| &= H(\sigma(1), \dots, \sigma(n)) \\
&= \sum_{i=1}^n H(\sigma(i) \mid \sigma(1), \dots, \sigma(i-1)) \\
&\leq \sum_{i=1}^n H(\sigma(i)).
\end{split}$$

We note that for any $i$, $\sigma(i)$ can take $d_i$ values. Therefore,
$$|\text{PF}| \leq \prod_{i=1}^n d_i.$$
However, this is not a tight enough bound.

Define $D_i = \{j : a_{ij} = 1\}$. Then we noted above that $\sigma(i)$ can only take values in $D_i$. However, we can restrict this further – we know that it can only take values in
$$D_i - \{\sigma(1), \dots, \sigma(i-1)\}.$$

Let $\tau \in S_n$ be a fixed (arbitrary) permutation. Then
$$\begin{split}
H(\sigma) &= H(\sigma(1), \dots, \sigma(n)) \\
&= H(\sigma(\tau(1)), \dots, \sigma(\tau(n))),
\end{split}$$
which means that we can say that
$$H(\sigma) = \frac1{n!} \sum_{\tau \in S_n} H(\sigma(\tau(1)), \dots, \sigma(\tau(n))).$$

We can express the term in the sum as
$$\begin{split}
H(\sigma(\tau(1)), \dots, \sigma(\tau(n))) &= \sum_{k=1}^n H(\sigma(\tau(k)) \mid \sigma(\tau(1)), \dots, \sigma(\tau(k-1))) \\
&= \sum_{i=1}^n H(\sigma(i) \mid \sigma(\tau(l)) : l < \tau^{-1}(i))
\end{split}$$

We will use the following lemma. If $\mathcal{X}$ is the disjoint union of sets $A_i$, $i \in [r]$, and we have a joint distribution $P_{XY}$ such that
$$|\text{supp}(Y \mid X = x_i)| \leq i$$
for all $x_i \in A_i$, then
$$H(Y \mid X) \leq \sum_{i=1}^r \log(i) P(X \in A_i).$$

रंजिश ही सही दिल ही दुखाने के लिए आ
आ फिर से मुझे छोड़के जाने के लिए आ

पहले से मरासिम ना सही फिर भी कभी तो
रस्मो-रहे-दुनिया ही निभाने के लिए आ

इक उम्र से हूँ लज़्ज़ते-गिर्या से भी महरूम
ऐ राहते-जाँ मुझको रुलाने के लिए आ

कुछ तो मेरे पिंदारे-मुहब्बत का भरम रख
तू भी तो कभी मुझको मनाने के लिए आ

किस किस को बताएँगे जुदाइ का सबब हम
तू मुझसे ख़फ़ा है तो ज़माने के लिए आ

अब तक दिले-ख़ुश-फ़हम को तुझसे हैं उम्मीदें
ये आख़री शम्में भी बुझाने के लिए आ
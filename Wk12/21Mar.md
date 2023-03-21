---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 21 March, Tuesday (Lecture 18)
author: Taught by Prof. Gowtham Kurri, Prof. Prasad Krishnan
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Entropy for Continuous Random Variables
## Quantisation (contd.)
We have seen how to quantise a continuous r.v. $X$ into a discrete one $X_\Delta$. We also have that
$$\begin{split}
H(X_\Delta) &= -\sum_i f(x_i)\Delta \log(f(x_i)\Delta) \\
&= -\sum_i f(x_i)\Delta \log(f(x_i)) - \sum_if(x_i)\Delta \log \Delta \\
&= -\sum_i f(x_i)\Delta \log(f(x_i)) - \log\Delta \\
\implies H(X_\Delta) + \log\Delta &= -\sum_i f(x_i)\Delta \log(f(x_i)).
\end{split}$$
The RHS tends to an integral as $\Delta \to 0$. Therefore we have
$$\lim_{\Delta \to 0} H(X_\Delta) + \log\Delta = h(X).$$

If $\Delta = 2^{-n}$, *i.e.*, we have an $n$-bit quantiser, then
$$H(X_\Delta) \operatorname*{\longrightarrow}_{\Delta \to 0} h(X) + n.$$

## Scaling
If $X \sim f$ is a continuous r.v., and $Y = aX$, then $h(Y) = h(X) + \log|a|$.

# Total Variational Distance
Let $P_X$ and $Q_X$ be two distributions on the same support $\mathcal{X}$. Then the total variational distance between them is defined as
$$\text{TVD}(P_X, Q_X) = \frac12 \sum_{x \in \mathcal{X}} |P_X(x) - Q_X(x)|.$$

This is a distance metric over probability distributions. Thus it satisfies the following properties:

* $\text{TVD}(P_X, P_X) = 0$
* $\text{TVD}(P_X, Q_X) \geq 0$
    - $\text{TVD}(P_X, Q_X) = 0 \iff P_X = Q_X$
* $\text{TVD}(P_X, Q_X) = \text{TVD}(Q_X, P_X)$
* $\text{TVD}(P_X, Q_X) \leq \text{TVD}(P_X, R_X) + \text{TVD}(R_X, Q_X)$
* $0 \leq \text{TVD}(P_X, Q_X) \leq 1$

We can easily show that if $\text{TVD}(P_X, Q_X) = 1$, then $\mathcal{X} = \text{supp}(P_X) \sqcup \text{supp}(Q_X)$.

**Lemma.** $\text{TVD}(P_X, Q_X) = \sup_{A \subseteq \mathcal{X}} (P_X(A) - Q_X(A)).$  
To prove this, let us define $S = \{x : P_X(x) > Q_X(x)\}$. Then we have
$$\begin{split}
P_X(S) - Q_X(S) &= \frac12 [P_X(S) - Q_X(S) + Q_X(S^c) + P_X(S^c)] \\
&= \frac12 \sum_{x \in S} P_X(x) - Q_X(x) + \frac12 \sum_{x \in S^c} Q_X(x) - P_X(x) \\
&= \frac12 \sum_{x \in \mathcal{X}} |P_X(x) - Q_X(x)| \\
&= \text{TVD}(P_X, Q_X).
\end{split}$$

Now we know that $\text{TVD}(P_X, Q_X) = P_X(S) - Q_X(S)$. We now need to show that $P_X(A) - Q_X(A) \leq P_X(S) - Q_X(S)$ for all $A \subseteq \mathcal{X}$. This can be done in a straightforward way, as follows.
$$\begin{split}
P_X(A) - Q_X(A) &= \sum_{x \in A \cap S} P_X(x) - Q_X(x) + \sum_{x \in A \cap S^c} P_X(x) - Q_X(x) \\
&\leq \sum_{x \in S} P_X(x) - Q_X(x) + \sum_{x \in A \cap S^c} P_X(x) - Q_x(x) \\
&\leq P_X(S) - Q_X(S) + 0 \\
\leq P_X(S) - Q_X(S),
\end{split}$$
QED.

Therefore, we have shown that the supremum of $P_X(A) - Q_X(A)$ is achieved at $A = S$, and that this value is equal to $\text{TVD}(P_X, Q_X)$.

आज जाने की ज़िद ना करो
यूँही पहलू में बैठे रहो
हाए मर जाएँगे हम तो लुट जाएँगे
ऐसी बातें किया ना करो

तुम ही सोचो ज़रा क्यों ना रोकें तुम्हें
जान जाती है जब उठके जाते हो तुम
तुमको अपनी क़सम जाने-जाँ
बात इतनी मेरी मान लो
आज जाने की ज़िद ना करो

कितना मासूमो-रंगीन है यह समाँ
हुस्न और इश्क़ की आज मेराज है
कल की किसको ख़बर जाने-जाँ
रोक लो आज की रात को
आज जाने की ज़िद ना करो

वक़्त की क़ैद में ज़िन्दगी है मगर
चंद घड़ियाँ यही हैं जो आज़ाद हैं
इनको खोकर मेरी जाने-जाँ
उम्रभर ना तरसते रहो
आज जाने की ज़िद ना करो
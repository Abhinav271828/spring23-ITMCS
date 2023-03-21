---
title: Information-Theoretic Methods in Computer Science (CS1.502)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 14 March, Tuesday (Lecture 17)
author: Taught by Prof. Prasad Krishnan
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Entropy for Continuous Random Variables
Consider a discrete r.v. $X$. It has an associated PMF $P_X$, based on which we define its entropy as
$$H(X) = -\sum_{x \in \text{supp}(P_X)} P_X(x) \log P_X(x).$$

If $X$ is continuous, its distribution is captured in the *density function* $f$, which has the property that
$$P(a \leq X \leq b) = \int_a^bf(x)dx.$$
We use this density function to calculate the entropy as
$$h(X) = \int_{x \in \text{supp}(f)} f(x) \log f(x) dx.$$
This is called *differential entropy*, and is defined only for continuous r.vs.

If $X \sim \text{Unif}[a, b]$, then
$$f(x) \begin{cases} \frac1{b-a} & x \in [a,b] \\ 0 & \text{otherwise}. \end{cases}$$
It can be shown then that $h(X) = \log(b-a)$. Note that this is negative when $b-a < 1$.

Consider the Gaussian distribution. We can take, without loss of generality, a distribution centred around 0. Thus, let $X \sim \mathcal{N}(0, \sigma^2)$. Then
$$f(x) = \frac1{\sigma\sqrt{2\pi}}e^{-\frac{x^2}{2\sigma^2}}.$$

We can then calculate
$$\begin{split}
h(X) &= \int_{-\infty}^{\infty} ke^{-\frac{x^2}{2\sigma^2}} (\log_2 e \cdot \frac{x^2}{2\sigma^2} - \log k) dx \\
&= \frac{\log_2 e}{2\sigma^2} \int_{-\infty}^{\infty} x^2 ke^{-\frac{x^2}{2\sigma^2}} dx - \log k \int_{-\infty}^{\infty} ke^{-\frac{x^2}{2\sigma^2}} dx \\
&= \frac{\log_2 e}{2\sigma^2} \mathbb{E}[X^2] - \log k \cdot 1 \\
&= \frac{\log_2 e}{2\sigma^2}(\text{Var}(X) + \mathbb{E}[X]^2) - \log k \\
&= \frac12 \log_2 e + \log(\sigma \sqrt{2\pi}) \\
&= \frac12\log(2\pi\sigma^2e).
\end{split}$$

The definition of entropy naturally extends to joint variables
$$h(\mathbf{X}) = -\int_{\mathbf{x} \in \text{supp}(f_\mathbf{X})} f_\mathbf{X}(\mathbf{x}) \log f_\mathbf{X}(\mathbf{x}) d\mathbf{x}.$$

In the two-variable case, we can show that $$h(X,Y) = h(Y) + h(X \mid Y).$$

Conditional entropy is defined analogous to the discrete case as
$$h(X \mid Y) = -\int_y f(y) \left[-\int_x f(x \mid y) \log f(x \mid y) dx \right]dy.$$

For example, let us consider the case of a jointly distributed Gaussian, or a multivariate Gaussian distribution $(X_1, \dots, X_n) \sim \mathcal{N}(\mu_X, K_X)$. Here, $\mu_X = (\mu_{X_1}, \dots, \mu_{X_n})$ is the mean vector, and $K_{ij} = \mathbb{E}[(X_i - \mu_{X_i})(X_j - \mu_{X_j})]$ is the covariance matrix. The PDF of this distribution is
$$\phi_\mathbf{X}(\mathbf{x}) = \frac1{(2\pi)^\frac{n}2 \sqrt{\det(K)}} e^{-\frac12(\mathbf{x}-\mu_X)^T K_X^{-1} (\mathbf{x} - \mu_X)}.$$

The entropy of this distribution is given by 
$$h(\mathbf{X}) = \frac12 \log \left((2\pi e)^\frac{n}{2} |\det(K)|\right).$$

Among all distributions (over $\mathbb{R}$) with variance $\sigma^2$, the Gaussian $\mathcal{N}(\mu, \sigma^2)$ has the highest entropy. This extends to the multivariate case as well.

## Mutual Information
The Kullback-Leibler divergence is defined for continuous r.vs. the same way as for discrete ones:
$$D(f || g) = \int_{x \in \text{supp}(f)} f(x) \log \frac{f(x)}{g(x)} dx.$$
This quantity is always non-negative.

Now, we define the mutual information, as usual, as
$$I(X;Y) = D(f_{X,Y} || f_X f_Y).$$

It can be shown that $I(X;Y) = h(X) + h(Y) - h(X;Y)$, as in the discrete case.

## Quantisation
Let $f$ be a PDF. We can say, by the intermediate value theorem, that for any $x_1, \Delta$, there exists $\tilde{x}_1 \in [x_1, x_1 + \Delta]$ such that
$$\int_{x_1}^{x_1+\Delta}f(x)dx = \Delta f(\tilde{x}_1).$$

We can therefore quantise the real number line  into intervals of $[\Delta i, \Delta(i+1)]$ for $i \in \mathbb{Z}$, and we can identify a discrete r.v. $X_\Delta = \tilde{x}_i$ as a function of a r.v. $i$.
$$p_{X_\Delta}(\tilde{x}_i) = \int_{\Delta i}^{\Delta(i+1)} f_X(x) dx.$$

What is the relationship between $h(X)$ and $H(X_\Delta)$? We can show that the following statement holds in the limit of $\Delta \to 0$:
$$H(X_\Delta) = h(X) + \log\Delta.$$

ऐसा देखा नहीं खूबसूरत कोइ
जिस्म जैसे अजन्ता की मूरत कोइ

जिस्म जैसे निगाहों में जादू कोइ
जिस्म नग़्मा कोइ जिस्म ख़ुशबू कोइ

जिस्म जैसे कि खिलता हुआ इक चमन
जिस्म जैसे कि सूरज की पहली किरन

जिस्म जैसे महकती हुइ चाँदनी
जिस्म जैसे मचलती हुइ रागिनी

जिस्म तरशा हुआ दिल-कशो-दिल-नशीं
सन्दलीं सन्दलीं मरमरीं मरमरीं

हुस्ने-जानाँ की तारीफ़ मुमकिन नहीं

चहरा इक फूल की तरह शादाब है
चहरा उसका है या कोइ महताब है

चहरा जैसे ग़ज़ल चहरा जाने-ग़ज़ल
चहरा जैसे कलि चहरा जैसे कँवल

चहरा जैसे तसव्वुर भी तस्वीर भी
चहरा इक ख़्वाब भी चहरा ताबीर भी

चहरा कोइ अलिफ़-लैलवी दास्ताँ
चहरा इक पल यक़ीं चहरा इक पल गुमाँ

चहरा जैसे कि चहरा कहीं भी नहीं
माहरू माहरू महजबीं महजबीं

हुस्ने-जानाँ की तारीफ़ मुमकिन नहीं
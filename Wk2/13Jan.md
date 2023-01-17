
$$
I(X;Y) = - \sum _{X} p(x) \log _2 {p(x)} - \sum _{Y} p(y) \log _2 {p(y)} + \sum _X \sum _Y p(x, y) \log _2 p(x, y)
$$

Generally, 

$$
D(p \mid \mid q) \neq D(q \mid \mid p)
$$

## Properties of KL divergence


$$
D( p \mid \mid q) \geq 0 \text{ with equality if and only if } p = q
$$

one of the proofs uses the property that log is a concave function, i.e. double derivative is less than 0.


$$
D(p \mid \mid q) = \sum _x p(x) \log_2 {\frac{p(x)}{q(x)}}
$$


We know for a concave function

$$
f(\sum \lambda_i x_i) \geq \sum \lambda_i f(x_i) \text{ such that } \sum \lambda_i = 1
$$

therefore

$$
D(p \mid \mid q) = \sum _x - p(x) \log _2 {\frac{q(x)}{p(x)}}
$$

by the concavity theorem

$$
D(p \mid \mid q) \geq - \log _2 {\sum _{x \in Supp(p(x))} p(x) \frac{q(x)}{p(x)}}
$$

We cancel the $p(x)$'s, then the quantity inside log is less than $1$ therefore the whole thing is greater than $0$

$$
D(p \mid \mid q) \geq 0
$$

Now, let us consider equal to $0$, since we have proven that $D(p \mid \mid q) \geq 0$.



% TODO: complete proof



$$
D(p \mid \mid q) \geq 0 \text{ and } p=q \Leftrightarrow D(p \mid \mid q) = 0
$$


Since mutual information is itself a divergence, we have

$$
I(X;Y) = D(P_{X, Y} || P_X P_Y) \geq 0
$$

and therefore is equal to $0$ when $X$ and $Y$ are independent.


$$
H(X) \geq 0
$$


and 

Claim:

$$
H(X) \leq \log _2 {|Supp(p_X)|}
$$


Consider that $X \sim p_X$

Let $u$ be the uniform distribution over the support of p

$$
D(p \mid \mid u) = \sum _{x \in Supp(x)} p(x) \log _2 {\frac{p(x)}{\frac{1}{|Supp(p_x)|}}}
$$



### Data processing inequality


You have three random variables $X$, $Y$. and $Z$

Suppose

$$
X \to Y \to Z
$$

form a Markov chain: that $X$ and $Z$ are independent except for the connection through $Y$

thus that means

$$
p_ {X, Y \mid Z} (x, z \mid y) = p_{X \mid Y} (x \mid y) p_{Z \mid Y}(z \mid y)
$$

So for this Markov chain property, we'll have

$$
I(X ; Y) \geq I(X ; Z)
$$

Intuition: $Y$ is a bottle-neck that is why

Proof:

Consider this quantity $I(X;Y, Z$)

$$
I(X ; Y, Z) = I(X ; Y) + I(X; Y \mid Z) = I(X; Z) + I (X ; Y \mid Z)
$$

We can say that $I(X; Y \mid Z) = 0$ because of the Markov chain property.
# Black-Scholes-Merton — Risk-Neutral Pricing

## Big Picture

There are two ways to obtain Black-Scholes prices:

1. **PDE / replication approach**
2. **Risk-neutral expectation approach**

The PDE method derives a differential equation and then solves it.

The risk-neutral method is more direct:

[
\text{Option price} =
E^Q[\text{discounted payoff}]
]

where (Q) is the risk-neutral probability measure.

For a European option, this means:

[
C(t,S)=E_t^Q\left[e^{-r(T-t)}g(S(T))\right]
]

For a European call:

[
C(t,S)=E_t^Q\left[e^{-r(T-t)}(S(T)-K)^+\right]
]

---

# 1. Stock Dynamics Under the Real Probability

Under the real-world probability (P), the Black-Scholes-Merton stock model is:

[
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
]

The explicit solution is:

[
S(T)=S(t)\exp\left[\left(\mu-\frac{1}{2}\sigma^2\right)(T-t)+\sigma(W(T)-W(t))\right]
]

Here:

* (\mu) is the real-world expected return
* (\sigma) is volatility
* (W) is Brownian motion under the real-world measure (P)

---

# 2. Stock Dynamics Under the Risk-Neutral Probability

For pricing, we work under the risk-neutral probability (Q).

Under (Q), the stock must grow on average at the risk-free rate (r), not at (\mu).

So the stock dynamics become:

[
dS(t)=rS(t)dt+\sigma S(t)dW^Q(t)
]

The explicit stock formula under (Q) is:

[
S(T)=S(t)\exp\left[\left(r-\frac{1}{2}\sigma^2\right)(T-t)+\sigma(W^Q(T)-W^Q(t))\right]
]

## Key Point

To move from the real-world model to the pricing model:

[
\mu \rightarrow r
]

and:

[
W \rightarrow W^Q
]

This is the central practical step in Black-Scholes risk-neutral pricing.

---

# 3. Why This Is Useful

Under (Q), the option price becomes a discounted expected payoff.

For a European payoff (g(S(T))):

[
V(t,S)=E_t^Q\left[e^{-r(T-t)}g(S(T))\right]
]

Since (S(T)) can be written explicitly in terms of a normally distributed Brownian increment, pricing becomes a probability / integration problem.

This is often easier than solving the PDE directly.

---

# 4. Normal Distribution Connection

Under (Q):

[
W^Q(T)-W^Q(t)
]

is normally distributed with:

[
\text{mean}=0
]

[
\text{variance}=T-t
]

Therefore:

[
\frac{W^Q(T)-W^Q(t)}{\sqrt{T-t}}
]

is a standard normal random variable.

This is why the Black-Scholes formula contains the standard normal cumulative distribution function:

[
N(x)
]

where:

[
N(x)=P(Z\leq x)
]

and:

[
Z\sim N(0,1)
]

---

# 5. Standard Normal CDF

The function (N(x)) gives the probability that a standard normal random variable is less than or equal to (x):

[
N(x)=P(Z\leq x)
]

It can also be written as:

[
N(x)=\int_{-\infty}^{x}\frac{1}{\sqrt{2\pi}}e^{-y^2/2}dy
]

In words:

(N(x)) is the area under the standard normal bell curve to the left of (x).

---

# 6. European Call Price

For a European call:

[
g(S(T))=(S(T)-K)^+
]

So the price is:

[
C(t,S)=E_t^Q\left[e^{-r(T-t)}(S(T)-K)^+\right]
]

The payoff is positive only when:

[
S(T)>K
]

That is, only when the option finishes in the money.

---

# 7. Splitting the Call Payoff

The call payoff can be rewritten as:

[
(S(T)-K)^+
==========

## S(T)\mathbf{1}_{{S(T)>K}}

K\mathbf{1}_{{S(T)>K}}
]

where:

[
\mathbf{1}_{{S(T)>K}}
]

is an indicator function.

It equals:

[
1
]

if:

[
S(T)>K
]

and equals:

[
0
]

otherwise.

Therefore:

[
C(t,S)
======

## e^{-r(T-t)}E_t^Q[S(T)\mathbf{1}_{{S(T)>K}}]

Ke^{-r(T-t)}E_t^Q[\mathbf{1}_{{S(T)>K}}]
]

This creates the two terms of the Black-Scholes formula.

---

# 8. The Second Term

The easier term is:

[
E_t^Q[\mathbf{1}_{{S(T)>K}}]
]

The expectation of an indicator is the probability of the event.

So:

[
E_t^Q[\mathbf{1}_{{S(T)>K}}]
============================

Q(S(T)>K)
]

This is the risk-neutral probability that the option finishes in the money.

Therefore the second term is:

[
Ke^{-r(T-t)}Q(S(T)>K)
]

In the Black-Scholes formula, this probability becomes:

[
N(d_2)
]

So the second term becomes:

[
Ke^{-r(T-t)}N(d_2)
]

---

# 9. Finding (d_2)

Under (Q):

[
S(T)=S(t)\exp\left[\left(r-\frac{1}{2}\sigma^2\right)(T-t)+\sigma(W^Q(T)-W^Q(t))\right]
]

The event:

[
S(T)>K
]

can be rewritten by taking logarithms and isolating the standard normal variable.

This gives:

[
Q(S(T)>K)=N(d_2)
]

where:

[
d_2=
\frac{
\ln(S/K)+\left(r-\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
]

## Intuition

(d_2) measures how far the option is from being in the money, adjusted for:

* current stock price
* strike price
* interest rate
* volatility
* time to maturity

---

# 10. The First Term

The first term is:

[
e^{-r(T-t)}E_t^Q[S(T)\mathbf{1}_{{S(T)>K}}]
]

This is harder because it contains both:

* the stock price (S(T))
* the indicator that the option finishes in the money

The integral can be computed using normal distribution calculus.

The result is:

[
S(t)N(d_1)
]

where:

[
d_1=
\frac{
\ln(S/K)+\left(r+\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
]

and:

[
d_1=d_2+\sigma\sqrt{T-t}
]

---

# 11. Black-Scholes Call Formula

Putting the two terms together:

[
C(t,S)=S(t)N(d_1)-Ke^{-r(T-t)}N(d_2)
]

where:

[
d_1=
\frac{
\ln(S/K)+\left(r+\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
]

[
d_2=
\frac{
\ln(S/K)+\left(r-\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
]

or:

[
d_2=d_1-\sigma\sqrt{T-t}
]

---

# 12. What (N(d_2)) Means

In the risk-neutral approach:

[
N(d_2)
]

has a clear interpretation:

[
N(d_2)=Q(S(T)>K)
]

It is the risk-neutral probability that the call option finishes in the money.

This is why (N(d_2)) appears next to the discounted strike.

---

# 13. What (N(d_1)) Means

The term:

[
N(d_1)
]

comes from computing:

[
E_t^Q[S(T)\mathbf{1}_{{S(T)>K}}]
]

It is not simply the probability that the option finishes in the money.

It is a probability-like adjustment for the stock-price-weighted part of the payoff.

A practical way to remember the formula:

[
S(t)N(d_1)
]

is the stock-price part of the call value.

[
Ke^{-r(T-t)}N(d_2)
]

is the discounted strike-price part of the call value.

---

# 14. Risk-Neutral Pricing vs PDE Pricing

Both approaches produce the same Black-Scholes formula.

## PDE Approach

The PDE approach uses:

* Ito's rule
* replication
* self-financing portfolio
* elimination of Brownian risk

It leads to:

[
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
]

Then one solves the PDE.

## Risk-Neutral Approach

The risk-neutral approach uses:

* discounted expected payoff under (Q)
* stock dynamics with (\mu) replaced by (r)
* normal distribution calculations

It leads directly to:

[
C(t,S)=E_t^Q[e^{-r(T-t)}(S(T)-K)^+]
]

Then one computes the expectation.

## Main Difference

The PDE approach emphasizes replication.

The risk-neutral approach emphasizes expected discounted payoff under (Q).

They are equivalent in the Black-Scholes-Merton model.

---

# 15. Deriving the PDE from Risk-Neutral Pricing

The risk-neutral approach also gives a fast way to recover the Black-Scholes PDE.

Under (Q):

[
dS=rSdt+\sigma SdW^Q
]

If:

[
C=C(t,S)
]

then Ito's rule gives:

[
dC=
\left(
C_t+rSC_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma SC_SdW^Q
]

Now discount the option price:

[
e^{-rt}C(t,S(t))
]

For this discounted price to be a martingale under (Q), its (dt) term must be zero.

Applying the product rule gives the drift:

[
C_t+rSC_S+\frac{1}{2}\sigma^2S^2C_{SS}-rC
]

Set this equal to zero:

[
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
]

This is exactly the Black-Scholes PDE.

## Key Intuition

A discounted price process under the risk-neutral measure must be a martingale.

A martingale has zero drift.

Therefore, the discounted option price must have zero (dt) term.

---

# 16. Why This PDE Derivation Is Faster

The original replication derivation required:

1. writing option dynamics
2. writing portfolio dynamics
3. matching the Brownian terms
4. matching the drift terms
5. deriving the PDE

The risk-neutral derivation uses:

1. write stock dynamics under (Q)
2. apply Ito's rule to (C(t,S))
3. discount
4. set the drift equal to zero

This is often faster, especially for more advanced models.

---

# 17. Implied Volatility

Black-Scholes assumes volatility (\sigma) is constant.

But market prices often do not behave as if one constant volatility applies to every option on the same underlying asset.

## Definition

Implied volatility is the value of (\sigma) that makes the Black-Scholes model price equal to the observed market option price.

Symbolically:

[
C_{BSM}(\sigma_{\text{imp}})=C_{\text{market}}
]

## Meaning

The market price is observed.

The Black-Scholes formula is known.

We solve backward for the volatility that makes the formula match the market price.

---

# 18. Volatility Smile

If the Black-Scholes-Merton model were perfectly correct, then all options on the same stock with the same maturity should imply the same volatility.

So implied volatility as a function of strike should be flat.

But in real markets, implied volatility often varies by strike.

This produces a curve called a volatility smile.

## Interpretation

A volatility smile means the market is not pricing options exactly according to the simple Black-Scholes model.

Often, options with very high or very low strikes have higher implied volatility.

This means the market assigns higher prices to extreme outcomes than the basic Black-Scholes model would suggest.

---

# 19. Why Volatility Smile Matters

The volatility smile suggests that the assumptions of Black-Scholes-Merton are too simple.

Possible reasons include:

* volatility is not constant
* returns are not perfectly log-normal
* markets worry about extreme events
* hedging is not perfect in practice
* jumps or stochastic volatility may matter

This motivates more advanced models, especially stochastic volatility models.

---

# 20. Stochastic Volatility Motivation

A stochastic volatility model allows volatility to change randomly over time.

Instead of:

[
\sigma=\text{constant}
]

we allow:

[
\sigma(t)=\text{random process}
]

This was historically one of the first major extensions of the Black-Scholes-Merton model.

The motivation is simple:

In stock option pricing, (\sigma) is often the most important model parameter.

If market prices imply different volatility levels for different strikes, then constant volatility is not realistic enough.

---

# 21. Main Conceptual Flow

The risk-neutral pricing section follows this logic:

1. In Black-Scholes-Merton, the stock has log-normal dynamics.
2. Under the risk-neutral probability, replace (\mu) with (r).
3. Price a European payoff as discounted expected payoff under (Q).
4. For a call, split the payoff into two terms.
5. The strike term gives (Ke^{-r(T-t)}N(d_2)).
6. The stock term gives (S(t)N(d_1)).
7. Together they give the Black-Scholes formula.
8. The same risk-neutral martingale logic also gives the PDE.
9. Market implied volatilities show where the simple model fails.
10. This motivates stochastic volatility models.

---

# 22. Common Confusions

## Does (N(d_2)) Use Real Probability?

No.

(N(d_2)) is a risk-neutral probability, not a real-world probability.

## Is (N(d_1)) Also the Probability of Exercise?

Not directly.

(N(d_1)) comes from the stock-weighted expectation term.

## Why Replace (\mu) with (r)?

Under the risk-neutral measure, discounted traded asset prices must be martingales.

That makes the stock grow at the risk-free rate under (Q).

## Why Is the Payoff Split?

The call payoff is:

[
(S(T)-K)^+
]

When (S(T)>K), this equals:

[
S(T)-K
]

When (S(T)\leq K), it equals zero.

The indicator function lets us write this cleanly.

## Why Does the Discounted Price Have Zero Drift?

Under (Q), discounted asset prices and replicable claim prices are martingales.

A martingale has zero drift.

## Why Does Implied Volatility Vary by Strike?

Because real market prices are not perfectly described by the constant-volatility Black-Scholes model.

---

# 23. Exam Notes

You should be able to:

* write the stock price under (Q)
* explain why (\mu) is replaced by (r)
* write the risk-neutral pricing formula
* write the European call price as a discounted expectation
* split the call payoff using an indicator function
* explain what an indicator function does
* explain why expectation of an indicator equals probability
* derive the meaning of (N(d_2))
* state the Black-Scholes call formula
* define (d_1) and (d_2)
* distinguish between (N(d_1)) and (N(d_2))
* explain how the PDE can be obtained from the martingale property
* define implied volatility
* explain what a volatility smile means
* explain why volatility smile motivates stochastic volatility models

---

# 24. Core Formulas

## Stock Under (Q)

[
dS(t)=rS(t)dt+\sigma S(t)dW^Q(t)
]

## Explicit Stock Formula Under (Q)

[
S(T)=S(t)\exp\left[\left(r-\frac{1}{2}\sigma^2\right)(T-t)+\sigma(W^Q(T)-W^Q(t))\right]
]

## Risk-Neutral Pricing Formula

[
V(t,S)=E_t^Q\left[e^{-r(T-t)}g(S(T))\right]
]

## European Call Price as Expectation

[
C(t,S)=E_t^Q\left[e^{-r(T-t)}(S(T)-K)^+\right]
]

## Indicator Split

[
(S(T)-K)^+
==========

## S(T)\mathbf{1}_{{S(T)>K}}

K\mathbf{1}_{{S(T)>K}}
]

## Expectation of Indicator

[
E^Q[\mathbf{1}_{{S(T)>K}}]=Q(S(T)>K)
]

## (d_1)

[
d_1=
\frac{
\ln(S/K)+\left(r+\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
]

## (d_2)

[
d_2=
\frac{
\ln(S/K)+\left(r-\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
]

[
d_2=d_1-\sigma\sqrt{T-t}
]

## Black-Scholes Call Formula

[
C(t,S)=S(t)N(d_1)-Ke^{-r(T-t)}N(d_2)
]

## Black-Scholes PDE from Martingale Pricing

[
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
]

## Implied Volatility

[
C_{BSM}(\sigma_{\text{imp}})=C_{\text{market}}
]

---

# Final Intuition

Risk-neutral pricing gives a direct way to compute Black-Scholes prices.

Instead of solving the PDE, we price the option as the discounted expected payoff under the risk-neutral probability.

Under this pricing probability, the stock grows at the risk-free rate (r), not at the real-world expected return (\mu).

For a call option, the payoff is split into a stock part and a strike part.

The strike part gives (N(d_2)), the risk-neutral probability that the option finishes in the money.

The stock part gives (N(d_1)), which adjusts the expected stock value conditional on exercise.

The result is the Black-Scholes formula.

The same martingale logic also gives the Black-Scholes PDE quickly: under (Q), the discounted option price must have zero drift.

Finally, implied volatility shows that real markets often do not follow the simple constant-volatility Black-Scholes model, motivating more advanced models such as stochastic volatility.

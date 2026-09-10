# Black-Scholes-Merton Model — PDE Derivation

## Key Idea

The Black-Scholes-Merton model is the benchmark continuous-time model for option pricing.

The main goal is to price a European derivative whose payoff depends on the final stock price.

The derivation uses two main ideas:

* Ito's rule
* replication / self-financing portfolios

The final result is the Black-Scholes partial differential equation, or Black-Scholes PDE.

---

# 1. The Model

The model has two assets:

1. a risk-free bank account
2. one risky stock

---

# 2. Bank Account

The bank account grows at a continuously compounded constant interest rate (r).

[
B(t)=e^{rt}
]

In differential form:

[
dB(t)=rB(t)dt
]

with:

[
B(0)=1
]

## Intuition

The bank account is deterministic.

There is no randomness in (B(t)).

---

# 3. Stock Price Dynamics

The stock follows a geometric Brownian motion:

[
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
]

or:

[
dS(t)=S(t)(\mu dt+\sigma dW(t))
]

where:

* (\mu) = expected return rate of the stock
* (\sigma) = volatility
* (W(t)) = Brownian motion

## Intuition

The stock has two components:

* deterministic drift: (\mu S(t)dt)
* random Brownian shock: (\sigma S(t)dW(t))

---

# 4. Explicit Solution for the Stock

The stock price can also be written explicitly.

For future time (u>t):

[
S(u)=S(t)\exp\left[\left(\mu-\frac{1}{2}\sigma^2\right)(u-t)+\sigma(W(u)-W(t))\right]
]

This shows that the stock price is log-normal.

## Important

The model is usually written in differential form:

[
dS=\mu Sdt+\sigma SdW
]

but in the Black-Scholes-Merton model we also know the explicit solution.

The term:

[
-\frac{1}{2}\sigma^2
]

comes from Ito's rule.

---

# 5. The Derivative Payoff

We want to price a European path-independent claim.

At maturity (T), the claim pays:

[
g(S(T))
]

Examples:

European call:

[
g(S(T))=\max(S(T)-K,0)
]

European put:

[
g(S(T))=\max(K-S(T),0)
]

---

# 6. Main Guess

We guess that the derivative price at time (t) depends only on:

* current time (t)
* current stock price (S(t))

So:

[
\text{price at time }t = C(t,S(t))
]

## Intuition

We do not need the full past history of the stock.

The current stock price contains the relevant information needed for pricing.

This is related to the Markov property of the model.

---

# 7. Smoothness Assumption

We also assume that (C(t,S)) is smooth enough to apply Ito's rule.

That means we assume the necessary partial derivatives exist:

[
C_t,\quad C_S,\quad C_{SS}
]

---

# 8. Applying Ito's Rule to the Option Price

Since:

[
C=C(t,S(t))
]

and:

[
dS=\mu Sdt+\sigma SdW
]

Ito's rule gives:

[
dC=
\left(
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma S C_S dW
]

## Interpretation

The option price changes due to:

* passage of time: (C_t)
* stock drift: (\mu S C_S)
* stock randomness and curvature: (\frac{1}{2}\sigma^2S^2C_{SS})
* random Brownian exposure: (\sigma S C_SdW)

---

# 9. Replication Idea

Now we try to replicate the option by trading in:

* the stock
* the bank account

If the option can be replicated, then by no-arbitrage:

[
\text{option price} = \text{cost of replicating portfolio}
]

This is the key economic idea behind the derivation.

---

# 10. Self-Financing Portfolio

Let:

[
X(t)
]

be the value of a self-financing portfolio.

Let:

[
\pi(t)
]

be the amount of money invested in the stock at time (t).

Then:

[
X(t)-\pi(t)
]

is the amount invested in the bank account.

## Number of Shares in the Stock

If (\pi(t)) dollars are invested in the stock, and the stock price is (S(t)), then the number of shares is:

[
\frac{\pi(t)}{S(t)}
]

## Number of Units in the Bank Account

If (X(t)-\pi(t)) dollars are invested in the bank account, and the bank account value is (B(t)), then the number of bank account units is:

[
\frac{X(t)-\pi(t)}{B(t)}
]

---

# 11. Portfolio Dynamics

The self-financing condition means changes in wealth come only from changes in the assets.

Therefore:

[
dX=
\frac{\pi}{S}dS
+
\frac{X-\pi}{B}dB
]

## Intuition

This says:

[
\text{change in wealth}
=======================

\text{shares of stock} \times \text{change in stock}
+
\text{units of bank account} \times \text{change in bank account}
]

---

# 12. Substitute Black-Scholes Dynamics

We know:

[
\frac{dS}{S}=\mu dt+\sigma dW
]

and:

[
\frac{dB}{B}=rdt
]

Substitute into the portfolio equation:

[
dX=\pi(\mu dt+\sigma dW)+(X-\pi)rdt
]

Simplify:

[
dX=
[rX+\pi(\mu-r)]dt+\pi\sigma dW
]

This is the wealth process of a self-financing portfolio in the Black-Scholes-Merton model.

---

# 13. Matching the Portfolio with the Option

To replicate the option, we need:

[
X(t)=C(t,S(t))
]

and therefore:

[
dX=dC
]

Compare:

[
dC=
\left(
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma S C_S dW
]

with:

[
dX=
[rX+\pi(\mu-r)]dt+\pi\sigma dW
]

Since (X=C), we match the (dW) terms first:

[
\pi\sigma = \sigma S C_S
]

Therefore:

[
\pi = S C_S
]

## Interpretation

The amount invested in the stock must be:

[
\pi = S C_S
]

The number of shares is:

[
\frac{\pi}{S}=C_S
]

So the replicating strategy holds (C_S) shares of the stock.

This is the option delta.

---

# 14. Matching the Drift Terms

Now substitute:

[
X=C
]

and:

[
\pi=SC_S
]

into the portfolio drift:

[
rX+\pi(\mu-r)
]

This becomes:

[
rC+SC_S(\mu-r)
]

The drift of the option from Ito's rule is:

[
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
]

Set them equal:

[
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
==========================================

rC+SC_S(\mu-r)
]

Expand the right-hand side:

[
rC+\mu SC_S-rSC_S
]

Cancel (\mu SC_S) from both sides.

This gives:

[
C_t+\frac{1}{2}\sigma^2S^2C_{SS}
================================

rC-rSC_S
]

Rearrange:

[
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
]

This is the Black-Scholes PDE.

---

# 15. Black-Scholes PDE

The Black-Scholes partial differential equation is:

[
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
]

with terminal condition:

[
C(T,S)=g(S)
]

For a European call:

[
C(T,S)=\max(S-K,0)
]

For a European put:

[
P(T,S)=\max(K-S,0)
]

---

# 16. Why (\mu) Disappears

A very important result is that (\mu) does not appear in the Black-Scholes PDE.

The expected return of the stock disappears because the option is priced by replication, not by forecasting the stock's expected return.

## Key Intuition

Option pricing in Black-Scholes depends on:

* current stock price (S)
* strike (K)
* time to maturity (T-t)
* interest rate (r)
* volatility (\sigma)

It does not depend on the real-world expected return (\mu).

---

# 17. Why the PDE is Deterministic

The PDE is deterministic.

There is no (dW) term in it.

It must hold for every:

[
t
]

and every:

[
S>0
]

## Intuition

The replication works no matter what future stock path occurs.

Whatever the stock price turns out to be, the PDE holds at that point.

---

# 18. Solving the PDE

To get actual option prices, we must solve the PDE with the correct terminal payoff.

For a European call, the terminal condition is:

[
C(T,S)=\max(S-K,0)
]

Solving the PDE gives the Black-Scholes formula.

The course does not derive the full PDE solution step by step.

Instead, it gives the final solution.

---

# 19. Standard Normal CDF

The Black-Scholes formula uses the standard normal cumulative distribution function.

It is denoted:

[
N(x)
]

and defined as:

[
N(x)=P(Z\leq x)
]

where:

[
Z\sim N(0,1)
]

In integral form:

[
N(x)=\int_{-\infty}^{x}\frac{1}{\sqrt{2\pi}}e^{-y^2/2}dy
]

## Intuition

(N(x)) is the area under the standard normal bell curve to the left of (x).

---

# 20. Black-Scholes Formula for a European Call

For a European call option:

[
C(t,S)=SN(d_1)-Ke^{-r(T-t)}N(d_2)
]

where:

[
d_1=
\frac{
\ln(S/K)+(r+\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
]

and:

[
d_2=d_1-\sigma\sqrt{T-t}
]

Equivalently:

[
d_2=
\frac{
\ln(S/K)+(r-\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
]

---

# 21. Intuition for the Call Formula

The formula has two main terms:

[
SN(d_1)
]

and:

[
Ke^{-r(T-t)}N(d_2)
]

The payoff of a call is like:

[
S-K
]

when the option finishes in the money.

The formula adjusts both (S) and (K) by normal probabilities.

The strike is discounted because it is paid at maturity.

## Important

The precise intuition for (N(d_1)) and (N(d_2)) becomes clearer in the risk-neutral pricing approach.

In the PDE approach, they appear as part of the solution to the PDE.

---

# 22. European Put Formula

The put formula can be obtained from put-call parity.

Put-call parity:

[
C-P=S-Ke^{-r(T-t)}
]

Therefore:

[
P=C-S+Ke^{-r(T-t)}
]

Using the call formula:

[
P(t,S)=Ke^{-r(T-t)}N(-d_2)-SN(-d_1)
]

---

# 23. Shape of the Call Price

At maturity, the call payoff is:

[
\max(S-K,0)
]

This payoff is:

* zero when (S<K)
* linear when (S>K)

Before maturity, the call price is a smooth curve above the payoff line.

As time approaches maturity, the price curve approaches the payoff function.

---

# 24. Shape of the Put Price

At maturity, the put payoff is:

[
\max(K-S,0)
]

This payoff is:

* linear and positive when (S<K)
* zero when (S>K)

Before maturity, the put price is also a smooth curve.

As time approaches maturity, the price curve approaches the payoff function.

---

# 25. Main Steps of the PDE Derivation

The derivation follows this logic:

1. Define the bank account:

[
dB=rBdt
]

2. Define the stock:

[
dS=\mu Sdt+\sigma SdW
]

3. Guess the option price is:

[
C(t,S(t))
]

4. Apply Ito's rule to (C(t,S(t))).

5. Define a self-financing portfolio with amount (\pi) invested in stock.

6. Write the portfolio dynamics:

[
dX=[rX+\pi(\mu-r)]dt+\pi\sigma dW
]

7. Replicate the option by setting:

[
X=C
]

8. Match (dW) terms to get:

[
\pi=SC_S
]

9. Match (dt) terms.

10. Derive the Black-Scholes PDE:

[
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
]

11. Solve the PDE with terminal payoff (g(S)).

12. For a call, obtain:

[
C=SN(d_1)-Ke^{-r(T-t)}N(d_2)
]

---

# 26. Common Confusions

## Why Do We Guess (C(t,S))?

Because in this Markov model, the current stock price is enough to describe the relevant state.

The option does not need the full past history of the stock.

## Why Does (\mu) Disappear?

Because the option is priced by replication.

The real-world expected return is not needed once the payoff can be replicated.

## What Is (\pi)?

(\pi) is the amount of money invested in stock.

It is not the number of shares.

The number of shares is:

[
\frac{\pi}{S}
]

## What Is Delta?

Delta is:

[
C_S
]

It is the number of shares held in the replicating portfolio.

## Why Is the PDE Deterministic?

Because the random (dW) terms are eliminated through replication.

After hedging, the equation must hold for every (t) and (S).

## Why Is the Strike Discounted?

The strike (K) is paid at maturity, so its present value is:

[
Ke^{-r(T-t)}
]

## Why Are (N(d_1)) and (N(d_2)) There?

In the PDE approach, they appear as part of the solution to the PDE.

Their probabilistic interpretation becomes clearer in the risk-neutral pricing approach.

---

# 27. Exam Notes

You should be able to:

* write the bank account dynamics
* write the stock price dynamics
* write the explicit stock solution
* explain why the stock is log-normal
* define a European path-independent payoff
* explain the guess (C(t,S(t)))
* apply Ito's rule to (C(t,S))
* define (\pi) as amount invested in stock
* derive the self-financing wealth dynamics
* match (dW) terms
* identify the replicating stock position
* derive the Black-Scholes PDE
* explain why (\mu) disappears
* state the terminal condition
* state the Black-Scholes call formula
* define (N(x)), (d_1), and (d_2)
* explain how the put formula follows from put-call parity

---

# 28. Core Formulas

## Bank Account

[
B(t)=e^{rt}
]

[
dB(t)=rB(t)dt
]

## Stock Dynamics

[
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
]

## Stock Explicit Solution

[
S(u)=S(t)\exp\left[\left(\mu-\frac{1}{2}\sigma^2\right)(u-t)+\sigma(W(u)-W(t))\right]
]

## Ito's Rule for the Option

[
dC=
\left(
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma S C_S dW
]

## Self-Financing Portfolio

[
dX=\frac{\pi}{S}dS+\frac{X-\pi}{B}dB
]

## Black-Scholes Portfolio Dynamics

[
dX=[rX+\pi(\mu-r)]dt+\pi\sigma dW
]

## Replicating Stock Amount

[
\pi=SC_S
]

## Number of Shares

[
\frac{\pi}{S}=C_S
]

## Black-Scholes PDE

[
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
]

## Terminal Condition

[
C(T,S)=g(S)
]

## European Call Payoff

[
C(T,S)=\max(S-K,0)
]

## Standard Normal CDF

[
N(x)=P(Z\leq x)
]

## Black-Scholes Call Formula

[
C(t,S)=SN(d_1)-Ke^{-r(T-t)}N(d_2)
]

## (d_1)

[
d_1=
\frac{
\ln(S/K)+(r+\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
]

## (d_2)

[
d_2=d_1-\sigma\sqrt{T-t}
]

## Put-Call Parity

[
C-P=S-Ke^{-r(T-t)}
]

## Black-Scholes Put Formula

[
P(t,S)=Ke^{-r(T-t)}N(-d_2)-SN(-d_1)
]

---

# Final Intuition

The Black-Scholes PDE derivation shows that an option can be priced by replication.

We model the stock using geometric Brownian motion, apply Ito's rule to the option price, and build a self-financing portfolio that matches the option's random movements.

By matching the Brownian risk, the randomness disappears.

The remaining deterministic equation is the Black-Scholes PDE.

Solving that PDE gives the Black-Scholes formula for European calls and puts.

The most important conceptual result is:

the option price does not depend on the real-world expected return (\mu).

It depends on volatility, interest rate, time, strike, and current stock price because the option is priced by replication, not by prediction.

# Module 6 Summary — Black-Scholes-Merton Model

## 1. Purpose of Module 6

Module 6 introduces the Black-Scholes-Merton model, the benchmark continuous-time model for option pricing.

The module shows two ways to obtain the Black-Scholes formula:

1. PDE / replication approach
2. Risk-neutral pricing approach

Both methods give the same European option prices.

Main idea:

> Options are priced by no-arbitrage and replication, not by forecasting the real expected return of the stock.

---

## 2. The Black-Scholes-Merton Market

The model has two assets:

1. A risk-free bank account
2. One risky stock

The bank account grows at a constant continuously compounded interest rate `r`.

```math
B(t)=e^{rt}
```

In differential form:

```math
dB(t)=rB(t)dt
```

The bank account is deterministic.

---

## 3. Stock Price Dynamics

The stock follows geometric Brownian motion:

```math
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
```

Equivalently:

```math
dS(t)=S(t)(\mu dt+\sigma dW(t))
```

where:

- `mu` is the real-world expected return
- `sigma` is volatility
- `W(t)` is Brownian motion

The stock has a drift term:

```math
\mu S(t)dt
```

and a random Brownian term:

```math
\sigma S(t)dW(t)
```

---

## 4. Explicit Stock Price Solution

The stock price can also be written explicitly.

For `u > t`:

```math
S(u)=S(t)\exp\left[\left(\mu-\frac{1}{2}\sigma^2\right)(u-t)+\sigma(W(u)-W(t))\right]
```

This shows that the stock price is log-normal.

The term

```math
-\frac{1}{2}\sigma^2
```

appears because of Ito's rule.

---

## 5. European Path-Independent Claims

A European path-independent claim pays:

```math
g(S(T))
```

at maturity `T`.

European call payoff:

```math
g(S(T))=(S(T)-K)^+
```

European put payoff:

```math
g(S(T))=(K-S(T))^+
```

Path-independent means the payoff depends only on the final stock price, not on the full stock path.

---

## 6. Main Pricing Guess

The course assumes that the option price can be written as:

```math
C(t,S(t))
```

This means the price depends only on:

- current time `t`
- current stock price `S(t)`

It does not depend on the full past history of the stock.

This is natural because the Black-Scholes stock process is Markovian.

---

## 7. Ito's Rule Applied to the Option Price

Since:

```math
C=C(t,S(t))
```

and:

```math
dS=\mu Sdt+\sigma SdW
```

Ito's rule gives:

```math
dC=
\left(
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma S C_S dW
```

The option price has:

- a deterministic `dt` part
- a random `dW` part

The random part is:

```math
\sigma S C_S dW
```

The term `C_S` is the option delta.

---

## 8. Self-Financing Portfolio

Let `X(t)` be the wealth of a self-financing portfolio.

Let `pi(t)` be the amount of money invested in the stock.

Then:

```math
X(t)-\pi(t)
```

is the amount invested in the bank account.

The number of stock shares is:

```math
\frac{\pi(t)}{S(t)}
```

The self-financing wealth dynamics are:

```math
dX=
\frac{\pi}{S}dS
+
\frac{X-\pi}{B}dB
```

Substituting the Black-Scholes dynamics gives:

```math
dX=[rX+\pi(\mu-r)]dt+\pi\sigma dW
```

---

## 9. Replication Argument

To replicate the option, set:

```math
X=C
```

and require:

```math
dX=dC
```

Match the random `dW` terms:

```math
\pi\sigma=\sigma S C_S
```

Therefore:

```math
\pi=SC_S
```

So the number of shares held in the replicating portfolio is:

```math
\frac{\pi}{S}=C_S
```

This is the option delta.

---

## 10. Deriving the Black-Scholes PDE

From Ito's rule, the option drift is:

```math
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
```

From the portfolio, the drift is:

```math
rC+SC_S(\mu-r)
```

Set them equal:

```math
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
=
rC+SC_S(\mu-r)
```

Expand the right-hand side:

```math
rC+\mu SC_S-rSC_S
```

The `mu` terms cancel.

This leaves:

```math
C_t+\frac{1}{2}\sigma^2S^2C_{SS}
=
rC-rSC_S
```

Rearrange:

```math
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
```

This is the Black-Scholes PDE.

---

## 11. Why `mu` Disappears

The real-world expected return `mu` does not appear in the Black-Scholes PDE.

This is one of the most important results of the module.

Reason:

> The option is priced by replication, not by forecasting the stock's real-world average return.

The option price depends on:

- current stock price `S`
- strike `K`
- time to maturity `T-t`
- interest rate `r`
- volatility `sigma`

It does not depend on the real-world expected return `mu`.

---

## 12. Black-Scholes PDE

The Black-Scholes PDE is:

```math
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
```

with terminal condition:

```math
C(T,S)=g(S)
```

For a European call:

```math
C(T,S)=\max(S-K,0)
```

For a European put:

```math
P(T,S)=\max(K-S,0)
```

The PDE is deterministic.

There is no `dW` term because replication eliminates Brownian risk.

---

## 13. Black-Scholes Call Formula

For a European call option:

```math
C(T,S)=\max(S-K,0)
```

Solving the Black-Scholes PDE gives:

```math
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
```

where:

```math
d_1=
\frac{
\ln(S/K)+(r+\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
```

and:

```math
d_2=d_1-\sigma\sqrt{T-t}
```

Equivalently:

```math
d_2=
\frac{
\ln(S/K)+(r-\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
```

---

## 14. Standard Normal CDF

The function `N(x)` is the standard normal cumulative distribution function:

```math
N(x)=P(Z\leq x)
```

where:

```math
Z\sim N(0,1)
```

It is the area under the standard normal bell curve to the left of `x`.

---

## 15. Put Formula

The European put formula can be obtained using put-call parity.

Put-call parity is:

```math
C-P=S-Ke^{-r(T-t)}
```

Therefore:

```math
P=C-S+Ke^{-r(T-t)}
```

The Black-Scholes put formula is:

```math
P(t,S)=K e^{-r(T-t)}N(-d_2)-S N(-d_1)
```

---

## 16. Risk-Neutral Pricing Approach

The second approach prices options using discounted expected payoffs under the risk-neutral probability `Q`.

The general pricing formula is:

```math
V(t,S)=E_t^Q\left[e^{-r(T-t)}g(S(T))\right]
```

For a European call:

```math
C(t,S)=E_t^Q\left[e^{-r(T-t)}(S(T)-K)^+\right]
```

This method avoids directly solving the PDE.

---

## 17. Stock Dynamics Under `Q`

Under the real-world probability `P`:

```math
dS=\mu Sdt+\sigma SdW
```

Under the risk-neutral probability `Q`:

```math
dS=rSdt+\sigma SdW^Q
```

The key replacement is:

```math
\mu \rightarrow r
```

The volatility `sigma` stays the same.

---

## 18. Explicit Stock Formula Under `Q`

Under the risk-neutral probability:

```math
S(T)=S(t)\exp\left[
\left(r-\frac{1}{2}\sigma^2\right)(T-t)
+
\sigma(W^Q(T)-W^Q(t))
\right]
```

The Brownian increment satisfies:

```math
W^Q(T)-W^Q(t)\sim N(0,T-t)
```

So:

```math
\frac{W^Q(T)-W^Q(t)}{\sqrt{T-t}}
\sim N(0,1)
```

This is why the Black-Scholes formula involves `N(d_1)` and `N(d_2)`.

---

## 19. Splitting the Call Payoff

The call payoff can be written as:

```math
(S(T)-K)^+
=
S(T)\mathbf{1}_{\{S(T)>K\}}
-
K\mathbf{1}_{\{S(T)>K\}}
```

This separates the payoff into:

1. stock part
2. strike part

Then:

```math
C(t,S)
=
e^{-r(T-t)}E_t^Q[S(T)\mathbf{1}_{\{S(T)>K\}}]
-
K e^{-r(T-t)}E_t^Q[\mathbf{1}_{\{S(T)>K\}}]
```

---

## 20. Meaning of `N(d_2)`

The expectation of an indicator function is a probability.

So:

```math
E_t^Q[\mathbf{1}_{\{S(T)>K\}}]
=
Q(S(T)>K)
```

In Black-Scholes:

```math
Q(S(T)>K)=N(d_2)
```

Therefore, `N(d_2)` is the risk-neutral probability that the call finishes in the money.

This is why the strike term is:

```math
K e^{-r(T-t)}N(d_2)
```

---

## 21. Meaning of `N(d_1)`

The first term is:

```math
e^{-r(T-t)}E_t^Q[S(T)\mathbf{1}_{\{S(T)>K\}}]
```

This is not just a probability.

It is a stock-weighted expectation.

After evaluating the normal integral, it becomes:

```math
S N(d_1)
```

So `N(d_1)` is connected to the stock component of the call value.

Memory rule:

```math
S N(d_1)
```

is the stock part.

```math
K e^{-r(T-t)}N(d_2)
```

is the discounted strike part.

---

## 22. Risk-Neutral Derivation of the PDE

Under `Q`:

```math
dS=rSdt+\sigma SdW^Q
```

Apply Ito's rule to `C(t,S)`:

```math
dC=
\left(
C_t+rSC_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma SC_SdW^Q
```

Now discount:

```math
e^{-rt}C(t,S(t))
```

Under `Q`, discounted prices of tradable or replicable claims must be martingales.

A martingale has zero drift.

The drift of the discounted option price is:

```math
C_t+rSC_S+\frac{1}{2}\sigma^2S^2C_{SS}-rC
```

Set it equal to zero:

```math
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
```

This is the same Black-Scholes PDE.

---

## 23. PDE Approach vs Risk-Neutral Approach

### PDE / Replication Approach

Uses:

- Ito's rule
- self-financing portfolio
- matching `dW` terms
- replication
- no-arbitrage

It derives the PDE first, then solves it.

### Risk-Neutral Pricing Approach

Uses:

- risk-neutral probability `Q`
- discounted expected payoff
- stock dynamics under `Q`
- normal distribution calculations

It computes the price directly as an expectation.

Both methods give the same Black-Scholes formula.

---

## 24. Implied Volatility

The Black-Scholes model assumes that volatility is constant.

In real markets, different options on the same underlying often imply different volatilities.

Implied volatility is the value of `sigma` that makes the Black-Scholes price equal to the market price:

```math
C_{BSM}(\sigma_{\text{imp}})=C_{\text{market}}
```

It is the volatility implied by the observed option price.

---

## 25. Volatility Smile

If Black-Scholes were perfectly correct, then all options on the same stock and maturity should have the same implied volatility.

The implied volatility curve across strikes should be flat.

In practice, it is often curved.

This is called the volatility smile.

A volatility smile suggests that the simple constant-volatility Black-Scholes model does not fully describe real option prices.

---

## 26. Why the Volatility Smile Matters

The volatility smile shows that real markets may have features not captured by the basic Black-Scholes model, such as:

- stochastic volatility
- jumps
- fat tails
- imperfect hedging
- higher probability of extreme events

This motivates more advanced models.

---

## 27. Stochastic Volatility Motivation

A stochastic volatility model allows volatility to change randomly over time.

Instead of assuming:

```math
\sigma=\text{constant}
```

we allow:

```math
\sigma(t)=\text{random}
```

This is a natural extension because volatility is one of the most important inputs in stock option pricing.

---

## 28. Main Conceptual Flow

The module follows this logic:

1. Define the Black-Scholes-Merton market.
2. Model the stock using geometric Brownian motion.
3. Apply Ito's rule to the option price.
4. Build a self-financing portfolio.
5. Replicate the option and derive the PDE.
6. Observe that `mu` disappears.
7. Solve the PDE to get the Black-Scholes formula.
8. Re-derive the same formula using risk-neutral pricing.
9. Interpret `N(d_2)` as a risk-neutral probability.
10. Introduce implied volatility.
11. Use the volatility smile as motivation for more advanced models.

---

## 29. Common Confusions

### Why does `mu` disappear?

Because the option is priced by replication, not by forecasting.

### Is `N(d_2)` a real-world probability?

No. It is a risk-neutral probability.

### Is `N(d_1)` the probability of exercise?

Not exactly. It comes from the stock-weighted expectation term.

### What is delta?

Delta is:

```math
C_S
```

It is the number of shares needed in the replicating portfolio.

### What is `pi`?

`pi` is the dollar amount invested in the stock.

The number of shares is:

```math
\frac{\pi}{S}
```

### Why is the PDE deterministic?

Because replication eliminates the random Brownian term.

### Why does the discounted price have zero drift under `Q`?

Because discounted prices of tradable or replicable claims must be martingales under the risk-neutral measure.

### Why does a volatility smile contradict basic Black-Scholes?

Basic Black-Scholes assumes one constant volatility for the stock.

If different strikes imply different volatilities, the market is not using one constant-volatility model.

---

## 30. Exam Notes

You should be able to:

- write the bank account dynamics
- write the stock dynamics under `P`
- write the stock dynamics under `Q`
- write the explicit stock solution
- explain why the stock is log-normal
- apply Ito's rule to `C(t,S)`
- derive the self-financing portfolio dynamics
- explain the role of `pi`
- match `dW` terms and identify delta
- derive the Black-Scholes PDE
- explain why `mu` disappears
- state the Black-Scholes call formula
- define `N(x)`, `d_1`, and `d_2`
- obtain the put formula using put-call parity
- explain the risk-neutral pricing formula
- split the call payoff using an indicator function
- explain why `N(d_2)` is a risk-neutral probability
- explain why `N(d_1)` is not simply the probability of exercise
- derive the PDE using the martingale property
- define implied volatility
- explain the volatility smile
- explain why the volatility smile motivates stochastic volatility models

---

## 31. Core Formulas

### Bank account

```math
B(t)=e^{rt}
```

```math
dB(t)=rB(t)dt
```

### Stock under `P`

```math
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
```

### Stock under `Q`

```math
dS(t)=rS(t)dt+\sigma S(t)dW^Q(t)
```

### Explicit stock under `P`

```math
S(u)=S(t)\exp\left[
\left(\mu-\frac{1}{2}\sigma^2\right)(u-t)
+
\sigma(W(u)-W(t))
\right]
```

### Explicit stock under `Q`

```math
S(T)=S(t)\exp\left[
\left(r-\frac{1}{2}\sigma^2\right)(T-t)
+
\sigma(W^Q(T)-W^Q(t))
\right]
```

### Ito rule for option price

```math
dC=
\left(
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma S C_S dW
```

### Self-financing portfolio

```math
dX=
\frac{\pi}{S}dS+
\frac{X-\pi}{B}dB
```

### Wealth dynamics

```math
dX=[rX+\pi(\mu-r)]dt+\pi\sigma dW
```

### Replicating stock amount

```math
\pi=SC_S
```

### Number of shares / delta

```math
\frac{\pi}{S}=C_S
```

### Black-Scholes PDE

```math
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
```

### Terminal condition

```math
C(T,S)=g(S)
```

### Risk-neutral pricing formula

```math
V(t,S)=E_t^Q\left[e^{-r(T-t)}g(S(T))\right]
```

### Call payoff split

```math
(S(T)-K)^+
=
S(T)\mathbf{1}_{\{S(T)>K\}}
-
K\mathbf{1}_{\{S(T)>K\}}
```

### Black-Scholes call formula

```math
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
```

### d1

```math
d_1=
\frac{
\ln(S/K)+(r+\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
```

### d2

```math
d_2=
\frac{
\ln(S/K)+(r-\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
```

```math
d_2=d_1-\sigma\sqrt{T-t}
```

### Put-call parity

```math
C-P=S-Ke^{-r(T-t)}
```

### Black-Scholes put formula

```math
P(t,S)=K e^{-r(T-t)}N(-d_2)-S N(-d_1)
```

### Implied volatility

```math
C_{BSM}(\sigma_{\text{imp}})=C_{\text{market}}
```

---

## Final Intuition

Module 6 shows how the Black-Scholes-Merton formula comes from no-arbitrage pricing.

The PDE derivation shows that an option can be replicated by continuously trading the stock and the bank account.

The risk-neutral derivation shows that the same price can be computed as a discounted expected payoff under `Q`.

The key conceptual result is that the real-world expected return `mu` does not determine the option price.

Instead, the option price depends on the parameters needed for replication:

```math
S,\ K,\ r,\ \sigma,\ T-t
```

Finally, implied volatility and the volatility smile show that Black-Scholes is a benchmark model, not a perfect description of real markets.
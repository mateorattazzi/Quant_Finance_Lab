# Module 9 — Jump-Diffusion Models

## 1. Big Picture

Another way to extend Black-Scholes is to allow the stock price to jump.

Black-Scholes assumes continuous paths.

But in real markets, prices can move suddenly because of:

- earnings announcements
- macroeconomic news
- crashes
- liquidity shocks
- unexpected events

Jump models try to capture these sudden movements.

---

## 2. Two Broad Types of Jump Models

There are two broad families:

1. Jump-diffusion models
2. Pure-jump models

A jump-diffusion model adds jumps to a Brownian motion model.

A pure-jump model may have no Brownian motion and instead uses frequent jumps.

Pure-jump models are often built using Lévy processes.

The course focuses only on the basic intuition of jump-diffusion models.

---

## 3. Merton Jump-Diffusion Model

Merton’s jump-diffusion model extends Black-Scholes by adding random jumps.

The model has two sources of randomness:

- continuous Brownian motion
- discrete jumps

The Brownian part behaves like ordinary Black-Scholes.

The jump part creates sudden multiplicative changes in the stock price.

---

## 4. Poisson Process

Jump times are modeled with a Poisson process.

A Poisson process counts how many jumps have occurred by time `t`.

We write this as:

```math
N(t)
```

The probability of exactly `k` jumps by time `t` is:

```math
P(N(t)=k)
=
e^{-\lambda t}
\frac{(\lambda t)^k}{k!}
```

where:

- `lambda` = jump intensity
- larger `lambda` means jumps happen more frequently
- `k` = number of jumps

The time between jumps is exponentially distributed.

---

## 5. Jump Sizes

The Poisson process tells us when jumps occur.

We also need to model how large the jumps are.

In Merton’s model, each jump multiplies the stock price by a random factor.

Let the jump factors be:

```math
X_1,X_2,\ldots
```

If the first jump occurs, the stock is multiplied by:

```math
X_1
```

If a second jump occurs, it is multiplied by:

```math
X_2
```

and so on.

The jump factors are usually assumed independent and identically distributed.

Merton assumed lognormal jump sizes, which makes the model more tractable.

---

## 6. Stock Price Structure

In a jump-diffusion model, the stock price has:

1. a continuous Black-Scholes part
2. a product of jump factors

A simplified structure is:

```math
S(t)
=
S(0)
\exp\left[
\left(r-m-\frac{1}{2}\sigma^2\right)t
+
\sigma W^Q(t)
\right]
\prod_{i=1}^{N(t)}X_i
```

where:

- `sigma` = Brownian volatility
- `W^Q` = Brownian motion under the pricing measure
- `N(t)` = number of jumps by time `t`
- `X_i` = jump multiplier
- `m` = jump compensation term

---

## 7. Why the Compensation Term Appears

Jumps add expected growth to the stock.

But under the risk-neutral measure, the discounted stock price must be a martingale.

That means the expected return of the stock must be the risk-free rate.

So the model subtracts a compensation term from the drift.

This term adjusts for the expected effect of jumps.

Without it, the discounted stock price would not generally be a martingale.

---

## 8. Incompleteness

Jump-diffusion models are generally incomplete.

Why?

Because jump risk cannot usually be perfectly hedged by continuously trading the stock and bond.

In Black-Scholes, randomness comes only from Brownian motion, and the stock can hedge that Brownian risk.

With jumps, the stock can suddenly move by a random amount.

Continuous trading cannot fully protect against unexpected discrete jumps.

So no-arbitrage alone may not give a unique price.

The course assumes a pricing measure `Q` is chosen.

---

## 9. Pricing Idea

The basic pricing formula remains risk-neutral pricing:

```math
C(0)
=
E^Q
\left[
e^{-rT}g(S(T))
\right]
```

The difficulty is that `S(T)` now depends on:

- Brownian motion
- number of jumps
- jump sizes

Merton’s key trick is to condition on the number of jumps.

---

## 10. Conditioning on the Number of Jumps

The number of jumps by maturity can be:

```math
0,1,2,\ldots
```

So we split the price into cases.

```math
C(0)
=
\sum_{k=0}^{\infty}
E^Q
\left[
e^{-rT}g(S(T))
\mid N(T)=k
\right]
Q(N(T)=k)
```

Each term prices the option assuming exactly `k` jumps occurred.

Then each term is weighted by the probability of exactly `k` jumps.

---

## 11. Why This Helps

If we know that exactly `k` jumps occurred, then the stock price includes exactly `k` jump multipliers.

If the jump multipliers are lognormal, then the product of jump multipliers is also lognormal.

The Brownian part is also lognormal.

So conditional on `k`, the stock price has a form similar to Black-Scholes.

That means each conditional expectation can be computed using a Black-Scholes type formula.

---

## 12. Merton Pricing Formula Intuition

The final option price becomes an infinite weighted sum of Black-Scholes type prices.

The structure is:

```math
C_{\text{Merton}}
=
\sum_{k=0}^{\infty}
w_k C_{\text{BS},k}
```

where:

- `w_k` = probability weight for exactly `k` jumps
- `C_BS,k` = Black-Scholes type price conditional on `k` jumps

In practice, the infinite sum is truncated.

We compute enough terms until the remaining probabilities are negligible.

---

## 13. More Parameters

Black-Scholes has one main volatility parameter:

```math
\sigma
```

Merton’s jump-diffusion model adds jump parameters.

Typical jump parameters include:

- jump intensity
- average jump size
- jump-size volatility

This makes the model more flexible.

It can fit option prices better than one-parameter Black-Scholes.

---

## 14. Benefits and Costs

Benefits:

- captures sudden price movements
- can fit volatility smiles better
- has economic intuition
- extends Black-Scholes while keeping some tractability

Costs:

- mathematically harder
- usually incomplete
- needs more parameters
- calibration is more complex
- jump risk is difficult to hedge perfectly

---

## 15. Exam Notes

You should be able to:

- explain why jumps are added to Black-Scholes
- define a jump-diffusion model
- explain what a Poisson process counts
- interpret the jump intensity `lambda`
- explain how jump sizes affect the stock price
- explain why a drift compensation term is needed
- explain why jump models are generally incomplete
- describe the conditioning-on-jumps pricing trick
- explain why Merton prices are weighted sums of Black-Scholes type prices

---

## 16. Core Formulas

### Poisson probability

```math
P(N(t)=k)
=
e^{-\lambda t}
\frac{(\lambda t)^k}{k!}
```

### Jump-diffusion stock structure

```math
S(t)
=
S(0)
\exp\left[
\left(r-m-\frac{1}{2}\sigma^2\right)t
+
\sigma W^Q(t)
\right]
\prod_{i=1}^{N(t)}X_i
```

### Risk-neutral pricing

```math
C(0)
=
E^Q
\left[
e^{-rT}g(S(T))
\right]
```

### Conditioning on number of jumps

```math
C(0)
=
\sum_{k=0}^{\infty}
E^Q
\left[
e^{-rT}g(S(T))
\mid N(T)=k
\right]
Q(N(T)=k)
```

### Merton weighted-sum intuition

```math
C_{\text{Merton}}
=
\sum_{k=0}^{\infty}
w_k C_{\text{BS},k}
```

---

## Final Intuition

Jump-diffusion models extend Black-Scholes by adding sudden price moves.

The Poisson process models when jumps happen.

Random jump factors model how large the jumps are.

Merton’s model prices options by conditioning on the number of jumps.

Given the number of jumps, the price can be computed using Black-Scholes type formulas.

The final price is an infinite weighted sum of those conditional prices.

The model is more realistic and flexible than Black-Scholes, but it is also harder to hedge and usually incomplete.
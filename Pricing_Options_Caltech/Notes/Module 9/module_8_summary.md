# Module 9 — Summary: Extensions of Black-Scholes

## 1. Big Picture

Module 9 studies extensions of the Black-Scholes model.

Black-Scholes assumes:

- constant volatility
- continuous stock paths
- complete markets
- one Brownian motion
- one risky asset that can hedge all risk

These assumptions are useful, but too simple for many real markets.

Module 9 introduces two important extensions:

1. stochastic volatility models
2. jump-diffusion models

The main lesson is:

> More realistic models can fit market behavior better, but they often make markets incomplete and hedging harder.

---

## 2. Complete Markets

A market is complete if every derivative payoff can be replicated perfectly by trading available assets.

In a complete market:

- every claim has one no-arbitrage price
- there is one risk-neutral measure
- hedging can be perfect in theory

A useful intuition:

> If the number of independent risk sources equals the number of tradable risky assets, the market may be complete.

Example:

```text
1 stock + 1 Brownian motion = complete Black-Scholes market
```

---

## 3. Incomplete Markets

A market is incomplete if some risks cannot be perfectly hedged.

This happens when there are more sources of randomness than tradable risky assets.

Example:

```text
1 stock + 2 Brownian motions = usually incomplete
```

In an incomplete market:

- not every payoff can be replicated
- there may be many risk-neutral measures
- no-arbitrage alone does not give one unique price
- pricing may require calibration or additional assumptions

---

## 4. Local Volatility

One extension of Black-Scholes allows volatility to depend on time and stock price.

```math
\sigma=\sigma(t,S)
```

The stock process becomes:

```math
dS(t)=rS(t)dt+\sigma(t,S(t))S(t)dW^Q(t)
```

Since there is still one stock and one Brownian motion, the model can remain complete.

The pricing PDE becomes:

```math
C_t
+
\frac{1}{2}\sigma^2(t,S)S^2C_{SS}
+
rSC_S
-
rC
=
0
```

---

## 5. CEV Model

The CEV model is a local volatility model.

CEV means Constant Elasticity of Variance.

A common form is:

```math
\sigma(S)=\frac{\sigma}{S^\beta}
```

Then the stock diffusion term is:

```math
\sigma(S)S dW
=
\sigma S^{1-\beta}dW
```

Intuition:

> If stock prices fall, volatility can rise.

This helps capture equity-market behavior better than constant-volatility Black-Scholes.

---

## 6. Deterministic Time-Dependent Volatility

If volatility changes over time but is deterministic, then total variance is:

```math
\int_0^T \sigma^2(u)du
```

In Black-Scholes, constant volatility gives total variance:

```math
\sigma^2T
```

So with deterministic volatility, replace:

```math
\sigma^2
```

by the average variance:

```math
\frac{1}{T}\int_0^T \sigma^2(u)du
```

---

## 7. Stochastic Volatility

In stochastic volatility models, volatility itself is random.

The option price must now depend on more than just time and stock price.

Instead of:

```math
C(t,S)
```

we usually need:

```math
C(t,S,V)
```

where `V` is the stochastic variance.

This adds a new source of risk.

If volatility cannot be traded directly, the market is usually incomplete.

---

## 8. Heston Model

The Heston model is a famous stochastic volatility model.

The stock follows:

```math
dS(t)=rS(t)dt+\sqrt{V(t)}S(t)dW^Q(t)
```

The variance follows:

```math
dV(t)=a(b-V(t))dt+\gamma\sqrt{V(t)}dZ^Q(t)
```

with correlation:

```math
dW^Q(t)dZ^Q(t)=\rho dt
```

where:

- `V(t)` = stochastic variance
- `b` = long-run average variance
- `a` = speed of mean reversion
- `gamma` = volatility of volatility
- `rho` = correlation between stock shocks and variance shocks

---

## 9. Mean Reversion

The variance drift is:

```math
a(b-V)
```

If:

```math
V<b
```

then the drift is positive and pushes variance upward.

If:

```math
V>b
```

then the drift is negative and pushes variance downward.

So variance tends to move back toward `b`.

---

## 10. Heston PDE Intuition

The Heston option price is:

```math
C(t,S,V)
```

The PDE includes:

- time derivative
- stock variance term
- variance variance term
- cross term from correlation
- stock drift term
- variance drift term
- discounting term

A typical structure is:

```math
0=
C_t
+
\frac{1}{2}VS^2C_{SS}
+
\rho\gamma VS C_{SV}
+
\frac{1}{2}\gamma^2VC_{VV}
+
rSC_S
+
a(b-V)C_V
-
rC
```

The exact variance drift under the pricing measure depends on the chosen risk-neutral measure.

---

## 11. Why Stochastic Volatility Creates Incompleteness

In Heston, there are two Brownian shocks:

```text
stock shock
volatility shock
```

But if only the stock is traded, there is only one risky tradable asset.

That means volatility risk cannot be perfectly hedged.

So there can be many possible risk-neutral measures.

No-arbitrage alone does not determine a unique option price.

---

## 12. Market Price of Volatility Risk

Because volatility is not directly traded, the risk-neutral drift of volatility is not uniquely determined.

A model needs an assumption about how the market prices volatility risk.

This is often represented by an additional parameter or process.

Different choices can produce different option prices.

In practice, this is handled through calibration.

---

## 13. SABR Model

The SABR model is another stochastic volatility model.

A simplified version is:

```math
dS=\alpha S^\beta dW
```

```math
d\alpha=\nu\alpha dZ
```

with:

```math
dW dZ=\rho dt
```

where:

- `alpha` = stochastic volatility
- `beta` = elasticity parameter
- `nu` = volatility of volatility
- `rho` = correlation

SABR is often used to fit volatility smiles and skews.

---

## 14. Calibration

Calibration means choosing model parameters so that model prices match market prices.

The process is:

1. choose a model
2. choose parameters
3. compute theoretical option prices
4. compare with market option prices
5. adjust parameters
6. use calibrated model for less liquid derivatives

A typical objective is:

```math
\min_{\theta}
\sum_i
\left(
C_{\text{model},i}(\theta)
-
C_{\text{market},i}
\right)^2
```

Calibration is like implied volatility, but with more parameters.

---

## 15. Jump-Diffusion Models

Black-Scholes assumes stock prices move continuously.

Jump-diffusion models allow sudden jumps.

This is useful because real markets can move suddenly after:

- earnings announcements
- macro news
- crashes
- liquidity shocks
- unexpected events

Jump models combine:

```text
continuous Brownian motion + discrete jumps
```

---

## 16. Poisson Process

Jump times are modeled with a Poisson process.

`N(t)` counts the number of jumps by time `t`.

The probability of exactly `k` jumps by time `t` is:

```math
P(N(t)=k)
=
e^{-\lambda t}
\frac{(\lambda t)^k}{k!}
```

where `lambda` is the jump intensity.

Higher `lambda` means jumps occur more often.

---

## 17. Jump Sizes

The Poisson process tells us when jumps occur.

We also need jump sizes.

In Merton’s jump-diffusion model, each jump multiplies the stock price by a random factor:

```math
X_1,X_2,\ldots
```

If there are `N(t)` jumps, the stock is multiplied by:

```math
\prod_{i=1}^{N(t)}X_i
```

---

## 18. Merton Jump-Diffusion Model

A simplified stock structure is:

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
- `N(t)` = number of jumps
- `X_i` = jump multiplier
- `m` = jump compensation term

---

## 19. Why the Compensation Term Appears

Jumps add expected growth to the stock.

Under the risk-neutral measure, the discounted stock price must be a martingale.

So the stock’s drift must be adjusted for the expected effect of jumps.

That is why the compensation term `m` appears.

Without it, the expected return would generally not equal the risk-free rate.

---

## 20. Pricing with Jumps

The risk-neutral pricing formula remains:

```math
C(0)
=
E^Q
\left[
e^{-rT}g(S(T))
\right]
```

But now `S(T)` depends on:

- Brownian motion
- number of jumps
- jump sizes

Merton’s key idea is to condition on the number of jumps.

---

## 21. Conditioning on Number of Jumps

The number of jumps can be:

```text
0, 1, 2, ...
```

So the price can be written as:

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

Each term is weighted by the probability of `k` jumps.

---

## 22. Merton Pricing Intuition

If jump sizes are lognormal, then conditional on `k` jumps, the stock price remains lognormal-like.

So each conditional price can be computed using a Black-Scholes type formula.

The final price has the structure:

```math
C_{\text{Merton}}
=
\sum_{k=0}^{\infty}
w_k C_{\text{BS},k}
```

In practice, the infinite sum is truncated.

---

## 23. Jump Models and Incompleteness

Jump-diffusion models are usually incomplete.

Why?

Because continuous trading in the stock and bond cannot perfectly hedge sudden unexpected jumps.

Jump risk cannot generally be eliminated.

So no-arbitrage alone may not determine one unique price.

---

## 24. Main Practical Trade-Off

More realistic models can fit markets better, but they are harder to use.

Benefits:

- better fit to volatility smiles and skews
- captures changing volatility
- captures sudden jumps
- more realistic risk behavior

Costs:

- more parameters
- harder calibration
- incomplete markets
- more complex hedging
- less transparent intuition

---

## 25. Exam Checklist

You should be able to:

- explain why Black-Scholes is restrictive
- define complete and incomplete markets
- explain local volatility
- write the local volatility PDE
- explain CEV intuition
- explain deterministic time-dependent volatility
- explain stochastic volatility
- describe Heston dynamics
- explain mean reversion
- explain why stochastic volatility can make markets incomplete
- explain calibration
- define a Poisson process
- explain jump intensity
- explain jump sizes
- explain why jump-diffusion models are incomplete
- explain Merton’s conditioning-on-jumps idea

---

## 26. Core Formulas

### Local volatility PDE

```math
C_t
+
\frac{1}{2}\sigma^2(t,S)S^2C_{SS}
+
rSC_S
-
rC
=
0
```

### Deterministic volatility average variance

```math
\frac{1}{T}\int_0^T \sigma^2(u)du
```

### Heston stock process

```math
dS=rSdt+\sqrt{V}SdW^Q
```

### Heston variance process

```math
dV=a(b-V)dt+\gamma\sqrt{V}dZ^Q
```

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

### Conditioning on jumps

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

---

## Final Intuition

Module 9 shows why Black-Scholes is only a starting point.

Local volatility changes volatility while keeping the model relatively complete.

Stochastic volatility adds a new risk factor and often makes the market incomplete.

Jump-diffusion models capture sudden price moves, but jump risk is hard to hedge.

In richer models, pricing usually relies on risk-neutral expectations, PDEs, Monte Carlo, and calibration to market option prices.
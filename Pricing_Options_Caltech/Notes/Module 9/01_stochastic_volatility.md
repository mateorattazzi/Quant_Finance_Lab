# Module 9 — Extensions of Black-Scholes: Stochastic Volatility and Incomplete Markets

## 1. Big Picture

The Black-Scholes-Merton model assumes constant volatility.

That is often unrealistic.

In real markets:

- volatility changes over time
- volatility tends to rise when markets fall
- option prices show volatility smiles and skews
- one volatility parameter is usually not enough to fit market data

So we extend Black-Scholes by allowing volatility, interest rates, or other factors to become stochastic.

---

## 2. Complete vs Incomplete Models

A model is complete when every claim can be replicated.

A rough rule is:

> A Brownian motion model is complete when the number of risky tradable assets equals the number of Brownian sources of risk.

Examples:

- one stock and one Brownian motion: usually complete
- three stocks and three Brownian motions: usually complete
- one stock and two Brownian motions: usually incomplete

If there are more Brownian motions than tradable risky assets, there is risk that cannot be perfectly hedged.

That creates more than one possible risk-neutral measure.

---

## 3. Local Volatility Models

One way to extend Black-Scholes is to let volatility depend on time and stock price.

Instead of constant `r` and constant `sigma`, we use:

```math
r=r(t,S)
```

```math
\sigma=\sigma(t,S)
```

The stock process becomes:

```math
dS(t)=r(t,S(t))S(t)dt+\sigma(t,S(t))S(t)dW^Q(t)
```

There is still only one Brownian motion and one risky asset.

So the model can still be complete.

---

## 4. Solution Intuition

In standard Black-Scholes, the explicit stock solution contains terms like:

```math
(r-\frac{1}{2}\sigma^2)(T-t)
```

When `r` and `sigma` vary with time, multiplication is replaced by integration.

The idea becomes:

```math
\int_t^T
\left(
r(u,S(u))-\frac{1}{2}\sigma^2(u,S(u))
\right)du
```

and the Brownian part becomes:

```math
\int_t^T \sigma(u,S(u))dW^Q(u)
```

The exact expression may not be easy to use, but the intuition is the same:

> changing parameters over time produces integrals instead of simple multiplication by time.

---

## 5. PDE in a Local Volatility Model

For a European claim with payoff:

```math
g(S(T))
```

the price is:

```math
C(t,S)
```

The PDE looks like Black-Scholes, except `r` and `sigma` are now functions of `t` and `S`:

```math
C_t
+
\frac{1}{2}\sigma^2(t,S)S^2C_{SS}
+
r(t,S)SC_S
-
r(t,S)C
=
0
```

Terminal condition:

```math
C(T,S)=g(S)
```

This may not have a closed-form solution.

So pricing is usually done by:

- solving the PDE numerically
- using risk-neutral expectation
- Monte Carlo simulation

---

## 6. CEV Model

The CEV model means Constant Elasticity of Variance.

It is an early extension of Black-Scholes.

The volatility is allowed to depend on the stock price.

A common form is:

```math
\sigma(S)=\frac{\sigma}{S^\beta}
```

with:

```math
0\leq \beta \leq 1
```

Then the stock diffusion term is:

```math
\sigma(S)S dW
=
\sigma S^{1-\beta}dW
```

---

## 7. CEV Intuition

The CEV model tries to capture an empirical fact:

> Market volatility often rises when stock prices fall.

If:

```math
\sigma(S)=\frac{\sigma}{S^\beta}
```

then lower `S` gives higher volatility.

So the model can produce behavior closer to equity markets than constant-volatility Black-Scholes.

---

## 8. Deterministic Time-Dependent Volatility

If volatility is a deterministic function of time, then:

```math
\int_0^T \sigma(u)dW(u)
```

is normally distributed with mean zero and variance:

```math
\int_0^T \sigma^2(u)du
```

This is why in Black-Scholes with deterministic volatility, we replace total variance:

```math
\sigma^2T
```

by:

```math
\int_0^T \sigma^2(u)du
```

Equivalently, the average variance is:

```math
\frac{1}{T}\int_0^T \sigma^2(u)du
```

---

## 9. Why Add More Brownian Motions?

Market data often cannot be explained by only one source of risk.

Option prices across different strikes and maturities may require more than one factor.

Examples of extra factors:

- stochastic volatility
- stochastic interest rates
- stochastic dividends
- jumps in stock price
- jumps in volatility

A more realistic model may combine several Brownian motions and jumps.

---

## 10. Heston Model

The Heston model is a famous stochastic volatility model.

Under the risk-neutral measure:

```math
dS(t)=rS(t)dt+\sqrt{V(t)}S(t)dW^Q(t)
```

The variance process follows:

```math
dV(t)=a(b-V(t))dt+\gamma\sqrt{V(t)}dZ^Q(t)
```

with correlation:

```math
dW^Q(t)dZ^Q(t)=\rho dt
```

where:

- `V(t)` = stochastic variance
- `b` = long-run mean variance
- `a` = speed of mean reversion
- `gamma` = volatility of variance
- `rho` = correlation between stock returns and variance shocks

---

## 11. Mean Reversion

The drift of `V` is:

```math
a(b-V)
```

If:

```math
V<b
```

then:

```math
a(b-V)>0
```

so the drift pushes `V` upward.

If:

```math
V>b
```

then:

```math
a(b-V)<0
```

so the drift pushes `V` downward.

So `V` tends to move back toward `b`.

That is why `b` is interpreted as the long-run mean.

---

## 12. Why the Square Root?

The volatility term in the Heston variance process is:

```math
\gamma\sqrt{V}dZ^Q
```

This helps keep variance non-negative.

It also makes the model mathematically tractable.

The square root is more a mathematical modeling choice than a direct economic law.

---

## 13. Pricing in Heston

Once volatility becomes stochastic, the option price depends on the extra state variable.

So instead of:

```math
C(t,S)
```

we write:

```math
C(t,S,V)
```

This is important.

Whenever the model has an extra stochastic factor, the derivative price normally depends on that factor.

---

## 14. Incompleteness in Stochastic Volatility Models

If volatility is stochastic but cannot be traded directly, the model is incomplete.

Why?

Because there are two sources of risk:

```text
stock risk
volatility risk
```

but only one risky tradable asset:

```text
the stock
```

So not every claim can be perfectly replicated.

This creates many possible risk-neutral measures.

---

## 15. Heston PDE Intuition

The Heston PDE contains:

- time derivative
- stock variance term
- variance-process variance term
- cross derivative from correlation
- stock drift under risk-neutral pricing
- variance drift under the chosen risk-neutral measure
- discounting term

A typical PDE structure is:

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

The exact drift of `V` depends on the chosen risk-neutral measure.

That is one place where incompleteness matters.

---

## 16. SABR Model

The SABR model is another popular stochastic volatility model.

It combines ideas from:

- CEV
- stochastic volatility

A simplified structure is:

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

- `alpha` is stochastic volatility
- `beta` controls elasticity
- `nu` controls volatility of volatility
- `rho` controls correlation

The model is popular because it can fit volatility smiles and skews.

---

## 17. Many Risk-Neutral Measures

In incomplete markets, there may be many risk-neutral measures.

The stock can be made a martingale under many different changes of probability.

The issue is that only the stock must have discounted martingale dynamics.

Extra non-tradable factors can have different risk-neutral drifts.

This is why pricing is not unique from no-arbitrage alone.

---

## 18. Market Price of Volatility Risk

When volatility is not tradable, the risk-neutral drift of volatility is not uniquely determined by no-arbitrage.

A parameter is needed to specify how the market prices volatility risk.

In the lecture, this is represented by a process like:

```math
\kappa
```

Different choices of `kappa` give different risk-neutral measures.

Different risk-neutral measures can give different prices for non-replicable claims.

---

## 19. Calibration

In practice, traders usually do not choose the risk-neutral measure only from theory.

They calibrate the model to market option prices.

The process is:

1. choose a model
2. choose parameters
3. compute theoretical option prices
4. compare them with liquid market option prices
5. adjust parameters to reduce pricing errors
6. use calibrated parameters to price less liquid or custom derivatives

A simple calibration objective is:

```math
\min_{\theta}
\sum_i
\left(
C_{\text{model},i}(\theta)
-
C_{\text{market},i}
\right)^2
```

where `theta` is the vector of model parameters.

For Heston:

```math
\theta=(a,b,\gamma,\rho,\ldots)
```

---

## 20. Calibration Intuition

Calibration is like implied volatility, but with more parameters.

In Black-Scholes, the market implies one volatility.

In Heston or SABR, the market can imply several parameters.

Benefit:

- better fit to observed option prices

Cost:

- more complex model
- more computation
- possible overfitting
- parameters may change from day to day
- some state variables, like volatility, are not directly observable

---

## 21. Complete vs Practical Pricing

Theory says:

- complete market: one risk-neutral measure
- incomplete market: many risk-neutral measures

Practice often says:

> The market uses one pricing measure, so we try to estimate it from liquid market prices.

This works better when there are many liquid traded options.

It is much harder in new or illiquid markets with little price history.

---

## 22. Pricing Methods

In these extended models, prices are usually computed by:

### Risk-neutral expectation

```math
C(t,x)=E_t^Q
\left[
e^{-\int_t^T r(u)du}
g(X(T))
\right]
```

### PDE methods

Write the PDE using Ito’s rule and solve numerically.

### Monte Carlo

Simulate paths of all relevant stochastic factors and average discounted payoffs.

---

## 23. Exam Notes

You should be able to:

- explain why constant volatility is restrictive
- explain what local volatility means
- write the local volatility PDE
- explain what the CEV model tries to capture
- explain why deterministic time-dependent volatility uses average variance
- explain why extra Brownian motions can make the market incomplete
- explain why stochastic volatility adds an extra state variable
- describe the Heston model
- explain mean reversion in Heston
- explain why volatility risk may not be hedgeable
- explain why incomplete markets have many risk-neutral measures
- explain calibration to market option prices

---

## 24. Core Formulas

### Local volatility stock process

```math
dS=r(t,S)Sdt+\sigma(t,S)SdW^Q
```

### Local volatility PDE

```math
C_t
+
\frac{1}{2}\sigma^2(t,S)S^2C_{SS}
+
r(t,S)SC_S
-
r(t,S)C
=
0
```

### CEV volatility

```math
\sigma(S)=\frac{\sigma}{S^\beta}
```

### Deterministic volatility variance

```math
Var\left(\int_0^T\sigma(u)dW(u)\right)
=
\int_0^T\sigma^2(u)du
```

### Heston stock process

```math
dS=rSdt+\sqrt{V}SdW^Q
```

### Heston variance process

```math
dV=a(b-V)dt+\gamma\sqrt{V}dZ^Q
```

### Brownian correlation

```math
dW^QdZ^Q=\rho dt
```

### Generic pricing expectation

```math
C(t,x)=E_t^Q
\left[
e^{-\int_t^T r(u)du}g(X(T))
\right]
```

### Calibration objective

```math
\min_{\theta}
\sum_i
\left(
C_{\text{model},i}(\theta)
-
C_{\text{market},i}
\right)^2
```

---

## Final Intuition

The Black-Scholes model is elegant because it is complete and gives closed-form prices.

But real option markets need richer models.

Local volatility keeps one Brownian motion and can remain complete.

Stochastic volatility introduces extra risk factors and often makes the market incomplete.

In incomplete markets, no-arbitrage alone does not give one unique price.

In practice, the model is calibrated to liquid option prices, and then used to price or hedge more complex derivatives.
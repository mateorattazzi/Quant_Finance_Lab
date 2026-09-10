# Module 10 — Forward Rate Models, HJM, BGM and Caplets

## 1. Big Picture

Short-rate models start by modeling:

```math
r(t)
```

and then compute bond prices from the short rate.

Forward-rate models take a different approach.

They model forward rates directly.

Two important frameworks are:

- Heath-Jarrow-Morton, or HJM
- BGM / LIBOR Market Model

The main idea is:

> Instead of modeling only the short rate, model the whole term structure of future rates.

---

## 2. Forward Rates from Bond Prices

Let:

```math
P(t,T)
```

be the price at time `t` of a zero-coupon bond maturing at `T`.

A continuously compounded forward rate between future dates `S` and `T` is defined by:

```math
e^{r(t,S,T)(T-S)}
=
\frac{P(t,S)}{P(t,T)}
```

So:

```math
r(t,S,T)
=
-\frac{\log P(t,T)-\log P(t,S)}{T-S}
```

This comes from a zero-cost strategy:

- short the `S`-maturity bond
- buy `T`-maturity bonds
- invest 1 at time `S`
- receive a known amount at time `T`

---

## 3. Instantaneous Forward Rate

The instantaneous forward rate is the limit as `S` approaches `T`.

It is written:

```math
f(t,T)
```

and is defined by:

```math
f(t,T)
=
-\frac{\partial}{\partial T}\log P(t,T)
```

This is the forward rate today for an infinitesimally short period around future time `T`.

---

## 4. Bond Prices from Forward Rates

The relationship can also be reversed.

If we know the whole forward-rate curve, we can recover bond prices:

```math
P(t,T)
=
e^{-\int_t^T f(t,u)du}
```

This is central to HJM.

Instead of modeling `P(t,T)` or `r(t)` directly, HJM models:

```math
f(t,T)
```

for all maturities `T`.

---

## 5. Short Rate as Immediate Forward Rate

The short rate is the instantaneous forward rate for today:

```math
r(t)=f(t,t)
```

So the short rate is just one point on the forward-rate curve.

---

## 6. HJM Model

In HJM, each forward rate follows a stochastic process:

```math
df(t,T)=\alpha(t,T)dt+\sigma(t,T)dW(t)
```

where:

- `alpha(t,T)` is the drift of the forward rate
- `sigma(t,T)` is the volatility of the forward rate
- `T` is the maturity being modeled

The model describes how the entire forward-rate curve evolves over time.

---

## 7. HJM No-Arbitrage Drift Condition

The key HJM result is that the drift is not freely chosen.

To avoid arbitrage, once we choose the volatility, the drift is determined.

In the one-factor case:

```math
\alpha(t,T)
=
\sigma(t,T)
\int_t^T \sigma(t,u)du
```

Key intuition:

> In HJM, volatility is the modeling input. The drift is forced by no-arbitrage.

This is different from many models where drift and volatility are chosen separately.

---

## 8. Why the Drift Is Restricted

Bond prices are related to forward rates by:

```math
P(t,T)
=
e^{-\int_t^T f(t,u)du}
```

Under the pricing probability, discounted bond prices must be martingales.

That requirement forces the bond-price drift to equal the short rate.

When this condition is translated back into forward-rate dynamics, it gives the HJM drift restriction.

---

## 9. Constant-Volatility HJM Example

Suppose forward-rate volatility is constant:

```math
\sigma(t,T)=\sigma
```

Then the HJM drift becomes:

```math
\alpha(t,T)=\sigma^2(T-t)
```

So:

```math
df(t,T)=\sigma^2(T-t)dt+\sigma dW(t)
```

The corresponding short rate is:

```math
r(t)=f(t,t)
```

This leads to a short-rate model with deterministic drift and constant volatility.

That is closely related to the Ho-Lee model.

---

## 10. Why HJM Was Important

HJM directly models the term structure.

This is useful because market data gives us many bond prices or yields across maturities.

The model starts from the current forward curve and describes how it evolves.

Main benefit:

> HJM connects the dynamics of the whole yield curve with no-arbitrage pricing.

---

## 11. LIBOR Forward Rate

The BGM model works with discrete-tenor LIBOR forward rates.

For dates:

```math
T_{i-1}<T_i
```

define:

```math
\Delta T=T_i-T_{i-1}
```

The forward LIBOR rate is defined by:

```math
1+L(t,T_i)\Delta T
=
\frac{P(t,T_{i-1})}{P(t,T_i)}
```

So:

```math
L(t,T_i)
=
\frac{1}{\Delta T}
\left(
\frac{P(t,T_{i-1})}{P(t,T_i)}
-
1
\right)
```

This is a simple interest rate, not a continuously compounded rate.

---

## 12. BGM / LIBOR Market Model

The BGM model is also called the LIBOR Market Model.

It models forward LIBOR rates directly.

The motivation is practical:

> Traders were already using Black-Scholes type formulas for caplets and floorlets. BGM provides a model that justifies those formulas.

Under the correct forward measure, each relevant LIBOR forward rate can be modeled like a lognormal process.

That gives Black-Scholes type caplet pricing.

---

## 13. Forward Measure Idea

In standard risk-neutral pricing, we discount using the bank account.

For LIBOR derivatives, it is often more convenient to use a zero-coupon bond as the numeraire.

For a payoff paid at `T_i`, we use the `T_i`-forward measure.

Under the `T_i`-forward measure, prices discounted by the `T_i` bond become martingales.

This simplifies caplet pricing.

---

## 14. Caplets

A caplet is a call option on a LIBOR rate.

It pays when the LIBOR rate is above a fixed cap rate.

The payoff at time `T_i` is proportional to:

```math
(L(T_{i-1},T_i)-R_C)^+
```

where:

- `R_C` is the cap rate
- the rate is observed at `T_{i-1}`
- the payoff is paid at `T_i`

A floorlet is the corresponding put option on the LIBOR rate.

---

## 15. Caplet as a Put on a Bond

At time `T_{i-1}`, let:

```math
P=P(T_{i-1},T_i)
```

Then:

```math
L\Delta T
=
\frac{1}{P}-1
```

So:

```math
L
=
\frac{1}{\Delta T}
\left(
\frac{1}{P}-1
\right)
```

The caplet payoff can be rewritten using this bond price.

After algebra, define:

```math
K=\frac{1}{1+R_C\Delta T}
```

Then the caplet payoff paid at `T_i` is equivalent to:

```math
\frac{1}{K}(K-P)^+
```

paid at `T_{i-1}`.

So:

> A caplet can be priced as `1/K` put options on a zero-coupon bond.

The underlying bond matures at `T_i`.

The put option matures at `T_{i-1}`.

The put strike is `K`.

---

## 16. Why the Timing Trick Works

The caplet payoff is paid at `T_i`.

But the payoff is already known at `T_{i-1}`, because the LIBOR rate is fixed then.

If a payoff `C` is known at `T_{i-1}` but paid at `T_i`, then its value at `T_{i-1}` is:

```math
P(T_{i-1},T_i)C
```

Why?

Because buying `C` zero-coupon bonds at `T_{i-1}` costs:

```math
P(T_{i-1},T_i)C
```

and pays exactly `C` at `T_i`.

This turns the delayed caplet payoff into an equivalent payoff one period earlier.

That is what makes the bond-put interpretation possible.

---

## 17. Main Connections

Short-rate models:

```text
model r(t)
```

HJM:

```text
model instantaneous forward rates f(t,T)
```

BGM:

```text
model discrete LIBOR forward rates L(t,T_i)
```

Caplet pricing:

```text
can be seen as Black-Scholes pricing on LIBOR,
or as put-option pricing on a zero-coupon bond
```

---

## 18. Exam Notes

You should be able to:

- define an instantaneous forward rate
- derive bond prices from forward rates
- explain the HJM modeling idea
- state the HJM no-arbitrage drift restriction
- explain why HJM drift is determined by volatility
- define the forward LIBOR rate
- explain what a forward measure is used for
- describe BGM as the LIBOR Market Model
- explain what a caplet and floorlet are
- rewrite a caplet as a put option on a zero-coupon bond

---

## 19. Core Formulas

### Forward rate from bond prices

```math
r(t,S,T)
=
-\frac{\log P(t,T)-\log P(t,S)}{T-S}
```

### Instantaneous forward rate

```math
f(t,T)
=
-\frac{\partial}{\partial T}\log P(t,T)
```

### Bond price from forward rates

```math
P(t,T)
=
e^{-\int_t^T f(t,u)du}
```

### Short rate

```math
r(t)=f(t,t)
```

### HJM forward-rate dynamics

```math
df(t,T)=\alpha(t,T)dt+\sigma(t,T)dW(t)
```

### HJM drift restriction

```math
\alpha(t,T)
=
\sigma(t,T)
\int_t^T \sigma(t,u)du
```

### Forward LIBOR rate

```math
1+L(t,T_i)\Delta T
=
\frac{P(t,T_{i-1})}{P(t,T_i)}
```

### LIBOR formula

```math
L(t,T_i)
=
\frac{1}{\Delta T}
\left(
\frac{P(t,T_{i-1})}{P(t,T_i)}
-
1
\right)
```

### Caplet bond-option strike

```math
K=\frac{1}{1+R_C\Delta T}
```

### Caplet as bond put

```math
\text{Caplet}
\equiv
\frac{1}{K}(K-P(T_{i-1},T_i))^+
```

---

## Final Intuition

HJM models the whole instantaneous forward-rate curve.

Its main no-arbitrage result is that the drift is determined by volatility.

BGM models market LIBOR forward rates directly and leads to Black-Scholes type caplet pricing.

A caplet can also be viewed as a put option on a zero-coupon bond, because the LIBOR rate is fixed one period before the caplet is paid.
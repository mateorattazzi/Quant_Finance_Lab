# Module 10 — Summary: Fixed Income Derivatives

## 1. Big Picture

Module 10 extends the course to fixed income derivatives.

Earlier, interest rates were treated as deterministic.

Now interest rates are modeled as stochastic processes.

The main objects are:

- zero-coupon bonds
- short rates
- forward rates
- bond options
- caplets and floorlets
- credit-risky securities

Core idea:

> In fixed income, derivative pricing depends on how interest rates, bond prices, and default risk evolve over time.

---

## 2. Zero-Coupon Bond Pricing

A zero-coupon bond pays 1 at maturity `T`.

Its price at time `t` is:

```math
P(t,T)
```

If the interest rate is constant:

```math
P(t,T)=e^{-r(T-t)}
```

If the short rate is stochastic:

```math
P(t,T)
=
E_t
\left[
e^{-\int_t^T r(u)du}
\right]
```

All expectations in this module are under the pricing probability.

---

## 3. Why Model the Short Rate?

Instead of modeling every bond maturity separately, short-rate models model:

```math
r(t)
```

Then bond prices are derived from the short rate.

This helps create an internally consistent and arbitrage-free bond market.

The discounted bond price is:

```math
e^{-\int_0^t r(u)du}P(t,T)
```

Under the pricing probability, this must be a martingale.

---

## 4. Bond Options

A call option on a zero-coupon bond gives the right to buy a bond at strike `K`.

If the option matures at `T_1` and the bond matures at `T_2`, with `T_1<T_2`, the payoff is:

```math
(P(T_1,T_2)-K)^+
```

The price is the discounted expected payoff under the pricing probability.

---

## 5. One-Factor Short-Rate Models

A general one-factor short-rate model is:

```math
dr(t)=\mu(t,r(t))dt+\sigma(t,r(t))dW(t)
```

There is one Brownian source of interest-rate risk.

A derivative price depending on the short rate is written:

```math
C(t,r)
```

The pricing PDE is:

```math
C_t
+
\frac{1}{2}\sigma^2(t,r)C_{rr}
+
\mu(t,r)C_r
-
rC
=
0
```

---

## 6. Vasicek Model

The Vasicek model is:

```math
dr=a(b-r)dt+\sigma dW
```

where:

- `b` is the long-run mean
- `a` is the speed of mean reversion
- `sigma` is volatility

If `r<b`, the drift pushes rates up.

If `r>b`, the drift pushes rates down.

Advantage:

> Tractable and gives explicit bond-price formulas.

Drawback:

> Rates are normally distributed, so they can become negative.

---

## 7. CIR Model

The CIR model is:

```math
dr=a(b-r)dt+\sigma\sqrt{r}dW
```

It keeps the same mean-reverting drift as Vasicek.

The square-root volatility helps keep rates non-negative.

When `r=0`:

```math
\sigma\sqrt{r}=0
```

and the drift is positive:

```math
ab>0
```

So the rate is pushed upward.

---

## 8. Ho-Lee, Hull-White and BDT

Ho-Lee:

```math
dr=b(t)dt+\sigma dW
```

The time-dependent drift helps fit the current yield curve.

Hull-White:

```math
dr=(b(t)-ar)dt+\sigma dW
```

It adds mean reversion to Ho-Lee.

Black-Derman-Toy style model:

```math
dr=b(t)r\,dt+\sigma r\,dW
```

It keeps rates positive, but the continuous-time version can create mathematical problems.

---

## 9. Affine Models

Affine models look for bond prices of the form:

```math
P(t,T)=e^{A(t,T)+B(t,T)r(t)}
```

The exponent is linear in the short rate.

At maturity:

```math
P(T,T)=1
```

so:

```math
A(T,T)=0
```

```math
B(T,T)=0
```

Vasicek and CIR are affine models.

They are useful because they often give explicit or semi-explicit bond prices.

---

## 10. Forward Rates

Forward-rate models describe future interest rates directly.

The instantaneous forward rate is:

```math
f(t,T)
=
-\frac{\partial}{\partial T}\log P(t,T)
```

Bond prices can be recovered from forward rates:

```math
P(t,T)
=
e^{-\int_t^T f(t,u)du}
```

The short rate is the immediate forward rate:

```math
r(t)=f(t,t)
```

---

## 11. HJM Model

The Heath-Jarrow-Morton model describes the evolution of the whole forward-rate curve.

A basic HJM form is:

```math
df(t,T)=\alpha(t,T)dt+\sigma(t,T)dW(t)
```

The key no-arbitrage result is:

> Once the forward-rate volatility is chosen, the drift is determined.

In the one-factor case:

```math
\alpha(t,T)
=
\sigma(t,T)
\int_t^T \sigma(t,u)du
```

---

## 12. BGM / LIBOR Market Model

The BGM model is also called the LIBOR Market Model.

It models discrete forward LIBOR rates directly.

For dates `T_{i-1}` and `T_i`:

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

BGM is useful because it gives Black-Scholes type pricing formulas for caplets and floorlets.

---

## 13. Caplets

A caplet is a call option on a LIBOR rate.

It pays when LIBOR is above a cap rate `R_C`.

The rate is fixed at `T_{i-1}`, but the payoff is paid at `T_i`.

The caplet payoff depends on:

```math
(L(T_{i-1},T_i)-R_C)^+
```

A floorlet is the corresponding put option on LIBOR.

---

## 14. Caplet as a Bond Put

At time `T_{i-1}`, let:

```math
P=P(T_{i-1},T_i)
```

Then:

```math
L\Delta T=\frac{1}{P}-1
```

Define:

```math
K=\frac{1}{1+R_C\Delta T}
```

The caplet can be rewritten as:

```math
\frac{1}{K}(K-P)^+
```

So:

> A caplet is equivalent to `1/K` put options on a zero-coupon bond.

The bond matures at `T_i`.

The put matures at `T_{i-1}`.

---

## 15. Change of Numeraire

A numeraire is the asset used as the unit of measurement.

The general formula is:

```math
C(t)
=
S(t)
E_t^S
\left[
\frac{C(T)}{S(T)}
\right]
```

where `S(t)` is the numeraire.

Standard risk-neutral pricing uses the bank account as numeraire.

For bond options, it is often easier to use a zero-coupon bond as numeraire.

---

## 16. Bond Option Formula

For a call option on a bond maturing at `T_2`, with option maturity `T_1`, the payoff is:

```math
(P(T_1,T_2)-K)^+
```

Using the `T_1` bond as numeraire gives a Black-Scholes type formula:

```math
C(0)
=
P(0,T_2)N(d_1)
-
K P(0,T_1)N(d_2)
```

where:

```math
d_2=d_1-\Sigma
```

and `Sigma` is the total volatility of the bond-price ratio.

---

## 17. Credit Risk Models

Credit risk models include the possibility of default.

Two main approaches:

1. structural models
2. reduced-form models

---

## 18. Structural Credit Models

Structural models model the value of the firm.

In Merton’s model:

```math
dV=rVdt+\sigma_V VdW
```

where `V` is firm value.

The firm has debt with face value `D`.

At maturity, equity holders receive:

```math
E(T)=(V(T)-D)^+
```

So:

> Equity is a call option on firm value.

Risky debt pays:

```math
\min(V(T),D)
```

which can be written as:

```math
D-(D-V(T))^+
```

So:

> Risky debt equals risk-free debt minus a put.

---

## 19. Reduced-Form Credit Models

Reduced-form models model the default time directly.

Let:

```math
\tau
```

be the default time.

If default intensity is constant:

```math
\lambda
```

then survival probability is:

```math
P(\tau>T)=e^{-\lambda T}
```

If a payoff is paid only if default does not occur, its price is:

```math
E
\left[
e^{-rT}C(T)\mathbf{1}_{\{\tau>T\}}
\right]
```

With independence and constant intensity, this becomes:

```math
E
\left[
e^{-(r+\lambda)T}C(T)
\right]
```

So default risk acts like extra discounting.

---

## 20. Main Lessons

Fixed income derivatives are different from equity derivatives because the discount rate itself is random.

The main modeling approaches are:

- short-rate models
- forward-rate models
- LIBOR market models
- change of numeraire
- credit risk models

The practical goal is to price and hedge products linked to:

- bond prices
- yield curves
- LIBOR rates
- default events

---

## 21. Exam Checklist

You should be able to:

- write the zero-coupon bond pricing formula
- explain why short-rate models are useful
- describe Vasicek and CIR
- explain mean reversion
- explain affine bond pricing
- define forward rates
- explain the HJM drift restriction
- define LIBOR forward rates
- explain caplets and floorlets
- rewrite a caplet as a bond put
- explain change of numeraire
- write the bond option formula
- explain structural credit models
- explain reduced-form credit models

---

## 22. Core Formulas

### Zero-coupon bond price

```math
P(t,T)
=
E_t
\left[
e^{-\int_t^T r(u)du}
\right]
```

### One-factor short-rate PDE

```math
C_t
+
\frac{1}{2}\sigma^2(t,r)C_{rr}
+
\mu(t,r)C_r
-
rC
=
0
```

### Vasicek

```math
dr=a(b-r)dt+\sigma dW
```

### CIR

```math
dr=a(b-r)dt+\sigma\sqrt{r}dW
```

### Forward rate

```math
f(t,T)
=
-\frac{\partial}{\partial T}\log P(t,T)
```

### Bond from forward rates

```math
P(t,T)
=
e^{-\int_t^T f(t,u)du}
```

### HJM drift restriction

```math
\alpha(t,T)
=
\sigma(t,T)
\int_t^T \sigma(t,u)du
```

### LIBOR forward rate

```math
1+L(t,T_i)\Delta T
=
\frac{P(t,T_{i-1})}{P(t,T_i)}
```

### Caplet as bond put

```math
\text{Caplet}
\equiv
\frac{1}{K}(K-P(T_{i-1},T_i))^+
```

### Change of numeraire

```math
C(t)
=
S(t)
E_t^S
\left[
\frac{C(T)}{S(T)}
\right]
```

### Bond option formula

```math
C(0)
=
P(0,T_2)N(d_1)
-
K P(0,T_1)N(d_2)
```

### Equity as call

```math
E(T)=(V(T)-D)^+
```

### Risky debt

```math
\min(V(T),D)
=
D-(D-V(T))^+
```

### Survival probability

```math
P(\tau>T)=e^{-\lambda T}
```

---

## Final Intuition

Module 10 shows how derivative pricing changes when interest rates are random.

Short-rate models start with `r(t)` and derive bond prices.

Forward-rate models model the yield curve directly.

BGM models LIBOR rates and supports caplet pricing.

Change of numeraire simplifies bond option pricing.

Credit models add default risk, either by modeling firm value or by modeling default intensity.
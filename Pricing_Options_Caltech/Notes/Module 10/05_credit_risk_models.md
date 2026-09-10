# Module 10 — Credit Risk Models

## 1. Big Picture

Credit risk models include the possibility that a company may default.

Default matters for:

- corporate bonds
- credit derivatives
- credit default swaps
- collateralized debt obligations

The course introduces two basic approaches:

1. structural models
2. reduced-form models

---

## 2. Structural Models

Structural models model the value of the firm directly.

The simplest structural model is Merton’s credit risk model.

The firm value is modeled like a Black-Scholes asset:

```math
dV=rVdt+\sigma_V VdW
```

where:

- `V` = value of the firm
- `r` = risk-free rate
- `sigma_V` = volatility of firm value

Sometimes payments leaving the firm, such as dividends, can also be subtracted.

---

## 3. Firm Value, Debt and Equity

The firm has:

- equity
- debt

In a simplified setting:

```math
V(t)=E(t)+D(t)
```

where:

- `E(t)` = equity value
- `D(t)` = debt value

Assume the firm has one zero-coupon bond with face value `D` maturing at time `T`.

---

## 4. Default in the Merton Model

Default can only happen at maturity `T`.

At `T`, the firm must pay bondholders the promised amount `D`.

If:

```math
V(T)\geq D
```

the firm can pay the debt.

If:

```math
V(T)<D
```

the firm defaults.

Bondholders receive what is left, and equity holders receive zero.

---

## 5. Equity as a Call Option

At maturity, equity holders receive what remains after paying debt:

```math
E(T)=(V(T)-D)^+
```

This is exactly the payoff of a call option on the firm value.

So in the Merton model:

> Equity is a call option on the value of the firm.

Underlying asset:

```math
V(T)
```

Strike:

```math
D
```

---

## 6. Debt as Risk-Free Debt Minus a Put

Bondholders receive:

```math
\min(V(T),D)
```

This can be rewritten as:

```math
D-(D-V(T))^+
```

So risky debt is equivalent to:

```text
risk-free debt minus a put option on firm value
```

Therefore, the value of risky debt is:

```math
\text{Risky Debt}
=
De^{-rT}
-
\text{Put}(V,D,T)
```

where the put has:

- underlying `V`
- strike `D`
- maturity `T`

---

## 7. Why This Is Useful

Merton’s model connects corporate debt valuation to option pricing.

It shows that:

- equity behaves like a call option
- defaultable debt behaves like risk-free debt minus a put
- Black-Scholes ideas can be used to price corporate debt

The model is intuitive and tractable.

---

## 8. Main Problem with Structural Models

The value of the firm is not directly observable.

We can observe:

- equity value
- possibly equity volatility

But we do not directly observe:

```math
V
```

or:

```math
\sigma_V
```

This makes calibration difficult.

---

## 9. Estimating Firm Value and Firm Volatility

In the Black-Scholes version of Merton’s model, equity is a call option on firm value.

So one equation is:

```math
E=\text{Call}(V,D,T,\sigma_V)
```

A second equation comes from matching equity volatility:

```math
\sigma_E E=N(d_1)\sigma_V V
```

where:

- `sigma_E` = equity volatility
- `N(d_1)` = call delta
- `sigma_V` = firm-value volatility

These two equations can be solved numerically for:

```math
V
```

and:

```math
\sigma_V
```

---

## 10. Reduced-Form Models

Reduced-form models do not model firm value directly.

Instead, they model the default time directly.

They are also called intensity-based models.

The simplest assumption is:

```math
\tau \sim \text{Exponential}(\lambda)
```

where:

- `tau` = default time
- `lambda` = default intensity

Higher `lambda` means default is more likely to arrive sooner.

---

## 11. Survival Probability

If default time is exponentially distributed, then the probability of no default by time `T` is:

```math
P(\tau>T)=e^{-\lambda T}
```

This is called the survival probability.

---

## 12. Simple Defaultable Payoff

Suppose a payoff `C(T)` is paid only if default has not occurred.

If default occurs, the payoff is zero.

The payoff is:

```math
C(T)\mathbf{1}_{\{\tau>T\}}
```

Assume:

- constant interest rate `r`
- default is independent of `C(T)`

Then the price is:

```math
E\left[e^{-rT}C(T)\mathbf{1}_{\{\tau>T\}}\right]
```

Using independence:

```math
=
E\left[e^{-rT}C(T)\right]P(\tau>T)
```

So:

```math
=
E\left[e^{-rT}C(T)\right]e^{-\lambda T}
```

This is equivalent to discounting at:

```math
r+\lambda
```

instead of only `r`.

---

## 13. Main Reduced-Form Intuition

Default risk acts like extra discounting.

With constant `r` and constant `lambda`:

```math
\text{Defaultable Price}
=
E\left[e^{-(r+\lambda)T}C(T)\right]
```

The higher the default intensity, the lower the price.

---

## 14. Stochastic Rates and Stochastic Intensity

The same idea can be generalized.

If both the short rate and default intensity change over time, the discounting becomes:

```math
e^{-\int_0^T (r(u)+\lambda(u))du}
```

So the pricing formula has the form:

```math
E
\left[
e^{-\int_0^T (r(u)+\lambda(u))du}
C(T)
\right]
```

The model now combines:

- interest-rate risk
- default risk

---

## 15. Pricing Probability vs Real Probability

The default intensity used for pricing is under the pricing probability.

It is not necessarily the historical default intensity.

In practice, `lambda` is calibrated to market prices such as:

- corporate bonds
- credit default swaps
- other liquid credit instruments

The pricing default probability is often higher than the historical default probability.

This reflects risk aversion and compensation for unhedgeable default risk.

---

## 16. Structural vs Reduced-Form Models

Structural models:

- model firm value
- connect default to the firm’s balance sheet
- have strong economic intuition
- treat equity as a call option
- treat risky debt as risk-free debt minus a put
- require estimating unobservable firm value

Reduced-form models:

- model default time directly
- use default intensity `lambda`
- are more pragmatic
- often easier to calibrate
- do not explain default through firm value

---

## 17. Exam Notes

You should be able to:

- explain structural credit risk models
- describe Merton’s model
- explain why equity is a call option on firm value
- explain why risky debt equals risk-free debt minus a put
- explain why firm value is difficult to observe
- define reduced-form or intensity-based models
- interpret default intensity `lambda`
- compute survival probability under exponential default time
- explain why default risk acts like extra discounting
- explain why pricing default probabilities differ from historical probabilities

---

## 18. Core Formulas

### Firm value dynamics

```math
dV=rVdt+\sigma_V VdW
```

### Firm value decomposition

```math
V=E+D
```

### Equity payoff

```math
E(T)=(V(T)-D)^+
```

### Debt payoff

```math
\min(V(T),D)
=
D-(D-V(T))^+
```

### Risky debt value

```math
\text{Risky Debt}
=
De^{-rT}
-
\text{Put}(V,D,T)
```

### Equity volatility relation

```math
\sigma_E E=N(d_1)\sigma_V V
```

### Survival probability

```math
P(\tau>T)=e^{-\lambda T}
```

### Defaultable payoff price

```math
E
\left[
e^{-rT}C(T)\mathbf{1}_{\{\tau>T\}}
\right]
```

### Constant intensity pricing

```math
E
\left[
e^{-(r+\lambda)T}C(T)
\right]
```

### Stochastic rate and intensity pricing

```math
E
\left[
e^{-\int_0^T (r(u)+\lambda(u))du}
C(T)
\right]
```

---

## Final Intuition

Credit risk models price securities when default is possible.

Merton’s structural model explains default through firm value: equity is like a call option, and risky debt is risk-free debt minus a put.

Reduced-form models skip firm value and model default arrival directly with an intensity.

In the simplest reduced-form model, default risk behaves like an extra discount rate added to the risk-free rate.
# Module 10 — Short-Rate Models and Bond Options

## 1. Big Picture

Earlier in the course, interest rates were treated as deterministic.

Now we model interest rates as stochastic processes.

The key object is the short rate:

```math
r(t)
```

This is the instantaneous interest rate at time `t`.

Instead of modeling every bond price directly, short-rate models model `r(t)` first.

Then bond prices are computed from the short rate.

---

## 2. Zero-Coupon Bond

A zero-coupon bond pays one fixed amount at maturity and no coupons before maturity.

In the course, the payoff is normalized to:

```math
1
```

at maturity `T`.

The price at time `t` is written:

```math
P(t,T)
```

where:

- `t` = today
- `T` = bond maturity
- `P(t,T)` = price today of receiving 1 at time `T`

---

## 3. Constant Interest Rate Case

If the continuously compounded interest rate is constant, the zero-coupon bond price is:

```math
P(t,T)=e^{-r(T-t)}
```

This is just the present value of 1 paid at time `T`.

---

## 4. Stochastic Interest Rate Case

If the short rate changes over time, discounting uses the integral of the short rate.

The discount factor from `t` to `T` is:

```math
e^{-\int_t^T r(u)du}
```

Because `r(u)` is random, the bond price is the risk-neutral expectation:

```math
P(t,T)
=
E_t
\left[
e^{-\int_t^T r(u)du}
\right]
```

In this section, all expectations are under the pricing probability.

The course stops writing the `Q`, but the idea is still risk-neutral pricing.

---

## 5. Why Model the Short Rate?

There are many bonds with different maturities.

If we model every bond price separately, we must ensure that all bond prices are consistent and arbitrage-free.

A short-rate model avoids this problem.

The procedure is:

1. model the short rate `r(t)`
2. compute every bond price from the same discounting formula
3. obtain bond prices that are internally consistent

The key formula is:

```math
P(t,T)
=
E_t
\left[
e^{-\int_t^T r(u)du}
\right]
```

---

## 6. Why This Avoids Arbitrage

Under this construction, discounted bond prices are martingales.

The discounted bond price is:

```math
e^{-\int_0^t r(u)du}P(t,T)
```

Using the bond pricing formula:

```math
e^{-\int_0^t r(u)du}P(t,T)
=
E_t
\left[
e^{-\int_0^T r(u)du}
\right]
```

The right-hand side is a conditional expectation of a fixed future random variable.

A process of the form:

```math
M(t)=E_t[X]
```

is a martingale.

So discounted bond prices are martingales under the pricing probability.

By the no-arbitrage theorem, this implies the bond market is arbitrage-free.

---

## 7. Calibration

In practice, short-rate models are not mainly used to price simple bonds from scratch.

Market bond prices and yields are already observable.

Instead, we use them to calibrate the model.

The practical procedure is:

1. choose a short-rate model
2. choose model parameters
3. compute theoretical bond prices
4. compare them with observed market bond prices
5. adjust parameters until the model fits the yield curve

The model is calibrated to today’s bond prices or yield curve.

Parameters calibrated today may differ from parameters calibrated tomorrow.

This is theoretically imperfect, but common in practice.

---

## 8. Bond Options

A bond option is an option whose underlying asset is a bond.

Example:

A European call option on a zero-coupon bond.

Let:

- `T` = maturity of the bond
- `tau` = maturity of the option
- `tau < T`
- `K` = option strike

At time `tau`, the option payoff is:

```math
(P(\tau,T)-K)^+
```

The option price at time `t` is:

```math
E_t
\left[
e^{-\int_t^\tau r(u)du}
(P(\tau,T)-K)^+
\right]
```

The option payoff depends on the bond price at the option maturity.

That bond price itself is:

```math
P(\tau,T)
=
E_\tau
\left[
e^{-\int_\tau^T r(u)du}
\right]
```

---

## 9. Discrete-Time Short-Rate Tree

A simple way to model stochastic interest rates is with a binomial tree.

At each date, the interest rate can move:

- up
- down

Once the interest-rate tree is built, bond prices are computed by backward induction.

The logic is:

1. start from the bond payoff at maturity
2. move backward through the tree
3. discount expected future values using the short rate at each node

---

## 10. Example Setup

Current one-year interest rate:

```math
r_0=4\%
```

After one year, the interest rate can be:

```math
5\%
```

or:

```math
3\%
```

There is a two-year zero-coupon bond with face value:

```math
100
```

Its current market price is:

```math
92.278
```

We want to price a European call option on this bond.

The option matures in one year.

The strike is:

```math
K=96
```

---

## 11. Step 1: Bond Prices After One Year

If the short rate after one year is `5%`, the one-year remaining bond price is:

```math
P_u=\frac{100}{1.05}=95.238
```

If the short rate after one year is `3%`, the one-year remaining bond price is:

```math
P_d=\frac{100}{1.03}=97.087
```

Important intuition:

> Bond prices move opposite to interest rates.

When rates go up, the bond price goes down.

When rates go down, the bond price goes up.

---

## 12. Step 2: Find the Risk-Neutral Probability

Let `p` be the pricing probability of the up-rate state.

Today’s bond price must equal the discounted expected future bond price:

```math
92.278
=
\frac{1}{1.04}
\left[
p(95.238)+(1-p)(97.087)
\right]
```

Solving gives:

```math
p=0.605
```

So:

```math
1-p=0.395
```

This is not the real-world probability.

It is the pricing probability that makes today’s bond price consistent with the tree.

---

## 13. Step 3: Bond Option Payoffs

The call payoff after one year is:

```math
(P(1,2)-K)^+
```

If rates go up:

```math
P_u=95.238
```

The payoff is:

```math
(95.238-96)^+=0
```

If rates go down:

```math
P_d=97.087
```

The payoff is:

```math
(97.087-96)^+=1.087
```

---

## 14. Step 4: Price the Bond Call Option

Discount the expected payoff using today’s one-year short rate:

```math
C_0
=
\frac{1}{1.04}
\left[
p(0)+(1-p)(1.087)
\right]
```

Substitute:

```math
C_0
=
\frac{1}{1.04}
\left[
0.395(1.087)
\right]
```

So:

```math
C_0
\approx 0.413
```

---

## 15. Main Intuition

In fixed income models, the short rate drives bond prices.

Bond prices are computed by discounting future cash flows using the path of the short rate.

In a binomial short-rate tree, we:

1. compute bond prices backward
2. infer the risk-neutral probability from observed bond prices
3. use that probability to price bond derivatives

---

## 16. Exam Notes

You should be able to:

- define a zero-coupon bond
- explain why bond prices depend on the short rate
- write the stochastic discounting formula
- explain why expectations are under the pricing probability
- explain why short-rate models help avoid arbitrage
- compute bond prices in a short-rate tree
- infer the risk-neutral probability from a bond price
- price a European call option on a bond by backward induction

---

## 17. Core Formulas

### Constant-rate zero-coupon bond price

```math
P(t,T)=e^{-r(T-t)}
```

### Stochastic short-rate bond price

```math
P(t,T)
=
E_t
\left[
e^{-\int_t^T r(u)du}
\right]
```

### Discounted bond price

```math
e^{-\int_0^t r(u)du}P(t,T)
```

### Bond option payoff

```math
(P(\tau,T)-K)^+
```

### Bond option price

```math
E_t
\left[
e^{-\int_t^\tau r(u)du}
(P(\tau,T)-K)^+
\right]
```

### One-step bond tree price

```math
P_0
=
\frac{1}{1+r_0}
\left[
pP_u+(1-p)P_d
\right]
```

### One-step bond call price

```math
C_0
=
\frac{1}{1+r_0}
\left[
p(P_u-K)^+
+
(1-p)(P_d-K)^+
\right]
```

---

## Final Intuition

Short-rate models make interest rates random.

Instead of modeling every bond price directly, we model the short rate and compute bond prices from risk-neutral discounted expectations.

This creates an internally consistent bond market.

Once bond prices are known in the tree, bond options are priced exactly like other derivatives: compute the payoff at option maturity and discount the risk-neutral expected payoff backward.
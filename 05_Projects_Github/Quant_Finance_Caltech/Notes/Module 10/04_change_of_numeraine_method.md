# Module 10 — Change of Numeraire and Bond Options

## 1. Big Picture

A numeraire is the asset used as the unit of measurement.

So far, most pricing used the bank account as numeraire.

That means prices were discounted by the bank account.

But the bank account is not the only possible numeraire.

We can also use:

- a stock
- a zero-coupon bond
- another traded asset

Changing the numeraire can make some expectations easier to compute.

---

## 2. General Change of Numeraire Formula

Let `S(t)` be the chosen numeraire asset.

We look for a probability measure `P^S` such that every traded asset price divided by `S(t)` is a martingale.

That means:

```math
\frac{C(t)}{S(t)}
=
E_t^{S}
\left[
\frac{C(T)}{S(T)}
\right]
```

Rearranging gives:

```math
C(t)
=
S(t)
E_t^{S}
\left[
\frac{C(T)}{S(T)}
\right]
```

This is the general pricing formula under a chosen numeraire.

---

## 3. Usual Risk-Neutral Pricing as a Special Case

If the numeraire is the bank account:

```math
B(t)=e^{rt}
```

then the formula becomes the usual risk-neutral formula:

```math
C(t)
=
E_t^Q
\left[
e^{-r(T-t)}C(T)
\right]
```

So standard risk-neutral pricing is just one special case of change of numeraire.

---

## 4. Why Change the Numeraire?

Sometimes a payoff contains a difficult random factor.

If we choose that factor as the numeraire, it can cancel inside the expectation.

This can turn a hard expectation into a probability.

That is why change of numeraire is useful.

---

## 5. Black-Scholes Call Example

For a European call:

```math
(S(T)-K)^+
=
S(T)\mathbf{1}_{\{S(T)>K\}}
-
K\mathbf{1}_{\{S(T)>K\}}
```

The second term is easy under the usual risk-neutral measure:

```math
K e^{-r(T-t)}
Q(S(T)>K)
```

The first term is harder:

```math
E_t^Q
\left[
e^{-r(T-t)}S(T)\mathbf{1}_{\{S(T)>K\}}
\right]
```

Change of numeraire helps by using the stock itself as numeraire.

Then `S(T)` cancels, and the expectation becomes a probability under the stock measure.

This gives the familiar Black-Scholes term:

```math
S(t)N(d_1)
```

The second term gives:

```math
K e^{-r(T-t)}N(d_2)
```

So:

```math
C(t,S)
=
S(t)N(d_1)
-
K e^{-r(T-t)}N(d_2)
```

---

## 6. Using a Bond as Numeraire

For interest-rate derivatives, it is often useful to use a zero-coupon bond as numeraire.

If a payoff is paid at time `T`, use the `T`-maturity zero-coupon bond:

```math
P(t,T)
```

as numeraire.

This leads to the `T`-forward measure.

Under this measure, prices divided by `P(t,T)` are martingales.

---

## 7. General Call Formula with Bond Numeraire

Consider a call option with maturity `T` and payoff:

```math
(S(T)-K)^+
```

Use the zero-coupon bond `P(t,T)` as numeraire.

If the ratio

```math
F(t)=\frac{S(t)}{P(t,T)}
```

has deterministic volatility, then a Black-Scholes type formula applies.

The call price at time `0` is:

```math
C(0)
=
S(0)N(d_1)
-
K P(0,T)N(d_2)
```

where:

```math
d_1
=
\frac{
\ln\left(\frac{S(0)}{KP(0,T)}\right)
+
\frac{1}{2}\Sigma_F^2(T)
}{
\Sigma_F(T)
}
```

```math
d_2=d_1-\Sigma_F(T)
```

and:

```math
\Sigma_F(T)
=
\sqrt{
\int_0^T \sigma_F^2(u)du
}
```

This is like Black-Scholes, but `e^{-rT}` is replaced by the bond price `P(0,T)`.

---

## 8. Why `P(0,T)` Replaces Discounting

When rates are deterministic:

```math
P(0,T)=e^{-rT}
```

So the formula becomes the usual Black-Scholes formula.

When rates are stochastic, we cannot simply write `e^{-rT}`.

Instead, discounting to maturity `T` is represented by the zero-coupon bond price:

```math
P(0,T)
```

---

## 9. Bond Option Setup

Now suppose we want to price a call option on a zero-coupon bond.

The underlying bond matures at:

```math
T_2
```

The option matures earlier at:

```math
T_1<T_2
```

The payoff at `T_1` is:

```math
(P(T_1,T_2)-K)^+
```

To use the bond-numeraire formula:

- underlying asset: `P(t,T_2)`
- numeraire: `P(t,T_1)`
- option maturity: `T_1`

---

## 10. Bond Price in an Affine Model

In affine short-rate models, bond prices often have the form:

```math
P(t,T)=e^{A(t,T)-B(t,T)r(t)}
```

where `A` and `B` are deterministic functions.

For the bond option, the key ratio is:

```math
\frac{P(t,T_2)}{P(t,T_1)}
```

Using the affine form:

```math
\frac{P(t,T_2)}{P(t,T_1)}
=
e^{
A(t,T_2)-A(t,T_1)
-
[B(t,T_2)-B(t,T_1)]r(t)
}
```

---

## 11. Deterministic Volatility of the Ratio

In the Vasicek model:

```math
dr=a(b-r)dt+\sigma dW
```

The volatility of `r` is constant.

Since the ratio depends on `r(t)` through a deterministic coefficient, the volatility of the ratio is deterministic.

Specifically, the volatility is proportional to:

```math
-[B(t,T_2)-B(t,T_1)]\sigma
```

The sign does not matter for total variance.

So the accumulated variance input is:

```math
\Sigma_F^2(T_1)
=
\int_0^{T_1}
\sigma^2
[B(u,T_2)-B(u,T_1)]^2du
```

---

## 12. Call Option on a Bond

Using the general bond-numeraire call formula, the price of a call on the `T_2` bond with option maturity `T_1` is:

```math
C(0)
=
P(0,T_2)N(d_1)
-
K P(0,T_1)N(d_2)
```

where:

```math
d_1
=
\frac{
\ln\left(\frac{P(0,T_2)}{KP(0,T_1)}\right)
+
\frac{1}{2}\Sigma_F^2(T_1)
}{
\Sigma_F(T_1)
}
```

```math
d_2=d_1-\Sigma_F(T_1)
```

and:

```math
\Sigma_F(T_1)
=
\sqrt{
\int_0^{T_1}
\sigma^2
[B(u,T_2)-B(u,T_1)]^2du
}
```

---

## 13. Main Intuition

Change of numeraire changes the asset used for discounting.

The pricing measure changes with the numeraire.

The goal is to make the payoff easier to price.

For bond options, using the option-maturity bond as numeraire turns the pricing problem into a Black-Scholes type formula.

---

## 14. Exam Notes

You should be able to:

- explain what a numeraire is
- write the general change-of-numeraire formula
- explain why standard risk-neutral pricing uses the bank account as numeraire
- explain why changing numeraire can simplify expectations
- describe the stock-numeraire idea behind the `S N(d_1)` term
- use a zero-coupon bond as numeraire for interest-rate derivatives
- price a call option on a bond using the bond-numeraire formula

---

## 15. Core Formulas

### Change of numeraire

```math
C(t)
=
S(t)
E_t^{S}
\left[
\frac{C(T)}{S(T)}
\right]
```

### Bond numeraire call formula

```math
C(0)
=
S(0)N(d_1)
-
K P(0,T)N(d_2)
```

### `d_1`

```math
d_1
=
\frac{
\ln\left(\frac{S(0)}{KP(0,T)}\right)
+
\frac{1}{2}\Sigma_F^2(T)
}{
\Sigma_F(T)
}
```

### `d_2`

```math
d_2=d_1-\Sigma_F(T)
```

### Total deterministic volatility

```math
\Sigma_F(T)
=
\sqrt{
\int_0^T \sigma_F^2(u)du
}
```

### Bond option formula

```math
C(0)
=
P(0,T_2)N(d_1)
-
K P(0,T_1)N(d_2)
```

### Bond option total volatility in Vasicek

```math
\Sigma_F(T_1)
=
\sqrt{
\int_0^{T_1}
\sigma^2
[B(u,T_2)-B(u,T_1)]^2du
}
```

---

## Final Intuition

The numeraire is the asset used to measure value.

Changing the numeraire changes the pricing probability.

This can make difficult expectations easier.

For bond options, using the option-maturity bond as numeraire gives a Black-Scholes type formula where stochastic discounting is replaced by zero-coupon bond prices.
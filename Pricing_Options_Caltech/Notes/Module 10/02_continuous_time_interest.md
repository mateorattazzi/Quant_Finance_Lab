# Module 10 — One-Factor Short-Rate Models

## 1. Big Picture

A short-rate model describes the instantaneous interest rate as a stochastic process:

```math
r(t)
```

Once `r(t)` is modeled, zero-coupon bond prices are computed from:

```math
P(t,T)
=
E_t
\left[
e^{-\int_t^T r(u)du}
\right]
```

All expectations are under the pricing probability.

The main idea is:

> Model the short rate first, then derive bond prices and bond option prices from it.

---

## 2. General One-Factor Model

A general one-factor short-rate model is:

```math
dr(t)=\mu(t,r(t))dt+\sigma(t,r(t))dW(t)
```

There is one Brownian motion, so there is one source of interest-rate risk.

A derivative price depending on the short rate is written:

```math
C(t,r)
```

---

## 3. Vasicek Model

The Vasicek model is:

```math
dr=a(b-r)dt+\sigma dW
```

where:

- `b` is the long-run mean
- `a` is the speed of mean reversion
- `sigma` is the volatility

The drift is:

```math
a(b-r)
```

If `r < b`, the drift is positive and pushes rates up.

If `r > b`, the drift is negative and pushes rates down.

So the process is mean-reverting.

Main advantage:

> Vasicek is tractable and gives explicit bond-price formulas.

Main drawback:

> Rates are normally distributed, so they can become negative.

---

## 4. CIR Model

The CIR model is:

```math
dr=a(b-r)dt+\sigma\sqrt{r}dW
```

It keeps the same mean-reverting drift as Vasicek but changes the volatility term.

The square-root term helps prevent negative rates.

If `r = 0`, then:

```math
\sigma\sqrt{r}=0
```

and the drift is:

```math
ab>0
```

So the rate is pushed upward.

Main intuition:

> CIR keeps mean reversion but makes negative rates much less problematic.

---

## 5. Ho-Lee and Hull-White

The Ho-Lee model is:

```math
dr=b(t)dt+\sigma dW
```

The function `b(t)` is chosen to fit the current yield curve.

The Hull-White model adds mean reversion:

```math
dr=(b(t)-ar)dt+\sigma dW
```

So Hull-White combines:

- yield-curve fitting
- mean reversion

---

## 6. Black-Derman-Toy

A simplified Black-Derman-Toy style model is:

```math
dr=b(t)r\,dt+\sigma r\,dW
```

This makes rates lognormal-like, so rates stay positive.

However, in continuous time it can create mathematical problems because:

```math
E
\left[
e^{\int_0^T r(u)du}
\right]
```

may become infinite.

So BDT is more commonly used in discrete-time tree settings.

---

## 7. Pricing PDE

For a one-factor short-rate model:

```math
dr=\mu(t,r)dt+\sigma(t,r)dW
```

the price `C(t,r)` solves:

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

Why each term appears:

- `C_t`: time passing
- `mu C_r`: drift of the short rate
- `1/2 sigma^2 C_rr`: Ito variance term
- `-rC`: discounting at the short rate

For a zero-coupon bond:

```math
P(T,T)=1
```

---

## 8. Affine Short-Rate Models

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

Affine models are useful because they often produce explicit bond-price formulas.

Vasicek and CIR are affine models.

---

## 9. Why Vasicek and CIR Are Affine

In Vasicek:

```math
dr=a(b-r)dt+\sigma dW
```

the drift is linear in `r`, and the variance is constant.

In CIR:

```math
dr=a(b-r)dt+\sigma\sqrt{r}dW
```

the drift is linear in `r`, and the variance is:

```math
\sigma^2r
```

which is also linear in `r`.

That is why both models are tractable.

---

## 10. Calibration

Short-rate models are calibrated to observed bond prices or the yield curve.

The process is:

1. choose a model
2. choose parameters
3. compute model bond prices
4. compare with market bond prices
5. adjust parameters until the model fits the curve

Time-dependent models such as Ho-Lee and Hull-White can fit the initial yield curve more flexibly.

---

## 11. Core Formulas

### Bond price

```math
P(t,T)
=
E_t
\left[
e^{-\int_t^T r(u)du}
\right]
```

### Vasicek

```math
dr=a(b-r)dt+\sigma dW
```

### CIR

```math
dr=a(b-r)dt+\sigma\sqrt{r}dW
```

### Ho-Lee

```math
dr=b(t)dt+\sigma dW
```

### Hull-White

```math
dr=(b(t)-ar)dt+\sigma dW
```

### General PDE

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

### Affine bond price

```math
P(t,T)=e^{A(t,T)+B(t,T)r(t)}
```

---

## Final Intuition

Short-rate models make interest rates random.

Vasicek is simple and mean-reverting but can produce negative rates.

CIR adds square-root volatility to help keep rates non-negative.

Ho-Lee and Hull-White use time-dependent parameters to fit the yield curve.

Affine models are useful because bond prices can often be written in explicit form.
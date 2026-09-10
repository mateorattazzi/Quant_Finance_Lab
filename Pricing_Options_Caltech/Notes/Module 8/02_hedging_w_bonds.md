# Module 8 — Static Hedging with Bonds: Duration and Convexity

## 1. Big Picture

Bond hedging is used when future payoffs are mainly exposed to interest-rate risk.

Examples:

- pension fund liabilities
- insurance liabilities
- fixed future payments

The goal is to build a bond portfolio whose value changes offset the value changes of the liabilities when yields move.

This is called immunization.

---

## 2. Bond Price

Assume annual compounding.

A bond with cash flows `C_i` has price:

```math
P(y)=\sum_{i=1}^{T}\frac{C_i}{(1+y)^i}
```

where:

- `y` = yield
- `C_i` = cash flow at time `i`
- final cash flow includes coupon plus face value

---

## 3. Duration

Duration measures first-order sensitivity of bond price to yield.

It is based on:

```math
\frac{dP}{dy}
```

For the bond price above:

```math
\frac{dP}{dy}
=
-\sum_{i=1}^{T}
\frac{iC_i}{(1+y)^{i+1}}
```

This can be written as:

```math
\frac{dP}{dy}
=
-\frac{P}{1+y}D
```

where duration is:

```math
D=
\sum_{i=1}^{T}
i
\frac{
C_i/(1+y)^i
}{
P
}
```

---

## 4. Duration Intuition

Duration is a weighted average payment time.

The weight of cash flow `C_i` is:

```math
\frac{
C_i/(1+y)^i
}{
P
}
```

These weights add to 1.

So duration gives more weight to large present-value cash flows.

For a zero-coupon bond, there is only one cash flow at maturity, so:

```math
D=T
```

Key idea:

> Higher duration means higher sensitivity to yield changes.

---

## 5. Price Change Approximation

For a small yield change `dy`, the first-order approximation is:

```math
dP
\approx
-\frac{P}{1+y}D\,dy
```

So if yield increases, bond price decreases.

If yield decreases, bond price increases.

---

## 6. Convexity

Convexity measures second-order sensitivity of bond price to yield.

It is the normalized second derivative:

```math
\text{Convexity}
=
\frac{1}{P}\frac{d^2P}{dy^2}
```

Duration is like delta.

Convexity is like gamma.

Duration captures the linear effect of a yield change.

Convexity captures the curvature effect.

---

## 7. Taylor Approximation

For a bond or bond portfolio, the change in value can be approximated by:

```math
\Delta P
\approx
\frac{dP}{dy}\Delta y
+
\frac{1}{2}
\frac{d^2P}{dy^2}
(\Delta y)^2
```

If duration and convexity exposure are close to zero, the portfolio value should be less sensitive to small yield changes.

---

## 8. Bond Immunization

Bond immunization means choosing a bond portfolio to hedge future liabilities.

The aim is to make the combined portfolio of bonds and liabilities have:

- duration close to zero
- convexity close to zero

At least initially.

This reduces sensitivity to interest-rate changes.

---

## 9. Static Nature of the Hedge

This is a static hedge.

We compute duration and convexity today and choose a portfolio today.

If yields change tomorrow, duration and convexity also change.

So the hedge may no longer be perfect.

To make this dynamic and theoretically consistent, we would need a full stochastic model for interest rates.

---

## 10. Common Confusions

### Is duration the same as maturity?

No.

Duration is a weighted average time of cash flows.

Only for a zero-coupon bond is duration equal to maturity.

### Why does bond price fall when yield rises?

Because future cash flows are discounted at a higher rate.

### Why use convexity?

Duration only gives a first-order approximation.

Convexity improves the approximation for larger yield changes.

### Is this like option hedging?

Conceptually yes.

Duration is similar to delta.

Convexity is similar to gamma.

But bond immunization here is static, while option hedging is usually dynamic.

---

## 11. Exam Notes

You should be able to:

- write the bond price as present value of cash flows
- explain duration as first-order yield sensitivity
- explain duration as weighted average payment time
- explain why zero-coupon duration equals maturity
- explain convexity as second-order yield sensitivity
- use the Taylor approximation for bond price changes
- explain bond immunization
- explain why this hedge is static

---

## 12. Core Formulas

### Bond price

```math
P(y)=\sum_{i=1}^{T}\frac{C_i}{(1+y)^i}
```

### Price derivative

```math
\frac{dP}{dy}
=
-\sum_{i=1}^{T}
\frac{iC_i}{(1+y)^{i+1}}
```

### Duration relation

```math
\frac{dP}{dy}
=
-\frac{P}{1+y}D
```

### Duration

```math
D=
\sum_{i=1}^{T}
i
\frac{
C_i/(1+y)^i
}{
P
}
```

### Convexity

```math
\text{Convexity}
=
\frac{1}{P}\frac{d^2P}{dy^2}
```

### Taylor approximation

```math
\Delta P
\approx
\frac{dP}{dy}\Delta y
+
\frac{1}{2}
\frac{d^2P}{dy^2}
(\Delta y)^2
```

---

## Final Intuition

Bond hedging is about controlling sensitivity to interest rates.

Duration measures the first-order effect of yield changes.

Convexity measures the second-order effect.

Immunization builds a bond portfolio whose sensitivities offset the sensitivities of future liabilities.

This is useful, but it is static: it works based on today’s yield curve and today’s sensitivities.
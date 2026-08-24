# Module 8 — Static Hedging with Futures

## 1. Big Picture

A static futures hedge means choosing a futures position now and holding it until the hedge date.

The goal is to reduce uncertainty in the future value of a position.

There are two main cases:

1. Perfect hedge
2. Cross hedge

---

## 2. Perfect Hedge

A perfect hedge is possible when the futures contract matches:

- the asset being hedged
- the amount
- the maturity date

Example:

A company will receive an asset at time `T`.

It can short futures on the same asset maturing at `T`.

At maturity, futures and spot prices converge:

```math
F(T,T)=S(T)
```

The hedge locks in the futures price.

If the company receives one unit of the asset and shorts one futures contract:

```math
S(T)+F(0,T)-F(T,T)=F(0,T)
```

So the final revenue is fixed.

---

## 3. Why Use Futures for Hedging?

Futures are often used because they are:

- liquid
- standardized
- cheaper to trade than the underlying
- useful for reducing price risk

But the futures contract may not perfectly match the exposure.

That creates hedge risk.

---

## 4. Cross Hedging

A cross hedge is used when there is no futures contract on the exact asset being hedged.

Instead, we hedge using a related futures contract.

Example:

A company will receive currency `A`, but there is no futures market for currency `A`.

So it hedges using futures on correlated currency `B`.

This is imperfect because currency `A` and currency `B` do not move exactly together.

---

## 5. Hedge Error

Suppose we want to hedge exposure to asset `S`.

We use a futures contract `F`.

If we short `delta` futures contracts, the hedged position is:

```math
X=S-\delta F
```

The hedge is good if the variance of `X` is small.

So the goal is:

```math
\min_{\delta} Var(S-\delta F)
```

---

## 6. Minimum-Variance Hedge Ratio

The optimal hedge ratio is:

```math
\delta^*
=
\frac{Cov(S,F)}{Var(F)}
```

Using correlation:

```math
Cov(S,F)=\rho\sigma_S\sigma_F
```

so:

```math
\delta^*
=
\rho\frac{\sigma_S}{\sigma_F}
```

where:

- `rho` = correlation between the exposure and the futures
- `sigma_S` = volatility of the exposure
- `sigma_F` = volatility of the futures

---

## 7. Minimum Hedge Variance

The variance after hedging is:

```math
Var(S-\delta^*F)
=
Var(S)
-
\frac{Cov(S,F)^2}{Var(F)}
```

Using correlation:

```math
Var(S-\delta^*F)
=
\sigma_S^2(1-\rho^2)
```

Key intuition:

- if `rho = 1`, the hedge can eliminate all variance
- if `rho = 0`, the hedge does not reduce variance
- the closer correlation is to 1 or -1, the more effective the hedge

---

## 8. Example: Hedging Currency A with Currency B Futures

A US company will receive:

```math
1{,}000{,}000
```

units of currency `A` in six months.

There is no futures contract on currency `A`.

So the company hedges using futures on correlated currency `B`.

Current exchange rates:

```math
Q_A=0.10
```

```math
Q_B=0.20
```

So one unit of currency `B` is worth twice one unit of currency `A`.

A naive hedge would short half as many units of currency `B`.

But this ignores volatility and correlation.

---

## 9. Data for the Hedge

Historical estimates:

```math
\sigma_A=0.03
```

```math
\sigma_B=0.02
```

```math
\rho=0.9
```

Covariance:

```math
Cov(A,B)=\rho\sigma_A\sigma_B
```

```math
Cov(A,B)=0.9(0.03)(0.02)=0.00054
```

Variance of currency `B`:

```math
Var(B)=0.02^2=0.0004
```

Optimal hedge ratio:

```math
\delta^*
=
\frac{0.00054}{0.0004}
=
1.35
```

---

## 10. Interpreting the Hedge Ratio

The optimal hedge says:

```math
\delta^*=1.35
```

This means that for each unit of currency `A`, the company should hedge with an amount of currency `B` equivalent to `1.35` units of currency `A`.

The company receives:

```math
1{,}000{,}000
```

units of currency `A`.

So the hedge exposure in currency `A` units is:

```math
1{,}000{,}000 \times 1.35=1{,}350{,}000
```

Since currency `B` is worth twice currency `A`, divide by 2:

```math
\frac{1{,}350{,}000}{2}=675{,}000
```

So the company should short:

```math
675{,}000
```

units of currency `B` futures.

---

## 11. Risk Reduction

Without hedging, the variance is:

```math
\sigma_A^2=0.03^2=0.0009
```

With the optimal hedge, the variance is approximately:

```math
0.000171
```

So the hedge greatly reduces risk, but does not eliminate it.

It is not perfect because currency `A` and currency `B` are highly correlated but not identical.

---

## 12. Metallgesellschaft Example

Metallgesellschaft sold long-term forward contracts to deliver oil at fixed prices.

To hedge, it used short-term oil futures and kept rolling them forward.

This was a natural hedge, but it created a cash-flow problem.

When oil prices fell:

- the long-term delivery contracts became more favorable
- but the futures hedge produced large margin losses
- the company had to post cash to the margin account
- public and political pressure increased
- the hedge was closed at a large loss

Key lesson:

> A hedge can reduce economic risk but still create serious cash-flow and liquidity risk.

---

## 13. Static vs Rolling Hedge

A static hedge is chosen once and held.

A rolling hedge repeatedly replaces expiring futures with new futures.

Rolling hedges introduce additional risks:

- margin calls
- liquidity pressure
- basis risk
- maturity mismatch
- pressure to close the hedge early

---

## 14. Main Intuition

A futures hedge is not just about matching the size of the exposure.

It must account for:

- volatility of the exposure
- volatility of the futures contract
- correlation between them
- exchange-rate or price ratios
- liquidity and margin requirements

The minimum-variance hedge ratio gives the statistically best static hedge:

```math
\delta^*
=
\rho\frac{\sigma_S}{\sigma_F}
```

---

## 15. Exam Notes

You should be able to:

- explain the difference between perfect hedging and cross hedging
- define hedge error
- derive or use the minimum-variance hedge ratio
- compute covariance from correlation and volatilities
- interpret the optimal hedge ratio
- explain why a naive hedge can be wrong
- explain why rolling futures hedges can create liquidity risk

---

## 16. Core Formulas

### Hedge error

```math
X=S-\delta F
```

### Objective

```math
\min_{\delta} Var(S-\delta F)
```

### Optimal hedge ratio

```math
\delta^*
=
\frac{Cov(S,F)}{Var(F)}
```

### Correlation form

```math
\delta^*
=
\rho\frac{\sigma_S}{\sigma_F}
```

### Minimum variance

```math
Var(S-\delta^*F)
=
Var(S)
-
\frac{Cov(S,F)^2}{Var(F)}
```

### Covariance

```math
Cov(S,F)=\rho\sigma_S\sigma_F
```

---

## Final Intuition

Static hedging with futures tries to reduce risk by taking an opposite futures position.

If the futures contract perfectly matches the exposure, the hedge can lock in a price.

If it does not match, the best hedge is chosen by minimizing variance.

The optimal hedge depends on correlation and relative volatility, not only on current price ratios.
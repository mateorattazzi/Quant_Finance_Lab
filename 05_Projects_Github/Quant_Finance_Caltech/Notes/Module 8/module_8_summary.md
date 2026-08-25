# Module 8 — Summary: Hedging and Risk Management

## 1. Big Picture

This module studies hedging.

Hedging means building a trading position that reduces the risk of another position.

The module covers four main types of hedging:

1. futures hedging
2. bond hedging
3. dynamic delta hedging
4. Greek hedging

The key lesson is:

> Models can show how to hedge risk, but real markets introduce liquidity risk, margin calls, transaction costs, model error, and stress scenarios.

---

## 2. Static Hedging with Futures

A static futures hedge is chosen today and held until the hedge date.

If the futures contract exactly matches the asset and maturity, the hedge can lock in a future price.

At maturity, futures and spot prices converge:

```math
F(T,T)=S(T)
```

If a company receives one unit of the asset and shorts one futures contract, final revenue is:

```math
S(T)+F(0,T)-F(T,T)=F(0,T)
```

So the company locks in the initial futures price.

---

## 3. Cross Hedging

A cross hedge is used when there is no futures contract on the exact asset being hedged.

Instead, we hedge using a related asset.

Example:

A company will receive currency `A`, but there are no futures on currency `A`.

So it hedges using futures on correlated currency `B`.

The hedge is imperfect because the two currencies do not move exactly together.

---

## 4. Minimum-Variance Hedge Ratio

The hedge error is:

```math
X=S-\delta F
```

The goal is to choose `delta` to minimize:

```math
Var(S-\delta F)
```

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

The minimum variance is:

```math
Var(S-\delta^*F)
=
Var(S)
-
\frac{Cov(S,F)^2}{Var(F)}
```

Key intuition:

- high correlation makes the hedge more effective
- different volatilities change the optimal hedge size
- price ratios alone are not enough

---

## 5. Currency Hedge Example

A company will receive:

```math
1{,}000{,}000
```

units of currency `A`.

Current exchange rates:

```math
Q_A=0.10
```

```math
Q_B=0.20
```

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

So the company should hedge with currency `B` exposure equivalent to `1.35` units of currency `A` per unit of currency `A`.

Since currency `B` is worth twice currency `A`:

```math
\frac{1{,}000{,}000 \times 1.35}{2}
=
675{,}000
```

The company should short:

```math
675{,}000
```

units of currency `B` futures.

---

## 6. Bond Hedging

Bond hedging is used to hedge interest-rate risk.

Examples:

- pension liabilities
- insurance liabilities
- fixed future payments

The basic bond price is:

```math
P(y)=\sum_{i=1}^{T}\frac{C_i}{(1+y)^i}
```

where:

- `y` = yield
- `C_i` = cash flow at time `i`

---

## 7. Duration

Duration measures first-order sensitivity to yield.

The derivative of bond price is:

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

Duration is a weighted average time of cash flows.

For a zero-coupon bond:

```math
D=T
```

Key intuition:

> Higher duration means greater price sensitivity to yield changes.

---

## 8. Convexity

Convexity measures second-order sensitivity to yield.

```math
\text{Convexity}
=
\frac{1}{P}\frac{d^2P}{dy^2}
```

Duration is similar to delta.

Convexity is similar to gamma.

For a yield change, the Taylor approximation is:

```math
\Delta P
\approx
\frac{dP}{dy}\Delta y
+
\frac{1}{2}
\frac{d^2P}{dy^2}
(\Delta y)^2
```

Duration captures the linear effect.

Convexity captures the curvature effect.

---

## 9. Bond Immunization

Bond immunization means choosing a bond portfolio whose sensitivities offset the sensitivities of liabilities.

The goal is to make the combined position less sensitive to interest-rate changes.

Ideally, the portfolio has:

- duration close to zero
- convexity close to zero

But this is static.

If yields change, duration and convexity also change.

So the hedge may need to be updated.

---

## 10. Dynamic Delta Hedging

In complete models, derivatives can be replicated perfectly in theory.

Examples:

- binomial tree model
- Black-Scholes model

In a one-period binomial model, the stock can move to:

```math
S_u
```

or:

```math
S_d
```

The option payoffs are:

```math
C_u
```

and:

```math
C_d
```

The replicating portfolio satisfies:

```math
B+\Delta S_u=C_u
```

```math
B+\Delta S_d=C_d
```

Subtracting gives:

```math
\Delta=
\frac{C_u-C_d}{S_u-S_d}
```

This is the binomial hedge ratio.

---

## 11. Connection to Black-Scholes Delta

The binomial hedge ratio is:

```math
\Delta=
\frac{\Delta C}{\Delta S}
```

As the time step becomes very small, this becomes:

```math
\Delta=C_S
```

For a European call option in Black-Scholes:

```math
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
```

The call delta is:

```math
\Delta=N(d_1)
```

where:

```math
d_1=
\frac{
\ln(S/K)+(r+\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
```

---

## 12. Practical Delta Hedging

If you sell a call option, you hedge by buying shares.

At each rebalancing date:

1. compute the new delta
2. hold `Delta` shares
3. put the remaining amount in the bank account
4. update the hedge as the stock price changes

Ignoring interest and transaction costs, hedging wealth updates as:

```math
X_{i+1}=X_i+\Delta_i(S_{i+1}-S_i)
```

Black-Scholes perfect replication requires continuous rebalancing.

Real hedging is discrete, so there is usually hedging error.

---

## 13. Gamma Hedging

Delta measures first-order sensitivity.

Gamma measures second-order sensitivity:

```math
\Gamma=\frac{\partial^2 V}{\partial S^2}
```

Gamma measures how delta changes when the underlying changes.

If a portfolio has original gamma:

```math
\Gamma_0
```

and we trade `n` units of another option with gamma:

```math
\Gamma_C
```

then total gamma becomes:

```math
\Gamma_{\text{new}}=\Gamma_0+n\Gamma_C
```

To make gamma zero:

```math
n=-\frac{\Gamma_0}{\Gamma_C}
```

---

## 14. Fixing Delta After Gamma Hedging

Gamma hedging usually changes delta.

After making gamma neutral, delta can be fixed by trading the underlying asset.

This works because the underlying stock has:

```math
\Delta_S=1
```

and:

```math
\Gamma_S=0
```

The stock has zero gamma because its value is linear in itself.

So trading the stock changes delta without changing gamma.

---

## 15. Gamma Hedging Example

Suppose the original portfolio has:

```math
\Delta_0=0
```

```math
\Gamma_0=-5000
```

There is an option with:

```math
\Delta_C=0.4
```

```math
\Gamma_C=2
```

The gamma-neutral position is:

```math
n=-\frac{-5000}{2}=2500
```

Buy `2500` options.

This changes delta by:

```math
2500 \times 0.4=1000
```

To restore delta neutrality, sell:

```math
1000
```

shares of the underlying.

---

## 16. Vega Hedging

Vega measures sensitivity to volatility:

```math
\text{Vega}=\frac{\partial V}{\partial \sigma}
```

To hedge both gamma and vega, we need two options.

Let the original portfolio have:

```math
\Gamma_0
```

and:

```math
\text{Vega}_0
```

Trade `n_1` units of option 1 and `n_2` units of option 2.

Set:

```math
\Gamma_0+n_1\Gamma_1+n_2\Gamma_2=0
```

```math
\text{Vega}_0+n_1\text{Vega}_1+n_2\text{Vega}_2=0
```

Solve this system for `n_1` and `n_2`.

Then fix delta by trading the underlying stock.

---

## 17. Portfolio Insurance

Portfolio insurance tries to protect a portfolio from large losses.

A simple version is equivalent to owning the portfolio and buying a put option.

If a real put is not available, the investor can create a synthetic put by dynamically trading the underlying assets.

This relies on the idea that, in a complete model, a put payoff can be replicated.

---

## 18. Why Portfolio Insurance Can Fail

Portfolio insurance often requires selling assets when prices fall.

During a market crash, this can create a feedback loop:

1. prices fall
2. the model says to sell more
3. selling pressure pushes prices lower
4. more selling is required
5. prices fall further

This shows that a hedge can work in a model but fail in a stressed market.

---

## 19. LTCM Lesson

Long-Term Capital Management used highly leveraged relative-value trades.

Many trades were based on the idea that spreads would converge.

When markets moved against the fund, spreads widened instead.

Because LTCM was highly leveraged, losses created margin pressure.

The fund had to sell assets, and many other firms held similar trades.

This created another feedback loop:

1. losses increased
2. margin calls arrived
3. assets had to be sold
4. prices moved further against the positions
5. losses increased again

The lesson is that leverage and liquidity risk can make a model-based strategy fail.

---

## 20. Main Lessons

Hedging is powerful, but it is not risk-free.

The main practical risks are:

- model error
- incorrect parameters
- discrete rebalancing
- transaction costs
- liquidity risk
- margin calls
- leverage
- crowded trades
- market jumps
- stress scenarios

A hedge can reduce one risk while creating another.

---

## 21. Exam Checklist

You should be able to:

- explain perfect hedging with futures
- explain cross hedging
- compute the minimum-variance hedge ratio
- interpret correlation and volatility in hedge sizing
- define duration and convexity
- explain bond immunization
- derive the binomial hedge ratio
- connect binomial delta to Black-Scholes delta
- state that call delta is `N(d_1)`
- explain why discrete delta hedging is imperfect
- compute a gamma hedge
- explain how to hedge gamma and vega together
- explain portfolio insurance
- explain why hedging can fail in crises

---

## 22. Core Formulas

### Futures hedge error

```math
X=S-\delta F
```

### Optimal futures hedge ratio

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

### Bond price

```math
P(y)=\sum_{i=1}^{T}\frac{C_i}{(1+y)^i}
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

### Duration relation

```math
\frac{dP}{dy}
=
-\frac{P}{1+y}D
```

### Convexity

```math
\text{Convexity}
=
\frac{1}{P}\frac{d^2P}{dy^2}
```

### Binomial delta

```math
\Delta=
\frac{C_u-C_d}{S_u-S_d}
```

### Black-Scholes call delta

```math
\Delta=N(d_1)
```

### Hedging wealth update

```math
X_{i+1}=X_i+\Delta_i(S_{i+1}-S_i)
```

### Gamma

```math
\Gamma=\frac{\partial^2 V}{\partial S^2}
```

### Gamma-neutral position

```math
n=-\frac{\Gamma_0}{\Gamma_C}
```

### Vega

```math
\text{Vega}=\frac{\partial V}{\partial \sigma}
```

---

## Final Intuition

Module 8 shows that hedging is the practical side of derivative pricing.

Futures hedges reduce price risk.

Bond hedges reduce interest-rate risk.

Delta hedging replicates options in complete models.

Greek hedging controls higher-order sensitivities.

But real markets are not perfect.

The most important lesson is that hedging decisions must consider not only mathematical risk, but also liquidity, leverage, margin calls, transaction costs, and market stress.
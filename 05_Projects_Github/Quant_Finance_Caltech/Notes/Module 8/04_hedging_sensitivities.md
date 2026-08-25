# Module 8 — Greek Hedging and Risk Management Failures

## 1. Big Picture

Dynamic hedging is not only about delta.

A portfolio can also have exposure to:

- gamma
- vega
- other Greeks

Traders often try to control these sensitivities by trading options and the underlying asset.

But real-world hedging can fail when model assumptions break down.

This section covers:

1. gamma and vega hedging
2. portfolio insurance
3. Long-Term Capital Management

---

## 2. Gamma

Gamma measures the second-order sensitivity of a portfolio to the underlying asset.

Delta measures the first-order sensitivity.

Gamma measures how delta changes when the underlying changes.

```math
\Gamma=\frac{\partial^2 V}{\partial S^2}
```

High gamma means the portfolio is very sensitive to large moves in the underlying.

Highly negative gamma can be dangerous because losses can accelerate when the market moves strongly.

---

## 3. Gamma Is Additive

If a portfolio has original gamma:

```math
\Gamma_0
```

and we trade `n` units of another option with gamma:

```math
\Gamma_C
```

then the new total gamma is:

```math
\Gamma_{\text{new}}=\Gamma_0+n\Gamma_C
```

To make the portfolio gamma neutral, set:

```math
\Gamma_{\text{new}}=0
```

So:

```math
\Gamma_0+n\Gamma_C=0
```

Solving for `n`:

```math
n=-\frac{\Gamma_0}{\Gamma_C}
```

If `n` is positive, buy the option.

If `n` is negative, sell the option.

---

## 4. Fixing Delta After Gamma Hedging

Gamma hedging usually changes delta.

If the option used for gamma hedging has delta:

```math
\Delta_C
```

then buying `n` units changes delta by:

```math
n\Delta_C
```

After making gamma neutral, we can fix delta by trading the underlying asset.

This works because the underlying asset has:

```math
\Delta_S=1
```

and:

```math
\Gamma_S=0
```

The stock has zero gamma because it is linear in itself.

So trading the stock changes delta but does not change gamma.

---

## 5. Numerical Example: Gamma Hedging

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

The number of options needed to make gamma zero is:

```math
n=-\frac{-5000}{2}=2500
```

So we buy:

```math
2500
```

option contracts.

The new gamma is zero.

But the new delta is:

```math
2500 \times 0.4=1000
```

To make delta zero again, sell:

```math
1000
```

shares of the underlying asset.

After this:

- gamma is zero
- delta is zero

---

## 6. Hedging Both Gamma and Vega

Vega measures sensitivity to volatility.

```math
\text{Vega}=\frac{\partial V}{\partial \sigma}
```

If we want to hedge both gamma and vega, one option is not enough.

We need two different options.

Let the original portfolio have:

```math
\Gamma_0
```

and:

```math
\text{Vega}_0
```

Trade:

- `n_1` units of option 1
- `n_2` units of option 2

To make gamma zero:

```math
\Gamma_0+n_1\Gamma_1+n_2\Gamma_2=0
```

To make vega zero:

```math
\text{Vega}_0+n_1\text{Vega}_1+n_2\text{Vega}_2=0
```

This gives a system of two equations with two unknowns.

Solve for:

```math
n_1
```

and:

```math
n_2
```

After that, delta may no longer be zero.

So we fix delta by trading the underlying stock.

---

## 7. General Greek Hedging Logic

The general procedure is:

1. identify the portfolio sensitivities
2. choose instruments with the needed Greek exposures
3. solve for the number of units to trade
4. use the underlying asset to fix delta
5. rebalance when sensitivities change

The underlying asset is useful for delta hedging because it changes delta without changing gamma or vega.

---

## 8. Portfolio Insurance

Portfolio insurance was popular in the 1980s.

The idea was to protect a portfolio against large losses.

Suppose an institution owns a large portfolio and wants to guarantee that it does not lose more than 5% over one year.

If a put option existed on that portfolio, the institution could buy a put with strike equal to 95% of today’s portfolio value.

This would guarantee a minimum portfolio value.

---

## 9. Synthetic Put

Often there is no traded put option on a complex portfolio.

But in a complete market, like Black-Scholes or binomial models, any payoff can theoretically be replicated.

So instead of buying a real put, the institution can create a synthetic put by dynamically trading the underlying assets.

This is portfolio insurance.

The goal is to replicate the payoff of a protective put.

---

## 10. Why Portfolio Insurance Can Fail

To replicate a put option, the strategy usually sells assets as prices fall.

During normal markets, this may work reasonably well.

But during a market crash, many investors may try to sell at the same time.

Portfolio insurance can then create a feedback loop:

1. prices fall
2. the model says to sell more
3. selling pressure pushes prices lower
4. the strategy sells even more
5. prices fall further

This can amplify market declines.

---

## 11. 1987 Crash Lesson

During the October 1987 crash, portfolio insurance performed badly.

Some argue that it contributed to the crash because many institutions were following similar selling rules.

The key lesson is:

> A hedging strategy that works in a complete and liquid model may fail during a crisis.

During crashes:

- prices may jump
- liquidity may disappear
- many investors may trade in the same direction
- normal distribution assumptions fail
- markets become incomplete

In a jump or crash environment, perfect replication is no longer realistic.

---

## 12. Long-Term Capital Management

Long-Term Capital Management, or LTCM, was a very successful hedge fund in the 1990s.

Two of its partners were Robert Merton and Myron Scholes.

The fund searched for small relative pricing opportunities.

The trades were not necessarily complex option trades.

Many were based on spread convergence.

---

## 13. LTCM Strategy

LTCM often bet that spreads would narrow.

For example:

- corporate bonds had much higher yields than Treasury bonds
- European country interest rates were expected to converge before the euro

LTCM expected these spreads to move closer together.

The profit on each trade was small.

So the fund used very high leverage.

That means it borrowed heavily to make large positions.

---

## 14. What Went Wrong

The Russian crisis caused a flight to safety.

Investors rushed into safe assets such as US Treasury bonds.

As a result:

- Treasury prices rose
- Treasury yields fell
- spreads widened instead of narrowing

This hurt LTCM’s positions.

European interest-rate spreads also widened instead of converging.

The problem was not only that LTCM was wrong temporarily.

The bigger problem was that LTCM was highly leveraged.

---

## 15. Leverage and Margin Pressure

Because LTCM borrowed heavily, losses created pressure from lenders.

The fund had to meet margin calls.

To raise cash, it had to sell assets.

But many other firms held similar trades.

So they also sold.

This created another feedback loop:

1. LTCM loses money
2. lenders demand margin
3. LTCM sells assets
4. similar assets fall further
5. losses increase
6. more margin calls arrive

The fund almost collapsed.

Eventually, major banks organized a rescue package to avoid broader market disruption.

---

## 16. Common Lesson from Both Stories

Portfolio insurance and LTCM are different stories, but they share the same lesson.

Models can underestimate what happens in stress periods.

The main dangers are:

- leverage
- liquidity risk
- margin calls
- model error
- crowded trades
- market incompleteness
- feedback loops

A hedge can reduce risk in a model but create new risks in reality.

---

## 17. Exam Notes

You should be able to:

- define gamma as second-order sensitivity
- explain why gamma is additive
- compute the number of options needed for gamma hedging
- explain why delta can be fixed with the underlying
- explain why the stock has zero gamma
- set up equations for gamma and vega hedging
- explain portfolio insurance as a synthetic put
- explain why portfolio insurance can fail during crashes
- explain the LTCM spread-convergence strategy
- explain how leverage and margin calls amplified LTCM’s losses

---

## 18. Core Formulas

### Gamma

```math
\Gamma=\frac{\partial^2 V}{\partial S^2}
```

### Total gamma after trading another option

```math
\Gamma_{\text{new}}=\Gamma_0+n\Gamma_C
```

### Gamma-neutral position

```math
n=-\frac{\Gamma_0}{\Gamma_C}
```

### Vega

```math
\text{Vega}=\frac{\partial V}{\partial \sigma}
```

### Gamma and vega hedging system

```math
\Gamma_0+n_1\Gamma_1+n_2\Gamma_2=0
```

```math
\text{Vega}_0+n_1\text{Vega}_1+n_2\text{Vega}_2=0
```

### Delta adjustment

```math
\Delta_{\text{new}}
=
\Delta_0+n\Delta_C+\text{shares held}
```

---

## Final Intuition

Greek hedging tries to control the sensitivities of a portfolio.

Gamma and vega can be hedged by trading options.

Delta can then be adjusted by trading the underlying asset.

But hedging depends on model assumptions.

In real markets, crashes, liquidity problems, leverage, and crowded trades can make theoretically sound hedges fail.
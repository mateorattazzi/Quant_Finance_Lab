# Module 8 — Dynamic Delta Hedging in Black-Scholes

## 1. Big Picture

In complete models, every derivative payoff can be replicated by trading in the stock and the bank account.

Two key examples are:

- binomial tree model
- Black-Scholes model

Because these models are complete, they allow perfect hedging in theory.

In practice, the hedge is not perfect because:

- trading is discrete, not continuous
- volatility is estimated, not known
- transaction costs exist
- the model may not be exactly correct

---

## 2. Replication in a One-Period Binomial Model

Suppose the stock can move to only two possible values:

```math
S_u
```

or

```math
S_d
```

A derivative has two possible payoffs:

```math
C_u
```

and

```math
C_d
```

To replicate the derivative, hold:

- `Delta` shares of stock
- some amount in the bank account

The value of the portfolio must match the derivative payoff in both states.

So we solve:

```math
B+\Delta S_u=C_u
```

```math
B+\Delta S_d=C_d
```

Subtracting the second equation from the first gives:

```math
\Delta=
\frac{C_u-C_d}{S_u-S_d}
```

This is the binomial hedge ratio.

---

## 3. Intuition for Delta

Delta measures how much the option price changes when the stock price changes.

In the binomial model:

```math
\Delta=
\frac{\Delta C}{\Delta S}
```

In the Black-Scholes model, as the time step becomes very small, this becomes the derivative:

```math
\Delta=C_S
```

So Black-Scholes delta is the continuous-time version of the binomial hedge ratio.

---

## 4. Black-Scholes Delta

For a European call option, the Black-Scholes price is:

```math
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
```

The delta of the call is:

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

Although `d_1` and `d_2` depend on `S`, the extra derivative terms cancel out.

That is why the final call delta is simply:

```math
N(d_1)
```

---

## 5. Dynamic Hedging Procedure

Suppose you sell a call option.

You receive the option premium and use it to start the hedging portfolio.

At each date:

1. compute the option delta
2. hold `Delta` shares of stock
3. put the remaining amount in the bank account
4. next day, recompute delta
5. rebalance the portfolio

The theoretical Black-Scholes hedge requires continuous rebalancing.

In practice, the example rebalances once per day.

---

## 6. Initial Hedge

At time `0`, compute:

```math
\Delta_0=N(d_1)
```

Then buy:

```math
\Delta_0
```

shares of stock.

The stock investment is:

```math
\Delta_0 S_0
```

If the option premium is:

```math
C_0
```

then the amount borrowed is:

```math
\Delta_0 S_0-C_0
```

For a call option, delta is positive, so selling a call is hedged by buying shares.

---

## 7. Rebalancing

At the next date, the stock price changes.

The option delta also changes.

So we compute a new delta:

```math
\Delta_1=N(d_1)
```

using:

- the new stock price
- the new time to maturity
- the same estimated volatility
- the interest rate

If the stock price falls, call delta usually falls.

Then we sell some shares.

If the stock price rises, call delta usually rises.

Then we buy more shares.

---

## 8. Wealth Update

Ignoring interest rates and transaction costs, the hedging wealth updates as:

```math
X_{i+1}=X_i+\Delta_i(S_{i+1}-S_i)
```

where:

- `X_i` = value of the hedging portfolio at date `i`
- `Delta_i` = shares held during the period
- `S_{i+1}-S_i` = stock price change

This formula says:

> the hedge gains or loses money according to the shares held times the stock price change.

---

## 9. Example Interpretation

In the example, the stock starts near:

```math
55.5
```

and ends at:

```math
68.81
```

The call strike is:

```math
55
```

So the option finishes in the money.

The payoff is approximately:

```math
68.81-55=13.81
```

If the seller did not hedge, the option loss would be large.

With delta hedging, the hedging portfolio grows as the stock rises.

The portfolio ends near:

```math
13.66
```

The option payoff is approximately:

```math
13.81
```

So the hedging error is only about:

```math
0.15
```

The hedge is not perfect, but it greatly reduces the loss.

---

## 10. Why the Hedge Is Not Perfect

Black-Scholes perfect replication assumes:

- continuous trading
- no transaction costs
- known constant volatility
- frictionless markets
- exact model dynamics

In the real example, the hedge is rebalanced only once per day.

So the result is close, but not exactly perfect.

---

## 11. Hedging as Insurance

A hedge is like insurance.

If the stock price rises a lot, the call seller loses on the option, but gains on the hedge.

If the stock price falls and the option expires out of the money, the hedge may lose money.

That does not mean the hedge was wrong.

The hedge protects against the risky scenario.

---

## 12. Practical View

Option traders do not always hedge every option perfectly.

Instead, they manage the sensitivities of their total portfolio.

The main sensitivity here is delta.

Delta hedging tries to keep the portfolio less exposed to movements in the underlying stock.

This is similar in spirit to:

- futures hedging
- bond duration hedging
- convexity hedging

But in Black-Scholes, the model gives a theoretically exact dynamic replication strategy.

---

## 13. Main Intuition

Binomial hedging solves for the number of shares that makes the portfolio match the option payoff in both states.

Black-Scholes delta hedging is the continuous-time limit of the same idea.

The hedge ratio becomes:

```math
\Delta=C_S
```

For a call option:

```math
\Delta=N(d_1)
```

By repeatedly updating delta, the option seller builds a portfolio that offsets most of the option payoff risk.

---

## 14. Exam Notes

You should be able to:

- explain why binomial and Black-Scholes models are complete
- solve for the binomial hedge ratio
- explain why delta is `Delta C / Delta S`
- connect binomial delta to Black-Scholes delta
- state that call delta is `N(d_1)`
- describe the daily rebalancing procedure
- compute the wealth update of a hedging portfolio
- explain why real hedging is not perfect
- explain why hedging is similar to insurance

---

## 15. Core Formulas

### Binomial replication equations

```math
B+\Delta S_u=C_u
```

```math
B+\Delta S_d=C_d
```

### Binomial delta

```math
\Delta=
\frac{C_u-C_d}{S_u-S_d}
```

### Black-Scholes call price

```math
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
```

### Black-Scholes call delta

```math
\Delta=N(d_1)
```

### `d_1`

```math
d_1=
\frac{
\ln(S/K)+(r+\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
```

### Wealth update

```math
X_{i+1}=X_i+\Delta_i(S_{i+1}-S_i)
```

### Option payoff

```math
(S(T)-K)^+
```

---

## Final Intuition

Dynamic delta hedging means continuously adjusting the stock position so that the portfolio tracks the option value.

In theory, Black-Scholes gives perfect replication.

In practice, discrete rebalancing creates a small hedging error.

The goal is not always to eliminate all risk, but to control the portfolio’s exposure to movements in the underlying stock.
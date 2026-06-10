# Discrete-Time Models and Binomial Trees

## Key Idea

Until now, we used no-arbitrage arguments without specifying how the underlying asset moves.

However, to price options exactly, we need a mathematical model for the evolution of the underlying asset.

Module 4 begins with discrete-time models.

These models are simpler than continuous-time models and help build intuition before Black-Scholes.

---

# 1. Why We Need Mathematical Models

Forwards, futures and swaps are linear derivatives.

They can often be priced using:

- replication
- no-arbitrage
- current prices
- interest rates

Options are different because their payoffs are non-linear.

To obtain exact option prices, we need a model for the possible future values of the underlying asset.

---

# 2. Single-Period Model

## Definition

A single-period model has only two dates:

- time 0
- time 1

At time 0, prices are known.

At time 1, risky asset prices can take different possible values.

## Assets in the Model

The model includes:

- a risk-free bank account
- one or more risky assets

## Bank Account

The bank account is normalized as:

B(0) = 1

At time 1:

B(1) = 1 + r

where:

r = risk-free interest rate for the period

The bank account is deterministic.

---

# 3. Portfolio Strategy

A portfolio strategy specifies how many units of each asset the investor holds.

Notation:

- delta_0 = amount invested in the bank account
- delta_i = number of shares held in risky asset i

The symbol delta is standard in option theory.

It represents the position in the asset.

---

# 4. Wealth Process

The wealth process represents the total value of the portfolio.

At time 0:

X(0) = initial wealth

At time 1, wealth equals the value of all holdings:

X(1) = value of bank position + value of risky asset positions

## Intuition

Wealth is not a separate asset.

It is the total value of the portfolio created from the assets.

---

# 5. Budget Constraint

## Definition

The budget constraint says that initial wealth must be fully allocated across available assets.

In a single-period model:

initial wealth = money in bank + money in risky assets

## Intuition

You cannot invest more than you have unless borrowing is explicitly part of the strategy.

The portfolio must be constructed from the initial wealth.

---

# 6. Self-Financing Condition

## Definition

A strategy is self-financing if no external money enters or leaves the portfolio after the initial investment.

Changes in portfolio composition must be funded internally.

## Intuition

If you buy more of one asset, you must finance it by selling another asset or using cash already inside the portfolio.

No new money is added.

No money is withdrawn.

## Why This Matters

Self-financing strategies are central to derivative pricing.

Replication only works if the replicating portfolio does not require extra external cash later.

---

# 7. Gains and Losses

The gain of a portfolio is the change in wealth over time.

In a single-period model:

Gain = X(1) - X(0)

The total gain can be decomposed into:

- gain from the bank account
- gain from each risky asset

For each risky asset:

gain = number of shares × change in asset price

## Core Idea

Portfolio gains come from holding assets while their prices change.

---

# 8. Discounting

Discounting means dividing by the bank account.

For any process Y(t), the discounted value is:

Y_bar(t) = Y(t) / B(t)

## Intuition

Discounting expresses values in units of the risk-free asset.

This allows us to compare values across time after removing the effect of risk-free growth.

## Why It Matters

Discounted wealth and discounted gains will become very important later.

In more advanced models, martingales and risk-neutral pricing are usually expressed in discounted terms.

---

# 9. Multi-Period Model

## Definition

A multi-period model extends the single-period model to several dates:

0, 1, 2, ..., T

At each time step, the risky asset may move to different possible future values.

## Portfolio Rebalancing

In a multi-period model, the investor can adjust the portfolio over time.

The number of shares held during period t-1 to t is chosen at the start of that period.

## Self-Financing in Multi-Period Models

At each rebalancing date:

wealth before rebalancing = wealth after rebalancing

This means portfolio changes are financed internally.

---

# 10. Discrete Gains Process

In a multi-period model, total gains are the sum of gains over each period.

Conceptually:

Total gain = sum of period-by-period gains

Each period gain is:

number of shares held during the period × price change during the period

## Link to Continuous Time

This discrete sum prepares the intuition for continuous-time models.

Later, sums of gains will become stochastic integrals.

The discrete idea is:

add up small gains over time

The continuous-time idea is:

integrate infinitesimal gains over time

---

# 11. Binomial Tree Model

## Definition

The binomial tree model is the simplest useful model for a risky asset.

At each time step, the stock can move to only two possible values:

- up
- down

This creates a tree of possible future prices.

## Stock Dynamics

If the current stock price is S, then next period:

Up move:

S goes to Su

Down move:

S goes to Sd

where:

- u = up factor
- d = down factor

Usually:

u > d

## Probabilities

The real-world probability of an up move is often denoted by p.

The probability of a down move is:

1 - p

Important:

The real-world probability p is not necessarily the probability used later for pricing.

This distinction will become important when risk-neutral probabilities are introduced.

---

# 12. No-Arbitrage Condition in the Binomial Model

The model assumes:

d < 1 + r < u

## Meaning

The risk-free return must lie between the down return and the up return of the stock.

## Intuition

If the stock always did better than the bank account, one could borrow money and buy the stock to create arbitrage.

If the bank account always did better than the stock, one could short the stock and invest in the bank to create arbitrage.

So the bank must be better than the stock in the down state, but worse than the stock in the up state.

---

# 13. Recombining Tree

A binomial tree is usually recombining.

This means:

up then down = down then up

Mathematically:

S × u × d = S × d × u

So both paths reach the same final stock price.

## Why This Matters

A recombining tree is computationally efficient.

The number of final nodes grows linearly, not exponentially.

This makes binomial models practical for option pricing.

---

# 14. Cox-Ross-Rubinstein Model

The standard binomial tree is also called the Cox-Ross-Rubinstein model.

It is often abbreviated as:

CRR model

## Importance

The CRR model is one of the most important discrete-time models in option pricing.

It is useful because:

- it is mathematically simple
- it gives intuition for replication
- it can price American options numerically
- as time steps become smaller, it connects to Black-Scholes

---

# 15. Common Confusions

## Real Probability vs Pricing Probability

The probability p describes the real-world chance of an up move.

Later, option pricing will use risk-neutral probabilities.

They are not necessarily the same.

## Wealth vs Gain

Wealth is the total value of the portfolio.

Gain is the change in wealth.

## Budget Constraint vs Self-Financing

Budget constraint:

- initial wealth must be allocated across assets

Self-financing:

- after the initial investment, no external cash is added or removed

## Bank Account vs Stock

The bank account is risk-free and deterministic.

The stock is risky because its future value is uncertain.

## Binomial Tree vs Real Market

The binomial tree is not meant to perfectly describe reality.

It is a simplified mathematical model used to price derivatives.

---

# 16. Exam Notes

You should be able to:

- explain why options require mathematical models
- define a single-period model
- define a multi-period model
- describe a portfolio strategy using delta positions
- explain the wealth process
- explain the budget constraint
- explain the self-financing condition
- define gains and losses
- understand discounting by the bank account
- describe the binomial tree model
- explain the no-arbitrage condition d < 1 + r < u
- explain why the binomial tree recombines
- understand why the CRR model is useful for option pricing

---

# 17. Core Formulas

## Bank Account

B(0) = 1

B(1) = 1 + r

## Discounted Value

Y_bar(t) = Y(t) / B(t)

## Stock Movement in Binomial Model

Up state:

S_up = Su

Down state:

S_down = Sd

## No-Arbitrage Condition

d < 1 + r < u

## Portfolio Gain

Gain = sum of shares × asset price changes

---

# Final Intuition

Module 4 starts the transition from no-arbitrage relations to mathematical option pricing models.

The binomial model is the simplest useful model because it introduces uncertainty while remaining mathematically manageable.

The key idea is that option pricing will come from building self-financing portfolios that replicate option payoffs.
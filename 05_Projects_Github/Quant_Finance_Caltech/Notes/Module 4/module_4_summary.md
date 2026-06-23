# Module 4 Summary — Discrete-Time Models and Risk-Neutral Pricing

## 1. Purpose of Module 4

Module 4 introduces the first mathematical models for option pricing.

Until now, many pricing relations were obtained using no-arbitrage without specifying a model for the stock price.

However, to price options exactly, we need a model for how the underlying asset can evolve.

The module introduces:

* discrete-time models
* single-period and multi-period models
* self-financing portfolios
* binomial trees
* risk-neutral probabilities
* equivalent martingale measures
* fundamental theorems of asset pricing
* European and American option pricing by backward induction

---

# 2. Single-Period Model

## Key Idea

A single-period model has only two dates:

* time 0
* time 1

At time 0, prices are known.

At time 1, the risky asset can take different possible values.

## Bank Account

The risk-free asset is the bank account.

It is usually normalized as:

B(0) = 1

At time 1:

B(1) = 1 + r

where:

r = risk-free interest rate for the period

## Portfolio Strategy

A portfolio strategy specifies how many units of each asset the investor holds.

Notation:

* delta_0 = position in the bank account
* delta_i = number of shares in risky asset i

## Wealth

Initial wealth:

X(0) = x

End-of-period wealth:

X(1) = delta_0 B(1) + delta_1 S_1(1) + ... + delta_N S_N(1)

## Budget Constraint

The initial wealth must be allocated across the available assets:

X(0) = delta_0 B(0) + delta_1 S_1(0) + ... + delta_N S_N(0)

## Self-Financing Condition

A strategy is self-financing if no external cash enters or leaves the portfolio after the initial investment.

All changes in the portfolio must be financed internally.

---

# 3. Gains and Discounting

## Gains Process

The gain of a portfolio is the change in wealth:

G(1) = X(1) - X(0)

The gain can be written as the sum of gains from each asset.

For a risky asset:

gain = number of shares × change in price

## Change in Price

Delta S_i(1) = S_i(1) - S_i(0)

## Wealth Decomposition

The wealth at time 1 can be written as:

X(1) = X(0) + G(1)

## Discounted Process

For any process Y(t), its discounted version is:

Y_bar(t) = Y(t) / B(t)

Discounting means expressing values in units of the risk-free asset.

## Discounted Wealth

The discounted wealth satisfies:

X_bar(1) = X(0) + G_bar(1)

This discounted representation becomes important for martingale pricing.

---

# 4. Multi-Period Model

## Key Idea

A multi-period model extends the single-period model to several dates:

0, 1, 2, ..., T

The investor can rebalance the portfolio over time.

## Bank Account

The bank account evolves as:

B(0) = 1

B(t) = [1 + r(t)] B(t - 1)

## Portfolio Positions

The number of shares held during the period from t - 1 to t is denoted:

delta_i(t)

This means the position is chosen at the beginning of the period and held during that period.

## Wealth Process

At time t:

X(t) = delta_0(t) B(t) + delta_1(t) S_1(t) + ... + delta_N(t) S_N(t)

## Multi-Period Self-Financing

At each rebalancing time, wealth before rebalancing must equal wealth after rebalancing.

This means:

The portfolio can change composition, but no external money is added or removed.

## Total Gains

Total gains up to time t are the sum of period-by-period gains.

Conceptually:

X(t) = X(0) + G(t)

and in discounted terms:

X_bar(t) = X(0) + G_bar(t)

---

# 5. Binomial Tree Model

## Key Idea

The binomial tree is the simplest useful model for option pricing.

At each time step, the stock can move to only two possible values:

* up
* down

## Stock Dynamics

If the stock price is S(t), then next period:

Up move:

S(t + 1) = u S(t)

Down move:

S(t + 1) = d S(t)

where:

* u = up factor
* d = down factor

## Real-World Probabilities

The model may assign real-world probabilities:

p = probability of up move

1 - p = probability of down move

However, these probabilities are not used directly for pricing options.

## No-Arbitrage Condition

The no-arbitrage condition is:

d < 1 + r < u

or, with continuous compounding:

d < e^(r Delta t) < u

## Intuition

The risk-free return must lie between the down return and the up return of the stock.

If the stock always outperformed the bank account, arbitrage would exist.

If the bank account always outperformed the stock, arbitrage would also exist.

---

# 6. Risk-Neutral Pricing

## Key Idea

Risk-neutral pricing says that derivative prices can be computed as discounted expected payoffs under artificial probabilities.

These probabilities are called:

* risk-neutral probabilities
* martingale probabilities
* pricing probabilities

They are usually denoted by:

Q

or, in binomial models:

q

## Important

Risk-neutral probabilities are not necessarily real-world probabilities.

They are used for pricing, not for forecasting.

---

# 7. Martingale Property

## Definition

A process M(t) is a martingale if:

M(t) = E_t[M(T)]

This means that the best estimate today of the future value is the current value.

## Discounted Stock Martingale

Under the risk-neutral probability Q, the discounted stock price is a martingale.

This means:

S(t) / B(t) = E_Q,t[S(T) / B(T)]

With continuous discounting:

e^(-rt) S(t) = E_Q,t[e^(-rT) S(T)]

## Intuition

Under Q, the discounted stock behaves like a fair game.

---

# 8. Risk-Neutral Pricing Formula

If a claim pays C(T) at maturity, then its price at time t is:

C(t) = E_Q,t[e^(-r(T-t)) C(T)]

where:

* C(t) = price today
* C(T) = payoff at maturity
* Q = risk-neutral probability
* r = continuously compounded risk-free rate

## Interpretation

The price is the discounted expected payoff under Q.

The expectation is not taken under the real-world probability.

---

# 9. Replication and Risk-Neutral Pricing

Risk-neutral pricing is justified by replication.

If a self-financing portfolio replicates the claim payoff, then:

X(T) = C(T)

If discounted wealth is a martingale under Q:

X_bar(t) = E_Q,t[X_bar(T)]

Since the portfolio replicates the claim:

X_bar(t) = E_Q,t[C_bar(T)]

Therefore, the cost of replication equals the risk-neutral expected discounted payoff.

## Key Point

Price = cost of replication = discounted expected payoff under Q

---

# 10. One-Period Binomial Option Pricing

In a one-period binomial model:

* up stock price: S_u = S(0)u
* down stock price: S_d = S(0)d

The risk-neutral probability is:

q = [(1 + r) - d] / [u - d]

and:

1 - q = [u - (1 + r)] / [u - d]

With continuous compounding:

q = [e^(r Delta t) - d] / [u - d]

## One-Period Option Price

If the payoff is:

* C_u in the up state
* C_d in the down state

then:

C(0) = [q C_u + (1 - q) C_d] / (1 + r)

or with continuous compounding:

C(0) = e^(-r Delta t) [q C_u + (1 - q) C_d]

---

# 11. Example: One-Period Call

Suppose:

* S(0) = 100
* S_u = 101
* S_d = 99
* K = 100
* r = 0.005

The call payoff is:

* up state: 101 - 100 = 1
* down state: 0

The risk-neutral probability is:

q = (1.005 - 0.99) / (1.01 - 0.99)

q = 0.75

The call price is:

C(0) = [0.75 × 1 + 0.25 × 0] / 1.005

C(0) = 0.746

This is the same price obtained by replication.

---

# 12. Replicating Portfolio Example

For the one-period call, the replicating portfolio solves:

delta_0(1.005) + delta_1(101) = 1

delta_0(1.005) + delta_1(99) = 0

The solution is:

delta_1 = 0.5

delta_0 = -49.254

This means:

* borrow 49.254
* buy half a share of stock

The cost is:

0.5 × 100 - 49.254 = 0.746

Therefore, the no-arbitrage price is:

C(0) = 0.746

---

# 13. Forward Pricing Under Risk-Neutral Pricing

Risk-neutral pricing can also recover the forward price.

The forward price F(t) is chosen so that the initial value of the forward contract is zero.

The forward payoff is:

S(T) - F(t)

The zero value condition is:

0 = E_Q,t[discount factor × (S(T) - F(t))]

With deterministic continuous interest rates, this gives:

F(t) = S(t)e^(r(T-t))

This matches the no-arbitrage formula from earlier modules.

---

# 14. Equivalent Martingale Measures

## Definition

An equivalent martingale measure is a probability measure Q such that:

1. Q is equivalent to the real-world probability measure P
2. discounted asset prices are martingales under Q

It is abbreviated as:

EMM

## Equivalent Means

P and Q are equivalent if they agree on which events are possible and impossible.

Events with zero probability under P also have zero probability under Q, and vice versa.

## In the Binomial Model

Q is equivalent if:

0 < q < 1

and:

0 < 1 - q < 1

This happens when:

d < 1 + r < u

So the binomial no-arbitrage condition guarantees that Q is a valid equivalent martingale measure.

---

# 15. First Fundamental Theorem of Asset Pricing

## Statement

A market has no arbitrage if and only if there exists at least one equivalent martingale measure.

In simple terms:

No arbitrage ⇔ at least one EMM exists

## Meaning

If a model is arbitrage-free, risk-neutral probabilities exist.

If risk-neutral probabilities exist, the model is arbitrage-free.

---

# 16. Arbitrage Definition

A strategy is an arbitrage if, for some future time T:

X(0) = 0

X(T) ≥ 0 with probability 1

P[X(T) > 0] > 0

## Intuition

An arbitrage starts with zero wealth, never loses money, and has a positive probability of making money.

---

# 17. Second Fundamental Theorem of Asset Pricing

## Completeness

A market is complete if every claim can be replicated by trading in the market.

## Statement

In an arbitrage-free market:

Completeness ⇔ unique equivalent martingale measure

## Meaning

If the market is complete, there is exactly one EMM.

Therefore, every claim has one unique price.

That price equals:

* cost of replication
* discounted expected payoff under the unique Q

---

# 18. Complete vs Incomplete Markets

## Complete Market

In a complete market:

* every payoff can be replicated
* there is one unique EMM
* every derivative has one unique no-arbitrage price

## Incomplete Market

In an incomplete market:

* not every payoff can be replicated
* there may be many EMMs
* there may be many no-arbitrage prices
* no-arbitrage gives a price range instead of one exact price

## Practical Interpretation

In incomplete markets, practitioners often choose one Q by calibration to market prices.

---

# 19. Binomial Tree Pricing

## Key Idea

In a multi-period binomial tree, option pricing is done by backward induction.

The process is:

1. build the stock price tree
2. compute option payoffs at maturity
3. move backwards through the tree using risk-neutral probabilities
4. the value at the root is the option price today

---

# 20. European Option Backward Induction

At each node:

C(t) = e^(-r Delta t) [q C_up + (1 - q) C_down]

where:

* C_up = option value after an up move
* C_down = option value after a down move

## European Call Payoff

C(T) = max[S(T) - K, 0]

## European Put Payoff

P(T) = max[K - S(T), 0]

---

# 21. Example: Two-Period European Call

Suppose:

* S(0) = 100
* K = 100
* u = 1.1
* d = 0.9
* r = 0.05
* Delta t = 1

Risk-neutral probability:

q = [e^(0.05) - 0.9] / [1.1 - 0.9]

q = 0.7564

Stock prices at maturity:

* 121
* 99
* 81

Call payoffs:

* max[121 - 100, 0] = 21
* max[99 - 100, 0] = 0
* max[81 - 100, 0] = 0

Backward induction gives:

C(0) = 10.8703

---

# 22. American Option Pricing

American options can be exercised before maturity.

In a binomial tree, they are priced using backward induction plus an exercise decision.

At each node:

American value = max[exercise value, continuation value]

where:

continuation value = e^(-r Delta t) [q C_up + (1 - q) C_down]

## Exercise Values

For an American call:

max[S(t) - K, 0]

For an American put:

max[K - S(t), 0]

---

# 23. Example: Two-Period American Put

Suppose:

* S(0) = 100
* K = 100
* u = 1.1
* d = 0.9
* r = 0.05
* Delta t = 1

Stock prices at maturity:

* 121
* 99
* 81

Put payoffs:

* max[100 - 121, 0] = 0
* max[100 - 99, 0] = 1
* max[100 - 81, 0] = 19

At each earlier node, compare:

* immediate exercise value
* continuation value

At the node where S = 90:

immediate exercise = 100 - 90 = 10

continuation value = 5.1229

Since:

10 > 5.1229

early exercise is optimal.

The American put price is:

P(0) = 2.4844

---

# 24. European vs American Options

## European Option

Can only be exercised at maturity.

Pricing:

C(t) = discounted risk-neutral expected future value

## American Option

Can be exercised before maturity.

Pricing:

C_A(t) = max[exercise now, wait]

## Important

For non-dividend-paying stocks:

American call = European call

American put may be more valuable than European put.

---

# 25. Connection to Black-Scholes

The binomial tree is a discrete-time model.

Black-Scholes is a continuous-time model.

As:

Delta t goes to 0

and the number of time steps increases,

the binomial tree price converges to the Black-Scholes price.

A common practical parameterization is:

u = e^(sigma sqrt(Delta t))

d = 1 / u

where:

sigma = volatility

---

# 26. Main Intuition of the Module

The module builds the bridge from no-arbitrage pricing to full mathematical option pricing.

The logic is:

1. Define a financial market model.
2. Require no arbitrage.
3. Find a risk-neutral probability Q.
4. Price derivatives using discounted expected payoff under Q.
5. In complete markets, prices are unique because every payoff can be replicated.
6. In binomial trees, compute prices by backward induction.

---

# 27. Common Confusions

## Real Probability vs Risk-Neutral Probability

Real probability is used for forecasting.

Risk-neutral probability is used for pricing.

## No Arbitrage vs Completeness

No arbitrage means at least one Q exists.

Completeness means exactly one Q exists.

## Replication vs Expectation

Replication gives the economic reason for the price.

Risk-neutral expectation gives the computational formula.

## European vs American Backward Induction

European:

discount expected future values.

American:

discount expected future values and compare with immediate exercise.

## Option Price vs Payoff

Payoff is what the option pays at maturity or exercise.

Price is the value today.

## Incomplete Markets

In incomplete markets, no-arbitrage may only determine a range of possible prices.

---

# 28. Exam Notes

You should be able to:

* define single-period and multi-period models
* explain the budget constraint
* explain the self-financing condition
* define gains and discounted wealth
* describe the binomial tree model
* state the no-arbitrage condition
* define martingale and risk-neutral probability
* compute the binomial risk-neutral probability q
* price a one-period option using replication
* price a one-period option using risk-neutral expectation
* explain why real probabilities do not directly determine option prices
* define equivalent martingale measure
* state the First Fundamental Theorem of Asset Pricing
* state the Second Fundamental Theorem of Asset Pricing
* explain complete vs incomplete markets
* price European options by backward induction
* price American options by backward induction
* identify when early exercise is optimal in a binomial tree
* explain how binomial trees connect to Black-Scholes

---

# 29. Core Formulas

## Bank Account

B(0) = 1

B(1) = 1 + r

or:

B(t) = [1 + r(t)] B(t - 1)

## Wealth

X(t) = sum of holdings × asset prices

## Gains

G(t) = X(t) - X(0)

## Discounted Value

Y_bar(t) = Y(t) / B(t)

## Binomial Stock Movement

S_up = Su

S_down = Sd

## No-Arbitrage Condition

d < 1 + r < u

or:

d < e^(r Delta t) < u

## Risk-Neutral Probability

q = [(1 + r) - d] / [u - d]

or:

q = [e^(r Delta t) - d] / [u - d]

## One-Period Option Price

C(0) = [q C_u + (1 - q) C_d] / (1 + r)

or:

C(0) = e^(-r Delta t) [q C_u + (1 - q) C_d]

## Risk-Neutral Pricing Formula

C(t) = E_Q,t[e^(-r(T-t)) C(T)]

## First Fundamental Theorem

No arbitrage ⇔ at least one EMM exists

## Second Fundamental Theorem

Completeness ⇔ exactly one EMM exists

## European Backward Induction

C(t) = e^(-r Delta t) [q C_up + (1 - q) C_down]

## American Backward Induction

C_A(t) = max[exercise value, continuation value]

where:

continuation value = e^(-r Delta t) [q C_up + (1 - q) C_down]

## Call Payoff

max[S(T) - K, 0]

## Put Payoff

max[K - S(T), 0]

---

# Final Intuition

Module 4 introduces the first real option pricing framework.

The binomial model is simple, but it contains the essential logic of modern derivative pricing.

The core message is:

Derivatives are priced by replication and no-arbitrage.

Risk-neutral probabilities are the tool that makes this computation possible.

In complete markets, the price is unique.

In the binomial tree, the price is found by working backwards from the final payoff to today.

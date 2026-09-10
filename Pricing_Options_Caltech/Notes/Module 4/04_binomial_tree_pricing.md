# Binomial Tree Option Pricing

## Key Idea

The binomial tree is the first practical mathematical model for option pricing.

It uses a simple structure:

* at each time step, the stock can move up or down
* option values are computed at maturity
* prices are then calculated backwards through the tree

This method works because discounted option prices are martingales under the risk-neutral probability.

---

# 1. Cox-Ross-Rubinstein Model

The binomial tree model is also called the Cox-Ross-Rubinstein model.

It is often abbreviated as:

CRR model

## Stock Dynamics

At each time step, the stock price moves to one of two possible values.

If the current stock price is S:

Up move:

S goes to Su

Down move:

S goes to Sd

where:

* u = up factor
* d = down factor

Usually:

u > 1 > d

---

# 2. Recombining Tree

A binomial tree is usually recombining.

This means:

up then down = down then up

Mathematically:

S × u × d = S × d × u

## Why It Matters

The tree recombines, so the number of nodes does not grow too fast.

This makes the model efficient to compute.

---

# 3. Risk-Free Growth

In previous sections, one-period risk-free growth was written as:

1 + r

In this section, the course often uses continuous compounding over a time step Delta t:

e^(r Delta t)

where:

* r = annual continuously compounded risk-free rate
* Delta t = length of one period in years

---

# 4. No-Arbitrage Condition

The no-arbitrage condition in the binomial model is:

d < e^(r Delta t) < u

## Intuition

The risk-free return must lie between the stock’s down return and up return.

If the stock always outperformed the bank account, arbitrage would exist.

If the bank account always outperformed the stock, arbitrage would also exist.

So the bank account must be better than the stock in the down state, but worse than the stock in the up state.

---

# 5. Risk-Neutral Probability

The risk-neutral probability q is chosen so that the discounted stock price is a martingale.

With continuous compounding over Delta t:

q = [e^(r Delta t) - d] / [u - d]

and:

1 - q = [u - e^(r Delta t)] / [u - d]

## Important

The real-world probability p does not matter for pricing.

Option pricing uses q, not p.

## Why q Is Valid

If:

d < e^(r Delta t) < u

then:

0 < q < 1

So the no-arbitrage condition guarantees that q is a valid probability.

---

# 6. Martingale Pricing in the Tree

Under the risk-neutral probability Q, discounted prices are martingales.

For an option price C(t):

discounted C(t) = expected discounted C(t + Delta t)

This gives the one-step pricing formula:

C(t) = e^(-r Delta t) [q C_up(t + Delta t) + (1 - q) C_down(t + Delta t)]

where:

* C_up = option value if the stock moves up
* C_down = option value if the stock moves down

## Intuition

At each node:

1. take the two future option values
2. compute their risk-neutral weighted average
3. discount back one period

---

# 7. Backward Induction

Binomial option pricing works by backward induction.

## Step 1

Build the stock price tree.

## Step 2

Compute option payoffs at maturity.

For a European call:

C(T) = max[S(T) - K, 0]

For a European put:

P(T) = max[K - S(T), 0]

## Step 3

Move backwards through the tree.

At each node:

C(t) = e^(-r Delta t) [q C_up + (1 - q) C_down]

## Step 4

Continue until reaching time 0.

The value at time 0 is the option price today.

---

# 8. Path-Independent Payoffs

A payoff is path-independent if it depends only on the final value of the stock.

Examples:

European call:

max[S(T) - K, 0]

European put:

max[K - S(T), 0]

## Important

For path-independent options, we only need the final stock price to compute the payoff.

We do not need to know how the stock got there.

---

# 9. European Option Pricing Algorithm

For a European option in a binomial tree:

1. construct the stock price tree
2. compute payoff at maturity
3. discount expected values backwards using q
4. the root value is the option price

## Core Formula

At each node:

C = e^(-r Delta t) [q C_up + (1 - q) C_down]

This formula is applied repeatedly from maturity back to today.

---

# 10. Example: Two-Period European Call

Suppose:

* S0 = 100
* K = 100
* u = 1.1
* d = 0.9
* r = 0.05
* Delta t = 1

## Stock Tree

At time 0:

S0 = 100

At time 1:

Up: 100 × 1.1 = 110

Down: 100 × 0.9 = 90

At time 2:

Up-Up: 100 × 1.1² = 121

Up-Down: 100 × 1.1 × 0.9 = 99

Down-Down: 100 × 0.9² = 81

## Call Payoffs at Maturity

For a call:

C(T) = max[S(T) - K, 0]

So:

At 121:

max[121 - 100, 0] = 21

At 99:

max[99 - 100, 0] = 0

At 81:

max[81 - 100, 0] = 0

## Backward Pricing

First compute q:

q = [e^(0.05) - 0.9] / [1.1 - 0.9]

q ≈ 0.7564

Then price backwards.

At the upper node:

C = e^(-0.05) [q × 21 + (1 - q) × 0]

At the lower node:

C = e^(-0.05) [q × 0 + (1 - q) × 0] = 0

Then go back one more step:

C0 = e^(-0.05) [q × C_up + (1 - q) × C_down]

In the example, the call price is approximately:

C0 ≈ 10.87

---

# 11. American Options

American options can be exercised before maturity.

This makes them harder to price in general.

However, in a one-stock binomial tree, American options are almost as easy to price as European options.

## Main Difference

For a European option, at each node we only compute the continuation value.

For an American option, at each node we compare:

1. value of waiting
2. value of exercising immediately

Then we take the maximum.

---

# 12. American Option Pricing Formula

At each node:

American value = max[immediate exercise value, continuation value]

where:

Continuation value:

e^(-r Delta t) [q C_up + (1 - q) C_down]

Immediate exercise value depends on the option.

For an American call:

max[S(t) - K, 0]

For an American put:

max[K - S(t), 0]

---

# 13. Dynamic Programming Principle

The dynamic programming principle says that the value today is determined by the best decision today plus optimal decisions in the future.

For an American option, the decision at each node is simple:

* exercise now
* wait one more period

So the value is:

max[exercise now, wait]

## Intuition

The holder chooses the action that gives the higher value.

This turns American option pricing into a backward optimization problem.

---

# 14. Optimal Stopping

American option pricing is an optimal stopping problem.

The holder chooses the best exercise time.

This exercise time is often denoted by:

Tau

Tau can be random because it depends on the future path of the stock.

Example:

Exercise the first time the stock falls below a certain level.

## Important

In general models, optimal stopping problems can be difficult.

In a binomial tree, they are manageable because we solve them node by node backwards.

---

# 15. Example: Two-Period American Put

Suppose:

* S0 = 100
* K = 100
* u = 1.1
* d = 0.9
* r = 0.05
* Delta t = 1

The stock tree is the same as before:

* 121
* 99
* 81

## Put Payoffs at Maturity

For a put:

P(T) = max[K - S(T), 0]

At 121:

max[100 - 121, 0] = 0

At 99:

max[100 - 99, 0] = 1

At 81:

max[100 - 81, 0] = 19

## Backward Induction

At each earlier node, compute:

continuation value = e^(-r Delta t) [q P_up + (1 - q) P_down]

Then compare with immediate exercise value:

immediate exercise = max[K - S, 0]

The American value is the maximum of the two.

---

# 16. Early Exercise Example

At the node where the stock price is 90:

Immediate exercise value:

100 - 90 = 10

Continuation value:

e^(-0.05) [q × 1 + (1 - q) × 19]

This continuation value is approximately 5.12.

Since:

10 > 5.12

it is optimal to exercise early at that node.

## Key Intuition

For American puts, early exercise can be optimal.

This happens when the stock price is sufficiently low.

---

# 17. American Put Price

Continuing the backward induction gives the American put price at time 0.

In the example, the price is approximately:

P0 ≈ 2.48

This price is higher than or equal to the corresponding European put price because the American option gives the holder more flexibility.

---

# 18. Why American Calls Are Different

For a non-dividend-paying stock, American calls should not be exercised early.

Therefore, in that case:

American call price = European call price

This is why the example uses an American put rather than an American call.

A put is more interesting because early exercise may be optimal.

---

# 19. Choosing u and d

The model requires choosing:

* u
* d
* Delta t
* r

The course later connects u and d to volatility.

A common choice is:

u = e^(sigma sqrt(Delta t))

d = 1 / u

where:

* sigma = volatility of the stock
* Delta t = length of each period

## Important

This connects the binomial tree to Black-Scholes.

As Delta t becomes small and the number of time steps increases, the binomial price converges toward the Black-Scholes price.

---

# 20. Practical Implementation

For practical option pricing, a binomial tree can use many time steps.

Example:

For a three-month option, using about one trading day per step may be enough.

A typical trading-year convention is:

252 trading days per year

So:

Delta t = 1 / 252

## Intuition

More steps make the binomial tree more accurate.

As the time step becomes smaller, the tree becomes a better approximation to continuous-time pricing.

---

# 21. Common Confusions

## Real Probability p vs Risk-Neutral Probability q

The real probability p may describe how likely the stock is to go up.

The risk-neutral probability q is used for pricing.

The pricing algorithm uses q, not p.

## European vs American Backward Induction

European option:

discount expected future values only.

American option:

discount expected future values and compare with immediate exercise.

## Path-Independent vs Path-Dependent

Path-independent payoff:

depends only on S(T).

Path-dependent payoff:

depends on the path followed by the stock.

The notes here focus on path-independent options.

## Continuation Value vs Exercise Value

Continuation value:

value of waiting.

Exercise value:

cash received if exercised immediately.

American option value:

maximum of the two.

## Binomial Tree vs Black-Scholes

The binomial tree is discrete.

Black-Scholes is continuous.

But as the number of time steps increases, binomial prices can converge to Black-Scholes prices.

---

# 22. Exam Notes

You should be able to:

* define the CRR binomial tree model
* explain why the tree recombines
* state the no-arbitrage condition d < e^(r Delta t) < u
* compute the risk-neutral probability q
* explain why discounted option prices are martingales under Q
* price a European option using backward induction
* compute terminal call and put payoffs
* explain path-independent payoffs
* price an American option using backward induction
* distinguish continuation value from exercise value
* explain why American puts may be exercised early
* explain why non-dividend-paying American calls are not exercised early
* understand how u and d relate to volatility
* explain why binomial trees approximate Black-Scholes as Delta t becomes small

---

# 23. Core Formulas

## Stock Movement

S_up = Su

S_down = Sd

## Risk-Free Growth

Bank account grows by:

e^(r Delta t)

## No-Arbitrage Condition

d < e^(r Delta t) < u

## Risk-Neutral Probability

q = [e^(r Delta t) - d] / [u - d]

1 - q = [u - e^(r Delta t)] / [u - d]

## European Backward Induction

C(t) = e^(-r Delta t) [q C_up + (1 - q) C_down]

## European Call Payoff

C(T) = max[S(T) - K, 0]

## European Put Payoff

P(T) = max[K - S(T), 0]

## American Backward Induction

C_A(t) = max[exercise value, continuation value]

where:

continuation value = e^(-r Delta t) [q C_up + (1 - q) C_down]

## American Call Exercise Value

max[S(t) - K, 0]

## American Put Exercise Value

max[K - S(t), 0]

## CRR Parameter Choice

u = e^(sigma sqrt(Delta t))

d = 1 / u

---

# Final Intuition

The binomial tree prices options by moving backwards through the tree.

At maturity, the option payoff is known.

Before maturity, the option value is the discounted risk-neutral expected value of future option values.

For American options, we add one extra step:

at each node, compare waiting with exercising immediately.

This makes the binomial tree one of the simplest and most useful tools for understanding option pricing.

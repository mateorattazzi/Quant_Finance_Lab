# Fundamental Theorems of Asset Pricing

## Key Idea

The Fundamental Theorems of Asset Pricing connect three major ideas:

* no-arbitrage
* risk-neutral probabilities
* market completeness

These theorems explain why risk-neutral pricing works and when derivative prices are unique.

---

# 1. Big Picture

Financial market models can be divided into two categories:

1. models with arbitrage
2. models with no arbitrage

If a model has arbitrage, the theory is not very useful.

There is no meaningful pricing theory because one can create risk-free profits.

If a model has no arbitrage, then risk-neutral pricing becomes possible.

---

# 2. Equivalent Martingale Measure

## Definition

An equivalent martingale measure is a probability measure Q such that:

1. Q is equivalent to the real-world probability measure P
2. discounted asset prices are martingales under Q

It is often abbreviated as:

EMM

Equivalent martingale measures are also called:

* risk-neutral measures
* martingale measures
* pricing measures

---

# 3. What “Equivalent” Means

Two probability measures P and Q are equivalent if they agree on which events are impossible.

That means:

* if an event has zero probability under P, it also has zero probability under Q
* if an event has zero probability under Q, it also has zero probability under P

## Intuition

P and Q may assign different probabilities to events.

But they must agree on which events can happen and which events cannot happen.

## In the Binomial Model

If the real probability of an up move is p and the risk-neutral probability is q, equivalence means:

0 < p < 1

and:

0 < q < 1

So both the real-world model and the risk-neutral model agree that both up and down moves are possible.

---

# 4. Lowercase q vs Uppercase Q

In binomial models:

* q = risk-neutral probability of an up move
* 1 - q = risk-neutral probability of a down move

Uppercase Q refers to the whole probability measure.

In a simple binomial model:

Q = {q, 1 - q}

In more complex models, Q represents the full system of probabilities across all possible outcomes.

## Important

When we write:

E_Q[ ]

we mean expected value under the probability measure Q.

---

# 5. First Fundamental Theorem of Asset Pricing

## Statement

A market model has no arbitrage if and only if there exists at least one equivalent martingale measure.

In simple words:

No arbitrage ⇔ at least one risk-neutral probability exists

## Meaning

If a model has no arbitrage, we can find a probability measure Q under which discounted asset prices are martingales.

If such a Q exists, then the model has no arbitrage.

---

# 6. Why the First Theorem Matters

The theorem gives a practical way to check whether a model is arbitrage-free.

Instead of checking every possible trading strategy, we can ask:

Can we find an equivalent martingale measure?

If yes, the model is arbitrage-free.

If no, the model contains arbitrage.

## Practical Meaning

When using standard models, this has usually already been checked.

But if we create a new model, the theorem becomes important.

---

# 7. Arbitrage Definition

A strategy is an arbitrage if:

1. it starts with zero initial wealth
2. it never produces a loss
3. it has a strictly positive probability of producing a profit

Mathematically:

X(0) = 0

X(T) ≥ 0 with probability 1

P[X(T) > 0] > 0

## Intuition

An arbitrage is a free opportunity:

* no initial cost
* no possible loss
* some chance of profit

This is slightly weaker than saying profit is guaranteed in every scenario.

---

# 8. Why an EMM Implies No Arbitrage

Assume an equivalent martingale measure Q exists.

Then discounted wealth must satisfy the martingale property:

X(0) = E_Q[discounted X(T)]

If a strategy were an arbitrage:

* X(0) = 0
* X(T) is never negative
* X(T) is sometimes positive

Then:

E_Q[discounted X(T)] > 0

So:

X(0) > 0

But this contradicts X(0) = 0.

Therefore, arbitrage cannot exist.

## Key Intuition

If future payoff is never negative and sometimes positive, its expectation must be positive.

So it cannot have zero cost under a martingale measure.

---

# 9. Second Fundamental Theorem of Asset Pricing

## Statement

In an arbitrage-free market:

the market is complete if and only if there is exactly one equivalent martingale measure.

In simple words:

Completeness ⇔ unique risk-neutral probability

## Meaning

If the market is complete, every payoff can be replicated.

If every payoff can be replicated, every derivative has one unique no-arbitrage price.

That unique price is computed under the unique Q.

---

# 10. Market Completeness

## Definition

A market is complete if every contingent claim can be replicated by trading in the available assets.

A contingent claim is any random future payoff.

Examples:

* call option payoff
* put option payoff
* digital option payoff
* any payoff depending on future states

## Intuition

In a complete market, derivatives are theoretically redundant.

Why?

Because their payoffs can be created by trading in the underlying assets and the bank account.

---

# 11. Complete Markets

In a complete market:

* every payoff can be replicated
* there is exactly one equivalent martingale measure
* every derivative has a unique no-arbitrage price
* price equals cost of replication
* price equals discounted expected payoff under the unique Q

## Formula

C(0) = E_Q[discounted C(T)]

Because Q is unique, the price is unique.

---

# 12. Incomplete Markets

A market is incomplete if not every payoff can be replicated.

In an incomplete market:

* there may be many equivalent martingale measures
* there may be many no-arbitrage prices
* derivative prices may lie in an interval
* additional criteria are needed to choose a price

## Intuition

If a payoff cannot be perfectly replicated, no-arbitrage alone may not determine one exact price.

Instead, it determines a range of acceptable prices.

---

# 13. No-Arbitrage Price Interval

In an incomplete market, different equivalent martingale measures can give different prices.

A no-arbitrage price may lie between:

minimum price under all Q

and

maximum price under all Q

Conceptually:

min_Q E_Q[discounted payoff] ≤ price ≤ max_Q E_Q[discounted payoff]

## Practical Interpretation

This resembles a bid-ask spread.

More complete markets tend to have tighter price ranges.

Less complete markets tend to have wider price ranges.

---

# 14. Bid-Ask Spread and Completeness

In developed and liquid markets:

* many instruments exist
* hedging is easier
* replication is closer
* bid-ask spreads tend to be smaller

In less developed or illiquid markets:

* fewer instruments exist
* hedging is harder
* replication is less precise
* bid-ask spreads tend to be wider

## Intuition

A tighter bid-ask spread can be interpreted as the market being closer to complete.

A wider bid-ask spread reflects more uncertainty and less perfect replication.

---

# 15. Calibration

Even in incomplete markets, practitioners often choose one risk-neutral measure Q from market data.

This process is called calibration.

## Meaning

Calibration means choosing model parameters so that the model matches observed market prices.

Once calibrated, the model can be used to price other derivatives.

## Important

In incomplete markets, this chosen Q is not forced uniquely by no-arbitrage.

It is selected using market prices and modeling assumptions.

---

# 16. Connection to Binomial Model

In the one-period binomial model, the no-arbitrage condition is:

d < 1 + r < u

Under this condition, the risk-neutral probability is:

q = [(1 + r) - d] / [u - d]

and:

1 - q = [u - (1 + r)] / [u - d]

Because both probabilities are strictly between 0 and 1, Q is equivalent to P.

## Key Point

The binomial model has:

* no arbitrage
* one equivalent martingale measure
* completeness

Therefore, every derivative payoff has a unique price.

---

# 17. Common Confusions

## No Arbitrage vs Completeness

No arbitrage means there is at least one risk-neutral measure.

Completeness means there is exactly one risk-neutral measure.

These are different ideas.

## Risk-Neutral Measure vs Real Probability

The real probability P describes beliefs about what may happen.

The risk-neutral measure Q is used for pricing.

They are equivalent if they agree on which events are possible, but they do not need to assign the same probabilities.

## Complete Market vs Realistic Market

Complete markets are idealized.

Real markets are usually incomplete.

However, complete models are useful because they provide clear benchmark prices.

## Unique Q vs Many Qs

One Q means unique prices.

Many Qs means no-arbitrage gives a price range, not one exact price.

## Arbitrage-Free Does Not Mean Complete

A market can have no arbitrage and still be incomplete.

That means risk-neutral measures exist, but there may be more than one.

---

# 18. Exam Notes

You should be able to:

* define equivalent martingale measure
* explain what “equivalent” means
* distinguish lowercase q from uppercase Q
* state the First Fundamental Theorem of Asset Pricing
* state the Second Fundamental Theorem of Asset Pricing
* define arbitrage formally
* explain why existence of an EMM implies no arbitrage
* define market completeness
* explain why complete markets have unique prices
* explain why incomplete markets may have price intervals
* connect binomial no-arbitrage condition to existence of Q
* understand why bid-ask spreads relate to incompleteness

---

# 19. Core Formulas and Statements

## Equivalent Martingale Measure

Q is an EMM if:

discounted asset prices are martingales under Q

and Q is equivalent to P.

## First Fundamental Theorem of Asset Pricing

No arbitrage ⇔ at least one EMM exists

## Second Fundamental Theorem of Asset Pricing

Completeness ⇔ exactly one EMM exists

## Arbitrage Definition

X(0) = 0

X(T) ≥ 0 with probability 1

P[X(T) > 0] > 0

## Binomial Risk-Neutral Probability

q = [(1 + r) - d] / [u - d]

1 - q = [u - (1 + r)] / [u - d]

## No-Arbitrage Condition in Binomial Model

d < 1 + r < u

## Complete Market Price

C(0) = E_Q[discounted C(T)]

## Incomplete Market Price Range

min_Q E_Q[discounted C(T)] ≤ C(0) ≤ max_Q E_Q[discounted C(T)]

---

# Final Intuition

The Fundamental Theorems of Asset Pricing explain the structure behind risk-neutral pricing.

The first theorem says that no-arbitrage is equivalent to the existence of at least one risk-neutral measure.

The second theorem says that market completeness is equivalent to having exactly one risk-neutral measure.

So:

* no arbitrage gives existence of Q
* completeness gives uniqueness of Q
* uniqueness of Q gives unique derivative prices

This is the theoretical foundation behind modern derivative pricing.

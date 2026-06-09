# Option Bounds and Put-Call Parity

## Key Idea

For options, unlike forwards, futures and swaps, we usually need mathematical models to obtain an exact price.

However, even without a full pricing model, we can derive important no-arbitrage bounds.

These bounds tell us what option prices cannot violate.

If they are violated, arbitrage is possible.

---

# 1. Notation

European options:

- c(t) = European call price
- p(t) = European put price

American options:

- C(t) = American call price
- P(t) = American put price

Other notation:

- S(t) = underlying price today
- K = strike price
- T = maturity
- r = continuously compounded risk-free rate

---

# 2. European vs American Options

## Key Difference

European option:

- can only be exercised at maturity

American option:

- can be exercised at any time before maturity

## Basic Value Relationship

Because the American option gives more flexibility:

c(t) ≤ C(t)

p(t) ≤ P(t)

American options are at least as valuable as European options.

---

# 3. Upper Bounds for Calls

## Relation

For calls:

c(t) ≤ C(t) ≤ S(t)

## Intuition

A call option gives the right to buy the underlying.

Its payoff can never be greater than the value of the underlying itself.

Therefore, the call price cannot exceed the stock price.

If it did, one could sell the call and buy the stock to create arbitrage.

---

# 4. Upper Bounds for Puts

## American Put

P(t) ≤ K

The payoff of a put can never exceed the strike price.

## European Put

p(t) ≤ K e^(-r(T-t))

A European put can only be exercised at maturity.

Therefore, its maximum future payoff K must be discounted back to today.

## Important Difference

American put upper bound:

P(t) ≤ K

European put upper bound:

p(t) ≤ K e^(-r(T-t))

The American put is not discounted because it could be exercised immediately.

---

# 5. Lower Bound for European Calls

Assume the underlying pays no dividends.

## Relation

c(t) ≥ S(t) - K e^(-r(T-t))

## Stronger Form

Because option prices cannot be negative:

c(t) ≥ max[S(t) - K e^(-r(T-t)), 0]

## Intuition

A European call must be worth at least the value of:

stock today minus present value of strike price

If the call were cheaper than this, arbitrage would be possible.

---

# 6. Lower Bound for European Puts

Assume the underlying pays no dividends.

## Relation

p(t) ≥ K e^(-r(T-t)) - S(t)

## Stronger Form

Because option prices cannot be negative:

p(t) ≥ max[K e^(-r(T-t)) - S(t), 0]

## Intuition

A European put must be worth at least the value of:

present value of strike price minus stock price today

If the put were too cheap, arbitrage would be possible.

---

# 7. American Call on a Non-Dividend-Paying Asset

## Key Result

If the underlying pays no dividends:

C(t) = c(t)

American call price = European call price

## Meaning

The right to exercise early has no extra value for a call when the asset pays no dividends.

## Practical Rule

An American call on a non-dividend-paying stock should not be exercised early.

If the holder wants to exit the position, it is better to sell the call than to exercise it.

## Intuition

Exercising early means paying K now.

But waiting preserves:

- upside exposure
- time value
- interest earned on the cash K until maturity

So early exercise destroys value.

---

# 8. What Changes With Dividends?

If the underlying pays dividends, the result may fail.

Then:

C(t) can be greater than c(t)

## Why?

Holding the stock gives dividends.

Holding a call does not.

Early exercise may become valuable if exercising allows the holder to receive dividends.

## Important

For dividend-paying assets, American calls may require numerical pricing methods.

The simple equality between American and European calls does not necessarily hold.

---

# 9. American Puts

For puts, even without dividends:

P(t) can be greater than p(t)

## Why?

Early exercise can be valuable for puts.

If the stock price becomes very low, exercising the put gives approximately K immediately.

That money can then be invested at the risk-free rate.

## Intuition

For a put, early exercise can convert a high intrinsic value into cash today.

This can be better than waiting until maturity.

Therefore:

American put value usually differs from European put value.

---

# 10. Put-Call Parity

## Key Result

For European options on a non-dividend-paying asset:

c(t) + K e^(-r(T-t)) = p(t) + S(t)

This is called put-call parity.

## Conditions

Put-call parity applies to:

- European call
- European put
- same underlying
- same strike K
- same maturity T
- no dividends

---

# 11. Put-Call Parity Intuition

Put-call parity says that two portfolios must have the same value today if they produce the same payoff at maturity.

## Portfolio A

- long European call
- cash equal to present value of K

Value today:

c(t) + K e^(-r(T-t))

## Portfolio B

- long European put
- long one share of the underlying

Value today:

p(t) + S(t)

## Payoff at Maturity

If S(T) > K:

- Portfolio A pays S(T)
- Portfolio B pays S(T)

If S(T) < K:

- Portfolio A pays K
- Portfolio B pays K

Both portfolios have the same payoff in all scenarios.

Therefore, by the law of one price, they must have the same price today.

---

# 12. Why Put-Call Parity Matters

Put-call parity creates a direct relationship between European call and put prices.

If we know:

- call price
- stock price
- strike price
- interest rate
- time to maturity

we can infer the put price.

Or vice versa.

## Rearranged Forms

Call price:

c(t) = p(t) + S(t) - K e^(-r(T-t))

Put price:

p(t) = c(t) + K e^(-r(T-t)) - S(t)

---

# 13. American Put-Call Bounds

For American options, we do not generally get equality.

Instead, we get bounds.

For non-dividend-paying assets:

S(t) - K ≤ C(t) - P(t) ≤ S(t) - K e^(-r(T-t))

## Intuition

American exercise flexibility breaks the exact equality.

The American put can be more valuable than the European put because early exercise may be useful.

The American call on a non-dividend-paying asset still equals the European call.

---

# 14. Common Confusions

## Option Bounds vs Option Pricing

Bounds do not give the exact option price.

They only tell us the range of prices that avoids arbitrage.

Exact pricing requires a model, such as:

- binomial model
- Black-Scholes
- Monte Carlo

## European vs American Call

For non-dividend-paying assets:

European call = American call

For dividend-paying assets:

American call may be more valuable.

## European vs American Put

American puts can be more valuable because early exercise may be optimal.

This can happen even if the asset pays no dividends.

## Intrinsic Value vs Option Value

Intrinsic value is the payoff if exercised now.

Option value includes:

- intrinsic value
- time value
- optionality

This is why exercising an American call early may be worse than selling it.

## Put-Call Parity vs Payoff Equality

Put-call parity is not saying calls and puts have the same payoff.

It says two portfolios involving calls, puts, stock and cash have the same payoff.

Therefore, their prices must match.

---

# 15. Exam Notes

You should be able to:

- define c(t), p(t), C(t), P(t)
- explain why American options are at least as valuable as European options
- state upper bounds for calls and puts
- state lower bounds for European calls and puts
- explain why European puts have a discounted upper bound
- explain why American calls on non-dividend-paying assets should not be exercised early
- explain why American puts may be exercised early
- state and use put-call parity
- understand why put-call parity is a no-arbitrage relation
- distinguish exact pricing from no-arbitrage bounds

---

# 16. Core Formulas

## American vs European

c(t) ≤ C(t)

p(t) ≤ P(t)

## Call Upper Bound

c(t) ≤ C(t) ≤ S(t)

## Put Upper Bounds

P(t) ≤ K

p(t) ≤ K e^(-r(T-t))

## European Call Lower Bound

c(t) ≥ max[S(t) - K e^(-r(T-t)), 0]

## European Put Lower Bound

p(t) ≥ max[K e^(-r(T-t)) - S(t), 0]

## American Call Without Dividends

C(t) = c(t)

## European Put-Call Parity

c(t) + K e^(-r(T-t)) = p(t) + S(t)

## American Put-Call Bounds

S(t) - K ≤ C(t) - P(t) ≤ S(t) - K e^(-r(T-t))

---

# Final Intuition

Options are harder to price exactly than forwards or futures because their payoffs are non-linear.

Without a full pricing model, we can still derive no-arbitrage bounds.

The most important result is put-call parity, which shows that European call and put prices are linked through a replication argument.

The central idea remains the same:

if two portfolios produce the same future payoff, they must have the same price today.
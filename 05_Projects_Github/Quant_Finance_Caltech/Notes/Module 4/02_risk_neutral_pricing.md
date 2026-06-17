# Risk-Neutral Pricing

## Key Idea

Risk-neutral pricing is one of the central ideas in option pricing theory.

The main idea is:

Option prices can be computed as discounted expected payoffs, but not using real-world probabilities.

Instead, we use artificial probabilities called:

* risk-neutral probabilities
* martingale probabilities
* pricing probabilities

These probabilities are usually denoted by:

Q

or sometimes:

P*

---

# 1. Why Real Probabilities Are Not Used

In insurance pricing, random claims are often priced using expected value under real-world probabilities.

Example intuition:

Price = discounted expected claim

This works when the insurer cannot hedge each individual claim and instead relies on the law of large numbers across many policies.

Financial markets are different because derivative sellers can hedge by trading the underlying asset.

## Key Difference

Insurance pricing:

* usually prices using real probabilities
* relies on diversification and law of large numbers

Financial derivative pricing:

* prices using hedging and replication
* uses risk-neutral probabilities

## Important Intuition

If we can replicate a derivative payoff by trading in the stock and the bank account, then the price is determined by the cost of replication.

The real probability of the stock moving up or down does not directly determine the option price.

---

# 2. Martingale

## Definition

A process M(t) is a martingale if:

M(t) = E_t[M(T)]

for all future times T.

This means:

The best estimate today of the future value is the current value.

## Intuition

A martingale is like a fair game.

On average, there is no expected gain or loss.

---

# 3. Discounted Stock Price

In risk-neutral pricing, we want the discounted stock price to be a martingale.

This means:

discounted stock price today = expected discounted stock price in the future under Q

Symbolically:

S(t) / B(t) = E_Q,t [S(T) / B(T)]

where:

* S(t) = stock price
* B(t) = bank account value
* Q = risk-neutral probability

## Why Discount?

Discounting removes the effect of risk-free growth.

After discounting, the stock should behave like a fair game under the risk-neutral probability.

---

# 4. Risk-Neutral Probability

## Definition

A risk-neutral probability is a probability measure Q under which discounted asset prices are martingales.

It is also called:

* martingale probability
* pricing probability

## Important

Risk-neutral probabilities are not necessarily real-world probabilities.

They are artificial probabilities used for pricing.

They are chosen so that discounted asset prices have the martingale property.

---

# 5. General Risk-Neutral Pricing Formula

If a claim pays C(T) at maturity and can be replicated, then its price at time t is:

C(t) = E_Q,t [discounted payoff]

With constant continuously compounded interest rate r:

C(t) = E_Q,t [e^(-r(T-t)) C(T)]

Equivalently:

C(t) = e^(-r(T-t)) E_Q,t[C(T)]

## Meaning

The price today is the discounted expected payoff under the risk-neutral probability Q.

## Key Assumptions

This formula requires:

1. a risk-neutral probability exists
2. the claim can be replicated
3. markets are frictionless enough for no-arbitrage pricing

---

# 6. Replication and Risk-Neutral Pricing

Suppose a portfolio replicates the claim payoff.

That means:

X(T) = C(T)

where:

* X(T) = terminal wealth of the replicating portfolio
* C(T) = derivative payoff

If discounted wealth is a martingale under Q:

X(t) / B(t) = E_Q,t [X(T) / B(T)]

Since X(T) = C(T):

X(t) / B(t) = E_Q,t [C(T) / B(T)]

Therefore:

X(t) = price of the claim

So:

Claim price = cost of replication = discounted expected payoff under Q

---

# 7. One-Period Binomial Model

In a one-period binomial model, the stock can move to only two values:

Up state:

S_u = S(0)u

Down state:

S_d = S(0)d

The bank account grows by:

1 + r

The no-arbitrage condition is:

d < 1 + r < u

## Meaning

The risk-free return must lie between the stock’s down return and up return.

If not, arbitrage would exist.

---

# 8. Risk-Neutral Probability in the Binomial Model

The risk-neutral probability q is chosen so that the discounted stock price is a martingale.

Formula:

q = [(1 + r) - d] / [u - d]

and:

1 - q = [u - (1 + r)] / [u - d]

## Important

The real-world probability p does not appear in this formula.

Only these inputs matter:

* u
* d
* r

## Why q Is a Valid Probability

If:

d < 1 + r < u

then:

0 < q < 1

So the no-arbitrage condition guarantees that the risk-neutral probability is valid.

---

# 9. Pricing a One-Period Option

Let the option payoff be:

C_u in the up state

C_d in the down state

Then the one-period binomial price is:

C(0) = [q C_u + (1 - q) C_d] / (1 + r)

## Interpretation

The option price is the discounted expected payoff under the risk-neutral probability.

This is not the same as using the real probability of an up move.

---

# 10. Replication in the One-Period Binomial Model

A one-period binomial option payoff can also be priced by replication.

We choose:

* delta_0 = position in the bank account
* delta_1 = number of shares of stock

so that the portfolio matches the option payoff in both states.

This gives two equations:

delta_0(1+r) + delta_1 S_u = C_u

delta_0(1+r) + delta_1 S_d = C_d

Solving these gives the replicating portfolio.

The option price is:

C(0) = delta_0 + delta_1 S(0)

## Key Point

Replication price and risk-neutral expected payoff give the same result.

---

# 11. Completeness

## Definition

A market is complete if every contingent claim can be replicated by trading in the available assets.

In the one-period binomial model:

* there are two possible future states
* there are two instruments: stock and bank account

Therefore, we can solve two equations with two unknowns.

This makes the model complete.

## Important

In a complete market, every derivative has a unique no-arbitrage price.

---

# 12. Why Actual Probabilities Do Not Matter

This is counterintuitive.

A call option pays more when the stock goes up.

So it seems like the real probability of an up move should matter.

However, in a complete model, the seller can perfectly hedge the payoff.

Because the payoff can be replicated exactly, the price is determined by the hedge, not by the real probability.

## Key Idea

Real probabilities matter for forecasting.

Risk-neutral probabilities matter for pricing.

---

# 13. Example Logic

Suppose:

* S(0) = 100
* S_u = 101
* S_d = 99
* K = 100
* r = 0.005

Call payoff:

* up state: 1
* down state: 0

The replicating portfolio can be found by solving:

delta_0(1+r) + delta_1(101) = 1

delta_0(1+r) + delta_1(99) = 0

This gives:

* delta_1 = 0.5
* delta_0 approximately -49.254

So the price is:

C(0) = 0.5 × 100 - 49.254

C(0) approximately 0.746

The same result is obtained with risk-neutral pricing.

---

# 14. Forward Pricing Using Risk-Neutral Pricing

Risk-neutral pricing can also recover the forward price.

A forward contract is chosen so that its initial value is zero.

The payoff is:

S(T) - F(t)

Using risk-neutral pricing:

0 = E_Q,t [discount factor × (S(T) - F(t))]

Solving this gives the forward price.

With deterministic continuous interest rates:

F(t) = S(t)e^(r(T-t))

This matches the no-arbitrage formula from Module 3.

---

# 15. Common Confusions

## Risk-Neutral Probability vs Real Probability

Real probability describes what we believe will happen.

Risk-neutral probability is used for pricing.

They are generally not the same.

## Expected Payoff vs Price

The option price is not the real-world expected payoff.

It is the discounted expected payoff under Q.

## Martingale vs Growing Asset

Under the real-world probability, stocks usually have expected returns above the risk-free rate.

Under Q, discounted stock prices behave like martingales.

## Replication vs Prediction

Pricing is not about predicting whether the stock will go up or down.

Pricing is about finding the cost of replicating the payoff.

## Complete Market

A complete market allows every payoff to be replicated.

If the payoff can be replicated, it has a unique no-arbitrage price.

---

# 16. Exam Notes

You should be able to:

* explain why option pricing uses risk-neutral probabilities
* define a martingale
* explain why discounted stock prices should be martingales under Q
* define risk-neutral / martingale / pricing probabilities
* state the general risk-neutral pricing formula
* compute q in a one-period binomial model
* explain why d < 1 + r < u is the no-arbitrage condition
* price a one-period option using risk-neutral expectation
* price the same option using replication
* explain why real probabilities do not appear in the price
* understand the connection between replication and expected discounted payoff

---

# 17. Core Formulas

## Martingale Property

M(t) = E_t[M(T)]

## Discounted Stock Martingale

S(t) / B(t) = E_Q,t [S(T) / B(T)]

## Risk-Neutral Pricing Formula

C(t) = E_Q,t [discounted payoff]

With constant continuously compounded rate:

C(t) = e^(-r(T-t)) E_Q,t[C(T)]

## Binomial Risk-Neutral Probability

q = [(1 + r) - d] / [u - d]

1 - q = [u - (1 + r)] / [u - d]

## One-Period Binomial Option Price

C(0) = [q C_u + (1 - q) C_d] / (1 + r)

## Replication Equations

delta_0(1+r) + delta_1 S_u = C_u

delta_0(1+r) + delta_1 S_d = C_d

## Replication Price

C(0) = delta_0 + delta_1 S(0)

---

# Final Intuition

Risk-neutral pricing says that derivative prices can be computed as discounted expected payoffs under artificial probabilities.

These probabilities are not forecasts.

They are chosen so that discounted asset prices become martingales.

The reason this works is replication:

if a portfolio can exactly reproduce the derivative payoff, then the derivative price must equal the cost of that portfolio.

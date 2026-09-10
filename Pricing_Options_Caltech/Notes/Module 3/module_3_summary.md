# Module 3 Summary — Model-Independent Pricing Relations

## 1. Purpose of Module 3

This module studies pricing relations that do not require a full stochastic model.

The main idea is:

Some derivatives can be priced or bounded using only no-arbitrage and replication.

Main instruments:

- forwards
- futures
- swaps
- option bounds
- put-call parity

For linear derivatives, we can often obtain exact pricing formulas.

For options, because payoffs are non-linear, we usually only obtain bounds unless we introduce a model.

---

# 2. Model-Independent Pricing

## Definition

A pricing relation is model-independent if it does not require assumptions about the probability distribution of the underlying asset.

We do not need:

- volatility
- drift
- Brownian motion
- expected future price

We only use:

- current asset price
- interest rates
- dividends
- bond prices
- no-arbitrage
- replication

## Key Idea

If two strategies produce the same future cash flows, they must have the same value today.

Otherwise, arbitrage would be possible.

---

# 3. Forward Contracts

## Definition

A forward contract is an agreement to buy or sell an asset at maturity T for a price fixed today.

Long forward payoff:

S(T) - F(t)

where:

- S(T) = underlying price at maturity
- F(t) = forward price agreed today

## Important

At initiation, a forward contract has value zero.

The forward price F(t) is chosen so that neither party pays anything upfront.

---

# 4. Forward Price Without Dividends

Let B(t,T) be the future value at T of 1 dollar invested risk-free at time t.

No-arbitrage forward price:

F(t) = S(t)B(t,T)

With continuous compounding:

F(t) = S(t)e^(r(T-t))

## Intuition

Buying the asset today and financing it until T must be equivalent to entering a forward contract to buy it at T.

If the forward price is too high or too low, arbitrage is possible.

---

# 5. Forward Price With Dividends

If the asset pays dividends before maturity, the forward price decreases.

Reason:

The owner of the asset receives dividends.

The holder of the forward does not receive dividends before maturity.

## Deterministic Dividends

If D(t) is the present value of known dividends:

F(t) = [S(t) - D(t)]B(t,T)

With continuous compounding:

F(t) = [S(t) - PV(dividends)]e^(r(T-t))

## Continuous Dividend Yield

If dividends are paid continuously at rate q:

F(t) = S(t)e^((r-q)(T-t))

---

# 6. Currency Forwards

A foreign currency behaves like an asset that pays a dividend yield.

The foreign interest rate acts like the dividend yield.

Currency forward formula:

F(t) = S(t)e^((r-r_f)(T-t))

where:

- S(t) = domestic price of one unit of foreign currency
- r = domestic risk-free rate
- r_f = foreign risk-free rate

## Intuition

The domestic interest rate increases the forward price.

The foreign interest rate decreases the forward price.

---

# 7. Futures

## Definition

A futures contract is similar to a forward, but it is exchange-traded and marked to market daily.

## Main Differences vs Forwards

Forward:

- OTC/private contract
- payoff settled at maturity
- counterparty risk
- delivery price fixed at initiation

Future:

- exchange-traded
- standardized
- daily settlement
- margin account
- lower counterparty risk

---

# 8. Mark-to-Market

Mark-to-market means daily gains and losses are settled in the margin account.

If the futures price increases:

- long futures gains
- short futures loses

If the futures price decreases:

- long futures loses
- short futures gains

Ignoring interest on the margin account, daily changes telescope:

Total futures payoff = S(T) - F(t)

At maturity:

F(T) = S(T)

Otherwise, arbitrage would be possible.

---

# 9. Forward-Futures Equivalence

If interest rates are deterministic:

Futures price = Forward price

## Intuition

Even though futures settle daily and forwards settle at maturity, deterministic rates allow daily gains/losses to be reinvested or financed in a known way.

If interest rates are random, futures and forward prices may differ.

The difference depends on the correlation between:

- underlying asset price
- interest rates

---

# 10. Swaps

## Definition

A swap is a contract in which two parties exchange a sequence of future payments.

The classical interest rate swap exchanges:

- floating-rate payments
- fixed-rate payments

## Long Swap

In the course notation, the long swap receives floating and pays fixed.

Long swap payment at Ti:

Ci = Delta T [L(Ti-1, Ti) - R]

where:

- L(Ti-1, Ti) = floating LIBOR rate
- R = fixed swap rate
- Delta T = period length

---

# 11. LIBOR and Zero-Coupon Bonds

Let P(Ti-1, Ti) be the price at Ti-1 of a zero-coupon bond paying 1 at Ti.

Then:

1 + L(Ti-1, Ti)Delta T = 1 / P(Ti-1, Ti)

So:

L(Ti-1, Ti) = [1 / P(Ti-1, Ti) - 1] / Delta T

## Intuition

LIBOR is the simple rate that makes the bond price grow to 1 over the period.

---

# 12. Swap Pricing

A swap is priced as the present value of all swap payments.

Long swap value:

Swap Value = PV(floating leg) - PV(fixed leg)

Using zero-coupon bond prices:

S(t) = P(t,T0) - R Delta T sum from i=1 to n of P(t,Ti) - P(t,Tn)

## Swap Rate

The swap rate is the fixed rate R that makes the initial swap value equal to zero.

At initiation:

PV(floating leg) = PV(fixed leg)

So:

R = [P(0,T0) - P(0,Tn)] / [Delta T sum from i=1 to n of P(0,Ti)]

## Intuition

The fixed rate is chosen so that neither party pays upfront.

This is similar to how the forward price is chosen so that the initial forward value is zero.

---

# 13. Options and Model-Independent Bounds

Options are non-linear derivatives.

Because of this, exact pricing usually requires a mathematical model.

However, no-arbitrage gives useful price bounds.

## Notation

European options:

- c(t) = European call price
- p(t) = European put price

American options:

- C(t) = American call price
- P(t) = American put price

---

# 14. Basic Option Bounds

## American vs European

American options are at least as valuable as European options:

c(t) ≤ C(t)

p(t) ≤ P(t)

## Call Upper Bound

A call cannot be worth more than the underlying:

c(t) ≤ C(t) ≤ S(t)

## Put Upper Bounds

An American put cannot be worth more than the strike:

P(t) ≤ K

A European put cannot be worth more than the discounted strike:

p(t) ≤ Ke^(-r(T-t))

---

# 15. European Option Lower Bounds

For a non-dividend-paying asset:

European call:

c(t) ≥ max[S(t) - Ke^(-r(T-t)), 0]

European put:

p(t) ≥ max[Ke^(-r(T-t)) - S(t), 0]

## Intuition

If an option were priced below these bounds, arbitrage would be possible by combining the option, the stock and risk-free borrowing/lending.

---

# 16. American Call Without Dividends

If the underlying pays no dividends:

C(t) = c(t)

## Meaning

The right to exercise early has no extra value for a call on a non-dividend-paying asset.

## Practical Rule

Do not exercise early.

If you want to exit, sell the call instead.

## Why?

Exercising early destroys time value and forces payment of K earlier than necessary.

---

# 17. Dividends and American Calls

If the underlying pays dividends, early exercise of an American call may become valuable.

Reason:

Exercising before the dividend date allows the holder to receive the dividend.

Therefore:

C(t) may be greater than c(t)

Dividend-paying American calls often require numerical pricing.

---

# 18. American Puts

American puts may be more valuable than European puts, even without dividends.

Reason:

If the stock price becomes very low, exercising the put gives cash K immediately.

That cash can then earn interest.

Therefore:

P(t) may be greater than p(t)

---

# 19. Put-Call Parity

For European options on a non-dividend-paying asset:

c(t) + Ke^(-r(T-t)) = p(t) + S(t)

## Conditions

Put-call parity applies to:

- European call
- European put
- same underlying
- same strike
- same maturity
- no dividends

## Intuition

Two portfolios have the same payoff at maturity:

Portfolio A:

- long call
- cash equal to present value of K

Portfolio B:

- long put
- one share of stock

At maturity, both portfolios are worth:

max[S(T), K]

Therefore, by law of one price, their prices must be equal today.

---

# 20. American Put-Call Bounds

For American options on a non-dividend-paying asset:

S(t) - K ≤ C(t) - P(t) ≤ S(t) - Ke^(-r(T-t))

Unlike European options, we get bounds rather than equality.

Reason:

American exercise flexibility changes the value of the put.

---

# 21. Main Conceptual Differences

## Linear vs Non-Linear Derivatives

Linear derivatives:

- forwards
- futures
- swaps

They can often be priced exactly by no-arbitrage.

Non-linear derivatives:

- options

They usually need models for exact prices.

## Exact Price vs Bounds

Forwards, futures and swaps:

- exact model-independent price

Options:

- no-arbitrage bounds
- exact price requires a model

## Arbitrage vs Forecasting

No-arbitrage pricing does not require predicting the future.

It only requires that equivalent cash flows have equivalent prices.

---

# 22. What You Must Know for the Exam

You should be able to:

- derive the no-dividend forward price
- explain why dividends reduce forward prices
- price a currency forward
- explain mark-to-market for futures
- explain when futures and forwards have equal prices
- define and value the basic structure of an interest rate swap
- explain the relation between LIBOR and zero-coupon bonds
- define the swap rate
- state basic option bounds
- explain early exercise for American calls and puts
- state and use put-call parity
- distinguish exact pricing from no-arbitrage bounds

---

# 23. Core Formulas

## No-Dividend Forward

F(t) = S(t)e^(r(T-t))

## Deterministic Dividends

F(t) = [S(t) - D(t)]e^(r(T-t))

## Continuous Dividend Yield

F(t) = S(t)e^((r-q)(T-t))

## Currency Forward

F(t) = S(t)e^((r-r_f)(T-t))

## Futures Payoff

Total payoff ≈ S(T) - F(t)

## Swap Payment

Ci = Delta T [L(Ti-1, Ti) - R]

## LIBOR from Bond Price

L(Ti-1, Ti) = [1 / P(Ti-1, Ti) - 1] / Delta T

## Swap Rate

R = [P(0,T0) - P(0,Tn)] / [Delta T sum from i=1 to n of P(0,Ti)]

## Call Bounds

c(t) ≤ C(t) ≤ S(t)

c(t) ≥ max[S(t) - Ke^(-r(T-t)), 0]

## Put Bounds

p(t) ≤ P(t) ≤ K

p(t) ≤ Ke^(-r(T-t))

p(t) ≥ max[Ke^(-r(T-t)) - S(t), 0]

## Put-Call Parity

c(t) + Ke^(-r(T-t)) = p(t) + S(t)

## American Put-Call Bounds

S(t) - K ≤ C(t) - P(t) ≤ S(t) - Ke^(-r(T-t))

---

# Final Intuition

Module 3 is about pricing through replication and no-arbitrage.

For linear derivatives, replication gives exact prices.

For options, no-arbitrage gives bounds and relationships, but exact pricing requires a model.

This prepares the transition into later modules, where option pricing models are introduced.
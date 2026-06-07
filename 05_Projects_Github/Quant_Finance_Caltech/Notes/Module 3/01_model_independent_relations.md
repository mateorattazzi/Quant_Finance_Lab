# Linear Derivatives — Model-Independent Pricing

## Key Idea

Some derivatives can be priced without specifying a stochastic model for the underlying asset.

These are called model-independent pricing relations.

The reason is that their payoffs are linear and can be replicated using:

- the underlying asset
- the risk-free asset
- no-arbitrage arguments

Main examples:

- forwards
- futures
- swaps

The pricing does not require assumptions about:

- volatility
- drift
- probability distribution
- Brownian motion
- expected future price

---

# 1. Forward Contract

## Definition

A forward contract is an agreement to buy or sell an underlying asset at a future date T for a price fixed today.

For a long forward:

Payoff at maturity:

S(T) - F(t)

where:

- S(T) = underlying price at maturity
- F(t) = forward price agreed at time t

## Important

A forward contract has zero value when it is initiated.

This means:

- no money is exchanged at time t
- F(t) is chosen so that the initial value of the contract is zero

---

# 2. Risk-Free Asset Notation

Let:

B(t,T)

be the amount received at time T from investing 1 dollar risk-free at time t.

With continuous compounding:

B(t,T) = e^(r(T-t))

This is the growth factor from t to T.

---

# 3. Forward Price Without Dividends

## Formula

For an asset with no dividends or intermediate payments:

F(t) = S(t)B(t,T)

With continuous compounding:

F(t) = S(t)e^(r(T-t))

## Intuition

Buying the asset today costs S(t).

If we instead put S(t) in the bank until T, it grows to:

S(t)B(t,T)

The forward price must equal this amount.

Otherwise, arbitrage is possible.

---

# 4. No-Arbitrage Logic

## If the forward price is too high

If:

F(t) > S(t)B(t,T)

then the forward is expensive.

Arbitrage strategy:

- borrow S(t)
- buy the underlying asset
- short the forward contract

At maturity:

- deliver the asset into the forward
- receive F(t)
- repay the loan S(t)B(t,T)

Since F(t) is larger, there is risk-free profit.

## If the forward price is too low

If:

F(t) < S(t)B(t,T)

then the forward is cheap.

Arbitrage strategy:

- short sell the underlying asset
- invest S(t) in the risk-free asset
- go long the forward contract

At maturity:

- use the bank account to pay F(t)
- receive the asset through the forward
- return the asset to close the short position

Since the bank account is larger than the forward price, there is risk-free profit.

## Core Principle

If the forward price is not equal to the no-arbitrage price, arbitrage exists.

Therefore:

F(t) = S(t)B(t,T)

---

# 5. Perfect Market Assumptions

These pricing relations assume a perfect market.

That means:

- no transaction costs
- no taxes
- borrowing and lending at the same risk-free rate
- free short selling
- no margin restrictions
- no default risk
- no bid-ask spreads

In real markets, the formula may not hold exactly because of frictions.

---

# 6. Forward Price With Deterministic Dividends

If the underlying pays known dividends before maturity, the forward price is lower.

Reason:

The holder of the forward does not receive dividends before maturity.

The holder of the stock does receive dividends.

## Formula

Let D(t) be the present value of all deterministic dividends paid before T.

Then:

F(t) = [S(t) - D(t)]B(t,T)

With continuous compounding:

F(t) = [S(t) - PV(dividends)]e^(r(T-t))

## Intuition

The forward is priced on the stock value excluding the dividends that the forward holder will not receive.

So we subtract the present value of dividends from the spot price.

---

# 7. Continuous Dividend Yield

Sometimes dividends are modeled as a continuous dividend yield q.

This is common for indices, where dividends are frequent and spread across many stocks.

## Formula

F(t) = S(t)e^((r-q)(T-t))

where:

- r = risk-free rate
- q = continuous dividend yield

## Intuition

The dividend yield reduces the forward price.

Higher q means lower forward price.

---

# 8. Currency Forwards

A foreign currency can be treated like an asset that pays a dividend yield.

Why?

If you hold foreign currency, you can deposit it in a foreign bank and earn the foreign risk-free rate.

So the foreign risk-free rate acts like a dividend yield.

## Formula

For a currency forward:

F(t) = S(t)e^((r - r_f)(T-t))

where:

- S(t) = current exchange rate in domestic currency per unit of foreign currency
- r = domestic risk-free rate
- r_f = foreign risk-free rate
- T-t = time to maturity

## Intuition

The domestic rate increases the forward price.

The foreign rate decreases the forward price.

If:

r > r_f

then the forward exchange rate is higher than the spot exchange rate.

If:

r < r_f

then the forward exchange rate is lower than the spot exchange rate.

---

# 9. Futures

## Definition

A futures contract is similar to a forward contract, but it is traded through an exchange.

Main features:

- standardized contract
- exchange reduces counterparty risk
- daily mark-to-market
- margin account required

## Forward vs Future

Forward contract:

- private agreement
- usually OTC
- payoff settled at maturity
- counterparty risk exists

Futures contract:

- exchange-traded
- standardized
- gains and losses settled daily
- lower counterparty risk

---

# 10. Mark-to-Market

## Definition

Mark-to-market means that gains and losses are settled daily.

If the futures price increases:

- the long futures position gains
- the short futures position loses

If the futures price decreases:

- the long futures position loses
- the short futures position gains

## Important

In a forward contract, the entire payoff is settled at maturity.

In a futures contract, the payoff is split into daily gains and losses.

---

# 11. Futures Payoff

Ignoring interest earned on the margin account, the total futures payoff equals:

S(T) - F(t)

This is the same total payoff as a forward contract.

Reason:

Daily price changes telescope.

The intermediate terms cancel, leaving only:

S(T) - F(t)

At maturity:

F(T) = S(T)

Otherwise, arbitrage would be possible.

---

# 12. Forward Price vs Futures Price

## Key Result

If interest rates are deterministic, then:

Futures price = Forward price

## Why?

Even though futures cash flows occur daily and forward cash flows occur only at maturity, deterministic interest rates allow the futures cash flows to be reinvested or financed in a known way.

Therefore, the forward payoff can be replicated using futures.

## Important Exception

If interest rates are random, futures and forward prices may differ.

The difference depends on the correlation between:

- the underlying asset price
- the interest rate

## Intuition

With futures, gains and losses arrive daily.

If gains tend to arrive when interest rates are high, the futures contract may be more valuable.

If gains tend to arrive when interest rates are low, it may be less valuable.

---

# 13. Swaps

## Definition

A swap is a contract where two parties exchange a series of future payments.

A classical interest rate swap exchanges:

- floating-rate payments
- fixed-rate payments

## Long Swap Position

In this course, the long swap position is defined as:

- receiving the floating rate
- paying the fixed rate

The floating rate is usually represented by LIBOR.

The fixed rate is denoted by R.

---

# 14. Interest Rate Swap Payoff

Payments happen at dates:

T1, T2, ..., Tm

Assume each period has the same length:

Delta T

At each payment date Ti, the long swap receives the floating rate for the period and pays the fixed rate.

The payment is proportional to:

L(Ti-1, Ti) - R

where:

- L(Ti-1, Ti) = floating LIBOR rate for the period
- R = fixed swap rate
- Delta T = length of each period

So each payment has the form:

Ci = Delta T [L(Ti-1, Ti) - R]

This is usually multiplied by a notional principal.

---

# 15. LIBOR and Zero-Coupon Bonds

LIBOR can be expressed using zero-coupon bond prices.

Let:

P(Ti-1, Ti)

be the price at time Ti-1 of a zero-coupon bond maturing at Ti and paying 1.

Then the LIBOR rate for the period satisfies:

1 + L(Ti-1, Ti) Delta T = 1 / P(Ti-1, Ti)

Therefore:

L(Ti-1, Ti) = [1 / P(Ti-1, Ti) - 1] / Delta T

## Intuition

The LIBOR rate is the simple rate that makes an investment grow from the bond price to 1 over the period.

---

# 16. Swap Pricing Logic

A swap is basically a portfolio of forward-rate agreements.

To price the swap:

1. price each future payment
2. discount it to today
3. sum the values of all payments

Total swap value:

Swap Value = sum of PV of all swap payments

## Important

The swap is linear because each payment is linear in the interest rate.

This is why swaps belong with forwards and futures as linear derivatives.

---

# 17. Fixed Leg vs Floating Leg

An interest rate swap can be decomposed into two legs:

## Floating Leg

The floating leg pays the market floating rate.

It resets periodically.

## Fixed Leg

The fixed leg pays the fixed rate R.

## Long Swap Value

For the long swap:

Value = PV(floating leg) - PV(fixed leg)

because the long party receives floating and pays fixed.

---

# 18. Swap Rate

## Definition

The swap rate is the fixed rate R that makes the initial swap value equal to zero.

At initiation:

PV(floating leg) = PV(fixed leg)

Therefore:

Swap Value = 0

This is similar to a forward contract, where the forward price is chosen so that the initial contract value is zero.

## Intuition

The fixed rate is chosen so that neither party pays anything upfront.

---

# 19. Swaps and Bonds

Interest rate swaps can be priced using zero-coupon bond prices.

This is because floating rates such as LIBOR are related to discount bond prices.

The value of each future swap payment can be expressed using bond prices.

## Important

This creates a link between:

- swaps
- zero-coupon bonds
- forward rates
- no-arbitrage pricing

---

# 20. Model-Independent Pricing

## Definition

A pricing relation is model-independent if it does not require a probability model for the underlying variable.

For forwards, futures and swaps, prices are determined by:

- spot prices
- interest rates
- dividends
- foreign interest rates
- zero-coupon bond prices
- no-arbitrage

We do not need a stochastic model for S(t) or interest rates at this stage.

---

# 21. Common Confusions

## Forward Price vs Forward Contract Value

Forward price:

- the delivery price agreed in the contract

Forward contract value:

- the current value of an existing forward contract

At initiation, the contract value is zero.

After initiation, the contract value can be positive or negative.

## Forward Price vs Expected Future Price

The forward price is not necessarily what the market expects S(T) to be.

It is the no-arbitrage delivery price.

## Holding the Stock vs Holding a Forward

Holding the stock gives ownership today.

Holding a forward gives ownership only at maturity.

Therefore, if the stock pays dividends before maturity, the forward is worth less than the stock financed forward.

## Futures vs Forwards

They may have the same total payoff, but the timing of cash flows differs.

Futures settle daily.

Forwards settle at maturity.

## Forward/Futures vs Swaps

A swap can be understood as a sequence of forward-type contracts.

Instead of one future exchange, there are several future payment exchanges.

## Floating Rate vs Fixed Rate

Floating rate:

- changes over time
- resets at each period

Fixed rate:

- agreed in advance
- remains constant during the swap

## Swap Value vs Swap Rate

Swap value:

- current value of the swap contract

Swap rate:

- fixed rate R that makes the initial swap value zero

## Arbitrage vs Speculation

Arbitrage:

- risk-free profit from mispricing

Speculation:

- profit depends on a future market view

---

# 22. Exam Notes

You should be able to:

- define a forward contract
- explain why the initial value of a forward is zero
- derive the no-dividend forward price
- explain why dividends reduce the forward price
- price a forward with deterministic dividends
- price a forward with continuous dividend yield
- price a currency forward
- explain the difference between forward and futures contracts
- explain daily mark-to-market
- understand when futures and forwards have the same price
- explain why random interest rates can create a difference between futures and forwards
- define an interest rate swap
- explain fixed leg and floating leg
- explain why a swap is a sequence of forward-type payments
- explain the relation between LIBOR and zero-coupon bond prices
- explain that the swap rate makes the initial swap value equal to zero
- understand that swap value equals PV(floating leg) minus PV(fixed leg)

---

# 23. Core Formulas

## No-Dividend Forward

F(t) = S(t)B(t,T)

With continuous compounding:

F(t) = S(t)e^(r(T-t))

## Deterministic Dividends

F(t) = [S(t) - D(t)]B(t,T)

With continuous compounding:

F(t) = [S(t) - PV(dividends)]e^(r(T-t))

## Continuous Dividend Yield

F(t) = S(t)e^((r-q)(T-t))

## Currency Forward

F(t) = S(t)e^((r-r_f)(T-t))

## Futures Payoff

Total payoff ≈ S(T) - F(t)

## Forward-Futures Equivalence

If interest rates are deterministic:

Futures price = Forward price

## LIBOR from Zero-Coupon Bond Price

1 + L(Ti-1, Ti) Delta T = 1 / P(Ti-1, Ti)

Therefore:

L(Ti-1, Ti) = [1 / P(Ti-1, Ti) - 1] / Delta T

## Swap Payment

Ci = Delta T [L(Ti-1, Ti) - R]

## Swap Value

Long Swap Value = PV(floating leg) - PV(fixed leg)

---

# Final Intuition

Forwards, futures and swaps are linear derivatives.

Their prices are determined mainly by no-arbitrage and replication.

A forward is priced by comparing buying the asset today versus agreeing to buy it later.

A future is similar to a forward, but gains and losses are settled daily.

A swap is a sequence of forward-type exchanges, usually exchanging floating-rate payments for fixed-rate payments.

The central idea is always the same:

if a payoff can be replicated, its price is determined by the cost of replication.
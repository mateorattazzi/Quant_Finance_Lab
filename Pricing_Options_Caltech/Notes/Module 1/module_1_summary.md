# Unit 1 Summary — Stocks, Bonds, Derivatives and Option Payoffs

## Purpose of Unit 1

This unit introduces the basic financial instruments used in option pricing:

- stocks
- bonds
- forwards
- swaps
- options
- option combinations

The main goal is to understand how different contracts create different payoff structures.

---

# 1. Basic Securities vs Derivatives

## Basic Securities

Basic securities are instruments whose value does not depend on another financial contract.

Main examples:

- stocks
- bonds

## Derivatives

A derivative is a contract whose value depends on an underlying asset.

Examples of underlying assets:

- stock price
- bond price
- interest rate
- exchange rate
- commodity price
- index level

Important distinction:

A derivative in finance means “derived from an underlying asset”, not a mathematical derivative.

---

# 2. Stocks and Bonds

## Stocks

A stock represents ownership in a company.

Main uncertainty:

- future stock price is unknown

Stocks may also pay dividends.

## Bonds

A bond is a loan to a company or government.

Known elements:

- face value / principal
- coupon payments
- maturity date

Main risk:

- default risk
- market price risk before maturity

A bond can have known promised payments, but its market price before maturity can still move randomly.

---

# 3. Forwards

## Definition

A forward contract is an agreement to buy or sell an underlying asset in the future at a price agreed today.

Notation:

- S(T) = spot price at maturity
- F = forward price
- T = maturity

## Long Forward

Obligation to buy the underlying at maturity.

Payoff:

S(T) - F

Profits when:

S(T) > F

## Short Forward

Obligation to sell the underlying at maturity.

Payoff:

F - S(T)

Profits when:

S(T) < F

## Key Idea

A forward has zero value at initiation.

No money is paid at time 0.

The contract is settled at maturity.

## Forward vs Option

Forward:

- obligation
- zero initial value

Option:

- right, not obligation
- positive initial premium

This difference is fundamental.

---

# 4. Swaps

## Definition

A swap is an agreement to exchange two series of payments.

A classic example is the interest rate swap.

## Interest Rate Swap

One party pays:

- fixed interest payments

The other party pays:

- floating interest payments

The notional amount is used to compute payments but is usually not exchanged.

## Why Swaps Exist

In theory, fixed and floating payments should be priced fairly.

In practice, swaps exist because of:

- different borrowing costs
- market imperfections
- regulation
- institutional constraints
- credit risk differences

## Important Intuition

A swap changes economic exposure without necessarily changing asset ownership.

Example:

A pension fund may keep stocks but swap stock returns for fixed-income-like returns.

---

# 5. Options

## Definition

An option gives the holder the right, but not the obligation, to buy or sell the underlying asset.

## Call Option

Right to buy the underlying.

Long call payoff:

max(S(T) - K, 0)

## Put Option

Right to sell the underlying.

Long put payoff:

max(K - S(T), 0)

## Premium

The premium is the price paid to buy the option.

Profit equals payoff minus premium.

---

# 6. European vs American Options

## European Option

Can only be exercised at maturity.

## American Option

Can be exercised at any time before maturity.

## Why This Matters

European options are easier to price mathematically.

American options usually require numerical methods.

This is why Black-Scholes theory usually starts with European options.

---

# 7. Moneyness

## At the Money

The strike price is close to the current underlying price.

For a call:

S = K

## In the Money

Immediate exercise would generate value.

For a call:

S > K

For a put:

S < K

## Out of the Money

Immediate exercise would not generate value.

For a call:

S < K

For a put:

S > K

---

# 8. Long vs Short Option Positions

## Long Option

The buyer pays premium.

Potential result:

- limited loss
- possible large gain

Maximum loss:

premium paid

## Short Option

The seller receives premium.

Potential result:

- limited gain
- potentially large loss

Selling options can require collateral or margin.

---

# 9. Implicit Leverage

Options create implicit leverage.

Small changes in the underlying can generate very large percentage changes in the option position.

Example:

A stock may rise only 5%, while a call option position may return 100%.

But the reverse is also true:

The option can lose most or all of its value even when the stock does not move much.

## Core Idea

Options magnify both upside and downside.

This makes them powerful but risky.

---

# 10. Options as Insurance

Put options can be used as downside protection.

Example:

An executive receives company stock but cannot sell it.

Buying put options can protect against a fall in the stock price.

## Insurance Analogy

If the bad event does not happen:

- the option expires worthless
- the premium is lost

If the bad event happens:

- the option pays off
- losses are reduced

---

# 11. Structured Products

Some bank products contain hidden option-like payoffs.

Example:

Equity-linked deposit = bond + call option on an index

This means the investor receives:

- capital protection
- some participation in market upside

## Important Insight

Many products that look simple are actually combinations of bonds and options.

Banks need option pricing models to decide whether these products are profitable.

---

# 12. Option Combinations

Options can be combined to create specific payoff shapes.

This is called payoff engineering.

## Bull Spread

Used when expecting the underlying to rise.

Created with calls:

- buy call with lower strike K1
- sell call with higher strike K2

Result:

- limited loss
- limited profit
- cheaper than buying only a call

## Bear Spread

Used when expecting the underlying to fall.

Created with puts:

- buy put with higher strike K2
- sell put with lower strike K1

Result:

- limited loss
- limited profit

## Butterfly Spread

Used when expecting the underlying to stay close to a central price.

Created with calls:

- buy 1 call with strike K1
- sell 2 calls with strike K2
- buy 1 call with strike K3

where:

K2 = (K1 + K3) / 2

Result:

- profit if price stays near K2
- loss if price moves too far away

## Calendar Spread

Uses options with:

- same strike
- different maturities

Example:

- sell shorter maturity call
- buy longer maturity call

Unlike simple spreads, the payoff can be curved because the longer maturity option still has time value.

## Straddle

Created by buying:

- one call
- one put

with same strike and maturity.

Used when expecting high volatility.

The investor profits if the underlying moves strongly up or down.

## Strangle

Similar to a straddle but uses different strikes.

Usually:

- buy lower strike put
- buy higher strike call

It is usually cheaper than a straddle but requires a larger price move to profit.

---

# 13. Static Replication

The combinations in this unit are static strategies.

Static means:

- positions are created at time 0
- no rebalancing before maturity

This is different from dynamic hedging, which appears later in the course.

## Core Idea

Options are building blocks.

By combining calls, puts, stocks and bonds, investors can create customized payoff profiles.

---

# 14. Most Important Concepts to Remember

## Linear vs Non-Linear Payoffs

Linear instruments:

- forwards
- swaps

Non-linear instruments:

- options

## Obligation vs Right

Forward:

- obligation

Option:

- right, not obligation

## Payoff vs Profit

Payoff:

- value received at maturity

Profit:

- payoff minus initial cost

## Hedging vs Speculation

The same derivative can be used for:

- reducing risk
- increasing risk

The instrument is neutral.

The strategy determines the risk.

## Pricing Logic

The course will later price derivatives using:

- no-arbitrage
- replication
- binomial trees
- stochastic models
- Black-Scholes

---

# Core Intuition of Unit 1

Derivatives allow investors to reshape risk.

Forwards and swaps transfer linear risk.

Options create non-linear exposure.

Option combinations allow investors to design almost any desired payoff shape.
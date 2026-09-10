# Options — Calls and Puts

## Definition

An option gives the holder the right, but not the obligation, to buy or sell an underlying asset.

## Main Types of Options

## Call Option

A call option gives the holder the right to buy the underlying asset.

## Put Option

A put option gives the holder the right to sell the underlying asset.

## Forward vs Option

A forward contract creates an obligation.

An option creates a choice.

This flexibility gives options positive initial value.

## European vs American Options

## European Option

Can only be exercised at maturity.

## American Option

Can be exercised at any time before maturity.

## Bermudan Option

Can be exercised only at specific dates during the life of the option.

## Important Observation

Most theoretical pricing models, such as Black-Scholes, focus on European options because they are mathematically simpler.

American options usually require numerical methods.

## Possible Underlyings

Options can be written on almost anything.

Examples:

- stocks
- stock indices
- futures
- currencies
- interest rates
- energy prices
- mortgages
- weather variables

## Insurance Intuition

Derivatives often act as financial insurance.

Example:

A ski resort may buy derivatives that pay if there is no snow.

## Exotic Options

Any option that is not a plain vanilla call or put is usually called an exotic option.

## Asian Options

An Asian option has a payoff that depends on the average price of the underlying during the life of the option.

Asian options reduce payoff volatility.

This is useful when the underlying price is highly volatile, such as electricity prices.

## Lookback Options

A lookback option has a payoff that depends on the maximum or minimum price of the underlying during the life of the option.

## Barrier Options

A barrier option only pays if the underlying reaches a certain level.

Barrier options are usually cheaper than standard options because they pay in fewer scenarios.

## Basket Options

A basket option is written on multiple assets.

Examples:

- a portfolio of stocks
- a stock index
- a linear combination of assets

## Mathematical Difficulty

Basket and Asian options are harder to price analytically.

Reason:

sum of exponentials is not equal to an exponential.

This creates difficulties in Black-Scholes style formulas.

Numerical methods can still be used.

## Option Terminology

## Writing an Option

Writing an option means selling an option.

## Premium

The premium is the initial payment made by the buyer of the option.

It can also be called:

- option price
- option value

## Moneyness

## At the Money (ATM)

The strike price is equal to the current underlying price.

## In the Money (ITM)

Exercising the option generates profit.

For a call option:

stock price > strike price

## Out of the Money (OTM)

Exercising the option generates no profit.

For a call option:

stock price < strike price

## Important Quant Finance Ideas

Options create non-linear payoffs.

Unlike forwards and swaps, option gains and losses are asymmetric.

This makes options powerful for:

- hedging
- speculation
- risk management

## Core Intuition

Options allow exposure to upside potential while limiting downside risk.

# Call and Put Option Payoffs

## Call Option

A call option gives the holder the right to buy the underlying asset at the strike price.

## Long Call Position

The buyer of the call option is long the call.

At maturity, there are two possible cases.

## Case 1 — Option Out of the Money

If:

S(T) < K

the holder does not exercise the option.

Reason:

Buying at the strike price would be more expensive than buying directly in the market.

Payoff:

0

Total profit/loss:

- option premium

## Case 2 — Option In the Money

If:

S(T) > K

the holder exercises the option.

The payoff equals:

S(T) - K

Total profit/loss:

S(T) - K - premium

## Call Option Payoff Formula

The payoff of a long call at maturity is:

max(S(T) - K, 0)

Also written as:

(S(T) - K)^+

## Long Call Payoff Shape

Characteristics:

- non-linear payoff
- convex payoff
- upside potential is theoretically unlimited

## Break-Even Point

Break-even occurs when:

stock payoff = premium paid

Example:

- strike = 50
- premium = 6

Break-even:

56

because:

56 - 50 - 6 = 0

## Short Call Position

The seller of the option is short the call.

The payoff is the negative of the long call payoff.

Characteristics:

- limited upside
- potentially unlimited losses

Reason:

Stock price can increase indefinitely.

## Important Trading Insight

Selling call options can be very risky.

Potential losses may become extremely large.

Because of this:

- brokerages require margin accounts
- sellers must hold collateral

## Put Option

A put option gives the holder the right to sell the underlying asset at the strike price.

## Long Put Position

The buyer of the put option is long the put.

## Case 1 — Option In the Money

If:

S(T) < K

the holder exercises the option.

Reason:

Selling at the strike price is better than selling in the market.

Payoff:

K - S(T)

Total profit/loss:

K - S(T) - premium

## Case 2 — Option Out of the Money

If:

S(T) > K

the holder does not exercise.

Payoff:

0

Total profit/loss:

- premium

## Put Option Payoff Formula

The payoff of a long put at maturity is:

max(K - S(T), 0)

Also written as:

(K - S(T))^+

## Long Put Payoff Shape

Characteristics:

- non-linear payoff
- profits when stock price decreases
- downside protection

## Put Option Break-Even

Example:

- strike = 50
- premium = 8

Break-even:

42

because:

50 - 42 - 8 = 0

## Short Put Position

The seller of the put option is short the put.

The payoff is the negative of the long put payoff.

Characteristics:

- limited profit
- losses increase as stock price falls

However, maximum loss is bounded because stock prices cannot go below zero.

## Important Quant Finance Ideas

Options have asymmetric payoffs.

Unlike forwards and swaps:

- gains and losses are not symmetric

This creates non-linear risk exposure.

## Convexity

Call and put options create convex payoff structures.

Convexity is one of the most important concepts in derivatives pricing.

## Core Intuition

A call option gives exposure to upward price movements with limited downside.

A put option gives protection against downward price movements.

# Options, Leverage and Hedging

## Implicit Leverage in Options

Options create implicit leverage.

This means that small investments in options can generate:

- very large profits
- very large losses

compared to trading the underlying asset directly.

## Example — Stock vs Call Option

Initial situation:

- stock price today = 100
- call option price = 2.5
- strike price = 100
- investment amount = 100

Possible choices:

- buy 1 stock
- buy 40 call options

## Possible Outcomes at Maturity

## Good State

Stock price:

105

Stock return:

+5%

Option payoff per contract:

105 - 100 = 5

Total option payoff:

40 × 5 = 200

Initial investment:

100

Profit:

100

Option return:

+100%

## Intermediate State

Stock price:

101

Stock return:

+1%

Option payoff per contract:

1

Total option payoff:

40

Initial investment:

100

Profit/loss:

40 - 100 = -60

Option return:

-60%

Important observation:

Even though the stock increased, the option position still loses money.

## Bad State

Stock price:

98

The call option expires out of the money.

Option payoff:

0

Loss:

-100%

## Important Quant Finance Idea

Options magnify returns.

This creates:

- higher upside potential
- higher downside risk

This effect is called implicit leverage.

## Structured Products and Hidden Options

Option-like payoffs often appear inside seemingly simple financial products.

## Example — Equity Linked Deposit

A bank offers:

- invest 10,000
- maturity = 5.5 years

If the stock index stays below a certain level:

- investor only receives original investment

If the index rises above the level:

- investor receives additional return linked to index performance

## Example Formula

If index performance is positive:

Final Value = 10,000 + 10,000 × 0.7 × index return

Example:

Index moves from 1300 to 1500.

Final value is approximately:

11,077

## Important Insight

This product is essentially:

- a bond
- plus a call option on the index

The payoff is non-linear.

Therefore, structured products are often combinations of simpler instruments and options.

## Role of Quantitative Finance

Banks need mathematical models to determine:

- strike levels
- participation rates
- pricing
- profitability

Models such as Black-Scholes help determine whether the product is fairly priced.

## Competition Between Banks

In competitive markets, similar products tend to have similar pricing.

This indirectly reflects option pricing theory in practice.

## Put Options as Insurance

Put options naturally provide downside protection.

## Executive Compensation Example

An executive receives company stock as compensation.

Problem:

- stock value may fall
- shares may be restricted from sale

## Hedging with Put Options

Solution:

- buy put options on the stock

Example:

- 100 company shares
- buy 50 put options
- strike price = 150

This guarantees the ability to sell part of the shares at 150.

## Insurance Analogy

Put options work like insurance.

If the stock price rises:

- put option expires worthless
- premium is lost

If the stock price falls:

- put option gains value
- losses are partially offset

## Example

Stock price after five years:

100

Loss on shares:

50 × 100 = 5,000

Gain from put options:

50 × 50 = 2,500

minus the option premium.

## Trade-Off

Hedging reduces risk but also reduces expected profit.

This creates a balance between:

- protection
- upside exposure

## Important Quant Finance Ideas

## Options as Insurance

Put options are natural hedging instruments against downside risk.

## Non-Linear Risk Management

Options allow investors to reshape risk exposure in ways impossible using only stocks and bonds.

## Core Intuition

Options are not only speculative instruments.

They are fundamental tools for:

- hedging
- insurance
- portfolio risk management
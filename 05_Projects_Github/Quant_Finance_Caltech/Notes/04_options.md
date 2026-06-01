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
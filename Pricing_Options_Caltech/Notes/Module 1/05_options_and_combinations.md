# Options Combinations — Spreads

## Main Idea

Options can be combined to create specific payoff profiles.

A portfolio may include:

- calls
- puts
- stocks
- bonds

The goal is to design the payoff we want at maturity.

## Bull Spread

A bull spread is a strategy used when the investor expects the underlying price to increase.

It creates:

- limited profit if the underlying goes up
- limited loss if the underlying goes down

## Bull Spread Using Calls

To create a bull spread with calls:

- buy a call with lower strike K1
- sell a call with higher strike K2

where:

K1 < K2

Both options have:

- same underlying
- same maturity

## Bull Spread Intuition

The investor benefits if the underlying rises.

However, the profit is capped because the investor sold the higher strike call.

This makes the strategy cheaper than simply buying the stock or buying only one call.

## Bull Spread Payoff Regions

There are three relevant cases at maturity.

## Case 1 — S(T) < K1

Both calls expire out of the money.

Payoff from options:

0

Total profit/loss:

premium received from selling K2 call - premium paid for buying K1 call

This is usually negative.

## Case 2 — K1 < S(T) < K2

The K1 call is exercised.

The K2 call is not exercised.

Payoff:

S(T) - K1

Total profit/loss increases linearly with S(T).

## Case 3 — S(T) > K2

Both calls are exercised.

The stock price terms cancel out.

Payoff:

K2 - K1

Profit is capped.

## Bull Spread Break-Even Example

Example:

- K1 = 50
- K2 = 60
- price of K1 call = 10
- price of K2 call = 6

Initial net cost:

10 - 6 = 4

Break-even:

54

because:

54 - 50 - 4 = 0

## Bull Spread Using Puts

A bull spread can also be created using puts.

To create it with puts:

- buy a put with strike K1
- sell a put with strike K2

where:

K1 < K2

The final payoff shape is similar to the bull spread created with calls.

## Bear Spread

A bear spread is used when the investor expects the underlying price to decrease.

It creates:

- limited profit if the underlying goes down
- limited loss if the underlying goes up

## Bear Spread Using Puts

To create a bear spread with puts:

- buy a put with higher strike K2
- sell a put with lower strike K1

where:

K1 < K2

## Bear Spread Intuition

The investor benefits if the underlying falls.

However, profit is capped because of the option sold.

## Bear Spread Payoff Regions

There are three relevant cases at maturity.

## Case 1 — S(T) < K1

Both puts are exercised.

The stock price terms cancel out.

The payoff is related to:

K2 - K1

This is the maximum profit region.

## Case 2 — K1 < S(T) < K2

Only the K2 put is exercised.

The payoff decreases linearly as S(T) increases.

## Case 3 — S(T) > K2

Both puts expire out of the money.

Payoff from options:

0

Total profit/loss depends only on the initial premiums paid and received.

## Bear Spread Using Calls

A bear spread can also be created using calls.

To create it with calls:

- buy a call with higher strike K2
- sell a call with lower strike K1

where:

K1 < K2

## Butterfly Spread

A butterfly spread is used when the investor expects the underlying price to stay close to a central value.

It creates profit if the underlying does not move too much.

## Butterfly Spread Using Calls

To create a butterfly spread with calls:

- buy 1 call with strike K1
- sell 2 calls with strike K2
- buy 1 call with strike K3

where:

K1 < K2 < K3

Usually:

K2 is in the middle of K1 and K3.

## Butterfly Spread Intuition

The investor profits if the stock price stays close to K2.

The investor loses if the stock price moves too far up or down.

Both profit and loss are limited.

## Butterfly Spread Using Puts

A butterfly spread can also be created using puts:

- buy 1 put with strike K1
- sell 2 puts with strike K2
- buy 1 put with strike K3

where:

K1 < K2 < K3

## Important Quant Finance Ideas

## Payoff Engineering

Option combinations allow investors to engineer specific payoff shapes.

This is one of the most important ideas in derivatives.

## Limited Risk / Limited Reward

Spreads are often designed to limit both:

- maximum loss
- maximum profit

## Same Payoff, Different Instruments

The same payoff can often be created using different combinations of calls and puts.

This idea will be important later for:

- no-arbitrage pricing
- put-call parity
- replication

## Core Intuition

Options can be combined like building blocks.

By adding long and short positions, we can design the exact payoff profile we want.

# Options Combinations — Part 2

## Calendar Spread

A calendar spread uses options with:

- the same strike price
- different maturities

Example:

- sell a call with maturity T1
- buy a call with maturity T2

where:

T1 < T2

## Key Idea

At time T1, the short call has reached maturity.

The long call has not reached maturity yet, so it still has time value.

This creates a curved payoff rather than a simple piecewise linear payoff.

## Important Observation

Before maturity, the value of a call option is usually:

- smooth
- convex
- above its final payoff shape

As maturity approaches, the option value gets closer to its final payoff.

## Calendar Spread Intuition

A calendar spread can create a payoff similar to a butterfly spread, but smoother.

It depends on:

- market conditions
- time to maturity
- option pricing model

Later in the course, this can be priced using models such as Black-Scholes.

## Butterfly Spread Reminder

A butterfly spread can be created using three strike prices:

K1 < K2 < K3

Usually:

K2 = (K1 + K3) / 2

Using calls:

- buy 1 call with strike K1
- sell 2 calls with strike K2
- buy 1 call with strike K3

The strategy profits when the underlying stays close to K2.

## Bottom Straddle

A bottom straddle is created by buying:

- 1 call
- 1 put

with the same strike price and maturity.

## Bottom Straddle Intuition

The investor profits if the underlying moves significantly:

- upward
- downward

The investor loses if the underlying does not move enough.

## Volatility Bet

A straddle is a bet on high volatility.

The investor does not need to know the direction of the move.

The key idea is:

the stock must move far enough to cover the cost of both options.

## Bottom Strangle

A bottom strangle is similar to a straddle, but uses different strike prices.

Usually:

- buy a put with lower strike
- buy a call with higher strike

This creates a gap between the two strikes.

## Strangle Intuition

The investor profits if the underlying moves far enough up or down.

Compared with a straddle:

- it is usually cheaper
- it requires a larger move to become profitable

## Static Option Strategies

The option combinations studied so far are static strategies.

Static means:

- positions are created at time 0
- no trading is done until maturity

Examples:

- bull spread
- bear spread
- butterfly spread
- straddle
- strangle

Later, the course will introduce dynamic strategies, where positions are adjusted over time.

## Payoff Engineering

The main purpose of option combinations is to engineer desired payoff shapes.

By combining calls, puts, stocks and bonds, investors can create very specific risk exposures.

## Mathematical Result

Under idealized assumptions, many payoff functions can be approximated using combinations of call options.

Assumptions:

- fixed maturity
- call options available for many strike prices
- smooth target payoff function

## Main Formula Intuition

A smooth payoff function can be decomposed into:

- cash position
- stock position
- combination of call options with different strikes

This means that options can act as building blocks for complex payoffs.

## Interpretation

The formula shows that a desired payoff can be replicated using:

1. cash
2. shares of the underlying stock
3. many call options with different strike prices

## Role of the Second Derivative

The second derivative of the target payoff determines how many call options of each strike are needed.

This connects payoff curvature with option exposure.

## Important Quant Finance Ideas

## Static Replication

Static replication means creating a payoff using an initial portfolio that is held until maturity.

## Options as Building Blocks

Call options with different strikes can be combined to approximate many payoff shapes.

## Convexity and Curvature

The curvature of a payoff is linked to option positions.

More curvature usually requires more option-like exposure.

## Core Intuition

Options are not only individual trading products.

They are mathematical building blocks that allow investors to design almost any desired payoff shape.
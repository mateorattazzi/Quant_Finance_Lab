# Forward Contracts

## Definition

A forward contract is an agreement between two parties to exchange an asset in the future.

The exchange happens:

- at a predetermined price
- at a predetermined date

## Purpose of Forward Contracts

The main purpose is to hedge future price uncertainty.

Example:

A farmer can lock today the future selling price of wheat or sugar.

This removes exposure to future price fluctuations.

## Key Terminology

## Underlying Asset

The asset on which the derivative is written.

Examples:

- stock
- commodity
- currency

Notation:

S

## Maturity

The final date of the contract.

Notation:

T

## Forward Price

The price agreed today for the future exchange.

Notation:

F

## Long vs Short Position

## Long Forward

The long position has the obligation to buy the underlying at maturity.

Payoff:

S(T) - F

Profits when:

S(T) > F

## Short Forward

The short position has the obligation to sell the underlying at maturity.

Payoff:

F - S(T)

Profits when:

S(T) < F

## Important Property

Forward contracts are zero-sum games.

One party’s gain is the other party’s loss.

## Initial Value of a Forward

At initiation:

Value = 0

No money is exchanged at time 0.

Cash exchange occurs only at maturity.

This is different from options.

## Spot Price vs Forward Price

## Spot Price

The current market price of the underlying.

At maturity, this is:

S(T)

## Forward Price

The price agreed today for the future transaction.

Notation:

F

## Forward vs Option

## Forward

A forward creates an obligation to buy or sell.

Both parties must execute.

## Option

An option gives the right, but not the obligation, to buy or sell.

Because of this, options usually have positive initial value.

Forwards typically start with zero value.

## Example: Currency Forward

A US company knows it will need €1,000,000 in six months.

To avoid exchange rate uncertainty, it enters a forward contract today.

Result:

The future currency cost becomes known today.

## Forward Payoff Diagram

## Long Forward

Payoff:

S(T) - F

Characteristics:

- linear payoff
- upward sloping payoff line

## Short Forward

Payoff:

F - S(T)

Characteristics:

- mirror image of long payoff
- downward sloping payoff line

## Important Quant Finance Ideas

## Linear Payoff

Forward contracts are linear functions of the underlying asset.

This is different from options, which are non-linear.

## Hedging

Forward contracts are fundamental tools for:

- risk management
- locking future prices
- reducing uncertainty

## Core Intuition

A forward contract transfers future price risk from one party to another.
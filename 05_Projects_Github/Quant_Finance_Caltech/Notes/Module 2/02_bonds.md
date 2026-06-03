# Bonds, Yields, Spot Rates and Forward Rates

## Key Definitions

## Bond

A bond is a contract that promises future payments.

Typical payments:

- coupons during the life of the bond
- face value at maturity

## Face Value

The amount paid at maturity.

Also called:

- principal
- nominal value

## Coupon

A periodic payment made by the bond before maturity.

If a bond has annual coupon C and pays n times per year, each coupon payment is:

C / n

## Maturity

The final date when the bond pays its face value.

## Zero-Coupon Bond

A zero-coupon bond pays no coupons.

It only pays the face value at maturity.

Also called:

- pure discount bond

## Coupon Bond

A coupon bond pays:

- coupons during its life
- face value at maturity

---

# Bond Pricing

## Main Idea

The price of a bond equals the present value of all promised future payments.

Bond price = PV of coupons + PV of face value

## Coupon Bond Price Formula

For a bond with:

- price P
- face value V
- annual coupon C
- n coupon payments per year
- m total coupon periods
- yield y

the price satisfies:

P = V / (1 + y/n)^m + sum from k = 1 to m of (C/n) / (1 + y/n)^k

## Important Point

The unknown in this equation is often y.

This y is the bond yield.

---

# Yield to Maturity

## Definition

Yield to Maturity is the internal rate of return of a bond.

It is the discount rate that makes the present value of the bond’s future payments equal to its current market price.

## Interpretation

Yield is the return implied by:

- the bond price today
- the future coupons
- the face value at maturity

## Important

Yield is not directly paid by the bond.

The bond pays coupons and face value.

Yield is the rate that makes those payments consistent with the observed price.

---

# Price-Yield Relationship

## Core Rule

Bond price and yield move in opposite directions.

If yield increases:

- bond price decreases

If yield decreases:

- bond price increases

## Intuition

A higher yield means future payments are discounted more heavily.

Therefore, the present value is lower.

---

# Coupon Rate vs Yield

## Coupon Rate

The coupon rate determines the cash payments made by the bond.

## Yield

The yield is the implied return based on the bond’s current price.

## Important Difference

Coupon rate determines payments.

Yield determines valuation.

They are not the same concept.

---

# Bonds Trading at Par

## Definition

A bond trades at par when:

Price = Face Value

## Key Result

If the coupon rate equals the yield, the bond trades at par.

Example intuition:

If the bond pays 10% coupons and the market yield is also 10%, then the coupon payments exactly compensate for the required return.

So the bond price equals its face value.

---

# Premium and Discount Bonds

## Premium Bond

A bond trades at a premium when:

Price > Face Value

This usually happens when:

Coupon Rate > Yield

## Discount Bond

A bond trades at a discount when:

Price < Face Value

This usually happens when:

Coupon Rate < Yield

---

# Spot Rates

## Definition

A spot rate is the yield on a zero-coupon bond for a specific maturity.

Example:

The 1-year spot rate is the yield on a 1-year zero-coupon bond.

## Important

Spot rates are maturity-specific.

There is not one single “interest rate”.

There is a different spot rate for each maturity.

---

# Yield Curve

## Definition

The yield curve shows yields for different maturities.

X-axis:

- maturity

Y-axis:

- yield

Also called:

- term structure of interest rates

## Why It Matters

The yield curve describes how interest rates vary across time horizons.

It is central in fixed income pricing.

## Important Difference

Price-yield curve:

- shows bond price as a function of yield for one bond

Yield curve:

- shows yield as a function of maturity across bonds

Do not confuse them.

---

# No-Arbitrage and Bond Replication

## Strong Arbitrage

In a deterministic setting, arbitrage means making a sure positive profit with zero net investment.

## No-Arbitrage Principle

If two portfolios generate the same future cash flows at the same times, they must have the same price today.

Otherwise, arbitrage is possible.

## Replication

Replication means creating the cash flows of one asset using a portfolio of other assets.

If we can replicate a bond’s cash flows, then:

Bond price = cost of replicating portfolio

## Why This Matters

This is the central economic idea of the course.

Derivative pricing later uses the same logic:

Price = cost of replication

---

# Bond Arbitrage Logic

## Main Idea

If a bond is mispriced relative to a replicating portfolio:

- buy the cheap asset
- sell the expensive replicating portfolio

or reverse the trade.

## Important

The future cash flows cancel.

The profit comes from the initial price difference.

This is the basic structure of arbitrage.

---

# Bootstrapping Spot Rates

## Definition

Bootstrapping is the process of deriving spot rates from observed bond prices.

## Logic

If we know:

- the price of a short-maturity zero-coupon bond
- the price of a coupon bond

we can solve for unknown longer-maturity spot rates.

## Intuition

A coupon bond is a package of cash flows at different dates.

Each cash flow should be discounted using the spot rate for its own maturity.

---

# Forward Rates

## Definition

A forward rate is an interest rate agreed today for a future period.

Example:

The rate from year 1 to year 2 implied by today’s bond prices.

## Core Idea

By trading bonds with different maturities today, we can lock in a future borrowing or lending rate.

## Notation

f(i,j) = forward rate between period i and period j

where:

j > i

## Relationship Between Spot Rates and Forward Rates

Investing from today to period j should be equivalent to:

1. investing from today to period i
2. then investing from period i to period j at the forward rate

This gives the no-arbitrage relationship:

(1 + r_j/n)^j = (1 + r_i/n)^i × (1 + f(i,j)/n)^(j-i)

where:

- r_i = spot rate for maturity i
- r_j = spot rate for maturity j
- f(i,j) = forward rate from i to j
- n = compounding frequency

## Simple Annual Compounding Case

If n = 1 and we want the forward rate from year 1 to year 2:

(1 + r_2)^2 = (1 + r_1)(1 + f(1,2))

So:

f(1,2) = (1 + r_2)^2 / (1 + r_1) - 1

---

# Forward Rate Intuition

A forward rate is not necessarily a prediction.

It is the rate implied today by current bond prices.

A trader may believe the future spot rate will be different from today’s forward rate, but that is speculation.

## Important Distinction

Forward rate:

- locked in today through bond prices

Future spot rate:

- unknown future market rate

They are not the same thing.

---

# Common Confusions

## Yield vs Coupon

Coupon is a cash payment.

Yield is an implied return.

## Yield vs Spot Rate

Yield usually refers to the internal rate of return of a coupon bond.

Spot rate refers to a zero-coupon yield for a specific maturity.

## Spot Rate vs Forward Rate

Spot rate starts today and ends at a future maturity.

Forward rate starts in the future and ends later.

## Arbitrage vs Speculation

Arbitrage:

- sure profit
- no future uncertainty
- no net risk

Speculation:

- profit only if your view about the future is correct

Trading based on forward rates can be speculative if it depends on future rates moving as expected.

---

# Exam Notes

You should be able to:

- define zero-coupon bond and coupon bond
- compute bond price as present value of future cash flows
- explain yield to maturity
- explain why price and yield move inversely
- understand when a bond trades at par
- distinguish coupon rate, yield, spot rate and forward rate
- explain the yield curve
- understand bond replication
- identify no-arbitrage logic in bond pricing
- derive a simple forward rate from two spot rates

Important formulas:

Bond price:

P = PV(coupons) + PV(face value)

Zero-coupon bond price:

P = V / (1 + r)^T

Yield to maturity:

the rate y that makes PV of bond cash flows equal to price

Forward rate:

(1 + r_j/n)^j = (1 + r_i/n)^i × (1 + f(i,j)/n)^(j-i)

---

# Link to Quant Finance

Bonds introduce the idea that interest rates depend on maturity.

This is essential because option pricing requires discounting future payoffs.

The no-arbitrage and replication logic used for bonds is the same logic used later for:

- forwards
- options
- binomial trees
- Black-Scholes
- fixed income derivatives

The key lesson is:

If a payoff can be replicated, its price is determined by the cost of replication.
# Module 2 Summary — Interest Rates, Present Value, Bonds and Forward Rates

## 1. Purpose of Module 2

This module introduces the tools needed to price deterministic payoffs.

A deterministic payoff is a future payment whose amount and timing are known.

Main topics:

- future value
- present value
- discounting
- cash flows
- loans
- internal rate of return
- bonds
- yield to maturity
- spot rates
- forward rates
- no-arbitrage pricing

The main idea is:

Pricing means converting future cash flows into today’s value.

---

# 2. Future Value

## Simple Interest

With simple interest:

FV = 1 + rT

where:

- r = annual interest rate
- T = time in years

Simple interest is easy, but less common in financial modeling.

## Discrete Compounding

If interest is compounded n times per year:

FV = (1 + r/n)^m

where:

- r = annual nominal rate
- n = number of compounding periods per year
- m = total number of compounding periods

## Effective Annual Rate

The effective annual rate is the actual one-year return after compounding.

1 + r_effective = (1 + r/n)^n

Important:

More frequent compounding increases the effective annual rate.

## Continuous Compounding

With continuous compounding:

FV = e^(rT)

This convention is very important in quantitative finance because it simplifies later formulas.

---

# 3. Present Value and Discounting

## Present Value

Present value is the value today of a future deterministic payment.

For discrete compounding:

PV = X(T) / (1 + r/n)^m

For continuous compounding:

PV = X(T)e^(-rT)

## Discount Factor

A discount factor converts future value into present value.

Discrete discount factor:

1 / (1 + r/n)^m

Continuous discount factor:

e^(-rT)

## Core Intuition

A future payment is worth less than the same amount today because money today can earn interest.

---

# 4. Law of One Price

## Definition

If two cash flows deliver exactly the same payments at exactly the same future dates, they must have the same price today.

## Why?

If two identical future payoffs had different prices:

- buy the cheaper one
- sell the more expensive one
- lock in a risk-free profit

This would create arbitrage.

## Importance

The law of one price is the foundation of no-arbitrage pricing.

It will later be used to price derivatives and options.

---

# 5. Present Value of Cash Flows

A cash flow is a sequence of payments over time.

The present value of a cash flow is the sum of the present values of all payments.

General idea:

PV = sum of discounted cash flows

Each cash flow must be discounted according to its payment date.

## Constant Cash Flows

If the same payment is made repeatedly, the present value becomes a geometric series.

This is used for:

- loans
- mortgages
- annuities
- coupon bonds

---

# 6. Loans and Amortization

## Fixed-Rate Loan

A fixed-rate loan can be seen as a present value problem.

The borrower receives money today and repays it through equal future payments.

The payment amount is chosen so that:

Loan value = PV of future payments

## Loan Balance Formula

Each period:

New balance = old balance × (1 + period rate) - payment

Meaning:

1. interest is added
2. payment is subtracted

## APR vs Interest Rate

The quoted mortgage interest rate is the contractual borrowing rate.

APR includes additional fees and gives a better measure of the total borrowing cost.

Usually:

APR > quoted interest rate

---

# 7. Internal Rate of Return

## Definition

The internal rate of return is the rate that makes the net present value of a cash flow equal to zero.

IRR solves:

NPV = 0

## Intuition

IRR is the implied return of a project or investment.

It is not directly given by the market.

It is solved from the cash flows.

## Why It Matters

Bond yield is defined as the internal rate of return of a bond.

---

# 8. Bonds

## Bond

A bond is a contract that promises future payments.

Usually:

- coupon payments before maturity
- face value at maturity

## Face Value

The amount paid at maturity.

Also called:

- principal
- nominal value

## Coupon

The periodic payment made by the bond.

If the annual coupon is C and the bond pays n times per year, each coupon is:

C / n

## Zero-Coupon Bond

A zero-coupon bond pays no coupons.

It only pays face value at maturity.

Also called:

- pure discount bond

## Coupon Bond

A coupon bond pays:

- coupons during its life
- face value at maturity

---

# 9. Bond Pricing

## Main Formula

Bond price equals the present value of all future payments.

P = PV(coupons) + PV(face value)

For a coupon bond:

P = V / (1 + y/n)^m + sum from k = 1 to m of (C/n) / (1 + y/n)^k

where:

- P = bond price today
- V = face value
- C = annual coupon
- n = coupon payments per year
- m = total coupon periods
- y = yield to maturity

---

# 10. Yield to Maturity

## Definition

Yield to maturity is the internal rate of return of a bond.

It is the rate y that makes the present value of the bond’s future payments equal to the current price.

## Important

Yield is not the same as coupon.

Coupon determines the payments.

Yield is the return implied by the current bond price.

## Price-Yield Relationship

Bond price and yield move in opposite directions.

If yield increases:

- price decreases

If yield decreases:

- price increases

Reason:

A higher yield means future payments are discounted more heavily.

---

# 11. Coupon Rate, Par, Premium and Discount

## Coupon Rate

The coupon rate determines the annual coupon payment as a percentage of face value.

## At Par

A bond trades at par when:

Price = Face Value

This happens when:

Coupon Rate = Yield

## Premium Bond

A bond trades at a premium when:

Price > Face Value

Usually:

Coupon Rate > Yield

## Discount Bond

A bond trades at a discount when:

Price < Face Value

Usually:

Coupon Rate < Yield

---

# 12. Spot Rates

## Definition

A spot rate is the yield on a zero-coupon bond for a specific maturity.

Example:

The 1-year spot rate is the yield on a 1-year zero-coupon bond.

## Important

There is not one single interest rate.

There is one spot rate for each maturity.

---

# 13. Yield Curve

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

It is essential in fixed income pricing.

## Important Difference

Price-yield curve:

- price of one bond as yield changes

Yield curve:

- yields across different maturities

Do not confuse them.

---

# 14. No-Arbitrage and Replication

## Strong Arbitrage

In this deterministic setting, arbitrage means:

- zero net investment
- sure positive profit
- no risk

## Replication

Replication means creating the same future cash flows of one asset using a portfolio of other assets.

If two portfolios have identical future cash flows, they must have the same price today.

## Pricing by Replication

If we can replicate an asset, then:

Asset price = cost of replicating portfolio

This is one of the most important ideas of the course.

---

# 15. Bond Arbitrage

## Main Logic

If a bond is mispriced relative to a replicating portfolio:

- buy the cheap asset
- sell the expensive asset or portfolio

The future cash flows cancel.

The arbitrage profit comes from the price difference today.

## Key Idea

Bond prices across maturities must be consistent.

Otherwise, arbitrage is possible.

---

# 16. Bootstrapping Spot Rates

## Definition

Bootstrapping is the process of deriving spot rates from observed bond prices.

## Intuition

A coupon bond is a package of future payments.

Each payment should be discounted using the spot rate corresponding to its maturity.

If some spot rates are known, we can solve for unknown longer maturity spot rates.

---

# 17. Forward Rates

## Definition

A forward rate is an interest rate agreed today for a future period.

Example:

The rate from year 1 to year 2 implied by today’s bond prices.

## Spot Rate vs Forward Rate

Spot rate:

- starts today
- ends at a future maturity

Forward rate:

- starts in the future
- ends at a later future date

## No-Arbitrage Relationship

Investing directly from today to period j must be equivalent to:

1. investing from today to period i
2. then investing from period i to period j at the forward rate

Formula:

(1 + r_j/n)^j = (1 + r_i/n)^i × (1 + f(i,j)/n)^(j-i)

where:

- r_i = spot rate to period i
- r_j = spot rate to period j
- f(i,j) = forward rate from i to j
- n = compounding frequency

## Annual Compounding Example

If n = 1:

(1 + r_2)^2 = (1 + r_1)(1 + f(1,2))

Therefore:

f(1,2) = (1 + r_2)^2 / (1 + r_1) - 1

---

# 18. Forward Rates Are Not Forecasts

A forward rate is implied by today’s prices.

It is not necessarily the market’s prediction of the future spot rate.

Future spot rates are uncertain.

A trader can speculate that the future spot rate will be different from today’s forward rate, but that is not arbitrage.

## Important Difference

Forward rate:

- locked in today
- derived from current bond prices

Future spot rate:

- unknown
- observed later

---

# 19. Common Confusions

## Future Value vs Present Value

Future value grows money forward.

Present value discounts money backward.

## Interest Rate vs Discount Factor

Interest rate measures growth.

Discount factor converts future money into today’s value.

## Coupon vs Yield

Coupon is a cash payment.

Yield is the implied return from the current price.

## Yield vs Spot Rate

Yield usually refers to the IRR of a coupon bond.

Spot rate refers to a zero-coupon yield for a specific maturity.

## Spot Rate vs Forward Rate

Spot rate starts today.

Forward rate starts in the future.

## Arbitrage vs Speculation

Arbitrage is risk-free profit.

Speculation depends on being right about the future.

---

# 20. What You Must Know for the Exam

You should be able to:

- compute future value under different compounding conventions
- compute effective annual rate
- understand continuous compounding
- compute present value of one future payment
- compute present value of a sequence of cash flows
- explain the law of one price
- understand loan amortization
- explain APR vs quoted interest rate
- define IRR
- price a bond as present value of future payments
- define yield to maturity
- explain why bond price and yield move inversely
- identify par, premium and discount bonds
- define spot rates
- explain the yield curve
- understand replication and no-arbitrage
- derive a forward rate from spot rates
- distinguish forward rates from future spot rates

---

# 21. Core Formulas

## Future Value

FV = (1 + r/n)^m

## Continuous Future Value

FV = e^(rT)

## Present Value

PV = X(T) / (1 + r/n)^m

## Continuous Present Value

PV = X(T)e^(-rT)

## Present Value of Cash Flows

PV = sum of discounted future payments

## Perpetual Annuity

PV = X / r

## Bond Price

P = V / (1 + y/n)^m + sum from k = 1 to m of (C/n) / (1 + y/n)^k

## Zero-Coupon Bond Price

P = V / (1 + r)^T

## Forward Rate

(1 + r_j/n)^j = (1 + r_i/n)^i × (1 + f(i,j)/n)^(j-i)

---

# Final Intuition

Module 2 teaches how to price known future cash flows.

The key principle is that the value today must equal the cost of replicating the future payoff.

This gives the foundation for no-arbitrage pricing.

Later, the same logic will be applied to random payoffs such as options.
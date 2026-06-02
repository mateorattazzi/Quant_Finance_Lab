# Pricing Deterministic Payoffs

## Main Idea

A deterministic payoff is a future payment whose amount and payment date are known in advance.

Examples:

- fixed loan payments
- bond coupons
- bond face value
- fixed cash flows

The goal is to determine how much a future payment is worth today.

This is called present value.

## Why This Matters for Option Pricing

Even though options have random payoffs, the same pricing logic will be used later.

The key idea is:

if a payoff can be replicated, its price must equal the cost of replication.

This connects deterministic pricing with no-arbitrage pricing.

---

# Risk-Free Asset

The basic risk-free asset is a bank account with a deterministic interest rate.

If we invest money today, we know exactly how much it will become in the future.

This is the simplest pricing environment.

---

# Interest Rate Conventions

Interest rates depend on how compounding is defined.

The same quoted rate can lead to different future values depending on the compounding method.

---

# Simple Interest

With simple interest, one dollar becomes:

1 + rT

after T years.

This is simple but not the most common convention in finance.

---

# Annual Compounding

If interest is compounded once per year, one dollar becomes:

(1 + r)^T

after T years.

Interest is paid on both:

- initial capital
- previous interest

This is the idea of interest on interest.

---

# Compounding n Times per Year

If the annual nominal rate is r and interest is compounded n times per year, one dollar grows by:

(1 + r/n)^m

where:

- r = annual nominal interest rate
- n = compounding frequency per year
- m = total number of compounding periods

Example:

If compounding is quarterly, then:

n = 4

---

# Effective Annual Interest Rate

The effective annual rate measures the actual one-year growth of money.

If the nominal rate is r and compounding happens n times per year:

1 + effective rate = (1 + r/n)^n

Example:

A nominal 8% rate compounded quarterly gives an effective annual rate of approximately 8.24%.

Important idea:

More frequent compounding creates a higher effective annual rate.

---

# Continuous Compounding

Continuous compounding is the limit of compounding infinitely often.

The future value of one dollar after T years is:

e^(rT)

where:

- r = continuously compounded interest rate
- T = time in years

For one year:

e^r

Example:

At r = 8%, continuous compounding gives an effective annual rate of approximately 8.33%.

This is slightly higher than quarterly compounding.

---

# Discounting

Discounting reverses compounding.

Instead of asking:

How much will money today become in the future?

we ask:

How much is a future payment worth today?

---

# Law of One Price

If two strategies generate the exact same future cash flows at the exact same times, they must have the same price today.

Otherwise, arbitrage would be possible.

This is one of the most important principles in finance.

## Intuition

If the same payoff had two different prices:

- buy the cheaper strategy
- sell the more expensive strategy
- lock in a risk-free profit

That should not be possible in an efficient market.

---

# Present Value

The present value is the amount of money needed today to generate a known future payoff.

If a future payoff is X(T), and the interest rate is compounded n times per year, then:

PV = X(T) / (1 + r/n)^m

where:

- X(T) = future payoff
- r = annual nominal rate
- n = compounding frequency
- m = number of compounding periods

---

# Discount Factor

The discount factor is the number used to convert future value into present value.

For discrete compounding:

discount factor = 1 / (1 + r/n)^m

For continuous compounding:

discount factor = e^(-rT)

So:

PV = X(T) × e^(-rT)

---

# Present Value of Cash Flows

If there is a sequence of future payments, the present value is the sum of the discounted values of each payment.

Each cash flow must be discounted according to when it is received.

General idea:

PV = sum of discounted future payments

---

# Constant Cash Flow Case

If the same payment X is received repeatedly over several periods, the present value becomes a geometric series.

This is useful for valuing:

- loans
- mortgages
- annuities
- fixed payment streams

---

# Important Quant Finance Ideas

## Pricing by Replication

If we can create the same future payoff by investing in a bank account, bond, stock, or option strategy, then the price must be the cost of creating that payoff.

This is the bridge between present value and option pricing.

## Deterministic vs Random Payoffs

Deterministic payoff:

- amount is known
- timing is known

Random payoff:

- amount depends on future uncertainty

Options are random payoffs, but the pricing logic will still rely on replication and no-arbitrage.

## Discounting Is Fundamental

Every pricing model needs a way to compare money across time.

Discounting is the mathematical tool that allows this.

---

# Core Intuition

A dollar in the future is worth less than a dollar today because money today can earn interest.

Pricing deterministic payoffs means finding the amount of money today that can grow into the known future payment.

This same logic will later be used to price options and other derivatives.
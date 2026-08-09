# Stochastic Integrals

## Key Idea

A stochastic integral is an integral with respect to Brownian motion.

Instead of integrating with respect to ordinary time:

dt

we integrate with respect to the random process:

dW(t)

This type of integral is essential for continuous-time finance because stock prices in the Black-Scholes-Merton model are driven by Brownian motion.

---

# 1. Why We Need Stochastic Integrals

In ordinary calculus, we integrate functions with respect to time.

Example:

Integral of f(t) dt

This works when the variable of integration is smooth and deterministic.

But Brownian motion is different.

Brownian motion paths are:

* continuous
* random
* extremely irregular
* nowhere differentiable

Because Brownian motion is not differentiable, ordinary calculus cannot directly handle expressions like:

dW(t)

So we need a new type of integral:

Integral of Y(t) dW(t)

This is called a stochastic integral or Ito integral.

---

# 2. Financial Motivation

In finance, stochastic integrals appear naturally when describing gains from trading.

Suppose W(t) represents a martingale-type price process.

If an investor holds Y(t) units of that asset, then the infinitesimal gain is:

Y(t) dW(t)

The cumulative gain from time 0 to time t is:

Integral from 0 to t of Y(u) dW(u)

## Intuition

The stochastic integral represents the total profit and loss from continuously trading a random asset.

In discrete time, this is similar to:

sum of position × price change

In continuous time, this becomes:

Integral of position d price

---

# 3. Discrete-Time Approximation

The stochastic integral is built as the limit of sums.

Divide time into small intervals:

0 = t_0 < t_1 < ... < t_n = t

A discrete approximation is:

sum from j = 0 to n - 1 of Y(t_j) [W(t_{j+1}) - W(t_j)]

## Meaning

At each time t_j:

* choose the position Y(t_j)
* hold it over the next interval
* earn the Brownian increment W(t_{j+1}) - W(t_j)

Then add all gains.

As the time intervals become smaller, this sum converges to the stochastic integral.

---

# 4. Definition of the Ito Integral

The Ito integral is written as:

I(t) = Integral from 0 to t of Y(u) dW(u)

It is defined as the limit of sums:

I(t) = limit of sum Y(t_j) [W(t_{j+1}) - W(t_j)]

where the partition becomes finer.

## Important

The value Y(t_j) is taken at the beginning of each interval.

This is important because trading strategies cannot depend on future information.

---

# 5. Adapted Integrands

The process Y(t) must be adapted.

This means:

Y(t) can only depend on information available up to time t.

It cannot depend on future Brownian motion values.

## Financial Interpretation

A trading strategy must be based only on current and past information.

You cannot choose your position today using tomorrow's stock price.

---

# 6. Square-Integrability Condition

A common condition for the stochastic integral to be well-defined is:

E[Integral from 0 to t of Y(u)^2 du] < infinity

## Meaning

The integrand Y must not be too large.

This condition ensures that the stochastic integral has finite variance.

## Intuition

If the trading strategy is too explosive, the risk of the cumulative gain may become infinite.

For this course, the examples usually satisfy this condition.

---

# 7. Stochastic Integral as a Process

The integral:

I(t) = Integral from 0 to t of Y(u) dW(u)

is itself a stochastic process.

As t changes, the value of the integral changes randomly.

So I(t) represents the accumulated random gain up to time t.

---

# 8. Martingale Property

One of the most important properties is:

I(t) = Integral from 0 to t of Y(u) dW(u)

is a martingale.

That means for s < t:

E[I(t) | information up to time s] = I(s)

## Intuition

If Brownian motion is a fair game, then gains from trading in Brownian motion are also a fair game.

There is no expected profit from trading a martingale, assuming the strategy is admissible.

---

# 9. Mean of the Stochastic Integral

Since I(t) is a martingale and starts at zero:

I(0) = 0

we have:

E[I(t)] = 0

## Meaning

The stochastic integral has zero expected value.

In finance:

If the underlying process is a martingale, then a self-financing trading strategy based on it does not generate positive expected profits.

---

# 10. Variance Formula

The variance of the stochastic integral is given by:

Var[I(t)] = E[Integral from 0 to t of Y(u)^2 du]

Since E[I(t)] = 0, this is also:

E[I(t)^2] = E[Integral from 0 to t of Y(u)^2 du]

This property is known as the Ito isometry.

## Intuition

The risk of the stochastic integral depends on the accumulated squared exposure Y(u)^2.

If the position Y is large, the variance of the gain is large.

---

# 11. Why the Integral is a Martingale

To understand why I(t) is a martingale, split the integral:

I(t) = Integral from 0 to s of Y(u) dW(u) + Integral from s to t of Y(u) dW(u)

The first part is already known at time s:

Integral from 0 to s of Y(u) dW(u) = I(s)

The second part has conditional expectation zero:

E[Integral from s to t of Y(u) dW(u) | information up to time s] = 0

Therefore:

E[I(t) | information up to time s] = I(s)

## Key Intuition

Past gains are known.

Future gains have zero expected value.

So the best prediction of the future integral is the current integral value.

---

# 12. Discrete Intuition for the Martingale Property

In discrete form, the future part of the integral looks like:

sum Y(t_j) [W(t_{j+1}) - W(t_j)]

For each term:

* Y(t_j) is known at time t_j
* W(t_{j+1}) - W(t_j) is independent of the past
* E[W(t_{j+1}) - W(t_j)] = 0

Therefore:

E[Y(t_j)(W(t_{j+1}) - W(t_j)) | information up to t_j] = 0

Adding these terms gives expected future gain equal to zero.

---

# 13. Law of Iterated Expectations

The proof uses the law of iterated expectations.

The idea is:

If s < t_j, then conditioning first on more information and then on less information gives the same final conditional expectation as conditioning only on the less information.

In simple terms:

averaging twice leaves the coarser average.

This allows us to condition on time t_j, where Y(t_j) is known, and then use the fact that Brownian increments have mean zero.

---

# 14. Discrete Intuition for the Variance Formula

In discrete form:

I(t) approximately equals sum Y(t_j) Delta W_j

where:

Delta W_j = W(t_{j+1}) - W(t_j)

To compute variance, we look at:

E[(Y(t_j) Delta W_j)^2]

Since Y(t_j) is known at time t_j, we can take it out of the conditional expectation:

E[Y(t_j)^2 (Delta W_j)^2]

Brownian increments satisfy:

E[(Delta W_j)^2] = Delta t

So:

E[Y(t_j)^2 (Delta W_j)^2] = E[Y(t_j)^2 Delta t]

Adding over all intervals gives:

E[sum Y(t_j)^2 Delta t]

As Delta t goes to zero, this becomes:

E[Integral from 0 to t of Y(u)^2 du]

---

# 15. Stochastic Integral vs Ordinary Integral

An ordinary integral:

Integral of Y(u) du

accumulates exposure over deterministic time.

A stochastic integral:

Integral of Y(u) dW(u)

accumulates exposure over random Brownian movements.

## Key Difference

In ordinary calculus, dt has size Delta t.

In Brownian motion, dW has size approximately sqrt(Delta t).

This difference is one reason stochastic calculus behaves differently from ordinary calculus.

---

# 16. Why Stochastic Integrals Are Not Ordinary Riemann Integrals

Brownian motion has infinite variation over any interval.

Its path is too irregular for the usual Riemann-Stieltjes integral to work directly.

The Ito integral solves this by defining the integral as a limit of non-anticipating sums.

The key is that Y(t_j) is chosen before the Brownian increment occurs.

---

# 17. Connection to Trading Strategies

The stochastic integral is the continuous-time version of a gains process.

In discrete time:

G(t) = sum of holdings × price changes

In continuous time:

G(t) = Integral from 0 to t of trading strategy d price process

If the price process is Brownian motion or a martingale, this becomes:

G(t) = Integral from 0 to t of Y(u) dW(u)

## Financial Meaning

The stochastic integral models cumulative trading gains and losses.

---

# 18. Connection to Black-Scholes-Merton

The Black-Scholes-Merton model will use a stock price process of the form:

dS(t) = mu S(t) dt + sigma S(t) dW(t)

This equation has two parts:

* mu S(t) dt = deterministic drift
* sigma S(t) dW(t) = random Brownian shock

To understand this model, we need to understand integrals with respect to dW(t).

That is why stochastic integrals are introduced before Ito's lemma and Black-Scholes pricing.

---

# 19. Common Confusions

## Stochastic Integral vs Ordinary Integral

An ordinary integral integrates over time.

A stochastic integral integrates over Brownian motion.

## dW(t) Is Not Like dt

The Brownian increment dW(t) is random and has size roughly sqrt(dt).

This makes stochastic calculus different from ordinary calculus.

## Martingale Does Not Mean Constant

The stochastic integral is a martingale, but it still moves randomly.

It only means that its expected future value, conditional on current information, equals its current value.

## Zero Mean Does Not Mean Zero Risk

The stochastic integral has expected value zero, but it can have positive variance.

So it can generate gains or losses, even though the average is zero.

## Y(t) Must Not Use Future Information

The integrand must be adapted.

A trading strategy cannot look into the future.

---

# 20. Exam Notes

You should be able to:

* explain why stochastic integrals are needed
* write the stochastic integral Integral from 0 to t of Y(u) dW(u)
* explain the discrete approximation using sums
* explain why Y(t_j) is evaluated at the beginning of the interval
* explain what adapted means
* state the square-integrability condition
* state that the stochastic integral is a martingale
* state that its expected value is zero
* state the variance formula / Ito isometry
* explain the intuition behind the martingale property
* explain the intuition behind the variance formula
* connect stochastic integrals to gains from trading
* connect stochastic integrals to the Black-Scholes-Merton model

---

# 21. Core Formulas

## Ito Integral

I(t) = Integral from 0 to t of Y(u) dW(u)

## Discrete Approximation

I(t) approximately equals:

sum Y(t_j) [W(t_{j+1}) - W(t_j)]

## Square-Integrability Condition

E[Integral from 0 to t of Y(u)^2 du] < infinity

## Martingale Property

E[I(t) | information up to time s] = I(s)

for s < t

## Mean

E[I(t)] = 0

## Variance / Ito Isometry

E[I(t)^2] = E[Integral from 0 to t of Y(u)^2 du]

## Split of the Integral

I(t) = I(s) + Integral from s to t of Y(u) dW(u)

## Conditional Expectation of Future Gain

E[Integral from s to t of Y(u) dW(u) | information up to time s] = 0

---

# Final Intuition

A stochastic integral measures accumulated exposure to Brownian motion.

In finance, it represents the cumulative gains and losses from trading a risky asset whose randomness is driven by Brownian motion.

The key properties are:

* it is a martingale
* its mean is zero
* its variance is determined by the accumulated squared exposure
* it requires non-anticipating strategies

This makes stochastic integrals one of the main tools needed for continuous-time option pricing.

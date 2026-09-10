# Module 5 Summary — Brownian Motion, Stochastic Integrals and Ito's Rule

## 1. Purpose of Module 5

Module 5 moves from discrete-time option pricing to continuous-time option pricing.

In earlier modules, the binomial tree model was used to price options in discrete time.

Now the course introduces the mathematical tools needed for the Black-Scholes-Merton model.

The main topics are:

* Brownian motion
* log-normal stock prices
* stochastic integrals
* Ito integrals
* Ito's rule / Ito's lemma
* exponential Brownian motion
* the connection to geometric Brownian motion

The goal is to understand the mathematical foundation behind continuous-time finance.

---

# 2. Why Continuous-Time Models Are Needed

The binomial tree is useful, but it works in discrete time.

In practice, asset prices change continuously.

To model this, we need a process that can represent continuous-time randomness.

Brownian motion provides that foundation.

It becomes the random driver behind the Black-Scholes-Merton stock price model.

---

# 3. Brownian Motion — Main Idea

Brownian motion is a stochastic process used to model continuous-time random movement.

It is denoted by:

W(t)

It starts at zero and moves randomly over time.

Brownian motion is important because it has:

* normally distributed increments
* independent increments
* continuous paths
* martingale property
* Markov property

It is the main building block of the Black-Scholes-Merton model.

---

# 4. Historical Background

Brownian motion is named after Robert Brown, who observed irregular particle movement in liquid.

Important historical names include:

* Brown
* Bachelier
* Einstein
* Wiener
* Lévy
* Ito
* Samuelson
* Black
* Scholes
* Merton

Louis Bachelier used Brownian motion to model stock prices in 1900.

Later, Black, Scholes and Merton used related continuous-time models to develop modern option pricing theory.

---

# 5. Bank Account in Continuous Time

The risk-free asset is the bank account.

With continuously compounded constant interest rate r:

B(t) = e^(rt)

This means one unit invested at time 0 grows deterministically to e^(rt) at time t.

---

# 6. Log-Normal Stock Price Model

In the Black-Scholes-Merton framework, the stock price is log-normal.

This means:

log S(t) is normally distributed.

The stock price is written as:

S(t) = S(0) exp[(mu - 1/2 sigma^2)t + sigma W(t)]

where:

* S(0) = initial stock price
* mu = expected return rate
* sigma = volatility
* W(t) = Brownian motion

## Meaning of mu

The parameter mu represents the expected return rate of the stock.

It can be shown that:

E[S(t)] = S(0)e^(mu t)

So, on average, the stock grows at rate mu.

## Meaning of sigma

The parameter sigma represents volatility.

More precisely:

sigma^2 is the variance rate of log returns.

That is:

Var[log(S(t) / S(0))] / t = sigma^2

Higher sigma means more uncertainty in the stock price.

---

# 7. Discretized Brownian Motion

Brownian motion can be understood as the limit of a random walk.

Start with:

W(0) = 0

Then define:

W(t_{k+1}) = W(t_k) + sqrt(Delta t) Z(t_k)

where:

* Z(t_k) are independent standard normal random variables
* Delta t is the time step

The scaling sqrt(Delta t) is crucial.

It makes the variance of the increment proportional to the length of the time interval.

---

# 8. Brownian Motion Increment Distribution

For s < t:

W(t) - W(s) ~ Normal(0, t - s)

This means:

* expected increment = 0
* variance of increment = t - s

## Intuition

The longer the time interval, the larger the uncertainty.

Uncertainty grows with time.

---

# 9. Defining Properties of Brownian Motion

A process W(t) is Brownian motion if it satisfies:

## 1. Normal Increments

For s < t:

W(t) - W(s) ~ Normal(0, t - s)

## 2. Independent Increments

Increments over non-overlapping time intervals are independent.

## 3. Starts at Zero

W(0) = 0

## 4. Continuous Paths

Sample paths are continuous functions of time.

There are no jumps.

---

# 10. Brownian Motion and Real Markets

Brownian motion is a benchmark model.

It is not a perfect description of reality.

Real markets may have:

* jumps
* changing volatility
* fat tails
* short-term dependence
* liquidity effects

However, Brownian motion is useful because it is mathematically tractable and leads to the Black-Scholes-Merton model.

---

# 11. Brownian Motion is Continuous but Not Smooth

Brownian motion paths are continuous.

However, they are nowhere differentiable.

This means:

* there are no jumps
* but there is no tangent at any point
* ordinary calculus cannot be directly applied

This is why stochastic calculus is needed.

---

# 12. Quadratic Variation

One of the most important properties of Brownian motion is quadratic variation.

For Brownian motion:

sum of squared increments converges to t

Informally:

(dW)^2 = dt

This is the key reason Ito's rule has an extra term.

## Important Intuition

In ordinary calculus, second-order terms disappear.

In stochastic calculus, second-order Brownian terms survive.

---

# 13. Markov Property

Brownian motion is a Markov process.

This means:

The future distribution depends only on the current value, not on the full past history.

In simple terms:

To predict the future of W(t), you only need to know W(s), not the path before s.

---

# 14. Brownian Motion is a Martingale

Brownian motion satisfies:

E[W(t) | information up to time s] = W(s)

for s < t.

## Intuition

The best prediction of the future Brownian motion value is its current value.

Brownian motion is a fair game.

---

# 15. Stochastic Integrals — Main Idea

A stochastic integral is an integral with respect to Brownian motion.

It is written as:

I(t) = Integral from 0 to t of Y(u) dW(u)

This is different from an ordinary integral because the integrator W(t) is random and irregular.

---

# 16. Why Stochastic Integrals Are Needed

In finance, stochastic integrals represent cumulative gains from trading.

In discrete time:

gain = sum of holdings × price changes

In continuous time:

gain = Integral of trading strategy d price process

If the price randomness is Brownian motion, we need integrals of the form:

Integral Y(u) dW(u)

---

# 17. Discrete Approximation of the Ito Integral

Divide time into small intervals:

0 = t_0 < t_1 < ... < t_n = t

The stochastic integral is approximated by:

sum Y(t_j) [W(t_{j+1}) - W(t_j)]

The position Y(t_j) is chosen at the beginning of each interval.

This is important because trading strategies cannot use future information.

---

# 18. Adapted Processes

The integrand Y(t) must be adapted.

This means:

Y(t) can only depend on information available up to time t.

## Financial Interpretation

A trading strategy cannot look into the future.

The investor chooses the position using only current and past information.

---

# 19. Square-Integrability Condition

A common condition for the Ito integral to be well-defined is:

E[Integral from 0 to t of Y(u)^2 du] < infinity

## Meaning

The trading strategy must not be too explosive.

This ensures the stochastic integral has finite variance.

---

# 20. Stochastic Integral is a Martingale

The stochastic integral:

I(t) = Integral from 0 to t of Y(u) dW(u)

is a martingale under suitable conditions.

That means:

E[I(t) | information up to time s] = I(s)

for s < t.

## Intuition

Past gains are known.

Future Brownian gains have conditional expectation zero.

So the best prediction of the future integral is its current value.

---

# 21. Mean of the Stochastic Integral

Since I(t) starts at zero and is a martingale:

E[I(t)] = 0

## Important

Zero mean does not mean no risk.

The integral can still move randomly and have positive variance.

---

# 22. Ito Isometry

The variance formula for the stochastic integral is:

E[I(t)^2] = E[Integral from 0 to t of Y(u)^2 du]

This is called the Ito isometry.

## Intuition

The risk of the stochastic integral depends on the accumulated squared exposure.

Larger trading positions create larger variance.

---

# 23. Why Ito Calculus Is Different

Brownian motion increments behave like:

dW ~ sqrt(dt)

Therefore:

(dW)^2 ~ dt

This is the essential difference from ordinary calculus.

In informal notation:

(dt)^2 = 0

dt dW = 0

(dW)^2 = dt

---

# 24. Ito's Rule — Main Idea

Ito's rule, also called Ito's lemma, is the stochastic version of the chain rule.

It tells us how a function of a stochastic process changes.

This is essential because an option price is a function of time and the stock price:

C(t, S(t))

If S(t) is stochastic, we need Ito's rule to compute dC.

---

# 25. General Ito's Rule

Suppose:

dX(t) = mu(t)dt + sigma(t)dW(t)

and:

f = f(t, X(t))

Then Ito's rule says:

df(t, X(t)) =
[f_t + mu f_x + 1/2 sigma^2 f_xx]dt

* sigma f_x dW(t)

where:

* f_t = partial derivative with respect to time
* f_x = first partial derivative with respect to x
* f_xx = second partial derivative with respect to x
* mu = drift of X
* sigma = volatility of X

---

# 26. The Extra Ito Term

The key new term is:

1/2 sigma^2 f_xx dt

This term does not exist in ordinary calculus.

It appears because Brownian motion has non-zero quadratic variation.

## Ordinary Chain Rule

df = f_t dt + f_x dX

## Ito Chain Rule

df = f_t dt + f_x dX + 1/2 sigma^2 f_xx dt

---

# 27. Taylor Expansion Intuition

Ito's rule comes from Taylor expansion.

For a smooth function:

Delta f ≈ f_t Delta t + f_x Delta X + 1/2 f_xx (Delta X)^2

If:

Delta X = mu Delta t + sigma Delta W

then:

(Delta X)^2 contains sigma^2 (Delta W)^2

Since:

(Delta W)^2 behaves like Delta t

this term does not disappear.

That is why Ito's rule includes:

1/2 sigma^2 f_xx dt

---

# 28. Example: Ito Rule for W(t)^2

Let:

f(x) = x^2

Then:

f_x = 2x

f_xx = 2

Since X(t) = W(t):

mu = 0

sigma = 1

Ito's rule gives:

d[W(t)^2] = 2W(t)dW(t) + dt

## Key Point

In ordinary calculus, we would expect only:

2W(t)dW(t)

But Ito calculus adds:

dt

---

# 29. Computing Integral W dW

From:

d[W(t)^2] = 2W(t)dW(t) + dt

Integrate from 0 to t:

W(t)^2 = 2 Integral from 0 to t of W(s)dW(s) + t

Therefore:

Integral from 0 to t of W(s)dW(s) = 1/2[W(t)^2 - t]

## Important

This differs from ordinary calculus by the correction term:

* t/2

---

# 30. Example: Exponential of Brownian Motion

Let:

Y(t) = exp[aW(t) + bt]

Using Ito's rule:

dY(t) = [b + 1/2 a^2]Y(t)dt + aY(t)dW(t)

## Key Point

The drift is not just b.

It is:

b + 1/2 a^2

The extra term comes from Ito's rule.

---

# 31. Connection to Geometric Brownian Motion

The Black-Scholes-Merton stock price model is:

dS(t) = mu S(t)dt + sigma S(t)dW(t)

Its solution is:

S(t) = S(0) exp[(mu - 1/2 sigma^2)t + sigma W(t)]

## Why the -1/2 sigma^2 Appears

From the exponential Brownian motion formula:

dY(t) = [b + 1/2 a^2]Y(t)dt + aY(t)dW(t)

To make the drift equal to mu, set:

a = sigma

b + 1/2 sigma^2 = mu

Therefore:

b = mu - 1/2 sigma^2

This explains the correction term in the stock price formula.

---

# 32. Ito's Rule for Option Prices

If the stock follows:

dS(t) = mu S(t)dt + sigma S(t)dW(t)

and the option price is:

C(t, S(t))

then Ito's rule gives:

dC =
[C_t + mu S C_S + 1/2 sigma^2 S^2 C_SS]dt

* sigma S C_S dW

## Financial Interpretation

The option price changes because of:

* passage of time
* stock price movement
* curvature of the option value

The curvature term is:

1/2 sigma^2 S^2 C_SS

This is related to gamma.

---

# 33. Why Ito's Rule Matters for Black-Scholes

Ito's rule is the key step in deriving the Black-Scholes equation.

The general logic is:

1. assume the stock follows geometric Brownian motion
2. apply Ito's rule to the option price C(t, S)
3. create a hedged portfolio using the stock and the option
4. eliminate the random dW term
5. force the risk-free portfolio to earn the risk-free rate
6. obtain the Black-Scholes PDE

Without Ito's rule, the Black-Scholes derivation is impossible.

---

# 34. Main Conceptual Flow of the Module

The module builds the continuous-time option pricing framework step by step.

## Step 1

Introduce Brownian motion as the continuous-time random driver.

## Step 2

Show that Brownian motion has independent normal increments, continuous paths, Markov property and martingale property.

## Step 3

Explain why Brownian motion is too irregular for ordinary calculus.

## Step 4

Define stochastic integrals as limits of non-anticipating trading gains.

## Step 5

Show that stochastic integrals are martingales and satisfy the Ito isometry.

## Step 6

Introduce Ito's rule as the correct chain rule for Brownian-driven processes.

## Step 7

Apply Ito's rule to examples that prepare the Black-Scholes-Merton model.

---

# 35. Common Confusions

## Brownian Motion vs Stock Price

Brownian motion itself is not the stock price.

It is the random factor driving the stock price.

## Normal vs Log-Normal

Brownian motion increments are normal.

In Black-Scholes-Merton, the stock price is log-normal.

This means log S(t) is normal.

## Continuous vs Differentiable

Brownian paths are continuous but not differentiable.

Continuous does not mean smooth.

## Real Probability vs Risk-Neutral Probability

This module focuses on the mathematical process.

Later pricing will use risk-neutral probabilities.

## Stochastic Integral vs Ordinary Integral

An ordinary integral integrates over time.

A stochastic integral integrates over Brownian motion.

## dW vs dt

dW is random and has size approximately sqrt(dt).

dt is deterministic and much smaller.

## Ito's Rule vs Ordinary Chain Rule

Ito's rule has an extra second-order term.

That term comes from Brownian quadratic variation.

## Zero Mean vs Zero Risk

A stochastic integral has mean zero but can still have significant variance.

## Martingale vs Constant

A martingale can move randomly.

It only means the conditional expected future value equals the current value.

---

# 36. Exam Notes

You should be able to:

* explain why Brownian motion is introduced
* define the Black-Scholes-Merton bank account B(t)
* explain log-normal stock prices
* interpret mu as expected return
* interpret sigma as volatility
* define Brownian motion
* state the distribution of Brownian increments
* explain independent increments
* explain continuous but nowhere differentiable paths
* explain the Markov property
* explain why Brownian motion is a martingale
* define the stochastic / Ito integral
* explain the discrete approximation of the Ito integral
* explain why the integrand must be adapted
* state the square-integrability condition
* state that the Ito integral is a martingale
* state the Ito isometry
* explain why (dW)^2 = dt
* state Ito's rule
* explain the extra Ito term
* compute d[W(t)^2]
* derive Integral W dW = 1/2[W(t)^2 - t]
* apply Ito's rule to exp[aW(t) + bt]
* explain the origin of the -1/2 sigma^2 term
* apply Ito's rule to C(t, S)
* explain how Ito's rule leads to Black-Scholes

---

# 37. Core Formulas

## Bank Account

B(t) = e^(rt)

## Log-Normal Stock Price

S(t) = S(0) exp[(mu - 1/2 sigma^2)t + sigma W(t)]

## Expected Stock Price

E[S(t)] = S(0)e^(mu t)

## Variance Rate of Log Returns

Var[log(S(t) / S(0))] / t = sigma^2

## Brownian Increment

W(t) - W(s) ~ Normal(0, t - s)

## Brownian Martingale Property

E[W(t) | information up to time s] = W(s)

## Ito Integral

I(t) = Integral from 0 to t of Y(u)dW(u)

## Ito Integral Approximation

I(t) ≈ sum Y(t_j)[W(t_{j+1}) - W(t_j)]

## Square-Integrability

E[Integral from 0 to t of Y(u)^2du] < infinity

## Ito Isometry

E[I(t)^2] = E[Integral from 0 to t of Y(u)^2du]

## Informal Ito Rules

(dt)^2 = 0

dt dW = 0

(dW)^2 = dt

## Ito's Rule

If:

dX(t) = mu(t)dt + sigma(t)dW(t)

then:

df(t, X(t)) =
[f_t + mu f_x + 1/2 sigma^2 f_xx]dt

* sigma f_x dW(t)

## Brownian Square

d[W(t)^2] = 2W(t)dW(t) + dt

## Integral W dW

Integral from 0 to t of W(s)dW(s) = 1/2[W(t)^2 - t]

## Exponential Brownian Motion

If:

Y(t) = exp[aW(t) + bt]

then:

dY(t) = [b + 1/2 a^2]Y(t)dt + aY(t)dW(t)

## Geometric Brownian Motion

dS(t) = mu S(t)dt + sigma S(t)dW(t)

## Ito's Rule for Option Prices

dC =
[C_t + mu S C_S + 1/2 sigma^2 S^2 C_SS]dt

* sigma S C_S dW

---

# Final Intuition

Module 5 introduces the mathematical machinery needed for continuous-time option pricing.

Brownian motion models continuous-time randomness.

Stochastic integrals allow us to integrate trading strategies against Brownian motion.

Ito's rule tells us how functions of Brownian-driven processes evolve.

Together, these tools prepare the derivation of the Black-Scholes-Merton model.

The most important idea is:

ordinary calculus is not enough for Brownian motion.

Because Brownian motion has quadratic variation, the stochastic chain rule contains an extra second-order term.

That extra term is the mathematical reason why Black-Scholes contains gamma and why option pricing in continuous time requires Ito calculus.

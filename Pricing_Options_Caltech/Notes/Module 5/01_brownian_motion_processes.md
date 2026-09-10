# Brownian Motion — Introduction

## Key Idea

Brownian motion is the main stochastic process used in the Black-Scholes-Merton model.

It is used to model continuous-time randomness.

In finance, Brownian motion becomes the building block for modeling stock price movements in continuous time.

---

# 1. Why Brownian Motion Matters

Until now, option pricing was done using discrete-time models, mainly the binomial tree.

In the binomial model:

* time moves in steps
* the stock can move up or down
* option prices are computed by backward induction

Brownian motion moves the course to a higher mathematical level.

It allows us to model stock prices continuously over time.

This prepares the transition to:

* continuous-time models
* stochastic calculus
* Ito's lemma
* Black-Scholes-Merton option pricing

---

# 2. Historical Background

Brownian motion is named after Robert Brown, a biologist who observed irregular movement of particles in liquid.

Later, the mathematical theory was developed by several important figures:

* Louis Bachelier
* Albert Einstein
* Norbert Wiener
* Paul Lévy
* Kiyoshi Ito

## Finance Connection

Louis Bachelier used Brownian motion to model stock prices in his 1900 PhD thesis.

His work was ahead of its time and was mostly forgotten for many years.

Later, Brownian motion became central to modern option pricing through the work of:

* Paul Samuelson
* Fischer Black
* Myron Scholes
* Robert Merton

---

# 3. Black-Scholes-Merton Model Preview

The model has two main assets:

## Risk-Free Asset

The bank account grows at a continuously compounded constant rate r:

B(t) = e^(rt)

## Risky Asset

The stock price follows a log-normal distribution.

This means:

log[S(t)] is normally distributed.

A simplified expression is:

log S(t) = log S(0) + (mu - 1/2 sigma^2)t + sigma sqrt(t) Z

where:

* S(0) = initial stock price
* mu = expected return rate
* sigma = volatility
* Z = standard normal random variable
* t = time

Equivalently:

S(t) = S(0) exp[(mu - 1/2 sigma^2)t + sigma sqrt(t) Z]

---

# 4. Meaning of mu

The parameter mu represents the expected return rate of the stock.

It can be shown that:

E[S(t)] = S(0)e^(mu t)

## Intuition

On average, the stock grows like a bank account with continuously compounded rate mu.

However, the stock is risky because its actual future value is random.

---

# 5. Meaning of sigma

The parameter sigma represents volatility.

More precisely:

sigma^2 is the variance rate of log returns.

The log return is:

log[S(t) / S(0)]

The variance per unit of time is:

Var[log(S(t) / S(0))] / t = sigma^2

## Intuition

* sigma measures the size of random fluctuations
* higher sigma means more uncertainty
* sigma is central to option pricing

Options become more valuable when volatility increases because there is more chance of large favorable movements.

---

# 6. Why We Need a Process, Not Just One Random Variable

For a fixed time t, the expression for S(t) is relatively simple.

But in finance we need to model the whole path of the stock price through time.

That means we need a stochastic process:

S(t), for all t ≥ 0

The difficult mathematical question is:

Can we construct a process that behaves consistently across all times?

Brownian motion provides this process.

---

# 7. Discretized Brownian Motion

Before defining continuous Brownian motion, we can approximate it in discrete time.

Let the process start at zero:

W(0) = 0

At each time step:

W(t_{k+1}) = W(t_k) + sqrt(Delta t) Z(t_k)

where:

* Z(t_k) are independent standard normal random variables
* Delta t = length of the time step
* sqrt(Delta t) is the correct scaling factor

## Intuition

Brownian motion can be understood as a random walk with many very small normally distributed shocks.

---

# 8. Brownian Motion Increments

For two times t_k and t_l:

W(t_l) - W(t_k)

is the sum of many small normal shocks.

Because sums of normal random variables are normal, the increment is also normally distributed.

The increment has:

mean = 0

variance = t_l - t_k

## Key Result

W(t) - W(s) ~ Normal(0, t - s)

for t > s

## Intuition

The longer the time interval, the larger the variance.

Uncertainty grows with time.

---

# 9. Brownian Motion as a Limit

The discretized process becomes Brownian motion when:

Delta t goes to 0

In that limit, the random walk converges to a continuous-time stochastic process.

This is one reason Brownian motion is a natural benchmark model.

It is connected to the Central Limit Theorem, because many small independent shocks tend to produce normal behavior.

---

# 10. Definition of Brownian Motion

A process W(t) is Brownian motion if it satisfies four properties.

## Property 1 — Normal Increments

For t > s:

W(t) - W(s) ~ Normal(0, t - s)

The change over any interval is normally distributed.

## Property 2 — Independent Increments

Changes over non-overlapping time intervals are independent.

For example:

W(t2) - W(t1)

is independent of:

W(t3) - W(t2)

for t1 < t2 < t3.

## Property 3 — Starts at Zero

W(0) = 0

## Property 4 — Continuous Paths

The sample paths of W(t) are continuous functions of time.

There are no jumps.

---

# 11. Financial Interpretation

## Normal Increments

The random shock over a time interval is normally distributed.

## Independent Increments

Tomorrow's shock is independent of today's shock.

This means the model has no memory.

## Continuous Paths

Prices move continuously without jumps.

This is a simplifying assumption.

Real markets can have jumps, but the Black-Scholes-Merton benchmark model assumes continuous paths.

---

# 12. Brownian Motion vs Real Markets

Brownian motion is a benchmark model, not a perfect description of reality.

In real markets:

* prices can jump
* returns may not be exactly normal
* volatility changes over time
* there may be short-term dependence

However, Brownian motion is still useful because:

* it is mathematically tractable
* it gives a clean benchmark
* it leads to the Black-Scholes-Merton model
* it provides intuition for stochastic calculus

---

# 13. Sample Paths

A sample path is one possible realization of Brownian motion through time.

Each sample path is:

* continuous
* random
* irregular
* oscillating around zero

Every simulation gives a different path.

## Important

Brownian motion has continuous paths, but those paths are extremely irregular.

---

# 14. Nowhere Differentiable Paths

Brownian motion paths are continuous but nowhere differentiable.

This means:

* the path has no jumps
* but there is no well-defined tangent at any point

## Intuition

The path is too irregular to have an ordinary derivative.

This is why ordinary calculus does not work directly with Brownian motion.

We need stochastic calculus.

---

# 15. Why Ordinary Derivatives Fail

For a differentiable deterministic function, changes over small time intervals behave smoothly.

For Brownian motion, the increments are too rough.

The expected squared rate of change behaves like:

E[(W(t) - W(s))^2] / (t - s)^2

Since:

E[(W(t) - W(s))^2] = t - s

we get:

1 / (t - s)

As s approaches t, this goes to infinity.

## Meaning

The Brownian path is too irregular for normal differentiation.

This motivates Ito calculus.

---

# 16. Markov Property

Brownian motion is a Markov process.

This means the conditional distribution of the future depends only on the current value, not on the full past history.

## Intuition

To predict the future distribution of Brownian motion, we only need to know where the process is now.

The past path does not matter once the current value is known.

---

# 17. Brownian Motion is a Martingale

Brownian motion is also a martingale.

For s < t:

E[W(t) | information up to time s] = W(s)

## Meaning

The best prediction of the future Brownian motion value is its current value.

## Intuition

Brownian motion is a fair game.

It has no drift.

Its expected future change is zero.

---

# 18. Why Brownian Motion is a Martingale

We can write:

W(t) = W(s) + [W(t) - W(s)]

Taking conditional expectation given information up to time s:

E[W(t) | information at s]
= E[W(s) | information at s] + E[W(t) - W(s) | information at s]

The first term is:

W(s)

because W(s) is already known at time s.

The second term is:

0

because the increment W(t) - W(s) is independent of the past and has mean zero.

Therefore:

E[W(t) | information at s] = W(s)

---

# 19. Why This Matters for Finance

Brownian motion will be used to model the random component of stock prices.

In the Black-Scholes-Merton model, stock prices are driven by Brownian motion.

The stock model will eventually be written in differential form as something like:

dS(t) = mu S(t) dt + sigma S(t) dW(t)

where:

* mu S(t) dt = deterministic drift component
* sigma S(t) dW(t) = random Brownian component

This will require stochastic calculus because dW(t) behaves differently from ordinary changes in time.

---

# 20. Common Confusions

## Brownian Motion vs Stock Price

Brownian motion itself is not the stock price.

It is the random driver behind the stock price.

## Normal vs Log-Normal

Brownian motion has normal increments.

In Black-Scholes-Merton, the stock price is log-normal.

This means log S(t) is normal, not S(t) itself.

## Continuous Does Not Mean Smooth

Brownian paths are continuous, but not smooth.

They have no jumps, but they are not differentiable.

## Independent Increments Does Not Mean Constant Path

The increments are independent, but the process still moves randomly.

## Martingale Does Not Mean Constant

A martingale can move up and down.

It only means the expected future value equals the current value.

---

# 21. Exam Notes

You should be able to:

* explain why Brownian motion is introduced
* describe the historical role of Brown, Bachelier, Wiener, Ito, Black, Scholes and Merton
* define the bank account in the Black-Scholes-Merton setting
* explain what log-normal stock prices mean
* interpret mu as expected return rate
* interpret sigma as volatility
* describe discretized Brownian motion
* state the four defining properties of Brownian motion
* explain independent increments
* explain why Brownian motion has continuous but nowhere differentiable paths
* explain the Markov property
* explain why Brownian motion is a martingale
* understand why Brownian motion motivates stochastic calculus

---

# 22. Core Formulas

## Bank Account

B(t) = e^(rt)

## Log-Normal Stock Price Form

log S(t) = log S(0) + (mu - 1/2 sigma^2)t + sigma sqrt(t) Z

## Stock Price Form

S(t) = S(0) exp[(mu - 1/2 sigma^2)t + sigma sqrt(t) Z]

## Expected Stock Price

E[S(t)] = S(0)e^(mu t)

## Variance of Log Returns

Var[log(S(t) / S(0))] / t = sigma^2

## Discretized Brownian Motion

W(t_{k+1}) = W(t_k) + sqrt(Delta t) Z(t_k)

where:

Z(t_k) ~ Normal(0, 1)

## Brownian Increment Distribution

W(t) - W(s) ~ Normal(0, t - s)

## Brownian Martingale Property

E[W(t) | information up to time s] = W(s)

for s < t

---

# Final Intuition

Brownian motion is the mathematical object that allows us to move from discrete-time binomial models to continuous-time option pricing.

It represents continuous-time randomness.

It has normally distributed independent increments, continuous but highly irregular paths, the Markov property, and the martingale property.

This process will become the foundation for the Black-Scholes-Merton model.

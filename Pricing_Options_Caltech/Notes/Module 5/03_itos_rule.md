# Ito's Rule / Ito's Lemma

## Key Idea

Ito's rule, also called Ito's lemma, is the stochastic calculus version of the chain rule.

It tells us how a function of a stochastic process changes over time.

This is essential for option pricing because in the Black-Scholes-Merton model:

* the stock price is stochastic
* the option price is a function of time and the stock price

So if we know how the stock price moves, Ito's rule tells us how the option price moves.

---

# 1. Why Ito's Rule Is Needed

In ordinary calculus, if:

f = f(t, x(t))

then the chain rule says:

df = f_t dt + f_x dx

where:

* f_t = partial derivative with respect to time
* f_x = partial derivative with respect to x
* dx = change in x

This works when x(t) is smooth.

But Brownian motion is not smooth.

Brownian motion paths are:

* continuous
* random
* nowhere differentiable

So ordinary calculus does not work directly when x(t) is driven by Brownian motion.

Ito's rule modifies the chain rule by adding an extra second-order term.

---

# 2. Stochastic Process Setup

Suppose X(t) follows a stochastic differential equation:

dX(t) = mu(t) dt + sigma(t) dW(t)

where:

* mu(t) = drift term
* sigma(t) = volatility term
* W(t) = Brownian motion
* dt = small time increment
* dW(t) = Brownian shock

Now suppose we have a function:

f(t, X(t))

Ito's rule tells us how this function changes.

---

# 3. Ito's Rule

If:

dX(t) = mu(t) dt + sigma(t) dW(t)

then:

df(t, X(t)) =
[f_t + mu f_x + 1/2 sigma^2 f_xx] dt

* sigma f_x dW(t)

where:

* f_t = partial derivative of f with respect to t
* f_x = first partial derivative of f with respect to x
* f_xx = second partial derivative of f with respect to x
* mu = drift of X
* sigma = volatility of X

## Important

The extra term is:

1/2 sigma^2 f_xx dt

This term does not appear in ordinary calculus.

It appears because Brownian motion has non-zero quadratic variation.

---

# 4. Comparison with Ordinary Chain Rule

## Ordinary calculus

df = f_t dt + f_x dx

## Ito calculus

df = f_t dt + f_x dX + 1/2 f_xx sigma^2 dt

or equivalently:

df =
[f_t + mu f_x + 1/2 sigma^2 f_xx] dt

* sigma f_x dW

## Key Difference

Ito's rule has an additional second-derivative term.

This term is the main difference between stochastic calculus and ordinary calculus.

---

# 5. Why the Extra Term Appears

In ordinary calculus, terms like:

(dx)^2

are usually negligible compared with dx.

But for Brownian motion:

dW is of size approximately sqrt(dt)

Therefore:

(dW)^2 is of size dt

So second-order terms involving Brownian motion do not disappear.

This is why Ito's rule includes the term:

1/2 sigma^2 f_xx dt

## Ito Multiplication Rules

The informal rules are:

(dt)^2 = 0

dt dW = 0

(dW)^2 = dt

These rules explain why the second derivative term survives.

---

# 6. Financial Interpretation

In finance, think of:

X(t) = stock price

f(t, X(t)) = option price

If the stock follows:

dX(t) = mu dt + sigma dW(t)

then the option price follows:

df =
[f_t + mu f_x + 1/2 sigma^2 f_xx] dt

* sigma f_x dW

## Interpretation

The option price changes for three reasons:

1. time passes
2. the stock price changes
3. the curvature of the option value matters because the stock price is random

The curvature effect is captured by:

1/2 sigma^2 f_xx dt

This is closely related to gamma in option pricing.

---

# 7. Example 1 — Computing Integral W dW

We want to compute:

Integral from 0 to t of W(s) dW(s)

In ordinary calculus, one might guess:

Integral x dx = x^2 / 2

So maybe:

Integral W dW = W(t)^2 / 2

But Ito calculus gives an extra correction.

---

## Step 1: Choose the function

Let:

f(x) = x^2

Then:

f_x = 2x

f_xx = 2

There is no time dependence, so:

f_t = 0

---

## Step 2: Apply Ito's rule to W(t)^2

Here:

X(t) = W(t)

So:

dX(t) = dW(t)

This means:

mu = 0

sigma = 1

Using Ito's rule:

d[W(t)^2] = 2W(t)dW(t) + dt

---

## Step 3: Integrate both sides

Integrate from 0 to t:

W(t)^2 - W(0)^2 = 2 Integral from 0 to t of W(s)dW(s) + Integral from 0 to t ds

Since:

W(0) = 0

and:

Integral from 0 to t ds = t

we get:

W(t)^2 = 2 Integral from 0 to t of W(s)dW(s) + t

Therefore:

Integral from 0 to t of W(s)dW(s) = 1/2 [W(t)^2 - t]

## Final Result

Integral from 0 to t of W(s)dW(s) = W(t)^2 / 2 - t / 2

## Key Intuition

The result is not just W(t)^2 / 2.

There is an extra correction term:

* t / 2

This correction comes from the fact that:

(dW)^2 = dt

---

# 8. Example 2 — Exponential of Brownian Motion

Consider:

Y(t) = exp[aW(t) + bt]

This type of process is important because it resembles the structure of stock prices in the Black-Scholes-Merton model.

Let:

f(t, x) = exp[ax + bt]

Then:

Y(t) = f(t, W(t))

---

## Step 1: Compute derivatives

First derivative with respect to time:

f_t = b f

First derivative with respect to x:

f_x = a f

Second derivative with respect to x:

f_xx = a^2 f

---

## Step 2: Apply Ito's rule

Since:

X(t) = W(t)

we have:

mu = 0

sigma = 1

Ito's rule gives:

dY(t) = [f_t + 1/2 f_xx]dt + f_x dW(t)

Substitute the derivatives:

dY(t) = [b f + 1/2 a^2 f]dt + a f dW(t)

Since:

f = Y(t)

we get:

dY(t) = [b + 1/2 a^2]Y(t)dt + aY(t)dW(t)

## Final Result

dY(t) = [b + 1/2 a^2]Y(t)dt + aY(t)dW(t)

## Key Intuition

Even though the exponent has drift b, the process Y(t) has drift:

b + 1/2 a^2

The extra term:

1/2 a^2

comes from Ito's rule.

---

# 9. Connection to Geometric Brownian Motion

The Black-Scholes-Merton stock price model is usually written as:

dS(t) = mu S(t) dt + sigma S(t) dW(t)

The solution has the form:

S(t) = S(0) exp[(mu - 1/2 sigma^2)t + sigma W(t)]

## Why the Term -1/2 sigma^2 Appears

From the exponential example:

If:

Y(t) = exp[aW(t) + bt]

then:

dY(t) = [b + 1/2 a^2]Y(t)dt + aY(t)dW(t)

To get drift mu and volatility sigma, set:

a = sigma

and choose b so that:

b + 1/2 sigma^2 = mu

Therefore:

b = mu - 1/2 sigma^2

That is why the stock price is written as:

S(t) = S(0) exp[(mu - 1/2 sigma^2)t + sigma W(t)]

---

# 10. Ito's Rule for a Stock Price Process

If the stock follows:

dS(t) = mu S(t) dt + sigma S(t) dW(t)

and the option price is:

C(t, S(t))

then Ito's rule gives:

dC =
[C_t + mu S C_S + 1/2 sigma^2 S^2 C_SS]dt

* sigma S C_S dW

where:

* C_t = theta-like time derivative
* C_S = delta
* C_SS = gamma
* sigma S = volatility of the stock price in dollars

## Financial Meaning

The option's random exposure is:

sigma S C_S dW

This depends on the option's delta.

The option's deterministic drift includes:

C_t + mu S C_S + 1/2 sigma^2 S^2 C_SS

The gamma term appears because the option is nonlinear in the stock price.

---

# 11. Link to Black-Scholes Equation

Ito's rule is the key mathematical step used to derive the Black-Scholes partial differential equation.

The general idea is:

1. assume the stock follows geometric Brownian motion
2. apply Ito's rule to the option price C(t, S)
3. form a hedged portfolio using the stock and option
4. eliminate the random dW term
5. force the hedged portfolio to earn the risk-free rate
6. obtain the Black-Scholes PDE

The PDE will contain:

C_t

C_S

C_SS

This is why Ito's rule is essential.

---

# 12. Common Confusions

## Ito's Rule vs Ordinary Chain Rule

Ito's rule is the chain rule for stochastic processes.

It has an extra term involving the second derivative.

## Why f_xx Appears

The second derivative appears because Brownian motion has quadratic variation.

In informal notation:

(dW)^2 = dt

## Why dt dW Disappears

Since dW is of size sqrt(dt):

dt dW is of size dt^(3/2)

This is negligible compared with dt.

## Why (dt)^2 Disappears

(dt)^2 is much smaller than dt, so it is ignored.

## Why W(t)^2 Has Extra dt

Because:

d[W(t)^2] = 2W(t)dW(t) + dt

not simply:

2W(t)dW(t)

## Why Stock Prices Use mu - 1/2 sigma^2

The correction ensures that the drift of S(t) is mu.

Without the correction, the exponential Brownian process would have drift shifted by:

1/2 sigma^2

---

# 13. Exam Notes

You should be able to:

* state Ito's rule
* explain how Ito's rule differs from ordinary calculus
* identify the extra second-order term
* explain why (dW)^2 = dt
* apply Ito's rule to f(W(t))
* compute d[W(t)^2]
* derive Integral W dW = 1/2[W(t)^2 - t]
* apply Ito's rule to exp[aW(t) + bt]
* explain the origin of the -1/2 sigma^2 term in geometric Brownian motion
* apply Ito's rule to an option price C(t, S)
* explain why Ito's rule leads to the Black-Scholes PDE

---

# 14. Core Formulas

## Stochastic Process

dX(t) = mu(t)dt + sigma(t)dW(t)

## Ito's Rule

df(t, X(t)) =
[f_t + mu f_x + 1/2 sigma^2 f_xx]dt

* sigma f_x dW(t)

## Informal Multiplication Rules

(dt)^2 = 0

dt dW = 0

(dW)^2 = dt

## Brownian Square

d[W(t)^2] = 2W(t)dW(t) + dt

## Integral W dW

Integral from 0 to t of W(s)dW(s)
= 1/2[W(t)^2 - t]

## Exponential Brownian Function

If:

Y(t) = exp[aW(t) + bt]

then:

dY(t) = [b + 1/2 a^2]Y(t)dt + aY(t)dW(t)

## Geometric Brownian Motion

dS(t) = mu S(t)dt + sigma S(t)dW(t)

## GBM Solution

S(t) = S(0) exp[(mu - 1/2 sigma^2)t + sigma W(t)]

## Ito's Rule for Option Price

dC =
[C_t + mu S C_S + 1/2 sigma^2 S^2 C_SS]dt

* sigma S C_S dW

---

# Final Intuition

Ito's rule is the stochastic version of the chain rule.

The ordinary chain rule is not enough because Brownian motion is too irregular.

The key correction is the second-order term:

1/2 sigma^2 f_xx dt

This correction is what makes stochastic calculus different from ordinary calculus.

In finance, Ito's rule explains how option prices move when the stock price follows Brownian motion, and it is the mathematical tool that leads directly to the Black-Scholes-Merton equation.

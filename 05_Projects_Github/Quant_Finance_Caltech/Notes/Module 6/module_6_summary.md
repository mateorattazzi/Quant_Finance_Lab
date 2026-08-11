# Module 6 Summary — Black-Scholes-Merton Model

## 1. Purpose of Module 6

Module 6 introduces the Black-Scholes-Merton model, the benchmark continuous-time model for option pricing.

The module explains two ways to obtain the Black-Scholes formula:

1. PDE / replication approach
2. Risk-neutral pricing approach

Both methods lead to the same European option prices.

The key idea is:

> Options are priced by no-arbitrage and replication, not by forecasting the real expected return of the stock.

---

## 2. The Black-Scholes-Merton Market

The model has two assets:

1. A risk-free bank account
2. One risky stock

### Bank Account

The bank account grows at a constant continuously compounded rate $r$:

$$
B(t)=e^{rt}
$$

In differential form:

$$
dB(t)=rB(t)dt
$$

The bank account is deterministic.

---

## 3. Stock Price Dynamics

The stock follows geometric Brownian motion:

$$
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
$$

or equivalently:

$$
dS(t)=S(t)(\mu dt+\sigma dW(t))
$$

where:

- $\mu$ = expected return rate under the real probability
- $\sigma$ = volatility
- $W(t)$ = Brownian motion
- $dt$ = deterministic time increment
- $dW(t)$ = random Brownian shock

The stock has two components:

$$
\mu S(t)dt
$$

is the deterministic drift component.

$$
\sigma S(t)dW(t)
$$

is the random Brownian component.

---

## 4. Explicit Stock Price Solution

The stock price can also be written explicitly.

For $u>t$:

$$
S(u)=S(t)\exp\left[\left(\mu-\frac{1}{2}\sigma^2\right)(u-t)+\sigma(W(u)-W(t))\right]
$$

This shows that the stock price is log-normal.

The correction term

$$
-\frac{1}{2}\sigma^2
$$

appears because of Ito’s rule.

---

## 5. European Path-Independent Claims

A European path-independent claim pays:

$$
g(S(T))
$$

at maturity $T$.

Examples:

European call:

$$
g(S(T))=(S(T)-K)^+
$$

European put:

$$
g(S(T))=(K-S(T))^+
$$

Path-independent means the payoff depends only on the final stock price, not on the full path followed by the stock.

---

## 6. Main Pricing Guess

The course assumes that the option price can be written as:

$$
C(t,S(t))
$$

That means the price depends only on:

- current time $t$
- current stock price $S(t)$

It does not depend on the full past history of the stock.

This is natural because the Black-Scholes-Merton stock process is Markovian.

---

## 7. Ito’s Rule Applied to the Option Price

Since:

$$
C=C(t,S(t))
$$

and:

$$
dS=\mu Sdt+\sigma SdW
$$

Ito’s rule gives:

$$
dC=
\left(
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma S C_S dW
$$

The option price has:

- a deterministic $dt$ part
- a random $dW$ part

The random part is:

$$
\sigma S C_S dW
$$

The term $C_S$ is the option delta.

---

## 8. Self-Financing Portfolio

Let $X(t)$ be the wealth of a self-financing portfolio.

Let $\pi(t)$ be the amount of money invested in the stock.

Then:

$$
X(t)-\pi(t)
$$

is the amount invested in the bank account.

The number of stock shares is:

$$
\frac{\pi(t)}{S(t)}
$$

The self-financing wealth dynamics are:

$$
dX=
\frac{\pi}{S}dS
+
\frac{X-\pi}{B}dB
$$

Substituting the Black-Scholes dynamics gives:

$$
dX=[rX+\pi(\mu-r)]dt+\pi\sigma dW
$$

---

## 9. Replication Argument

To replicate the option, set:

$$
X=C
$$

and require:

$$
dX=dC
$$

Match the random $dW$ terms:

$$
\pi\sigma=\sigma S C_S
$$

Therefore:

$$
\pi=SC_S
$$

So the number of shares held in the replicating portfolio is:

$$
\frac{\pi}{S}=C_S
$$

This is the option delta.

---

## 10. Deriving the Black-Scholes PDE

Now match the drift terms.

From Ito’s rule:

$$
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
$$

From the portfolio:

$$
rC+SC_S(\mu-r)
$$

Set them equal:

$$
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
=
rC+SC_S(\mu-r)
$$

Expand the right-hand side:

$$
rC+\mu SC_S-rSC_S
$$

The $\mu S C_S$ terms cancel.

This gives:

$$
C_t+\frac{1}{2}\sigma^2S^2C_{SS}
=
rC-rSC_S
$$

Rearrange:

$$
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
$$

This is the Black-Scholes PDE.

---

## 11. Why $\mu$ Disappears

The real expected return $\mu$ does not appear in the Black-Scholes PDE.

This is one of the most important ideas in the module.

The reason is:

> The option is priced by replication, not by predicting the stock’s real-world average return.

Once the payoff can be replicated, no-arbitrage determines the price.

The option price depends on:

- $S$: current stock price
- $K$: strike price
- $T-t$: time to maturity
- $r$: risk-free rate
- $\sigma$: volatility

It does not depend on:

- $\mu$: real-world expected stock return

---

## 12. Black-Scholes PDE

The Black-Scholes PDE is:

$$
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
$$

with terminal condition:

$$
C(T,S)=g(S)
$$

For a European call:

$$
C(T,S)=\max(S-K,0)
$$

For a European put:

$$
P(T,S)=\max(K-S,0)
$$

The PDE is deterministic.

There is no $dW$ term because replication eliminates the Brownian risk.

The PDE must hold for every $t<T$ and $S>0$.

---

## 13. Black-Scholes Call Formula

For a European call option:

$$
C(T,S)=\max(S-K,0)
$$

Solving the Black-Scholes PDE gives:

$$
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
$$

where:

$$
d_1=
\frac{
\ln(S/K)+(r+\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
$$

and:

$$
d_2=d_1-\sigma\sqrt{T-t}
$$

Equivalently:

$$
d_2=
\frac{
\ln(S/K)+(r-\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
$$

---

## 14. Standard Normal CDF

The function $N(x)$ is the standard normal cumulative distribution function:

$$
N(x)=P(Z\leq x)
$$

where:

$$
Z\sim N(0,1)
$$

It is the area under the standard normal bell curve to the left of $x$.

---

## 15. Put Formula

The European put formula can be obtained using put-call parity.

Put-call parity is:

$$
C-P=S-Ke^{-r(T-t)}
$$

Therefore:

$$
P=C-S+Ke^{-r(T-t)}
$$

The Black-Scholes put formula is:

$$
P(t,S)=K e^{-r(T-t)}N(-d_2)-S N(-d_1)
$$

---

## 16. Risk-Neutral Pricing Approach

The second approach prices options using discounted expected payoffs under the risk-neutral probability $Q$.

The general pricing formula is:

$$
V(t,S)=E_t^Q\left[e^{-r(T-t)}g(S(T))\right]
$$

For a European call:

$$
C(t,S)=E_t^Q\left[e^{-r(T-t)}(S(T)-K)^+\right]
$$

This method avoids directly solving the PDE.

---

## 17. Stock Dynamics Under $Q$

Under the real-world probability $P$:

$$
dS=\mu Sdt+\sigma SdW
$$

Under the risk-neutral probability $Q$:

$$
dS=rSdt+\sigma SdW^Q
$$

The key replacement is:

$$
\mu \rightarrow r
$$

The volatility $\sigma$ stays the same.

---

## 18. Explicit Stock Formula Under $Q$

Under the risk-neutral probability:

$$
S(T)=S(t)\exp\left[
\left(r-\frac{1}{2}\sigma^2\right)(T-t)
+
\sigma(W^Q(T)-W^Q(t))
\right]
$$

The Brownian increment satisfies:

$$
W^Q(T)-W^Q(t)\sim N(0,T-t)
$$

So:

$$
\frac{W^Q(T)-W^Q(t)}{\sqrt{T-t}}
\sim N(0,1)
$$

This is why the Black-Scholes formula involves $N(d_1)$ and $N(d_2)$.

---

## 19. Splitting the Call Payoff

The call payoff can be written as:

$$
(S(T)-K)^+
=
S(T)\mathbf{1}_{\{S(T)>K\}}
-
K\mathbf{1}_{\{S(T)>K\}}
$$

This separates the payoff into:

1. stock part
2. strike part

Then:

$$
C(t,S)
=
e^{-r(T-t)}E_t^Q[S(T)\mathbf{1}_{\{S(T)>K\}}]
-
K e^{-r(T-t)}E_t^Q[\mathbf{1}_{\{S(T)>K\}}]
$$

---

## 20. Meaning of $N(d_2)$

The expectation of an indicator function is a probability.

So:

$$
E_t^Q[\mathbf{1}_{\{S(T)>K\}}]
=
Q(S(T)>K)
$$

In Black-Scholes:

$$
Q(S(T)>K)=N(d_2)
$$

Therefore, $N(d_2)$ is the risk-neutral probability that the call finishes in the money.

This is why the strike term is:

$$
K e^{-r(T-t)}N(d_2)
$$

---

## 21. Meaning of $N(d_1)$

The first term is:

$$
e^{-r(T-t)}E_t^Q[S(T)\mathbf{1}_{\{S(T)>K\}}]
$$

This is not just a probability.

It is a stock-weighted expectation.

After evaluating the normal integral, it becomes:

$$
S N(d_1)
$$

So $N(d_1)$ is connected to the stock component of the call value.

A useful memory rule:

$$
S N(d_1)
$$

is the stock part.

$$
K e^{-r(T-t)}N(d_2)
$$

is the discounted strike part.

---

## 22. Risk-Neutral Derivation of the PDE

The PDE can also be obtained quickly from risk-neutral pricing.

Under $Q$:

$$
dS=rSdt+\sigma SdW^Q
$$

Apply Ito’s rule to $C(t,S)$:

$$
dC=
\left(
C_t+rSC_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma SC_SdW^Q
$$

Now discount:

$$
e^{-rt}C(t,S(t))
$$

Under $Q$, discounted prices of tradable or replicable claims must be martingales.

A martingale has zero drift.

The drift of the discounted option price is:

$$
C_t+rSC_S+\frac{1}{2}\sigma^2S^2C_{SS}-rC
$$

Set it equal to zero:

$$
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
$$

This is the same Black-Scholes PDE.

---

## 23. PDE Approach vs Risk-Neutral Approach

### PDE / Replication Approach

Uses:

- Ito’s rule
- self-financing portfolio
- matching $dW$ terms
- replication
- no-arbitrage

It derives the PDE first, then solves it.

### Risk-Neutral Pricing Approach

Uses:

- risk-neutral probability $Q$
- discounted expected payoff
- stock dynamics under $Q$
- normal distribution calculations

It computes the price directly as an expectation.

### Key Point

Both methods give the same Black-Scholes formula.

---

## 24. Implied Volatility

The Black-Scholes model assumes that $\sigma$ is constant.

However, in real markets, different options on the same underlying often imply different volatilities.

### Definition

Implied volatility is the value of $\sigma$ that makes the Black-Scholes price equal to the market price:

$$
C_{BSM}(\sigma_{\text{imp}})=C_{\text{market}}
$$

It is the volatility implied by the observed option price.

---

## 25. Volatility Smile

If Black-Scholes were perfectly correct, then all options on the same stock and maturity should have the same implied volatility.

The implied volatility curve across strikes should be flat.

In practice, it is often curved.

This is called the volatility smile.

### Interpretation

The market often prices extreme strikes as if they have higher volatility.

This suggests that the simple constant-volatility Black-Scholes model does not fully describe real option prices.

---

## 26. Why the Volatility Smile Matters

The volatility smile shows that real markets may have features not captured by the basic Black-Scholes model, such as:

- stochastic volatility
- jumps
- fat tails
- imperfect hedging
- higher probability of extreme events

This motivates more advanced models.

---

## 27. Stochastic Volatility Motivation

A stochastic volatility model allows volatility to change randomly over time.

Instead of assuming:

$$
\sigma=\text{constant}
$$

we allow:

$$
\sigma(t)=\text{random}
$$

This is a natural extension because volatility is one of the most important inputs in stock option pricing.

---

## 28. Main Conceptual Flow of Module 6

The module follows this logic:

1. Define the Black-Scholes-Merton market.
2. Model the stock using geometric Brownian motion.
3. Apply Ito’s rule to the option price.
4. Build a self-financing portfolio.
5. Replicate the option and derive the PDE.
6. Observe that $\mu$ disappears.
7. Solve the PDE to get the Black-Scholes formula.
8. Re-derive the same formula using risk-neutral pricing.
9. Interpret $N(d_2)$ as a risk-neutral probability.
10. Introduce implied volatility as a way to compare market prices with Black-Scholes prices.
11. Use the volatility smile as motivation for more advanced models.

---

## 29. Common Confusions

### Why Does $\mu$ Disappear?

Because the option is priced by replication, not by forecasting.

### Is $N(d_2)$ a Real-World Probability?

No.

It is a risk-neutral probability.

### Is $N(d_1)$ the Probability of Exercise?

Not exactly.

It comes from the stock-weighted expectation term.

### What Is Delta?

Delta is:

$$
C_S
$$

It is the number of shares needed in the replicating portfolio.

### What Is $\pi$?

$\pi$ is the dollar amount invested in the stock.

The number of shares is:

$$
\frac{\pi}{S}
$$

### Why Is the PDE Deterministic?

Because replication eliminates the random Brownian term.

### Why Does the Discounted Price Have Zero Drift Under $Q$?

Because discounted prices of tradable or replicable claims must be martingales under the risk-neutral measure.

### Why Does a Volatility Smile Contradict Basic Black-Scholes?

Basic Black-Scholes assumes one constant $\sigma$ for the stock.

If different strikes imply different $\sigma$, the market is not using one constant-volatility model.

---

## 30. Exam Notes

You should be able to:

- write the Black-Scholes bank account dynamics
- write the stock dynamics under $P$
- write the stock dynamics under $Q$
- write the explicit stock solution
- explain why the stock is log-normal
- apply Ito’s rule to $C(t,S)$
- derive the self-financing portfolio dynamics
- explain the role of $\pi$
- match $dW$ terms and identify delta
- derive the Black-Scholes PDE
- explain why $\mu$ disappears
- state the Black-Scholes call formula
- define $N(x)$, $d_1$, and $d_2$
- obtain the put formula using put-call parity
- explain the risk-neutral pricing formula
- split the call payoff using an indicator function
- explain why $N(d_2)$ is a risk-neutral probability
- explain why $N(d_1)$ is not simply the probability of exercise
- derive the PDE using the martingale property
- define implied volatility
- explain the volatility smile
- explain why the volatility smile motivates stochastic volatility models

---

## 31. Core Formulas

### Bank Account

$$
B(t)=e^{rt}
$$

$$
dB(t)=rB(t)dt
$$

### Stock Under $P$

$$
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
$$

### Stock Under $Q$

$$
dS(t)=rS(t)dt+\sigma S(t)dW^Q(t)
$$

### Explicit Stock Under $P$

$$
S(u)=S(t)\exp\left[
\left(\mu-\frac{1}{2}\sigma^2\right)(u-t)
+
\sigma(W(u)-W(t))
\right]
$$

### Explicit Stock Under $Q$

$$
S(T)=S(t)\exp\left[
\left(r-\frac{1}{2}\sigma^2\right)(T-t)
+
\sigma(W^Q(T)-W^Q(t))
\right]
$$

### Ito Rule for Option Price

$$
dC=
\left(
C_t+\mu S C_S+\frac{1}{2}\sigma^2S^2C_{SS}
\right)dt
+
\sigma S C_S dW
$$

### Self-Financing Portfolio

$$
dX=
\frac{\pi}{S}dS+
\frac{X-\pi}{B}dB
$$

### Wealth Dynamics

$$
dX=[rX+\pi(\mu-r)]dt+\pi\sigma dW
$$

### Replicating Stock Amount

$$
\pi=SC_S
$$

### Number of Shares / Delta

$$
\frac{\pi}{S}=C_S
$$

### Black-Scholes PDE

$$
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
$$

### Terminal Condition

$$
C(T,S)=g(S)
$$

### Risk-Neutral Pricing Formula

$$
V(t,S)=E_t^Q\left[e^{-r(T-t)}g(S(T))\right]
$$

### Call Payoff Split

$$
(S(T)-K)^+
=
S(T)\mathbf{1}_{\{S(T)>K\}}
-
K\mathbf{1}_{\{S(T)>K\}}
$$

### Black-Scholes Call Formula

$$
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
$$

### $d_1$

$$
d_1=
\frac{
\ln(S/K)+(r+\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
$$

### $d_2$

$$
d_2=
\frac{
\ln(S/K)+(r-\frac{1}{2}\sigma^2)(T-t)
}{
\sigma\sqrt{T-t}
}
$$

$$
d_2=d_1-\sigma\sqrt{T-t}
$$

### Put-Call Parity

$$
C-P=S-Ke^{-r(T-t)}
$$

### Black-Scholes Put Formula

$$
P(t,S)=K e^{-r(T-t)}N(-d_2)-S N(-d_1)
$$

### Implied Volatility

$$
C_{BSM}(\sigma_{\text{imp}})=C_{\text{market}}
$$

---

## Final Intuition

Module 6 shows how the Black-Scholes-Merton formula comes from no-arbitrage pricing.

The PDE derivation shows that an option can be replicated by continuously trading the stock and the bank account.

The risk-neutral derivation shows that the same price can be computed as a discounted expected payoff under $Q$.

The key conceptual result is that the real expected return $\mu$ does not determine the option price.

Instead, the option price depends on the parameters needed for replication:

$$
S,\ K,\ r,\ \sigma,\ T-t
$$

Finally, implied volatility and the volatility smile show that Black-Scholes is a benchmark model, not a perfect description of real markets.
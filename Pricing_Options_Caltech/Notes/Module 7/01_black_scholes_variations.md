# Module 7 — Black-Scholes-Merton Extensions: Dividends and Futures

## 1. Big Picture

The basic Black-Scholes-Merton model prices vanilla European calls and puts when the underlying stock pays no dividends.

This unit extends the same framework to two important cases:

1. Stocks that pay dividends
2. Options on futures or forward contracts

The key idea is that the Black-Scholes formula still works, but the effective underlying price or drift changes.

---

## 2. Continuous Dividend Yield

Assume the stock pays dividends continuously at a constant rate `q`.

This means that holding the stock gives two sources of gain:

1. Change in the stock price
2. Dividend payments

The total gain process is not just the stock price anymore.

It is:

```math
G(t)=S(t)+\text{cumulative dividends}
```

If dividends are paid continuously at rate `q`, then the dividend flow over a small interval is:

```math
qS(t)dt
```

So the total gain process satisfies:

```math
dG(t)=dS(t)+qS(t)dt
```

---

## 3. Why Dividends Matter

Without dividends, gains from holding the stock come only from price changes:

```math
dS(t)
```

With dividends, gains come from:

```math
dG(t)=dS(t)+qS(t)dt
```

So in a self-financing portfolio, the stock position earns both:

- stock price appreciation
- dividend income

This changes the dynamics of the replicating portfolio.

---

## 4. Wealth Process With Dividends

Let:

- `X(t)` = total wealth
- `pi(t)` = amount invested in the stock
- `X(t)-pi(t)` = amount invested in the bank account

The bank account still satisfies:

```math
dB(t)=rB(t)dt
```

The self-financing wealth process becomes:

```math
dX=
\frac{X-\pi}{B}dB
+
\frac{\pi}{S}dG
```

The difference from the no-dividend case is that we use `dG`, not `dS`.

Since:

```math
dG=dS+qSdt
```

the stock investment earns the stock return plus the dividend yield.

---

## 5. Stock Dynamics With Continuous Dividends

Under the real-world probability:

```math
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
```

Including dividends, the total return from holding the stock is effectively:

```math
\mu + q
```

because the holder receives both price appreciation and dividends.

Under the risk-neutral probability `Q`, the stock price itself has drift:

```math
r-q
```

So:

```math
dS(t)=(r-q)S(t)dt+\sigma S(t)dW^Q(t)
```

---

## 6. Intuition for the Drift `r - q`

Under the risk-neutral measure, the total expected return from holding the stock must be the risk-free rate `r`.

But the stockholder already receives dividend yield `q`.

Therefore, the stock price growth rate must be reduced to:

```math
r-q
```

So:

```math
\text{stock price drift} + \text{dividend yield} = r
```

or:

```math
(r-q)+q=r
```

This is why dividends reduce the drift of the stock price under `Q`.

---

## 7. Stock Formula Under `Q` With Continuous Dividends

With continuous dividend yield `q`, the stock price under `Q` is:

```math
S(T)=S(t)\exp\left[
\left(r-q-\frac{1}{2}\sigma^2\right)(T-t)
+
\sigma(W^Q(T)-W^Q(t))
\right]
```

Compare this with the no-dividend case:

```math
S(T)=S(t)\exp\left[
\left(r-\frac{1}{2}\sigma^2\right)(T-t)
+
\sigma(W^Q(T)-W^Q(t))
\right]
```

The only change is:

```math
r \rightarrow r-q
```

inside the stock dynamics.

---

## 8. Black-Scholes PDE With Continuous Dividends

The usual Black-Scholes PDE without dividends is:

```math
C_t+\frac{1}{2}\sigma^2s^2C_{ss}+rsC_s-rC=0
```

With continuous dividends, the stock drift under `Q` becomes `(r-q)s`.

Therefore, the PDE becomes:

```math
C_t+\frac{1}{2}\sigma^2s^2C_{ss}+(r-q)sC_s-rC=0
```

Important distinction:

- The `rsC_s` term becomes `(r-q)sC_s`
- The discounting term remains `-rC`

The term `-rC` does not change because option values are still discounted at the risk-free rate.

---

## 9. Black-Scholes Call Formula With Continuous Dividends

For a European call on a dividend-paying stock:

```math
C(t,S)=S e^{-q(T-t)}N(d_1)-K e^{-r(T-t)}N(d_2)
```

where:

```math
d_1=
\frac{
\ln(S/K)+\left(r-q+\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
```

and:

```math
d_2=d_1-\sigma\sqrt{T-t}
```

Equivalently:

```math
d_2=
\frac{
\ln(S/K)+\left(r-q-\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
```

---

## 10. Intuition for the Dividend Call Formula

The no-dividend call formula is:

```math
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
```

With continuous dividends, replace the stock price term by:

```math
S e^{-q(T-t)}
```

So the formula becomes:

```math
C(t,S)=S e^{-q(T-t)}N(d_1)-K e^{-r(T-t)}N(d_2)
```

The stock term is reduced because the option holder does not receive dividends before maturity.

Owning the stock gives dividends.

Owning the call does not.

Therefore, dividends make calls less valuable.

---

## 11. Discrete Deterministic Dividends

Now suppose dividends are paid at known future dates with known amounts.

These dividends are deterministic.

Let:

```math
\bar{D}(t)
```

be the present value of all future dividends paid before option maturity.

Then the Black-Scholes formula can still be used, but replace the stock price `S` with:

```math
S-\bar{D}(t)
```

So for a European call with known discrete dividends:

```math
C(t,S)=C_{BSM}(t,S-\bar{D}(t),K,r,\sigma,T)
```

In words:

> Use the usual Black-Scholes formula, but subtract the present value of known dividends from the current stock price.

---

## 12. Continuous vs Discrete Dividends

Continuous dividend yield:

```math
S \rightarrow S e^{-q(T-t)}
```

Discrete deterministic dividends:

```math
S \rightarrow S-\bar{D}(t)
```

Both adjustments reduce the effective stock price used in the option formula.

The reason is the same:

> The option holder does not receive dividends before exercising.

---

## 13. Options on Futures

Now consider options where the underlying is a futures contract.

Assume:

- no dividends
- deterministic interest rates
- Black-Scholes-Merton stock dynamics

When interest rates are deterministic, futures prices and forward prices are the same.

The futures price is:

```math
F(t)=S(t)e^{r(T-t)}
```

where `T` is the delivery date of the futures or forward contract.

---

## 14. Futures Price Dynamics

The stock follows:

```math
dS(t)=\mu S(t)dt+\sigma S(t)dW(t)
```

Using Ito's rule on:

```math
F(t)=S(t)e^{r(T-t)}
```

the futures price dynamics under the real-world probability are:

```math
dF(t)=(\mu-r)F(t)dt+\sigma F(t)dW(t)
```

Under the risk-neutral probability, the futures price has zero drift:

```math
dF(t)=\sigma F(t)dW^Q(t)
```

So the futures price itself is a martingale under `Q`.

---

## 15. Why Futures Have Zero Drift Under `Q`

A stock price under `Q` has drift `r` because holding stock involves financing and discounting.

A futures contract is different because it is marked to market.

Gains and losses are settled continuously.

Because of this marking-to-market feature, the futures price itself has zero drift under the risk-neutral probability:

```math
dF(t)=\sigma F(t)dW^Q(t)
```

So unlike a stock, the futures price does not have an `rFdt` drift term under `Q`.

---

## 16. PDE for Options on Futures

Let:

```math
C(t,F)
```

be the price of a European option on a futures contract.

Since under `Q`:

```math
dF=\sigma FdW^Q
```

Ito's rule gives no first-derivative drift term.

The PDE is:

```math
C_t+\frac{1}{2}\sigma^2F^2C_{FF}-rC=0
```

Compare this with the standard Black-Scholes PDE:

```math
C_t+\frac{1}{2}\sigma^2S^2C_{SS}+rSC_S-rC=0
```

The difference is that the futures PDE has no `rFC_F` term.

The discounting term `-rC` remains.

---

## 17. Call Option on Futures

A European call on a futures contract has payoff:

```math
(F(T)-K)^+
```

The Black-Scholes-type formula is:

```math
C(t,F)=e^{-r(T-t)}\left[F N(d_1)-K N(d_2)\right]
```

where:

```math
d_1=
\frac{
\ln(F/K)+\frac{1}{2}\sigma^2(T-t)
}{
\sigma\sqrt{T-t}
}
```

and:

```math
d_2=d_1-\sigma\sqrt{T-t}
```

Equivalently:

```math
d_2=
\frac{
\ln(F/K)-\frac{1}{2}\sigma^2(T-t)
}{
\sigma\sqrt{T-t}
}
```

This is often called Black's formula for options on futures.

---

## 18. Comparing Stock Options and Futures Options

### Stock Option, No Dividends

```math
C(t,S)=S N(d_1)-K e^{-r(T-t)}N(d_2)
```

### Stock Option With Continuous Dividends

```math
C(t,S)=S e^{-q(T-t)}N(d_1)-K e^{-r(T-t)}N(d_2)
```

### Futures Option

```math
C(t,F)=e^{-r(T-t)}\left[F N(d_1)-K N(d_2)\right]
```

---

## 19. Key Differences

For a stock option, the stock price term appears directly:

```math
S N(d_1)
```

For a dividend-paying stock, the stock price term is reduced:

```math
S e^{-q(T-t)}N(d_1)
```

For a futures option, the whole expected payoff is discounted:

```math
e^{-r(T-t)}\left[F N(d_1)-K N(d_2)\right]
```

because the futures price has zero drift under `Q`.

---

## 20. Common Confusions

### Why does the stock drift become `r-q` with dividends?

Because under `Q`, the total return must equal `r`.

The stockholder receives dividend yield `q`, so the stock price itself only needs drift `r-q`.

### Why does the `-rC` term remain in the PDE?

Because the option value is still discounted at the risk-free rate.

Dividends change the stock drift, not the discount rate.

### Why does the futures PDE have no first derivative term?

Because under `Q`, the futures price has zero drift.

The first derivative term in the PDE comes from the drift of the underlying.

No drift means no first derivative drift term.

### Why are futures and forwards the same here?

Because the interest rate is deterministic.

When rates are deterministic, the difference between futures and forwards disappears.

### Why are futures options useful?

In many markets, futures are easier or cheaper to trade than the physical underlying asset.

So options on futures are very important in practice.

---

## 21. Exam Notes

You should be able to:

- explain why dividends change the stock dynamics
- write the total gains process with dividends
- explain why the wealth process uses `dG` instead of `dS`
- write stock dynamics under `Q` with continuous dividend yield
- derive the dividend-adjusted Black-Scholes PDE
- state the call formula with continuous dividends
- explain why calls become less valuable when dividends increase
- explain the discrete dividend adjustment
- write the futures price formula
- explain why futures have zero drift under `Q`
- write the PDE for options on futures
- state the call formula for options on futures
- compare stock options, dividend-paying stock options, and futures options

---

## 22. Core Formulas

### Total gains with continuous dividends

```math
dG=dS+qSdt
```

### Stock under `Q` with continuous dividends

```math
dS=(r-q)Sdt+\sigma SdW^Q
```

### Dividend-adjusted stock formula under `Q`

```math
S(T)=S(t)\exp\left[
\left(r-q-\frac{1}{2}\sigma^2\right)(T-t)
+
\sigma(W^Q(T)-W^Q(t))
\right]
```

### Black-Scholes PDE with continuous dividends

```math
C_t+\frac{1}{2}\sigma^2s^2C_{ss}+(r-q)sC_s-rC=0
```

### Call formula with continuous dividends

```math
C(t,S)=S e^{-q(T-t)}N(d_1)-K e^{-r(T-t)}N(d_2)
```

### Dividend-adjusted `d_1`

```math
d_1=
\frac{
\ln(S/K)+\left(r-q+\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
```

### Dividend-adjusted `d_2`

```math
d_2=
\frac{
\ln(S/K)+\left(r-q-\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
```

### Discrete deterministic dividends adjustment

```math
S \rightarrow S-\bar{D}(t)
```

### Futures price

```math
F(t)=S(t)e^{r(T-t)}
```

### Futures dynamics under `Q`

```math
dF=\sigma FdW^Q
```

### PDE for options on futures

```math
C_t+\frac{1}{2}\sigma^2F^2C_{FF}-rC=0
```

### Call formula on futures

```math
C(t,F)=e^{-r(T-t)}\left[F N(d_1)-K N(d_2)\right]
```

### Futures option `d_1`

```math
d_1=
\frac{
\ln(F/K)+\frac{1}{2}\sigma^2(T-t)
}{
\sigma\sqrt{T-t}
}
```

### Futures option `d_2`

```math
d_2=d_1-\sigma\sqrt{T-t}
```

---

## Final Intuition

Dividends and futures do not require a completely new pricing theory.

They are extensions of the same Black-Scholes-Merton logic.

With continuous dividends, the stock drift under `Q` becomes `r-q`, and the stock term in the call formula becomes `S e^{-q(T-t)}`.

With deterministic discrete dividends, use the stock price net of the present value of dividends.

For options on futures, the futures price has zero drift under `Q`, so the PDE loses the first-derivative drift term.

The main skill is to identify the correct underlying dynamics under the risk-neutral probability, then apply the same Black-Scholes pricing logic.
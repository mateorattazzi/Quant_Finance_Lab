# Module 7 Summary — Extensions of Black-Scholes-Merton

## 1. Big Picture

Module 7 extends Black-Scholes-Merton beyond the basic vanilla option on a non-dividend-paying stock.

Main extensions:

1. Dividend-paying stocks
2. Options on futures
3. Currency options
4. Quanto forwards
5. Exotic options
6. Multi-asset options
7. Exchange options

The pricing principle remains the same:

```math
V(t)=E_t^Q\left[e^{-r(T-t)}\text{payoff}\right]
```

The main work is identifying the correct risk-neutral dynamics of the underlying.

---

## 2. Continuous Dividends

If a stock pays continuous dividend yield `q`, the stockholder receives dividends, but the call option holder does not.

Under the risk-neutral measure:

```math
dS=(r-q)Sdt+\sigma SdW^Q
```

So the stock drift becomes:

```math
r-q
```

The Black-Scholes PDE becomes:

```math
C_t+\frac{1}{2}\sigma^2s^2C_{ss}+(r-q)sC_s-rC=0
```

The call formula becomes:

```math
C(t,S)=S e^{-q(T-t)}N(d_1)-K e^{-r(T-t)}N(d_2)
```

with:

```math
d_1=
\frac{
\ln(S/K)+\left(r-q+\frac{1}{2}\sigma^2\right)(T-t)
}{
\sigma\sqrt{T-t}
}
```

```math
d_2=d_1-\sigma\sqrt{T-t}
```

Key intuition:

> Dividends reduce call values because the call holder does not receive dividends before exercise.

---

## 3. Discrete Deterministic Dividends

If dividends are known and paid at fixed dates, subtract their present value from the stock price.

Let:

```math
\bar{D}(t)=\text{present value of future dividends}
```

Then use the usual Black-Scholes formula with:

```math
S \rightarrow S-\bar{D}(t)
```

Continuous dividends:

```math
S \rightarrow S e^{-q(T-t)}
```

Discrete known dividends:

```math
S \rightarrow S-\bar{D}(t)
```

---

## 4. Options on Futures

When interest rates are deterministic, futures and forwards have the same price.

The futures price is:

```math
F(t)=S(t)e^{r(T-t)}
```

Under the risk-neutral measure, the futures price has zero drift:

```math
dF=\sigma FdW^Q
```

Therefore, an option on a futures contract satisfies:

```math
C_t+\frac{1}{2}\sigma^2F^2C_{FF}-rC=0
```

There is no first-derivative drift term because futures prices are martingales under `Q`.

The call option on futures formula is:

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

```math
d_2=d_1-\sigma\sqrt{T-t}
```

---

## 5. Currency Options

Let `R(t)` be the exchange rate:

```math
R(t)=\text{domestic currency value of 1 unit of foreign currency}
```

A currency call payoff is:

```math
(R(T)-K)^+
```

Foreign currency behaves like a dividend-paying asset.

The foreign interest rate `r_f` plays the role of dividend yield.

Under the domestic risk-neutral measure:

```math
dR=(r-r_f)Rdt+\sigma_R RdW^Q
```

The currency call formula is:

```math
C(t,R)=R e^{-r_f(T-t)}N(d_1)-K e^{-r(T-t)}N(d_2)
```

where:

```math
d_1=
\frac{
\ln(R/K)+\left(r-r_f+\frac{1}{2}\sigma_R^2\right)(T-t)
}{
\sigma_R\sqrt{T-t}
}
```

```math
d_2=d_1-\sigma_R\sqrt{T-t}
```

Key intuition:

> Holding foreign currency earns the foreign interest rate, so `r_f` acts like a dividend yield.

---

## 6. Quanto Forwards

A quanto payoff depends on one asset but is paid in another currency.

A typical payoff in domestic currency is:

```math
R(T)(S(T)-F)
```

To find the zero-value forward price:

```math
F=
\frac{
E^Q[S(T)R(T)]
}{
E^Q[R(T)]
}
```

If:

```math
dS=rSdt+\sigma_S SdZ^Q
```

```math
dR=(r-r_f)Rdt+\sigma_R RdW^Q
```

and:

```math
dZ^QdW^Q=\rho dt
```

then the quanto forward price is:

```math
F=S(0)e^{(r+\rho\sigma_S\sigma_R)T}
```

The extra term:

```math
\rho\sigma_S\sigma_R
```

is the quanto adjustment.

It comes from the Ito cross term:

```math
dS\,dR=\rho\sigma_S\sigma_R SRdt
```

Key intuition:

> Quanto contracts are model-dependent because correlation matters.

---

## 7. Exotic Options

Exotic options have more complex payoffs than vanilla calls and puts.

The pricing principle is still:

```math
V(t)=E_t^Q\left[e^{-r(T-t)}\text{payoff}\right]
```

but the payoff may depend on the path, an average, another option, or a future choice.

### Barrier Options

Depend on whether the underlying crosses a barrier.

Example up-and-out call:

- pays like a call if the barrier is not crossed
- becomes worthless if the barrier is crossed

Barrier options are usually cheaper than vanilla options but harder to hedge near the barrier.

### Asian Options

Depend on the average stock price.

Example:

```math
(\bar{S}-K)^+
```

They are useful when average prices matter, especially in commodity and energy markets.

Usually require numerical pricing.

### Compound Options

Options on options.

Example payoff:

```math
(C(T_1,S(T_1))-K_1)^+
```

### Forward Start Options

The strike is set in the future.

Example payoff:

```math
(S(T)-S(T_1))^+
```

At `T_1`, the option starts at the money.

### Chooser Options

The holder later chooses whether the option is a call or a put.

Using put-call parity:

```math
V_{\text{chooser}}(t)
=
C(t;T,K)
+
P(t;T_1,Ke^{-r(T-T_1)})
```

---

## 8. Multi-Asset Black-Scholes-Merton

Now there are two risky assets:

```math
S_1(t), \quad S_2(t)
```

Their dynamics are:

```math
dS_1=\mu_1S_1dt+\sigma_1S_1dW_1
```

```math
dS_2=\mu_2S_2dt+\sigma_2S_2dW_2
```

with correlated Brownian motions:

```math
dW_1dW_2=\rho dt
```

Under the risk-neutral measure:

```math
dS_i=rS_idt+\sigma_iS_idW_i^Q
```

The Brownian motions keep the same correlation:

```math
dW_1^QdW_2^Q=\rho dt
```

---

## 9. Two-Asset PDE

For a claim:

```math
C(t,S_1,S_2)
```

the two-asset Black-Scholes PDE is:

```math
C_t
+rS_1C_{S_1}
+rS_2C_{S_2}
+\frac{1}{2}\sigma_1^2S_1^2C_{S_1S_1}
+\frac{1}{2}\sigma_2^2S_2^2C_{S_2S_2}
+\rho\sigma_1\sigma_2S_1S_2C_{S_1S_2}
-rC
=0
```

The mixed derivative term appears because:

```math
dS_1dS_2=\rho\sigma_1\sigma_2S_1S_2dt
```

---

## 10. Exchange Options

An exchange option gives the right to exchange one asset for another.

Payoff:

```math
(S_2(T)-S_1(T))^+
```

This can be rewritten using the ratio:

```math
Z(T)=\frac{S_2(T)}{S_1(T)}
```

The relevant volatility is the volatility of the ratio:

```math
\sigma_Z=
\sqrt{
\sigma_1^2+\sigma_2^2-2\rho\sigma_1\sigma_2
}
```

The Margrabe formula is:

```math
C(t,S_1,S_2)=S_2N(d_1)-S_1N(d_2)
```

where:

```math
d_1=
\frac{
\ln(S_2/S_1)+\frac{1}{2}\sigma_Z^2(T-t)
}{
\sigma_Z\sqrt{T-t}
}
```

```math
d_2=d_1-\sigma_Z\sqrt{T-t}
```

Key intuition:

> Exchange options depend on relative performance, so correlation is crucial.

If correlation is high, the assets move together and the exchange option is less valuable.

If correlation is low or negative, relative movement is larger and the exchange option is more valuable.

---

## 11. Main Conceptual Links

The same BSM machinery is reused throughout the unit.

For each product:

1. Identify the underlying.
2. Find its risk-neutral dynamics.
3. Apply risk-neutral pricing or the PDE.
4. Adjust for dividends, foreign rates, futures, or correlation.

Main replacements:

| Case | Key Adjustment |
|---|---|
| Continuous dividends | `r` becomes `r-q` in stock drift |
| Discrete dividends | replace `S` by `S - PV(dividends)` |
| Currency options | replace `q` by `r_f` |
| Futures options | futures drift under `Q` is zero |
| Quanto forwards | add correlation adjustment |
| Multi-asset options | include mixed derivative term |
| Exchange options | use volatility of `S_2/S_1` |

---

## 12. Common Confusions

### Why does `-rC` remain in dividend and futures PDEs?

Because the option price is still discounted at the risk-free rate `r`.

### Why does `r_f` act like dividend yield?

Because holding foreign currency earns the foreign risk-free rate.

### Why does the futures PDE have no `FC_F` term?

Because futures prices have zero drift under `Q`.

### Why does quanto pricing depend on correlation?

Because the payoff involves a product of two stochastic variables.

### Why does the two-asset PDE have a mixed derivative?

Because the Brownian shocks are correlated.

### Why does an exchange option not have a normal strike `K`?

Because the strike is one unit of the other asset.

---

## 13. Exam Checklist

You should be able to:

- price calls with continuous dividend yield
- adjust for known discrete dividends
- write the PDE for options on futures
- state the futures option formula
- explain why currency options use `r_f` like dividend yield
- state the currency option formula
- explain the quanto adjustment
- identify common exotic option types
- explain why barrier and Asian options are path-dependent
- write the two-asset BSM PDE
- explain the mixed derivative term
- state the Margrabe exchange option formula
- explain how correlation affects exchange option value

---

## 14. Core Formulas

### Dividend stock under `Q`

```math
dS=(r-q)Sdt+\sigma SdW^Q
```

### Dividend call

```math
C=S e^{-q\tau}N(d_1)-K e^{-r\tau}N(d_2)
```

### Futures option call

```math
C=e^{-r\tau}\left[F N(d_1)-K N(d_2)\right]
```

### Currency option call

```math
C=R e^{-r_f\tau}N(d_1)-K e^{-r\tau}N(d_2)
```

### Quanto forward

```math
F=S(0)e^{(r+\rho\sigma_S\sigma_R)T}
```

### Two-asset PDE

```math
C_t
+rS_1C_{S_1}
+rS_2C_{S_2}
+\frac{1}{2}\sigma_1^2S_1^2C_{S_1S_1}
+\frac{1}{2}\sigma_2^2S_2^2C_{S_2S_2}
+\rho\sigma_1\sigma_2S_1S_2C_{S_1S_2}
-rC
=0
```

### Exchange option volatility

```math
\sigma_Z=
\sqrt{
\sigma_1^2+\sigma_2^2-2\rho\sigma_1\sigma_2
}
```

### Margrabe formula

```math
C=S_2N(d_1)-S_1N(d_2)
```

---

## Final Intuition

Module 7 shows that Black-Scholes-Merton is a flexible framework.

Most extensions do not require a new pricing theory.

They require correctly identifying how the underlying behaves under the risk-neutral measure.

Dividends, foreign interest rates, futures marking-to-market, and correlation all modify the effective dynamics.

Once those dynamics are known, the same no-arbitrage, PDE, and risk-neutral pricing ideas apply.
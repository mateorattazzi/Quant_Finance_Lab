# Module 7 — Multi-Asset BSM and Exchange Options

## 1. Big Picture

So far, Black-Scholes-Merton was applied to one underlying.

Now we extend it to two risky assets:

```math
S_1(t), \quad S_2(t)
```

This allows us to price claims whose payoff depends on both assets:

```math
g(S_1(T),S_2(T))
```

The same two pricing methods still apply:

1. risk-neutral expected value
2. PDE pricing

---

## 2. Two-Asset BSM Model

Each asset follows geometric Brownian motion:

```math
dS_1=\mu_1S_1dt+\sigma_1S_1dW_1
```

```math
dS_2=\mu_2S_2dt+\sigma_2S_2dW_2
```

The Brownian motions are correlated:

```math
E[W_1(t)W_2(t)]=\rho t
```

Equivalently:

```math
dW_1dW_2=\rho dt
```

where:

```math
-1\leq \rho \leq 1
```

---

## 3. Equivalent Independent Brownian Form

Instead of using correlated Brownian motions, we can use two independent Brownian motions:

```math
B_1, \quad B_2
```

Set:

```math
W_1=B_1
```

```math
W_2=\rho B_1+\sqrt{1-\rho^2}B_2
```

Then `W_2` is also Brownian motion and has correlation `rho` with `W_1`.

Why?

```math
E[W_1(t)W_2(t)]
=
E[B_1(t)(\rho B_1(t)+\sqrt{1-\rho^2}B_2(t))]
```

```math
=\rho E[B_1(t)^2]=\rho t
```

The second term is zero because `B_1` and `B_2` are independent.

---

## 4. Wealth Process With Two Stocks

Let:

- `X(t)` = total wealth
- `pi_1(t)` = amount invested in `S_1`
- `pi_2(t)` = amount invested in `S_2`

The amount in the bank is:

```math
X-\pi_1-\pi_2
```

The self-financing wealth process is:

```math
dX=
\frac{\pi_1}{S_1}dS_1
+
\frac{\pi_2}{S_2}dS_2
+
\frac{X-\pi_1-\pi_2}{B}dB
```

After substituting the asset dynamics:

```math
dX=
\left[
rX+\pi_1(\mu_1-r)+\pi_2(\mu_2-r)
\right]dt
+
\pi_1\sigma_1dW_1
+
\pi_2\sigma_2dW_2
```

---

## 5. Risk-Neutral Dynamics

Under the risk-neutral probability `Q`, discounted wealth processes must be martingales.

Therefore, each asset drift becomes `r`:

```math
dS_1=rS_1dt+\sigma_1S_1dW_1^Q
```

```math
dS_2=rS_2dt+\sigma_2S_2dW_2^Q
```

The Brownian motions under `Q` keep the same correlation:

```math
dW_1^QdW_2^Q=\rho dt
```

---

## 6. Pricing a Two-Asset European Claim

For a European payoff:

```math
g(S_1(T),S_2(T))
```

the risk-neutral price is:

```math
C(t,S_1,S_2)
=
E_t^Q\left[
e^{-r(T-t)}g(S_1(T),S_2(T))
\right]
```

This expectation may be computed analytically in special cases, or numerically by simulation.

---

## 7. Two-Asset Black-Scholes PDE

Let:

```math
C=C(t,S_1,S_2)
```

Apply two-dimensional Ito's rule under `Q`, then discount and set the drift equal to zero.

The PDE is:

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

Terminal condition:

```math
C(T,S_1,S_2)=g(S_1,S_2)
```

---

## 8. Hedging Interpretation

The replicating portfolio holds:

```math
C_{S_1}
```

shares of asset `S_1`, and:

```math
C_{S_2}
```

shares of asset `S_2`.

So the deltas are:

```math
\Delta_1=C_{S_1}
```

```math
\Delta_2=C_{S_2}
```

---

## 9. Exchange Option

An exchange option gives the right to exchange one asset for another.

Payoff:

```math
(S_2(T)-S_1(T))^+
```

You exercise if:

```math
S_2(T)>S_1(T)
```

This is like a call option where the underlying is the ratio:

```math
Z(T)=\frac{S_2(T)}{S_1(T)}
```

because:

```math
(S_2(T)-S_1(T))^+
=
S_1(T)\left(\frac{S_2(T)}{S_1(T)}-1\right)^+
```

---

## 10. Key Reduction

Guess that the price has the form:

```math
C(t,S_1,S_2)=S_1D(t,Z)
```

where:

```math
Z=\frac{S_2}{S_1}
```

Then `D` behaves like a Black-Scholes call price with:

- underlying `Z`
- strike `1`
- interest rate `0`
- volatility:

```math
\sigma_Z=
\sqrt{
\sigma_1^2+\sigma_2^2-2\rho\sigma_1\sigma_2
}
```

This volatility comes from the relative movement between the two assets.

---

## 11. Margrabe Exchange Option Formula

The exchange option price is:

```math
C(t,S_1,S_2)
=
S_2N(d_1)-S_1N(d_2)
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

and:

```math
\sigma_Z=
\sqrt{
\sigma_1^2+\sigma_2^2-2\rho\sigma_1\sigma_2
}
```

---

## 12. Intuition for Correlation

The exchange option depends on relative performance.

If correlation is high, the assets move together, so the ratio `S_2/S_1` is less volatile.

If correlation is low or negative, the ratio is more volatile.

Therefore:

```math
\sigma_Z^2=\sigma_1^2+\sigma_2^2-2\rho\sigma_1\sigma_2
```

Higher `rho` lowers the exchange-option volatility.

Lower `rho` raises it.

---

## 13. Common Confusions

### Why is there a mixed derivative in the PDE?

Because the Brownian motions are correlated.

The Ito cross term is:

```math
dS_1dS_2=\rho\sigma_1\sigma_2S_1S_2dt
```

This produces:

```math
\rho\sigma_1\sigma_2S_1S_2C_{S_1S_2}
```

### Why does the exchange option have no strike `K`?

The strike is effectively one unit of asset `S_1`.

You pay asset `S_1` to receive asset `S_2`.

### Why does the formula contain no explicit interest rate?

Both assets are tradable and the payoff is an exchange between them.

The interest-rate effect cancels in the final Margrabe formula.

---

## 14. Exam Notes

You should be able to:

- write a two-asset BSM model
- explain correlated Brownian motions
- rewrite correlated Brownian motions using independent Brownian motions
- write the risk-neutral dynamics for two assets
- write the two-asset BSM PDE
- identify the mixed derivative term
- explain two-asset deltas
- define an exchange option
- explain why the ratio `S_2/S_1` matters
- state the Margrabe formula
- explain the role of correlation

---

## 15. Core Formulas

### Correlation

```math
dW_1dW_2=\rho dt
```

### Two-asset risk-neutral dynamics

```math
dS_i=rS_idt+\sigma_iS_idW_i^Q
```

### Two-asset risk-neutral price

```math
C(t,S_1,S_2)
=
E_t^Q\left[
e^{-r(T-t)}g(S_1(T),S_2(T))
\right]
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

### Exchange option payoff

```math
(S_2(T)-S_1(T))^+
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
C(t,S_1,S_2)
=
S_2N(d_1)-S_1N(d_2)
```

---

## Final Intuition

Multi-asset Black-Scholes keeps the same pricing logic, but adds correlation.

Correlation enters through the Ito cross term and creates the mixed derivative in the PDE.

For exchange options, the key object is the ratio `S_2/S_1`.

The volatility of that ratio depends on both asset volatilities and their correlation.
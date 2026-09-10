# Module 7 — Currency Options and Quanto Forwards

## 1. Big Picture

This section applies Black-Scholes-Merton pricing to two related cases:

1. Currency options
2. Quanto forwards

Both use risk-neutral pricing, but now the underlying may involve exchange rates and more than one Brownian motion.

The key ideas are:

- an exchange rate behaves like a dividend-paying asset
- the foreign interest rate plays the role of the dividend yield
- under the domestic risk-neutral measure, the exchange rate drift becomes `r - r_f`
- quanto contracts require handling correlation between the exchange rate and another asset

---

## 2. Exchange Rate Setup

Let `R(t)` be the exchange rate.

Interpretation:

```math
R(t)=\text{domestic currency value of 1 unit of foreign currency}
```

Example:

If domestic currency is USD and foreign currency is EUR, then:

```math
R(t)=\text{USD value of 1 EUR}
```

A currency call option gives the right to buy one unit of foreign currency at strike `K`.

The payoff in domestic currency is:

```math
(R(T)-K)^+
```

---

## 3. Exchange Rate Dynamics

The exchange rate is modeled as a geometric Brownian motion:

```math
dR(t)=\mu_R R(t)dt+\sigma_R R(t)dW(t)
```

where:

- `mu_R` is the real-world drift of the exchange rate
- `sigma_R` is exchange rate volatility
- `W(t)` is Brownian motion

This is a Black-Scholes-style model for the exchange rate.

---

## 4. Currency as a Dividend-Paying Asset

For a domestic investor, foreign currency is like a risky asset that pays a continuous dividend.

Why?

If you hold foreign currency, you can invest it in the foreign bank account and earn the foreign risk-free rate:

```math
r_f
```

So the foreign interest rate plays the same role as a dividend yield.

Analogy:

```math
q \longleftrightarrow r_f
```

where:

- `q` = dividend yield for a stock
- `r_f` = foreign interest rate for a currency

---

## 5. Domestic and Foreign Bank Accounts

Domestic bank account:

```math
B_d(t)=e^{rt}
```

Foreign bank account:

```math
B_f(t)=e^{r_f t}
```

The domestic value of one unit invested in the foreign bank account is:

```math
R^*(t)=R(t)e^{r_f t}
```

This is the foreign bank account converted into domestic currency.

---

## 6. Dynamics of the Domestic Value of the Foreign Bank Account

Using the product rule:

```math
R^*(t)=R(t)e^{r_f t}
```

The dynamics become:

```math
dR^*(t)=R^*(t)\left[(\mu_R+r_f)dt+\sigma_R dW(t)\right]
```

The drift includes:

```math
\mu_R+r_f
```

because the domestic value changes due to:

1. movement in the exchange rate
2. interest earned in the foreign bank account

---

## 7. Risk-Neutral Measure for Currency Options

Under the domestic risk-neutral probability `Q`, discounted domestic wealth must be a martingale.

This implies that the exchange rate under `Q` has drift:

```math
r-r_f
```

So under `Q`:

```math
dR(t)=(r-r_f)R(t)dt+\sigma_R R(t)dW^Q(t)
```

This is exactly like the dividend-paying stock case:

```math
dS(t)=(r-q)S(t)dt+\sigma S(t)dW^Q(t)
```

with:

```math
q=r_f
```

---

## 8. Currency Option Formula

A European call on the exchange rate has payoff:

```math
(R(T)-K)^+
```

The Black-Scholes formula is the same as for a dividend-paying stock, replacing:

```math
S \rightarrow R
```

and:

```math
q \rightarrow r_f
```

So:

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

and:

```math
d_2=d_1-\sigma_R\sqrt{T-t}
```

Equivalently:

```math
d_2=
\frac{
\ln(R/K)+\left(r-r_f-\frac{1}{2}\sigma_R^2\right)(T-t)
}{
\sigma_R\sqrt{T-t}
}
```

---

## 9. Intuition for Currency Options

The call option holder does not receive the foreign interest rate before maturity.

The owner of foreign currency can earn `r_f`.

The option holder cannot.

Therefore, the foreign interest rate reduces the effective value of the exchange rate in the option formula, just like dividends reduce the value of a stock call.

That is why the first term is:

```math
R e^{-r_f(T-t)}N(d_1)
```

not simply:

```math
R N(d_1)
```

---

## 10. Quanto Forward Setup

A quanto forward is a contract linked to a domestic stock or index, but paid in foreign currency.

Example:

- `S(T)` is a domestic stock/index value
- payoff is `S(T)-F`
- but the payoff is paid in foreign currency

To price it in domestic currency, multiply by the exchange rate:

```math
R(T)(S(T)-F)
```

The domestic value of the payoff is:

```math
S(T)R(T)-F R(T)
```

The goal is usually to choose `F` so that the initial value of the contract is zero.

---

## 11. Models Under the Domestic Risk-Neutral Measure

Exchange rate under `Q`:

```math
dR(t)=(r-r_f)R(t)dt+\sigma_R R(t)dW^Q(t)
```

Domestic stock or index under `Q`, assuming no dividends:

```math
dS(t)=rS(t)dt+\sigma_S S(t)dZ^Q(t)
```

The two Brownian motions may be correlated:

```math
E^Q[W^Q(t)Z^Q(t)]=\rho t
```

Equivalently, in differential notation:

```math
dW^Q(t)dZ^Q(t)=\rho dt
```

where `rho` is the instantaneous correlation between the exchange rate and the stock/index.

---

## 12. Product Dynamics for `S(t)R(t)`

To price the quanto payoff, we need the dynamics of:

```math
S(t)R(t)
```

Using Ito's product rule:

```math
d(SR)=S\,dR+R\,dS+dS\,dR
```

The cross term is important because the Brownian motions are correlated.

Since:

```math
dS=\sigma_S S dZ^Q+\text{drift}
```

and:

```math
dR=\sigma_R R dW^Q+\text{drift}
```

the Ito cross term is:

```math
dS\,dR=\rho\sigma_S\sigma_R SRdt
```

So the drift of `SR` under `Q` becomes:

```math
(r-r_f+r+\rho\sigma_S\sigma_R)SR
```

Therefore:

```math
d(SR)
=
SR(r-r_f+r+\rho\sigma_S\sigma_R)dt
+
\text{Brownian terms}
```

---

## 13. Expected Value Rule

If a process satisfies:

```math
dX(t)=aX(t)dt+\text{Brownian terms}
```

where `a` is constant, then:

```math
E[X(T)]=X(0)e^{aT}
```

Reason:

- Brownian stochastic integral terms have expectation zero
- the expected value follows the ordinary differential equation:

```math
\frac{d}{dt}E[X(t)]=aE[X(t)]
```

whose solution is:

```math
E[X(T)]=X(0)e^{aT}
```

This rule is used to compute:

```math
E^Q[R(T)]
```

and:

```math
E^Q[S(T)R(T)]
```

---

## 14. Computing the Quanto Forward Price

The domestic value of the payoff is:

```math
R(T)(S(T)-F)
```

Risk-neutral value at time 0:

```math
e^{-rT}E^Q[R(T)(S(T)-F)]
```

Set initial value equal to zero:

```math
e^{-rT}E^Q[R(T)(S(T)-F)]=0
```

So:

```math
E^Q[S(T)R(T)]-F E^Q[R(T)]=0
```

Therefore:

```math
F=
\frac{
E^Q[S(T)R(T)]
}{
E^Q[R(T)]
}
```

---

## 15. Expected Values

From the exchange rate dynamics:

```math
E^Q[R(T)]=R(0)e^{(r-r_f)T}
```

From the product dynamics:

```math
E^Q[S(T)R(T)]
=
S(0)R(0)e^{(2r-r_f+\rho\sigma_S\sigma_R)T}
```

Substitute into the ratio:

```math
F=
\frac{
S(0)R(0)e^{(2r-r_f+\rho\sigma_S\sigma_R)T}
}{
R(0)e^{(r-r_f)T}
}
```

Cancel common terms:

```math
F=S(0)e^{(r+\rho\sigma_S\sigma_R)T}
```

---

## 16. Quanto Forward Formula

The quanto forward price is:

```math
F=S(0)e^{(r+\rho\sigma_S\sigma_R)T}
```

The extra term is:

```math
\rho\sigma_S\sigma_R
```

This is a covariance adjustment.

It comes from the Ito cross term:

```math
dS\,dR
```

---

## 17. Intuition for the Quanto Adjustment

A regular forward price on a non-dividend-paying stock is:

```math
F=S(0)e^{rT}
```

A quanto forward adds the covariance adjustment:

```math
F=S(0)e^{(r+\rho\sigma_S\sigma_R)T}
```

If the stock/index and exchange rate are positively correlated, then:

```math
\rho\sigma_S\sigma_R>0
```

and the quanto forward price is higher.

If they are negatively correlated, then:

```math
\rho\sigma_S\sigma_R<0
```

and the quanto forward price is lower.

---

## 18. Why This Cannot Be Derived by Simple No-Arbitrage Alone

For a standard forward, the price can be obtained by model-free no-arbitrage.

For a quanto forward, the formula depends on:

- stock volatility
- exchange rate volatility
- correlation between stock and exchange rate

So it is model-dependent.

The formula relies on the Black-Scholes-Merton assumptions and risk-neutral pricing.

---

## 19. Common Confusions

### Why does `r_f` act like a dividend yield?

Because holding foreign currency allows the investor to earn the foreign risk-free interest rate.

This is like receiving a continuous yield.

### Why is the exchange rate drift under `Q` equal to `r-r_f`?

The domestic value of foreign investment must earn the domestic risk-free rate under `Q`.

Since the foreign account already earns `r_f`, the exchange rate itself must drift at `r-r_f`.

### Why does the quanto formula contain correlation?

Because the payoff in domestic currency is the product `S(T)R(T)`.

When applying Ito's rule to a product driven by two correlated Brownian motions, a cross term appears.

### Why does the Brownian part disappear when computing expectations?

Because stochastic integrals with respect to Brownian motion have expectation zero.

Only the drift term determines the expected value.

---

## 20. Core Formulas

### Exchange rate under `Q`

```math
dR(t)=(r-r_f)R(t)dt+\sigma_R R(t)dW^Q(t)
```

### Currency call option

```math
C(t,R)=R e^{-r_f(T-t)}N(d_1)-K e^{-r(T-t)}N(d_2)
```

### Currency option `d_1`

```math
d_1=
\frac{
\ln(R/K)+\left(r-r_f+\frac{1}{2}\sigma_R^2\right)(T-t)
}{
\sigma_R\sqrt{T-t}
}
```

### Currency option `d_2`

```math
d_2=d_1-\sigma_R\sqrt{T-t}
```

### Brownian correlation

```math
dW^Q(t)dZ^Q(t)=\rho dt
```

### Ito product rule for `SR`

```math
d(SR)=S\,dR+R\,dS+dS\,dR
```

### Cross term

```math
dS\,dR=\rho\sigma_S\sigma_R SRdt
```

### Expected value rule

```math
dX=aXdt+\text{Brownian terms}
\quad\Longrightarrow\quad
E[X(T)]=X(0)e^{aT}
```

### Quanto forward price

```math
F=S(0)e^{(r+\rho\sigma_S\sigma_R)T}
```

---

## Final Intuition

Currency options are priced like options on dividend-paying stocks.

The foreign interest rate plays the role of the dividend yield, so the exchange rate drift under the domestic risk-neutral measure is `r-r_f`.

Quanto forwards add one new ingredient: correlation.

Because the domestic payoff involves the product `S(T)R(T)`, Ito's product rule produces a cross term involving `rho`, `sigma_S`, and `sigma_R`.

That covariance adjustment is what makes the quanto forward price different from the ordinary forward price.
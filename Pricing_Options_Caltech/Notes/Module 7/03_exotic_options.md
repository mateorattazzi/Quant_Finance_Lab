# Module 7 — Exotic Options

## 1. Big Picture

Exotic options are options with payoffs more complex than standard calls and puts.

The pricing logic is still the same:

```math
V(t)=E_t^Q\left[e^{-r(T-t)}\text{payoff}\right]
```

But the payoff may depend on:

- whether the stock crosses a barrier
- the average stock price
- the value of another option
- a strike determined in the future
- a future choice between call and put

The economics are often simple, but the calculations can become much harder.

---

## 2. Barrier Options

Barrier options depend on whether the underlying crosses a certain level before maturity.

Examples:

- up-and-out
- up-and-in
- down-and-out
- down-and-in

An up-and-out call pays like a normal call only if the stock never crosses the upper barrier.

If the barrier is crossed, the option becomes worthless.

---

## 3. Why Barrier Options Are Cheaper

A barrier option usually pays less than the corresponding vanilla option.

Reason:

It has the same payoff as a vanilla option in some scenarios, but pays zero in others.

So:

```math
\text{barrier option price} \leq \text{vanilla option price}
```

Investors buy them when they believe the barrier will not be crossed and want a cheaper option.

---

## 4. Pricing Barrier Options

Barrier option pricing requires the joint distribution of:

```math
S(T)
```

and the maximum or minimum of the stock price before maturity.

For example, for an up-and-out option, we need information about:

```math
\max_{0\leq u\leq T} S(u)
```

This is more complex than pricing a vanilla option, which only depends on `S(T)`.

In Black-Scholes-Merton, explicit formulas exist, but the course does not derive them.

---

## 5. Hedging Barrier Options

Barrier options can be difficult to hedge.

The problem is that the payoff can jump around the barrier.

For an up-and-out call:

- below the barrier, the option may have positive value
- if the barrier is crossed, the option becomes zero

Near maturity and near the barrier, delta can change very sharply.

This may force the hedger to move quickly between long and short stock positions.

That can be expensive because of:

- transaction costs
- liquidity problems
- frequent rebalancing

---

## 6. Practical Barrier Hedging Idea

One practical approach is to hedge as if the barrier were slightly higher.

For an up-and-out call with barrier `B`, hedge using a higher barrier:

```math
B' > B
```

This avoids extreme hedging behavior just below `B`.

The drawback is that the hedge is more expensive.

---

## 7. Asian Options

Asian options depend on the average price of the underlying over time.

Example payoff:

```math
\left(\bar{S}-K\right)^+
```

where:

```math
\bar{S}=\text{average stock price over the option life}
```

They are useful when the underlying is very volatile, such as in some energy markets.

Averages are less volatile than single final prices, so Asian options are often more stable.

---

## 8. Pricing Asian Options

Asian options depend on an average of stock prices, not only on `S(T)`.

This means pricing requires the distribution of an average of lognormal variables.

There is usually no simple closed-form Black-Scholes formula.

Pricing often requires numerical methods, transforms, or simulation.

---

## 9. Compound Options

A compound option is an option on another option.

Example:

A call on a call gives the right at time `T_1` to buy a call option that expires later at time `T_2`.

The payoff at `T_1` is:

```math
(C(T_1,S(T_1);T_2,K)-K_1)^+
```

where:

- `K_1` is the strike of the compound option
- `C(T_1,S(T_1);T_2,K)` is the value at `T_1` of the underlying call

Pricing uses risk-neutral expectation, but the payoff contains the Black-Scholes formula itself, so the computation is more complicated.

---

## 10. Forward Start Options

A forward start call is a call option whose strike is set in the future.

Typical payoff:

```math
(S(T)-S(T_1))^+
```

At time `T_1`, the strike becomes:

```math
S(T_1)
```

So the option starts at the money at `T_1`.

---

## 11. Pricing Forward Start Calls

At time `T_1`, the option is an at-the-money call with maturity `T-T_1`.

Using the Black-Scholes-Merton scaling and martingale property, the time 0 price is:

```math
C_{FS}(0)=C_{BSM}(0,S(0),S(0),r,\sigma,T-T_1)
```

Meaning:

Price it like a standard Black-Scholes call with:

- initial stock price `S(0)`
- strike `S(0)`
- maturity `T-T_1`

The key idea is that under BSM, future percentage returns are independent of the past and have the same distribution over equal time intervals.

---

## 12. Chooser Options

A chooser option gives the holder the right to decide later whether the option will be a call or a put.

At decision time `T_1`, the holder chooses the more valuable option:

```math
\max(C(T_1),P(T_1))
```

with final maturity `T`.

---

## 13. Pricing Chooser Options

Use put-call parity at time `T_1`:

```math
C(T_1)-P(T_1)=S(T_1)-Ke^{-r(T-T_1)}
```

So:

```math
P(T_1)=C(T_1)+Ke^{-r(T-T_1)}-S(T_1)
```

Then:

```math
\max(C(T_1),P(T_1))
=
C(T_1)+\left(Ke^{-r(T-T_1)}-S(T_1)\right)^+
```

Therefore, a chooser option can be priced as:

1. a call with maturity `T` and strike `K`
2. plus a put with maturity `T_1` and strike `Ke^{-r(T-T_1)}`

So:

```math
V_{\text{chooser}}(t)
=
C(t;T,K)
+
P(t;T_1,Ke^{-r(T-T_1)})
```

---

## 14. Key Intuitions

Barrier options are path-dependent because they depend on whether the stock crosses a level.

Asian options are path-dependent because they depend on an average.

Compound options are options on options.

Forward start options have a strike determined in the future.

Chooser options use put-call parity to turn a complicated choice into a call plus a put.

---

## 15. Core Formulas

### Risk-neutral pricing

```math
V(t)=E_t^Q\left[e^{-r(T-t)}\text{payoff}\right]
```

### Barrier condition example

```math
\max_{0\leq u\leq T}S(u)<B
```

### Asian average

```math
\bar{S}=\frac{1}{T}\int_0^T S(u)du
```

### Forward start payoff

```math
(S(T)-S(T_1))^+
```

### Chooser payoff at decision time

```math
\max(C(T_1),P(T_1))
```

### Chooser decomposition

```math
V_{\text{chooser}}(t)
=
C(t;T,K)
+
P(t;T_1,Ke^{-r(T-T_1)})
```

---

## 16. Exam Notes

You should be able to:

- define barrier, Asian, compound, forward start, and chooser options
- explain why barrier options are usually cheaper than vanilla options
- explain why barrier options may be hard to hedge
- explain why Asian options are useful for volatile underlyings
- explain why Asian options usually need numerical pricing
- explain the forward start option idea
- explain the chooser option decomposition using put-call parity

---

## Final Intuition

Exotic options use the same no-arbitrage and risk-neutral pricing logic as vanilla options.

The difficulty is not the pricing principle.

The difficulty is the payoff structure.

Some exotic payoffs depend on the path, some depend on another option, and some depend on a future decision.

The more complex the payoff, the harder it is to compute and hedge.s
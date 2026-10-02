# Joint tight lower bound for zero-order nonsmooth nonconvex stochastic optimization

## Status

**Partially resolved.** [Zhang et al. (2026)](https://arxiv.org/abs/2610.00275v1) solve the Euclidean query-ball formulation with a local gap and a stationary-point existence promise. The original global-gap, unrestricted-query variant remains open. See the [project and scope assessment](../../projects/zeroth-order-nonconvex-ball-lower-bound/).

## Problem definition

Minimize a Lipschitz, potentially nonsmooth and nonconvex population objective $`f:\mathbb R^d\to\mathbb R`$, with $`f(x)=\mathbb E_\xi F(x;\xi)`$. Matching Kornowski and Shamir's Assumption 2 and Theorem 5, sample functions have Lipschitz moduli $`L(\xi)`$ satisfying $`\mathbb E L(\xi)^2\leq L_0^2`$, and the initial point has a finite **global** gap:

```math
f(x_0)-\inf_{x\in\mathbb R^d}f(x)\leq\Delta.
```

The output is an ambient $`(\delta,\epsilon)`$-Goldstein stationary point:

```math
G_\delta(f,\widehat x)
=\operatorname{dist}\!\left(0,
\operatorname{cl}\operatorname{conv}
\bigcup_{\|y-\widehat x\|_2\leq\delta}\partial^C f(y)\right)
\leq\epsilon.
```

Use a fixed constant success probability, such as $`1/2`$. The known expected-residual upper bound gives this convention by running at tolerance $`\epsilon/2`$ and applying Markov's inequality.

## Oracle model

The algorithm observes scalar sample-function values $`F(x;\xi)`$ and receives no gradients. Queries and output may be anywhere in $`\mathbb R^d`$. Common-sample evaluations, including the two-point estimator in the cited algorithm, are allowed; each scalar observation costs one unit, so a pair costs two. The noise assumption is the sample-Lipschitz second-moment bound above, rather than an unspecified additive-noise variance bound. A lower-bound statement must specify adaptivity, randomization, and any limits on sample reuse.

## Known upper bound and target

Kornowski and Shamir give an upper bound of

```math
O\!\left(\frac{dL_0^2\Delta}{\delta\epsilon^3}\right).
```

The original target is a joint lower bound with the same parameter dependence under the same global-gap and unrestricted-query assumptions, for adaptive randomized algorithms. With $`L_0=\Delta=1`$, it is $`\Omega(d\delta^{-1}\epsilon^{-3})`$. Separately optimal dimension and accuracy bounds do not establish their product on one hard family.

## Related bounded-domain result and remaining gap

Corollary 4.2 of Zhang et al. v1 reports

```math
\Omega\!\left(\frac{dL_0^2\Delta}{\delta\epsilon^3}\right)
```

scalar evaluations, even with arbitrary reuse of retained sample functions, when

```math
0<\epsilon\leq cL_0,\qquad
\Delta\geq C\delta\epsilon,\qquad
d\geq C\left[1+\log\left(2+\frac{\Delta L_0^2}{\delta\epsilon^3}\right)\right].
```

However, queries and output are confined to a constructed ball $`X=B_2^d(x_0,R)`$ with $`R=\Theta(\Delta/\epsilon)`$, and only $`f(x_0)-\min_X f\leq\Delta`$ is required. Each hard instance contains a stationary point in the ball. Its linear carrier nevertheless gives $`\inf_{\mathbb R^d}f=-\infty`$ (Section 7), violating this benchmark's global-gap condition.

Proposition A.1 supplies a local-gap upper bound only at a larger radius, $`R\geq C_0(\Delta/\epsilon+\delta)`$. The lower-bound construction has $`R\leq\Delta/(8\epsilon)`$, so these results do not establish a matching minimax rate at a common radius. The unrestricted global-gap joint lower bound remains open and this result is not counted as a benchmark solution.

The [project record](../../projects/zeroth-order-nonconvex-ball-lower-bound/) documents the theorem, smooth reduction, AI disclosure, verification limits, and benchmark timeline. The v1 statement comparison was made on 2026-10-02; no independent complete proof audit or human repository verification is recorded.

## References

- [Kornowski and Shamir, *An Algorithm with Optimal Dimension-Dependence for Zero-Order Nonsmooth Nonconvex Stochastic Optimization*, JMLR 2024](https://arxiv.org/abs/2307.04504)
- [Zhang et al., *Joint Lower Bounds for Zeroth-Order Nonconvex Optimization on Euclidean Balls*, v1, 2026](https://arxiv.org/abs/2610.00275v1)

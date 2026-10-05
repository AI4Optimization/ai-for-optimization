# [RESOLVED] Tight lower bound for exact-value zeroth-order smooth convex optimization

## Status

**Resolved.** [Dorn et al. (2026)](https://arxiv.org/abs/2610.00345v1) prove the matching lower bound for adaptive randomized exact-value algorithms with unrestricted queries. Their result complements the earlier deterministic bounded-query theorem of [Wu et al. (2026)](https://arxiv.org/abs/2609.18230).

## Problem definition

Minimize a convex differentiable function $f$ on the Euclidean ball $B_2(R)\subset\mathbb R^d$, assuming $\nabla f$ is $L$-Lipschitz. The algorithm must return $\hat x$ satisfying $\mathbb E[f(\hat x)-\min_{B_2(R)}f]\leq\epsilon$ (or a constant-probability analogue).

## Oracle model

An exact-value zeroth-order oracle returns the scalar $f(x)$ at any adaptively chosen $x$. Algorithms may be randomized and queries need not be nonadaptive. No gradient, noisy side channel, or higher-order information is available. Complexity is the number of function-value queries. The 2026 deterministic theorem additionally restricts every query and the output to $B_2(R)$ and places the unique minimizer in $B_2(R/2)$; it does not cover queries outside that ball.

## Resolution

Recent near-optimal $\Omega(d\epsilon^{-2})$-type lower bounds cover Lipschitz convex functions that may be nonsmooth. For the smooth class, Wu et al. prove that every **deterministic adaptive** exact-value method with bounded queries needs

```math
\Omega\!\left(d\min\left\{\sqrt{\frac{LR^2}{\epsilon}},\left(\frac{d}{\log(ed)}\right)^{1/3}\right\}\right)
```

queries. This matches their $O(d\sqrt{LR^2/\epsilon})$ upper bound when $LR^2(\log(ed)/d)^{2/3}\leq\epsilon\leq cLR^2$ for a universal constant $c>0$. At higher accuracy the proved lower bound saturates. See the [deterministic result project](../../projects/zeroth-order-smooth-convex-deterministic-lower-bound/).

[Dorn et al. (2026)](https://arxiv.org/abs/2610.00345v1) close the randomized gap. For globally $`L`$-smooth convex functions with a minimizer in $`\mathbb B_2^d(R)`$, they prove for adaptive randomized algorithms with unrestricted queries

```math
\Omega\!\left(
d\min\!\left\{d,\sqrt{\frac{LR^2}{\epsilon}}\right\}
\right).
```

The bound holds already for quadratics and has no logarithmic loss. In the range $`LR^2/d^2\leq\epsilon\leq LR^2/32`$, it matches the upper bound and gives $`\Theta(d\sqrt{LR^2/\epsilon})`$. See the [combined result project](../../projects/zeroth-order-smooth-convex-deterministic-lower-bound/).

## Reference

- [Zhang, Zhang, Qi, and Lin, zeroth-order convex lower bounds (2026)](https://arxiv.org/abs/2607.16558)
- [Wu et al., *Near-Optimal Deterministic Exact-Value Complexity for Smooth Convex Optimization* (2026)](https://arxiv.org/abs/2609.18230)
- [Dorn et al., *Lower Bounds For Gradient-Free Convex Optimization And Convex-Concave Saddle-Point Problems* (2026)](https://arxiv.org/abs/2610.00345v1)

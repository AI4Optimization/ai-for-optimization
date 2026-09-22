# Tight lower bound for exact-value zeroth-order smooth convex optimization

## Status

**Partially resolved.** [Wu et al. (2026)](https://arxiv.org/abs/2609.18230) establish the matching deterministic adaptive lower bound in a bounded-query, moderate-accuracy regime. The lower bound for randomized adaptive algorithms remains open, as do the high-accuracy and unrestricted-query extensions.

## Problem definition

Minimize a convex differentiable function $f$ on the Euclidean ball $B_2(R)\subset\mathbb R^d$, assuming $\nabla f$ is $L$-Lipschitz. The algorithm must return $\hat x$ satisfying $\mathbb E[f(\hat x)-\min_{B_2(R)}f]\leq\epsilon$ (or a constant-probability analogue).

## Oracle model

An exact-value zeroth-order oracle returns the scalar $f(x)$ at any adaptively chosen $x$. Algorithms may be randomized and queries need not be nonadaptive. No gradient, noisy side channel, or higher-order information is available. Complexity is the number of function-value queries. The 2026 deterministic theorem additionally restricts every query and the output to $B_2(R)$ and places the unique minimizer in $B_2(R/2)$; it does not cover queries outside that ball.

## Known bounds and open target

Recent near-optimal $\Omega(d\epsilon^{-2})$-type lower bounds cover Lipschitz convex functions that may be nonsmooth. For the smooth class, Wu et al. prove that every **deterministic adaptive** exact-value method with bounded queries needs

$$
\Omega\!\left(d\min\left\{\sqrt{\frac{LR^2}{\epsilon}},\left(\frac{d}{\log(ed)}\right)^{1/3}\right\}\right)
$$

queries. This matches their $O(d\sqrt{LR^2/\epsilon})$ upper bound when $LR^2(\log(ed)/d)^{2/3}\leq\epsilon\leq cLR^2$ for a universal constant $c>0$. At higher accuracy the proved lower bound saturates. See the [deterministic result project](../../projects/zeroth-order-smooth-convex-deterministic-lower-bound/).

**Open target:** prove the corresponding $\Omega(d\sqrt{LR^2/\epsilon})$ lower bound for **randomized adaptive** exact-value methods in the appropriate regime. Extending the deterministic lower bound to unrestricted query locations and removing its high-accuracy saturation are separate open questions. A lower bound against deterministic algorithms alone cannot be transferred to randomized algorithms by a minimax argument without a common hard distribution.

## Reference

- [Zhang, Zhang, Qi, and Lin, zeroth-order convex lower bounds (2026)](https://arxiv.org/abs/2607.16558)
- [Wu et al., *Near-Optimal Deterministic Exact-Value Complexity for Smooth Convex Optimization* (2026)](https://arxiv.org/abs/2609.18230)

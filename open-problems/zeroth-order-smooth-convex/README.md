# Tight lower bound for exact-value zeroth-order smooth convex optimization

## Status

**Open; not solved by AI.**

## Problem definition

Minimize a convex differentiable function $f$ on the Euclidean ball $B_2(R)\subset\mathbb R^d$, assuming $\nabla f$ is $L$-Lipschitz. The algorithm must return $\hat x$ satisfying $\mathbb E[f(\hat x)-\min_{B_2(R)}f]\leq\epsilon$ (or a constant-probability analogue).

## Oracle model

An exact-value zeroth-order oracle returns the scalar $f(x)$ at any adaptively chosen $x$. Algorithms may be randomized and queries need not be nonadaptive. No gradient, noisy side channel, or higher-order information is available. Complexity is the number of function-value queries.

## Known bounds and open target

Recent near-optimal $\Omega(d\epsilon^{-2})$-type lower bounds cover Lipschitz convex functions that may be nonsmooth. For the smooth class above, prove $\Omega(d\epsilon^{-1/2})$ in the normalized regime, or equivalently the correctly scaled bound with explicit $L$, $R$, and $\epsilon$ dependence.

## Reference

- [Zhang, Zhang, Qi, and Lin, zeroth-order convex lower bounds (2026)](https://arxiv.org/abs/2607.16558)

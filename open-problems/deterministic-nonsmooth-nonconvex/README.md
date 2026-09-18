# Tight complexity bound for deterministic first-order nonsmooth nonconvex optimization

## Status

**Resolved by [Kornowski (2026)](https://arxiv.org/abs/2609.17780).** The paper proves the matching lower bound for randomized zero-respecting first-order algorithms, even when each oracle response reveals the entire Clarke subdifferential.

## Problem definition

Minimize a Lipschitz, potentially nonsmooth and nonconvex function $f:\mathbb R^d\to\mathbb R$, assuming a bounded initial objective gap. The goal is a $(\delta,\epsilon)$-stationary point under the Goldstein-style stationarity notion used by O2NC.

## Oracle model

At an adaptive query point, the deterministic and noiseless first-order oracle returns a function value and one valid (sub)gradient. Complexity counts oracle calls. The desired lower bound should cover the same algorithm class, regularity assumptions, and output convention as the O2NC upper bound; it must not use stochastic gradient noise as the source of hardness.

## Resolution

O2NC attains $O(\delta^{-1}\epsilon^{-3})$ calls, and the earlier work proves a matching stochastic lower bound. Kornowski (2026) proves that, for an $L$-Lipschitz objective with initial gap at most $\Delta$, finding a $(\delta,\epsilon)$-Goldstein stationary point requires

$$
\Omega\!\left(\frac{\Delta L^2}{\delta\epsilon^3}\right)
$$

first-order queries in the stated parameter regime. This matches the known upper bound up to absolute constants and shows that noiseless gradients do not improve the worst-case rate in this framework.

The theorem is formulated for possibly randomized **zero-respecting** algorithms. It should not be cited as a lower bound for completely unrestricted algorithms without preserving that qualification.

## Reference

- [Cutkosky, Mehta, and Orabona, *Optimal Stochastic Non-smooth Non-convex Optimization through Online-to-Non-convex Conversion* (2023)](https://arxiv.org/abs/2302.03775)
- [Kornowski, *The Complexity of Finding Stationary Points in Nonsmooth Nonconvex Optimization* (2026)](https://arxiv.org/abs/2609.17780)

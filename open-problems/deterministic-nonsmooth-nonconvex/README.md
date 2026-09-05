# Tight complexity bound for deterministic first-order nonsmooth nonconvex optimization

## Status

**Open; not solved by AI.**

## Problem definition

Minimize a Lipschitz, potentially nonsmooth and nonconvex function $f:\mathbb R^d\to\mathbb R$, assuming a bounded initial objective gap. The goal is a $(\delta,\epsilon)$-stationary point under the Goldstein-style stationarity notion used by O2NC.

## Oracle model

At an adaptive query point, the deterministic and noiseless first-order oracle returns a function value and one valid (sub)gradient. Complexity counts oracle calls. The desired lower bound should cover the same algorithm class, regularity assumptions, and output convention as the O2NC upper bound; it must not use stochastic gradient noise as the source of hardness.

## Known bounds and open target

O2NC attains $O(\delta^{-1}\epsilon^{-3})$ calls and the cited work proves a matching stochastic lower bound. Prove the deterministic lower bound $\Omega(\delta^{-1}\epsilon^{-3})$ with noiseless gradients.

## Reference

- [Cutkosky, Mehta, and Orabona, *Optimal Stochastic Non-smooth Non-convex Optimization through Online-to-Non-convex Conversion* (2023)](https://arxiv.org/abs/2302.03775)

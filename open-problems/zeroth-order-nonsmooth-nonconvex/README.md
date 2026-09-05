# Joint tight lower bound for zero-order nonsmooth nonconvex stochastic optimization

## Status

**Open; not solved by AI.**

## Problem definition

Minimize a Lipschitz, potentially nonsmooth and nonconvex function $f:\mathbb R^d\to\mathbb R$. The output is a $(\delta,\epsilon)$-stationary point: stationarity is measured after allowing perturbations within radius $\delta$, using the Goldstein/nearby-subgradient criterion fixed in the cited work.

## Oracle model

The algorithm observes noisy function values at adaptively selected points and receives no gradients. The estimator is unbiased or satisfies the noise assumptions of Kornowski and Shamir. Complexity counts scalar function-value observations; the lower-bound statement must specify the allowed adaptivity, randomization, and variance normalization.

## Known bounds and open target

Kornowski and Shamir give an $O(d\delta^{-1}\epsilon^{-3})$ algorithm. Dependence on $d$, $\delta$, and $\epsilon$ is known to be optimal separately, but no single construction jointly matches all three. Prove $\Omega(d\delta^{-1}\epsilon^{-3})$ under matching assumptions.

## Reference

- [Kornowski and Shamir, *An Algorithm with Optimal Dimension-Dependence for Zero-Order Nonsmooth Nonconvex Stochastic Optimization*, JMLR 2024](https://arxiv.org/abs/2307.04504)

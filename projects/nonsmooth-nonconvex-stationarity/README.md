# Tight complexity of finding stationary points in nonsmooth nonconvex optimization

## Status

**External public preprint; AI-assisted proof; resolves a recorded open problem.** Kornowski (2026) proves a matching first-order lower bound for Goldstein stationarity with noiseless oracle responses.

## Problem setting

Let $f:\mathbb R^d\to\mathbb R$ be an $L$-Lipschitz, possibly nonsmooth and nonconvex function satisfying

$$
f(0)-\inf_x f(x)\leq\Delta.
$$

The goal is to find a $(\delta,\epsilon)$-Goldstein stationary point $x$, meaning

$$
\operatorname{dist}\!\left(0,\partial_\delta f(x)\right)\leq\epsilon,
$$

where $\partial_\delta f(x)$ is the convex hull of Clarke subgradients at points within distance $\delta$ of $x$.

## Oracle and algorithm model

At each query $x_t$, the first-order oracle returns $f(x_t)$ and the entire Clarke subdifferential $\partial f(x_t)$. Granting the full subdifferential only strengthens the lower bound relative to an oracle returning a single subgradient.

The theorem covers adaptive, possibly randomized **zero-respecting** algorithms: a new iterate can have nonzero coordinates only among coordinates exposed by subdifferentials at earlier queries. The result therefore includes the usual linear-span methods but is not stated for completely unrestricted algorithms.

## Main result

For a universal constant $c>0$ and parameters satisfying

$$
\epsilon\leq c\min\!\left\{L,\frac{\delta L^2}{\Delta},\frac{\Delta}{\delta}\right\},
$$

there is an $L$-Lipschitz objective in dimension

$$
d=\Theta\!\left(\frac{\Delta L^2}{\delta\epsilon^3}\right)
$$

such that no zero-respecting first-order algorithm reaches a $(\delta,\epsilon)$-Goldstein stationary iterate before

$$
T=\Omega\!\left(\frac{\Delta L^2}{\delta\epsilon^3}\right)
$$

queries. Together with known upper bounds, this establishes the tight complexity

$$
\Theta\!\left(\frac{\Delta L^2}{\delta\epsilon^3}\right).
$$

In the normalized regime, this is $\Theta(\delta^{-1}\epsilon^{-3})$. Thus the optimal rate agrees with the stochastic rate: under Goldstein stationarity, noiseless gradients do not improve the worst-case query complexity in this algorithmic framework.

## Proof idea

The hard instance is a double-loop zero chain. It has $\Omega(\Delta L/(\delta\epsilon))$ sequential blocks, each containing $\Omega(L^2/\epsilon^2)$ coordinates. The inner chain forces many queries to activate a block, while the outer chain forces the blocks to be activated in sequence. Until the final block is reached, a common separating direction has positive inner product with every nearby subgradient, preventing any convex combination of those subgradients from having norm at most $\epsilon$.

## Additional result

The paper also proves a tight lower bound of

$$
\Omega\!\left(\frac{\Delta L^2\sqrt\lambda}{\epsilon^{7/2}}\right)
$$

for the relaxed $(\lambda,\epsilon)$-stationarity notion considered there.

## References

- [Kornowski, *The Complexity of Finding Stationary Points in Nonsmooth Nonconvex Optimization* (2026)](https://arxiv.org/abs/2609.17780)
- [Cutkosky, Mehta, and Orabona, *Optimal Stochastic Non-smooth Non-convex Optimization through Online-to-Non-convex Conversion* (2023)](https://arxiv.org/abs/2302.03775)
- [Original open-problem record](../../open-problems/deterministic-nonsmooth-nonconvex/)

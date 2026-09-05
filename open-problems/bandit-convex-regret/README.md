# Tight regret bound for stochastic bandit convex optimization

## Status

**Open; not solved by AI.**

## Problem definition

For rounds $t=1,\ldots,T$, an algorithm chooses $x_t$ in the $d$-dimensional Euclidean unit ball, incurs a convex $1$-Lipschitz loss $f_t(x_t)$, and seeks to minimize expected regret
$$
\mathbb E\left[\sum_{t=1}^T f_t(x_t)-\min_x\sum_{t=1}^T f_t(x)\right].
$$
The stochastic loss distribution and geometric assumptions should match the cited lower- and upper-bound results.

## Oracle model

Bandit feedback reveals only the scalar loss at the played point; gradients and unplayed losses are hidden. The algorithm may be adaptive and randomized. Cost is the horizon $T$, and the target is worst-case expected regret over the admissible stochastic instances.

## Known bounds and open target

For $T\geq d^{10/3}$, the current lower bound is $\Omega(d^{4/3}\sqrt T)$, while the best upper bound in the corresponding favorable geometry is $\widetilde O(d^{3/2}\sqrt T)$. Close the dimension gap by strengthening the lower bound or improving the upper bound.

## References

- [Rajaraman and Han, lower bound (2026)](https://arxiv.org/abs/2607.18652)
- [Fokkema et al., upper bound (2024)](https://arxiv.org/abs/2406.06506)

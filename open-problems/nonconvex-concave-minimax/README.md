# Tight complexity bound for nonconvex--concave minimax optimization

## Status

**Open; not solved by AI.**

## Problem definition

Consider $\min_{x\in\mathbb R^{d_x}}\max_{y\in\mathcal Y} f(x,y)$, where $f$ is jointly smooth, may be nonconvex in $x$, is concave (but not strongly concave) in $y$, and $\mathcal Y$ is convex and bounded. A standard target is an $\epsilon$-stationary point of the primal value function, interpreted through the smooth envelope or the precise stationarity measure used by Lin, Jin, and Jordan.

## Oracle model

A deterministic first-order oracle returns $f(x,y)$ and $(\nabla_x f(x,y),\nabla_y f(x,y))$. Algorithms may adapt their queries and use projections onto $\mathcal Y$; complexity counts gradient-oracle calls. Any lower bound must state whether it covers general randomized methods or a structural subclass such as zero-respecting methods.

## Known bounds and open target

The five classical regimes are C--C, SC--C, SC--SC, NC--SC, and NC--C. Tight lower bounds are known for the first four, while the $O(\epsilon^{-3})$ NC--C rate remains unmatched. Prove $\Omega(\epsilon^{-3})$, or at least $\Omega(\epsilon^{-2-\delta})$ for some $0<\delta\leq1$, under matching assumptions.

## References

- [Lin, Jin, and Jordan, *Near-Optimal Algorithms for Minimax Optimization*, COLT 2020](https://arxiv.org/abs/2002.02417)
- [Zhang, Hong, and Zhang, convex--concave lower bounds](https://arxiv.org/abs/1912.07481)
- [Ouyang and Xu, bilinear saddle-point lower bounds](https://arxiv.org/abs/1808.02901)
- [Li et al., NC--SC lower bounds, NeurIPS 2021](https://arxiv.org/abs/2104.08708)
- [Zhang et al., NC--SC complexity, UAI 2021](https://arxiv.org/abs/2103.15888)

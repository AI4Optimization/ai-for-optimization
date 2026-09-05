# Tight complexity bound for finite-sum nonconvex optimization

## Status

**Open; not solved by AI.**

## Problem definition

Minimize $F(x)=n^{-1}\sum_{i=1}^n f_i(x)$ over $x\in\mathbb R^d$, where $F$ may be nonconvex, every component $f_i$ has an $L$-Lipschitz gradient, and $F(x_0)-\inf F\leq\Delta$. The output criterion is $\mathbb E\|\nabla F(x)\|\leq\epsilon$.

## Oracle model

At each adaptive query $(i,x)$, an incremental first-order oracle returns $(f_i(x),\nabla f_i(x))$ or just $\nabla f_i(x)$. Complexity is the number of component-oracle calls. The lower-bound class should cover randomized algorithms under the standard success-probability or expected-stationarity convention.

## Known bounds and open target

SPIDER achieves $O(\sqrt n\,\epsilon^{-2})$ in the accuracy-dependent regime, while the best applicable lower bound here is only $\Omega(\epsilon^{-2})$ and has no polynomial $n$ dependence. Prove $\Omega(n^\delta\epsilon^{-2})$ for some $0<\delta\leq1/2$, ideally the matching $\Omega(\sqrt n\,\epsilon^{-2})$ bound, with full $L$ and $\Delta$ dependence stated.

## References

- [Fang et al., *SPIDER: Near-Optimal Non-Convex Optimization via Stochastic Path-Integrated Differential Estimator*, NeurIPS 2018](https://arxiv.org/abs/1807.01695)
- [Zhou and Gu, *Lower Bounds for Smooth Nonconvex Finite-Sum Optimization*, ICML 2019](https://proceedings.mlr.press/v97/zhou19b.html)

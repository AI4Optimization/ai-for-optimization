# Tight lower bound for fully first-order stochastic bilevel optimization

## Status

**Resolved for the standard bounded-variance first-order oracle.** [Gu, Wu, and Yang (2026)](https://arxiv.org/abs/2609.21905) prove the $\epsilon^{-6}$ lower-bound exponent for globally unbiased stochastic gradients, even against adaptive randomized algorithms. This was the principal open gap recorded here from Conjecture 1 of Kwon, Kwon, and Lyu (2024). The stronger stochastic-smoothness variant is distinguished below rather than attributed to this theorem.

## Problem definition

Consider
```math
\min_{x\in\mathbb R^{d_x}}\Phi(x):=f(x,y^*(x)),\qquad
y^*(x)\in\arg\min_{y\in\mathbb R^{d_y}}g(x,y),
```
where $g(x,\cdot)$ is strongly convex and the smoothness assumptions are those of the cited conjecture. The goal is an $x$ satisfying $`\mathbb E\|\nabla\Phi(x)\|\leq\epsilon`$ (or the paper's equivalent squared-norm convention).

## Oracle model

Algorithms access globally unbiased stochastic first-order information for the upper and lower objectives, with bounded variance and reliability radius $r=\infty$. The oracle must not reveal $`y^*(x)`$ or become more accurate merely because a query lies near it. Complexity counts stochastic oracle calls; Hessian-vector information is excluded in the fully first-order model.

## Resolved bounded-variance branch

For any fixed initial gap $\Delta>0$ and sufficiently small $\epsilon$, Gu, Wu, and Yang prove an oracle lower bound

```math
\Omega\!\left(\Delta\kappa_y^2\epsilon^{-2}\max\{1,\sigma^2\kappa_y^6\epsilon^{-4}\}\right).
```

In the noise-dominated regime this is $\Omega(\Delta\sigma^2\kappa_y^8\epsilon^{-6})$. Their oracle supplies globally unbiased gradients with variance at most $\sigma^2$; unlike the earlier $`y^*(x)`$-aware construction, it does not reveal a near-optimal lower-level solution. The exponent matches the known bounded-variance first-order upper bound. See the [result project](../../projects/stochastic-bilevel-first-order-lower-bound/).

## Scope of the resolution

The resolved status refers to the standard **bounded-variance** oracle and its tight $\epsilon^{-6}$ accuracy exponent. Conjecture 1 also discusses an $\Omega(\epsilon^{-4})$ lower bound **under additional stochastic smoothness**; the 2026 theorem does not establish that distinct strengthened-oracle statement. Matching the dependence on $\kappa_y$ is another separate question. Earlier $\epsilon^{-6}$ and $\epsilon^{-4}$ bounds for a $`y^*(x)`$-aware oracle have reliability radius $r_\epsilon=\Theta(\epsilon)$ and should not be conflated with the globally unbiased model.

## Finite-order smoothness follow-up

[Pan and Yang (2026)](https://arxiv.org/abs/2610.01843v1) study the same NC--SC bilevel structure under a globally unbiased bounded-variance stochastic first-order oracle and an order-$`p`$ smoothness condition, for any fixed finite integer $`p\geq1`$, on lower-level derivatives with respect to the lower variable.

Their single-loop MRT-FD method tracks the upper variable, lower solution, and implicit-differentiation response simultaneously. Order-$`p`$ finite differences approximate the required second-order derivative actions using only stochastic gradient queries. They prove matching upper and lower bounds

```math
\Theta\!\left(\epsilon^{-4-2/p}\right).
```

Thus $`p=1`$ recovers the $`\epsilon^{-6}`$ accuracy exponent, while every fixed finite smoothness order has an optimal interpolating exponent strictly above four. The result approaches $`\epsilon^{-4}`$ as $`p`$ grows but does not identify a fixed finite $`p`$ with an exact $`\epsilon^{-4}`$ rate. This repository records the paper as a follow-up rather than replacing the original bounded-variance resolution. No AI-use disclosure was located in the reviewed v1 source, and the complete proof has not been independently audited here.

## Reference

- [Kwon, Kwon, and Lyu, *On the Complexity of First-Order Methods in Stochastic Bilevel Optimization*, Conjecture 1 (2024)](https://arxiv.org/abs/2402.07101)
- [Gu, Wu, and Yang, *An $\Omega(\kappa_y^8\epsilon^{-6})$ Lower Bound for Stochastic NC-SC Bilevel Optimization with First-order Oracles* (2026)](https://arxiv.org/abs/2609.21905)
- [Pan and Yang, *Optimal Stochastic Bilevel Optimization with First-Order Oracles* (2026)](https://arxiv.org/abs/2610.01843v1)

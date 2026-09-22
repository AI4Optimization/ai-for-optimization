# Tight lower bound for fully first-order stochastic bilevel optimization

## Status

**Partially resolved.** [Gu, Wu, and Yang (2026)](https://arxiv.org/abs/2609.21905) prove the $\epsilon^{-6}$ lower-bound exponent for the standard globally unbiased bounded-variance first-order oracle, even against adaptive randomized algorithms. The separate $\epsilon^{-4}$ target under additional stochastic smoothness is not established by that theorem. This page originated from Conjecture 1 of Kwon, Kwon, and Lyu (2024).

## Problem definition

Consider
$$
\min_{x\in\mathbb R^{d_x}}\Phi(x):=f(x,y^*(x)),\qquad
y^*(x)\in\arg\min_{y\in\mathbb R^{d_y}}g(x,y),
$$
where $g(x,\cdot)$ is strongly convex and the smoothness assumptions are those of the cited conjecture. The goal is an $x$ satisfying $\mathbb E\|\nabla\Phi(x)\|\leq\epsilon$ (or the paper's equivalent squared-norm convention).

## Oracle model

Algorithms access globally unbiased stochastic first-order information for the upper and lower objectives, with bounded variance and reliability radius $r=\infty$. The oracle must not reveal $y^*(x)$ or become more accurate merely because a query lies near it. Complexity counts stochastic oracle calls; Hessian-vector information is excluded in the fully first-order model.

## Resolved bounded-variance branch

For any fixed initial gap $\Delta>0$ and sufficiently small $\epsilon$, Gu, Wu, and Yang prove an oracle lower bound

$$
\Omega\!\left(\Delta\kappa_y^2\epsilon^{-2}\max\{1,\sigma^2\kappa_y^6\epsilon^{-4}\}\right).
$$

In the noise-dominated regime this is $\Omega(\Delta\sigma^2\kappa_y^8\epsilon^{-6})$. Their oracle supplies globally unbiased gradients with variance at most $\sigma^2$; unlike the earlier $y^*(x)$-aware construction, it does not reveal a near-optimal lower-level solution. The exponent matches the known bounded-variance first-order upper bound. See the [result project](../../projects/stochastic-bilevel-first-order-lower-bound/).

## Remaining open scope

Conjecture 1 also asks for an $\Omega(\epsilon^{-4})$ lower bound **under additional stochastic smoothness** with the globally reliable oracle. The 2026 bounded-variance theorem does not by itself settle that strengthened-oracle branch. Matching the dependence on $\kappa_y$ is also open. Earlier $\epsilon^{-6}$ and $\epsilon^{-4}$ bounds for a $y^*(x)$-aware oracle have reliability radius $r_\epsilon=\Theta(\epsilon)$ and should not be conflated with the globally unbiased model.

## Reference

- [Kwon, Kwon, and Lyu, *On the Complexity of First-Order Methods in Stochastic Bilevel Optimization*, Conjecture 1 (2024)](https://arxiv.org/abs/2402.07101)
- [Gu, Wu, and Yang, *An $\Omega(\kappa_y^8\epsilon^{-6})$ Lower Bound for Stochastic NC-SC Bilevel Optimization with First-order Oracles* (2026)](https://arxiv.org/abs/2609.21905)

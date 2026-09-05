# Tight lower bound for fully first-order stochastic bilevel optimization

## Status

**Open; not solved by AI.** This is Conjecture 1 of Kwon, Kwon, and Lyu (2024).

## Problem definition

Consider
$$
\min_{x\in\mathbb R^{d_x}}\Phi(x):=f(x,y^*(x)),\qquad
y^*(x)\in\arg\min_{y\in\mathbb R^{d_y}}g(x,y),
$$
where $g(x,\cdot)$ is strongly convex and the smoothness assumptions are those of the cited conjecture. The goal is an $x$ satisfying $\mathbb E\|\nabla\Phi(x)\|\leq\epsilon$ (or the paper's equivalent squared-norm convention).

## Oracle model

Algorithms access globally unbiased stochastic first-order information for the upper and lower objectives, with bounded variance and reliability radius $r=\infty$. The oracle must not reveal $y^*(x)$ or become more accurate merely because a query lies near it. Complexity counts stochastic oracle calls; Hessian-vector information is excluded in the fully first-order model.

## Open target

Prove lower bounds of $\Omega(\epsilon^{-6})$ without stochastic smoothness and $\Omega(\epsilon^{-4})$ with stochastic smoothness. These rates are known only for a $y^*(x)$-aware oracle whose reliability radius is $r_\epsilon=\Theta(\epsilon)$; the open step is to obtain them for the standard globally reliable oracle.

## Reference

- [Kwon, Kwon, and Lyu, *On the Complexity of First-Order Methods in Stochastic Bilevel Optimization*, Conjecture 1 (2024)](https://arxiv.org/abs/2402.07101)

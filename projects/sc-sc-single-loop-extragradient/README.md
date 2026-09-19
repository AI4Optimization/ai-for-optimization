# Pure single-loop extragradient for SC--SC minimax optimization

## Status and attribution

**Public preprint.** This project records the result of Minhao Zhang and Zi Xu, [*Near-Optimal Pure Single-Loop Extragradient Method for Strongly Convex--Strongly Concave Minimax Optimization*](https://arxiv.org/abs/2609.20327), 2026. The result and proof are attributed to those authors. This repository does not claim an independent verification or infer AI involvement.

## Problem and oracle model

Consider the unconstrained deterministic saddle-point problem

$$
\min_x\max_y f(x,y),
$$

where $f$ may have nonlinear primal--dual coupling, its full gradient is $L$-Lipschitz, it is $\mu_x$-strongly convex in $x$, and it is $\mu_y$-strongly concave in $y$. Set $\kappa_x=L/\mu_x$ and $\kappa_y=L/\mu_y$. One oracle call returns the full gradient $(\nabla_x f,\nabla_y f)$ at a queried pair. The solution criterion is the squared Euclidean distance $D_T$ of the last iterate to the unique saddle point.

## Result

Theorem 3 of the paper proves a contraction of the form

$$
D_T\leq 64\kappa_x\kappa_y\left(1+\frac{1}{96\sqrt{2}\sqrt{\kappa_x\kappa_y}}\right)^{-T}D_0.
$$

Consequently, achieving $D_T\leq\varepsilon D_0$ takes

$$
O\!\left(\sqrt{\kappa_x\kappa_y}\log\frac{2\kappa_x\kappa_y}{\varepsilon}\right)
$$

full-gradient calls. This has the optimal square-root condition-number dependence up to logarithmic factors.

## Algorithmic feature and scope

The method is a pure single-loop damped extragradient scheme with fixed parameters. It uses one initialization full-gradient call and two new full-gradient evaluations per iteration, without an inner solver, accuracy schedule, or staged restarts. The theorem concerns **SC--SC**, not nonconvex--strongly-concave minimax optimization. A distinct [NC--SC project](../nc-sc-minimax-log-factors/) records an AI-assisted draft and the subsequent NC--SC results in [Zhang and Xu, arXiv:2609.17973](https://arxiv.org/abs/2609.17973); neither paper's guarantee should be substituted for the other without checking the assumptions and output criterion.

## Reference

- Minhao Zhang and Zi Xu, [*Near-Optimal Pure Single-Loop Extragradient Method for Strongly Convex--Strongly Concave Minimax Optimization*](https://arxiv.org/abs/2609.20327), 2026.

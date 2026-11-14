# Stochastic contracting cubic Newton and optimal acceleration

## Status and attribution

**External public preprint; AI involvement not stated.** Artem Agafonov, Aslan Ashabokov, Dmitry Kamzolov, Alexander D'yakonov, Alexander Gasnikov, and Martin Takáč, [*Matching the Lower Bounds: Stochastic Contracting Cubic Newton and Its Optimal Acceleration*](https://arxiv.org/abs/2610.11693), 2026 (v2). The inspected paper does not contain an AI-use disclosure; this records the absence of a statement, not evidence that AI was not used. This repository has not independently audited the proofs.

## Problem and oracle model

Minimize a convex twice continuously differentiable function $`f`$ over a nonempty compact convex set $`\mathcal X\subseteq\mathbb R^d`$ of diameter $`D`$, with an attained minimum. The Hessian is $`L_2`$-Lipschitz. Each iteration obtains stochastic gradient and Hessian estimates with variance bounds $`\sigma_1^2`$ and $`\sigma_2^2`$; stochastic Hessians are symmetric and positive semidefinite almost surely, and need not be unbiased. Complexity is measured in iterations and the convergence bounds are for expected objective gap.

## Results

The Stochastic Contracting Cubic Newton method gives

```math
\mathbb E[f(x_T)-f^*]
=O\!\left(
\frac{\sigma_1D}{\sqrt T}
+\frac{\sigma_2D^2}{T}
+\frac{L_2D^3}{T^2}
\right).
```

Its accelerated variant improves the latter two terms to

```math
\mathbb E[f(x_T)-f^*]
=O\!\left(
\frac{\sigma_1D}{\sqrt T}
+\frac{\sigma_2D^2}{T^2}
+\frac{L_2D^3}{T^{7/2}}
\right),
```

matching the known lower-bound terms of Agafonov et al. (2024) simultaneously: gradient noise, Hessian noise, and deterministic second-order smoothness. The basic method is a globally convergent, non-accelerated stochastic second-order method with optimal $`T^{-1/2}`$ gradient-noise dependence.

## Algorithmic ideas

The basic method adds quadratic regularization centered at the previous auxiliary point to contracting-domain Newton and minimizes a cubic model before contracting the step. Removing the Hessian and cubic terms reduces the method to projected stochastic gradient with averaging, explaining the optimal gradient-noise term. The accelerated method combines contracting-domain Newton, Monteiro--Svaiter acceleration, and accelerated stochastic cubic Newton techniques.

## Scope

- The stated main guarantees concern convex objectives on compact feasible sets with finite diameter.
- The stochastic Hessian assumption includes positive semidefiniteness almost surely; unbiased Hessian estimates are not required.
- The preprint reports AI involvement as not specified in the inspected version; no claim about whether AI was used is inferred.

## Reference

- Artem Agafonov, Aslan Ashabokov, Dmitry Kamzolov, Alexander D'yakonov, Alexander Gasnikov, and Martin Takáč, [*Matching the Lower Bounds: Stochastic Contracting Cubic Newton and Its Optimal Acceleration*](https://arxiv.org/abs/2610.11693), 2026.

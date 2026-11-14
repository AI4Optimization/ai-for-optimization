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

## Related work: parameter-free acceleration with inexact Hessians

Agafonov et al., [*Optimal Parameter-Free Second-order Acceleration with Inexact Hessians under Generalized Smoothness*](https://arxiv.org/abs/2609.32977), study a related deterministic/inexact-oracle setting. Under classical Lipschitz-Hessian smoothness and uniformly $`\delta`$-inexact Hessians, their parameter-free adaptive accelerated method attains

```math
O\!\left(
\left(\frac{LR^3}{\varepsilon}\right)^{2/7}
+\sqrt{\frac{\delta R^2}{\varepsilon}}
\right)
```

Hessian evaluations, up to an additive logarithmic term independent of $`\varepsilon`$, matching the corresponding lower bound. Under generalized Hessian smoothness

```math
\|\nabla^2 f(y)-\nabla^2 f(x)\|
\leq (M_0+M_1\|\nabla f(x)\|)\|y-x\|,
```

the same adaptive framework gives a far/near rate separation: geometric convergence far from the solution, followed by the classical near-solution rate with the gradient-independent smoothness parameter $`M_0`$. The algorithm requires neither smoothness constants nor the Hessian error level as input. For the paper's inexact oracle, $`\|H(x)-\nabla^2 f(x)\|\leq\delta`$.

This is complementary to the stochastic contracting cubic Newton results above: the related work treats deterministic bounded-error Hessian approximations and parameter-free adaptation, while this project's main paper gives stochastic variance-dependent rates on compact domains.

## Scope

- The stated main guarantees concern convex objectives on compact feasible sets with finite diameter.
- The stochastic Hessian assumption includes positive semidefiniteness almost surely; unbiased Hessian estimates are not required.
- The preprint reports AI involvement as not specified in the inspected version; no claim about whether AI was used is inferred.
- The related parameter-free inexact-Hessian work is recorded as a complementary result; its deterministic error model is distinct from the stochastic variance model of the main project.

## Reference

- Artem Agafonov, Aslan Ashabokov, Dmitry Kamzolov, Alexander D'yakonov, Alexander Gasnikov, and Martin Takáč, [*Matching the Lower Bounds: Stochastic Contracting Cubic Newton and Its Optimal Acceleration*](https://arxiv.org/abs/2610.11693), 2026.
- Artem Agafonov, Aslan Ashabokov, Alexander D'yakonov, Martin Takáč, Alexander Gasnikov, and Dmitry Kamzolov, [*Optimal Parameter-Free Second-order Acceleration with Inexact Hessians under Generalized Smoothness*](https://arxiv.org/abs/2609.32977), 2026.

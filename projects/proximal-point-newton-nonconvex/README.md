# Proximal point Newton methods for nonconvex optimization

## Status and attribution

**External public preprint.** This project records Chang He and Shuzhong Zhang, [*Proximal Point Newton Methods for Nonconvex Optimization*](https://arxiv.org/abs/2610.36256), 2026. The results and proofs are attributed to the authors. The public preprint does not state AI involvement, and this repository has not independently audited the proof.

## Problem and oracle model

Consider unconstrained minimization

```math
\min_{x\in\mathbb R^d} f(x),
```

where $f$ may be nonconvex and is bounded below. The goal is an $(\varepsilon_g,\varepsilon_H)$-approximate second-order stationary point satisfying

```math
\|\nabla f(x)\|\leq\varepsilon_g,
\qquad
\lambda_{\min}(\nabla^2 f(x))>-\varepsilon_H.
```

A second-order oracle returns $f(x)$, $\nabla f(x)$, and $\nabla^2f(x)$. The paper also analyzes an implementation using Hessian--vector products.

## Results

Under an $L_H$-Lipschitz Hessian, the single-loop proximal point Newton method alternates between negative-curvature and regularized Newton steps and uses

```math
O\!\left((f(x^0)-f_{\inf})
\max\{L_H^{1/2}\varepsilon_g^{-3/2},
L_H^2\varepsilon_H^{-3}\}\right)
```

second-order evaluations. In exponent-only form this is $`O(\max\{\varepsilon_g^{-3/2},\varepsilon_H^{-3}\})`$.

The main accelerated result additionally assumes an $L_T$-Lipschitz third derivative but still queries only gradients and Hessians. Theorem 4.7 gives the dimension-free bound

```math
\widetilde O\!\left((f(x^0)-f_{\inf})
\max\{L_T^{1/3}\varepsilon_g^{-4/3},
L_T\varepsilon_H^{-2}\}\right).
```

This matches the evaluation exponents of third-order tensor methods up to logarithmic factors without constructing third-order tensors or solving tensor subproblems. The adaptive inexact Newton--CG variant does not require the Lipschitz constants in advance. If queried Hessians have operator norm at most $U_H$, its Hessian--vector product complexity is

```math
\widetilde O\!\left((f(x^0)-f_{\inf})
\min\left\{
d\max\{\varepsilon_g^{-4/3},\varepsilon_H^{-2}\},
\sqrt{1+U_H}\max\{\varepsilon_g^{-5/3},\varepsilon_H^{-5/2}\}
\right\}\right)
```

with high probability, suppressing smoothness-dependent factors as in the paper's displayed comparison.

## Algorithmic idea

The framework approximately solves proximal subproblems

```math
f(x)+\mu\|x-x^k\|^2
```

using negative-curvature detection and Newton steps. Under third-derivative smoothness, tensor-free interpolation inequalities allow a larger fixed-radius step and reproduce the progress rate of a third-order method using only second-order information. The adaptive version replaces exact eigendecompositions and linear solves by Lanczos and capped conjugate-gradient routines.

## Scope and limitations

- The accelerated theorem assumes Lipschitz continuity of the third derivative even though the algorithm never queries it.
- The bound is optimal relative to third-order tensor-method upper bounds in its accuracy exponents; the paper leaves a matching lower bound for second-order oracles under this smoothness class open.
- The Newton--CG guarantee is probabilistic and additionally uses a uniform bound on queried Hessians for the stated Hessian--vector product complexity.

## Reference

- Chang He and Shuzhong Zhang, [*Proximal Point Newton Methods for Nonconvex Optimization*](https://arxiv.org/abs/2610.36256), 2026.

# Envelope cubic regularized Newton for NC--SC minimax optimization

## Status and attribution

**AI-assisted public preprint.** This project records Qihao Zhou, Lesi Chen, Luo Luo, and Chengchang Liu, [*Envelope Cubic Regularized Newton Method for Nonconvex-Strongly-Concave Minimax Optimization*](https://arxiv.org/abs/2610.20345), 2026. The paper reports that the authors found its sharp upper and lower bounds after several rounds of discussion with ChatGPT 6 Astra, then checked, reorganized, and simplified the results. The results and proofs are attributed to the authors; this repository has checked the theorem statements and scope against the preprint but has not independently audited the proof.

## Problem and oracle model

Consider

```math
\min_{x\in\mathbb R^{d_x}}\max_{y\in\mathbb R^{d_y}} f(x,y),
\qquad
\Phi(x)=\max_y f(x,y),
```

where $f$ has Hessian norm at most $L$, has a $\rho$-Lipschitz Hessian, and is $\mu$-strongly concave in $y$. Let $\kappa=L/\mu$ and assume $`\Phi(z_0)-\inf_z\Phi(z)\leq\Delta`$. The upper bound counts gradient and Hessian evaluations of $f$. The lower bound applies to deterministic second-order algorithms.

The target is an $(\varepsilon,\sqrt{\widetilde\rho\varepsilon})$-approximate second-order stationary point of the primal function:

```math
\|\nabla\Phi(x)\|\leq\varepsilon,
\qquad
\nabla^2\Phi(x)\succeq
-\sqrt{\widetilde\rho\varepsilon}\,I,
\qquad
\widetilde\rho=\rho(4+\kappa)^{3/2}.
```

## Matching upper and lower bounds

The Envelope Cubic Regularized Newton method (ECRN) applies inexact cubic regularization to the primal Moreau envelope $\Phi_{2L}$. Theorem 11 proves

```math
N_{\mathrm{grad}}+N_{\mathrm{Hess}}
=\widetilde O\!\left(
\Delta\sqrt\rho\,\kappa^{3/4}\varepsilon^{-3/2}
\right).
```

The key structural improvement is that the envelope has Hessian-Lipschitz parameter $`O(\rho\kappa^{3/2})`$, rather than the previously used $`O(\rho\kappa^3)`$ bound for $\Phi$ itself. NewtonTrack follows the sequence of unbalanced strongly-convex--strongly-concave subproblems and supplies sufficiently accurate envelope gradients and Hessians.

For $`0<\varepsilon\leq cL^2/(\rho\kappa^{3/2})`$, Theorem 18 constructs a resisting-oracle instance on which every deterministic second-order method needs

```math
\Omega\!\left(
\Delta\sqrt\rho\,\kappa^{3/4}\varepsilon^{-3/2}
\right)
```

queries before it can guarantee $`\|\nabla\Phi(x)\|\leq\varepsilon`$. Hence ECRN is optimal up to logarithmic factors in the deterministic second-order oracle model.

## Proof architecture

1. Prove the sharper $`\rho(4+\kappa)^{3/2}`$ Hessian-Lipschitz bound for the primal envelope.
2. Run inexact cubic regularization on that envelope and use NewtonTrack to warm-start the successive SC--SC inner problems.
3. Transfer envelope second-order stationarity back to the primal function.
4. For the lower bound, embed a smooth nonconvex zero-chain through Fenchel conjugation, preserve its second-order zero-chain structure, and hide it using adversarial rotations and a resisting oracle.

## Scope and limitations

- The matching lower bound is stated for deterministic second-order algorithms; randomized second-order algorithms are not covered.
- The result targets second-order stationarity of the primal function and should not be conflated with first-order NC--SC minimax bounds.
- ECRN uses exact Hessian evaluations and a nested tracking procedure; the paper lists more efficient and single-loop variants as open directions.

## Reference

- Qihao Zhou, Lesi Chen, Luo Luo, and Chengchang Liu, [*Envelope Cubic Regularized Newton Method for Nonconvex-Strongly-Concave Minimax Optimization*](https://arxiv.org/abs/2610.20345), 2026.

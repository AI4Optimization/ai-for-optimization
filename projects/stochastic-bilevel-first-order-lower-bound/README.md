# Stochastic NC--SC bilevel lower bound with first-order oracles

## Status and attribution

**Public preprint:** Zhihao Gu, Qilong Wu, and Junchi Yang, [*An $\Omega(\kappa_y^8\epsilon^{-6})$ Lower Bound for Stochastic NC-SC Bilevel Optimization with First-order Oracles*](https://arxiv.org/abs/2609.21905), 2026. The authors disclose assistance from GPT-5.6 Sol in refining their independently developed proof draft, report human checking, and provide an accompanying Lean formalization. This repository records their claim and disclosure; it has not independently audited the complete proof.

## Setting and oracle

The upper objective is nonconvex, while the lower objective is strongly convex in its inner variable. Under the paper's global smoothness and regularity assumptions, the goal is an $\epsilon$-stationary point of the hyper-objective $\Phi(x)=f(x,y^*(x))$. The standard stochastic first-order oracle returns globally unbiased stochastic gradients of both objectives, with variance at most $\sigma^2$ and no access to $y^*(x)$ or Hessian-vector products. The lower bound applies to arbitrary adaptive randomized first-order algorithms, with dimension permitted to grow with accuracy.

## Result

For fixed initial gap $\Delta>0$ and sufficiently small $\epsilon$, the paper proves

$$
\Omega\!\left(\Delta\kappa_y^2\epsilon^{-2}\max\{1,\sigma^2\kappa_y^6\epsilon^{-4}\}\right)
$$

oracle calls, where $\kappa_y$ is the intrinsic lower-level condition number. In the noise-dominated regime this is $\Omega(\Delta\sigma^2\kappa_y^8\epsilon^{-6})$. It settles the $\epsilon^{-6}$ exponent of the [original bounded-variance open question](../../open-problems/stochastic-bilevel/) for a globally unbiased oracle. It does not establish the distinct $\epsilon^{-4}$ target under an additional stochastic-smoothness assumption, nor optimal dependence on $\kappa_y$.

## Proof and provenance

The paper builds a smooth bilevel hard instance from a nonconvex zero-chain and a stochastic progress gate, then uses a random rotation to cover adaptive randomized algorithms. See its Section 4 and AI Disclosure for the exact construction, assumptions, and verification account.

- [Original conjecture: Kwon, Kwon, and Lyu (2024)](https://arxiv.org/abs/2402.07101)
- [Public result: Gu, Wu, and Yang (2026)](https://arxiv.org/abs/2609.21905)

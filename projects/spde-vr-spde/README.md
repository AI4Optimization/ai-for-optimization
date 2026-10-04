# SPDE and VR-SPDE for stochastic nonconvex--(strongly) concave minimax optimization

## Status and attribution

**External public preprint; independent project record.** Huiling Zhang, Minhao Zhang, and Zi Xu, [*Single-Loop Stochastic Projected Damped Extragradient Methods for Stochastic Nonconvex--(Strongly) Concave Minimax Optimization*](https://arxiv.org/abs/2609.21747v1), 2026.

The paper introduces SPDE and its recursive variance-reduced variant VR-SPDE. Both are single-loop methods. This repository has checked the stated settings, oracle assumptions, stationarity criteria, and headline complexities, but has not independently audited the complete proofs. AI involvement is unknown.

## Problem setting

Consider the stochastic minimax problem

```math
\min_{x\in\mathcal X}\max_{y\in\mathcal Y}
f(x,y)=\mathbb E_\xi[F(x,y;\xi)],
```

where $\mathcal X$ is closed and convex, $\mathcal Y$ is compact and convex, and $f$ is smooth but may be nonconvex in $x$. The paper treats:

- **NC--C:** $f(x,\cdot)$ is concave;
- **NC--SC:** $f(x,\cdot)$ is $\mu$-strongly concave, with $\kappa=L/\mu$.

SPDE assumes an unbiased stochastic gradient oracle with uniformly bounded variance. VR-SPDE additionally assumes common-sample paired evaluations and mean-square Lipschitz stochastic gradients.

## Stationarity criteria

The paper gives separate guarantees for two notions:

- **Game stationarity (GS):** the joint projected/normal-cone residual in both primal and dual variables.
- **Optimization stationarity (OS):** the gradient of a Moreau envelope of the constrained value function.

Each theorem controls the expected squared stationarity measure by $\epsilon^2$. A sample-gradient evaluation counts as one stochastic first-order oracle call; a common-sample paired difference costs two calls.

## Complexity results

With the remaining problem data fixed and in the small-$\epsilon$ regime, the reported stochastic first-order oracle complexities are:

| Method | Setting | Game stationarity | Optimization stationarity |
| --- | --- | --- | --- |
| SPDE | Stochastic NC--C | $O(\epsilon^{-5})$ | $O(\epsilon^{-6})$ |
| VR-SPDE | Stochastic NC--C | $O(\epsilon^{-9/2})$ | $O(\epsilon^{-6})$ |
| SPDE | Stochastic NC--SC | $O(\kappa\epsilon^{-4})$ | $O(\kappa\epsilon^{-4})$ |
| VR-SPDE | Stochastic NC--SC | $O(\kappa^{3/2}\epsilon^{-3})$ | $O(\kappa^{3/2}\epsilon^{-3})$ |

The OS guarantees match the best-known bounds of multi-loop methods while retaining a single-loop implementation. The paper reports the best-known SFO bounds among single-loop stochastic first-order methods for the respective settings and stationarity notions.

## Algorithmic structure

SPDE uses projected damped extragradient updates with stochastic gradients. VR-SPDE replaces the direct stochastic estimators by recursively updated estimators using common-sample gradient differences. The damping and projection keep the primal--dual dynamics stable, while the estimator recursion reduces the variance without introducing an outer loop.

## Scope and comparison notes

- The compact-domain, initialization, and noise quantities in the full theorems remain visible in the non-asymptotic bounds; the table records only the leading $\epsilon$ and $\kappa$ dependence.
- The NC--C game-stationarity rates do not improve the $O(\epsilon^{-6})$ optimization-stationarity rate.
- The results are upper bounds and do not establish matching lower bounds for unrestricted randomized stochastic first-order methods.
- Comparisons with deterministic or stochastic lower-bound projects must match the oracle, domain, initialization, and stationarity definitions.

## Verification record

- [x] Authors, version, settings, and single-loop claim checked against arXiv v1.
- [x] Four GS and OS complexity pairs checked against the abstract and the existing source-level record.
- [x] Bounded-variance and mean-square-Lipschitz oracle assumptions distinguished.
- [ ] Complete lemma-by-lemma proof audit.
- [ ] Independent human repository verifier recorded.

## References

- [Zhang, Zhang, and Xu, arXiv:2609.21747v1](https://arxiv.org/abs/2609.21747v1)
- [Original PDF](https://arxiv.org/pdf/2609.21747v1)
- [Related NC--C benchmark and literature record](../../open-problems/nonconvex-concave-minimax/)

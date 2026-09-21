# Tight complexity bound for nonconvex--concave minimax optimization

## Status

**Resolved for deterministic first-order methods by public preprints (September 2026).** Pan, Zheng, and Li establish matching lower and upper bounds, including removal of logarithmic factors. Wu, Gu, and Yang establish the same deterministic lower-bound rate for zero-respecting methods in a constrained-primal setting, together with a stochastic lower bound. Zhang and Xu independently obtain the matching lower bound and a matching single-loop upper bound for optimization stationarity in the projected zero-respecting framework.

See the [joint project record](../../projects/nc-c-minimax-tight-complexity/) for theorem statements, provenance, and verification scope. This status records the results of the v1 preprints; an independent repository proof audit has not been completed.

[Related stochastic methods](#related-stochastic-methods) are recorded below as external literature, separately from this deterministic benchmark resolution.

## Problem definition

Consider $\min_{x\in\mathbb R^{d_x}}\max_{y\in\mathcal Y} f(x,y)$, where $f$ is jointly $L$-smooth, may be nonconvex in $x$, is concave in $y$ with no positive strong-concavity parameter assumed, and $\mathcal Y$ is nonempty, compact, and convex. Write

$$
\Phi(x):=\max_{y\in\mathcal Y}f(x,y),\qquad
\operatorname{diam}(\mathcal Y)\leq D_{\mathcal Y},\qquad
\Phi(0)-\inf_x\Phi(x)\leq\Delta.
$$

The target is $\|\nabla\Phi_{1/(2L)}(x)\|\leq\epsilon$, where

$$
\Phi_{1/(2L)}(x):=\min_z\{\Phi(z)+L\|z-x\|^2\}.
$$

This is the Moreau-envelope stationarity criterion in Lin, Jin, and Jordan, Appendix A. It is also called optimization stationarity in the new preprints. For a constrained primal domain $\mathcal X$, the corresponding envelope is that of $\Phi+\iota_{\mathcal X}$, where the indicator is zero on $\mathcal X$ and $+\infty$ elsewhere.

## Oracle model

A first-order saddle oracle returns $(f(x,y),\nabla_x f(x,y),\nabla_y f(x,y))$ at each feasible query. Complexity counts joint oracle calls; projections onto the known domain and arithmetic are not charged as oracle calls. The resolved result concerns arbitrary deterministic adaptive algorithms, including outputs computed from the final transcript. It does not establish a lower bound for unrestricted randomized algorithms.

## Original target and resolution

The original target was $\Omega(\epsilon^{-3})$, or at least $\Omega(\epsilon^{-2-\delta})$ for some $0<\delta\leq1$, under matching assumptions. The previous NC--C upper bound was $\widetilde O(\epsilon^{-3})$ with the other parameters fixed; the original page suppressed its logarithmic factors.

**Pan, Zheng, and Li, Theorems 3.2 and 3.3.** For $L,D_{\mathcal Y},\Delta>0$ and

$$
0<\epsilon\leq c\min\{LD_{\mathcal Y},\sqrt{L\Delta}\},
$$

where $c>0$ is universal, the worst-case deterministic first-order oracle complexity is

$$
\Theta\!\left(\frac{L^2D_{\mathcal Y}\Delta}{\epsilon^3}\right).
$$

The lower-bound instances have $\mathcal X=\mathbb R^{d_x}$ and a bounded dual ball, so they directly address the original domain. Tracked-FOAM attains the upper bound without logarithmic factors. For every $\epsilon>0$, its full bound is

$$
O\!\left(\left(\frac{L\Delta}{\epsilon^2}+1\right)
\max\left\{1,\frac{LD_{\mathcal Y}}{\epsilon}\right\}\right).
$$

**Wu, Gu, and Yang, Theorem 4.1.** They obtain $\Omega(L^2D_{\mathcal Y}\Delta/\epsilon^3)$ in the same small-accuracy regime for deterministic zero-respecting methods. Their hard instance constrains auxiliary primal variables; this result alone is not a lower bound for the original unconstrained-primal, arbitrary-deterministic model. Their Theorem 5.5 additionally proves an additive deterministic-plus-stochastic lower bound with an $\epsilon^{-6}$ noise term; see the [project](../../projects/nc-c-minimax-tight-complexity/).

**Zhang and Xu, Theorem 5.1.** They prove

$$
\Omega\!\left(\frac{L^2D_{\mathcal Y}\Delta_\phi}{\epsilon^3}\right)
$$

for optimization stationarity over projected zero-respecting first-order methods, allowing randomized output rules at a fixed query budget. Their warm-started projected damped extragradient method achieves a matching leading upper bound, up to an additive lower-order warm-up cost. Thus this work independently certifies the $\epsilon^{-3}$ exponent in its stated oracle class; unlike Pan, Zheng, and Li, it does not extend the lower bound to arbitrary deterministic methods.

## Related stochastic methods

**External public preprint; AI involvement unknown.** Huiling Zhang, Minhao Zhang, and Zi Xu's [SPDE and VR-SPDE paper (arXiv:2609.21747v1; PDF)](https://arxiv.org/pdf/2609.21747v1) records single-loop stochastic methods for NC--C and NC--SC minimax optimization. The PDF is the method record; no separate project or AI benchmark success is assigned. This repository has not independently audited the proofs.

The population objective is smooth, with a closed convex primal domain and a compact convex dual domain. SPDE assumes unbiased gradients with uniformly bounded variance. VR-SPDE additionally requires common-sample paired evaluations and mean-square Lipschitz gradients (Assumption 4).

| Method | Setting | Game stationarity (GS) | Optimization stationarity (OS) |
| --- | --- | --- | --- |
| SPDE | Stochastic NC--C | $O(\epsilon^{-5})$ | $O(\epsilon^{-6})$ |
| VR-SPDE | Stochastic NC--C | $O(\epsilon^{-9/2})$ | $O(\epsilon^{-6})$ |
| SPDE | Stochastic NC--SC | $O(\kappa\epsilon^{-4})$ | $O(\kappa\epsilon^{-4})$ |
| VR-SPDE | Stochastic NC--SC | $O(\kappa^{3/2}\epsilon^{-3})$ | $O(\kappa^{3/2}\epsilon^{-3})$ |

These are small-$\epsilon$ stochastic first-order oracle bounds, with $\kappa=L/\mu$ and other data fixed, including positive noise, initialization budget $B$, and the VR smoothness ratio. One sample-gradient evaluation costs one call; a paired difference costs two. See Table 1 and Theorems 2--7 for full bounds; $B$ also depends on initial gradients, beyond the benchmark's value gap (equation (29)).

GS uses the joint normal-cone residual; OS uses the Moreau-envelope gradient of the constrained value function. Each guarantee bounds the expected squared measure by $\epsilon^2$ (Section 2). The faster NC--C GS rates therefore do not improve the OS rate. Comparisons with the [recorded stochastic lower bound](../../projects/nc-c-minimax-tight-complexity/#deterministic-and-stochastic-zero-respecting-lower-bounds) must also match oracle and initialization assumptions; this entry does not declare the stochastic setting fully resolved.

## Remaining scope

- Lower bounds for unrestricted randomized first-order methods remain open in these preprints.
- The tight deterministic rate above is established in the stated accuracy regime, with worst-case dimension allowed to grow.
- Separate primal/dual oracle costs and game stationarity require distinct results; they are not settled by this optimization-stationarity bound.

## References

- [Pan, Zheng, and Li, *Optimal Deterministic First-Order Oracle Complexity for Nonconvex-Concave Minimax Optimization*, arXiv:2609.14235v1](https://arxiv.org/abs/2609.14235v1)
- [Wu, Gu, and Yang, *Lower Bounds for Nonconvex-Concave Minimax Optimization*, arXiv:2609.14233v1](https://arxiv.org/abs/2609.14233v1)
- [Zhang and Xu, *Matching Multi-Loop Complexities with a Single Loop: Optimal Optimization Stationarity and Best-Known Game Stationarity in Nonconvex--Concave Minimax Optimization*, arXiv:2609.17973v1](https://arxiv.org/abs/2609.17973v1)
- [Lin, Jin, and Jordan, *Near-Optimal Algorithms for Minimax Optimization*, COLT 2020](https://arxiv.org/abs/2002.02417)
- [Zhang, Hong, and Zhang, convex--concave lower bounds](https://arxiv.org/abs/1912.07481)
- [Ouyang and Xu, bilinear saddle-point lower bounds](https://arxiv.org/abs/1808.02901)
- [Li et al., NC--SC lower bounds, NeurIPS 2021](https://arxiv.org/abs/2104.08708)
- [Zhang et al., NC--SC complexity, UAI 2021](https://arxiv.org/abs/2103.15888)

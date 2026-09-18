# Tight complexity bound for nonconvex--concave minimax optimization

## Status

**Resolved for deterministic first-order methods by public preprints (September 2026).** Pan, Zheng, and Li establish matching lower and upper bounds, including removal of logarithmic factors. Wu, Gu, and Yang establish the same deterministic lower-bound rate for zero-respecting methods in a constrained-primal setting, together with a stochastic lower bound. Zhang and Xu independently obtain the matching lower bound and a matching single-loop upper bound for optimization stationarity in the projected zero-respecting framework.

See the [joint project record](../../projects/nc-c-minimax-tight-complexity/) for theorem statements, provenance, and verification scope. This status records the results of the v1 preprints; an independent repository proof audit has not been completed.

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

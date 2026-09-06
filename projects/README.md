# Project catalog

This catalog contains both AI-assisted optimization-theory results and the open problems used as a research benchmark. Each completed-project entry links to a self-contained directory with its assumptions, bound, proof status, provenance, and references.

## Projects

| Project | Setting | Bound | Status |
| --- | --- | --- | --- |
| [Optimal upper bound for nonconvex-strongly-concave minimax optimization](nc-sc-minimax-log-factors/) | Deterministic first-order nonconvex-strongly-concave minimax optimization | Main term $O(\sqrt{\kappa}L\Delta/\epsilon^2)$, plus one-time logarithmic costs | Verified draft; cleanup needed |
| [Tight lower bound for stochastic nonconvex-strongly-concave minimax optimization](stochastic-nc-sc-tight-lower-bound/) | Bounded-variance stochastic first-order NC-SC minimax optimization for zero-respecting algorithms | $\Omega\!\left(L\Delta[\sqrt{\kappa}/\epsilon^2+\kappa\sigma^2/\epsilon^4]\right)$ oracle calls | Verified draft; cleanup needed |
| [Halpern acceleration for high-order monotone VIs](halpern-high-order-mvi/) | $p$th-order methods for smooth monotone variational inequalities | $\widetilde O_p\!\left(1+(L_pR^p/\epsilon)^{1/p}\right)$ oracle calls | Public preprint [(Chen et al., 2026)](https://arxiv.org/abs/2608.08463) |
| [Tight lower bounds for nonconvex-quadratic bilevel optimization](bilevel-condition-number-lower-bound/) | Deterministic nonconvex--quadratic bilevel optimization | $\Omega(\kappa_y^{5/2}L_1\Delta/\epsilon^2)$ first-order/HVP oracle calls | Public preprint [(Chen et al., 2026)](https://arxiv.org/abs/2511.22331), independently discovered by Kaiyi Ji |
| [Tight lower bounds for highly-smooth non-convex optimization](highly-smooth-nc-lower-bound/) | Deterministic first-order nonconvex optimization under higher-order smoothness | $\Omega(\epsilon^{-7/4})$ for $p=2$ and $\Omega(\epsilon^{-5/3})$ for $p\geq3$, with full parameter dependence | Public preprint [(Zhou 2026)](https://arxiv.org/abs/2606.05438), a simplified proof [(Chen et al., 2026, Sec 3.3)](https://arxiv.org/abs/2511.22331) |
| [Tight lower bound for the nonconvex Universal Heavy Ball method](universal-heavy-ball-lower-bound/) | Deterministic first-order nonconvex optimization with $L$-Lipschitz gradients and $\gamma$-Hölder Hessians | $\Omega\!\left(\epsilon^{-(4+3\gamma)/(2+2\gamma)}\right)$ in the normalized regime, simultaneously for every $\gamma\in[0,1]$ | Verified draft; cleanup needed; based on [(Chen et al., 2026, Sec. 3.3)](https://arxiv.org/abs/2511.22331) |
| [Tight lower bound for discrete minimax optimization](dmo-tight-lower-bound/) | Deterministic first-order discrete minimax optimization | $\Omega(N\Delta L/\epsilon^2)$ component-oracle calls | Verified draft; not yet written up |
| [Near-quadratic lower bound for derivative-free convex optimization](derivative-free-convex-near-quadratic-lower-bound/) | Deterministic convex Lipschitz optimization with an exact function-value oracle | $\Omega(d^2/\log(d+1))$ queries at accuracy $\Theta(LR/\sqrt d)$; $\widetilde\Theta(d^2)$ complexity | Public preprint [(Kerger, 2026)](https://arxiv.org/abs/2607.13335); human-verified; initial proof formally verified in Lean |
| [Optimal deterministic oracle complexity for weakly convex optimization](weakly-convex-deterministic-lower-bound/) | Deterministic first-order optimization of Lipschitz weakly convex functions with a full-subdifferential oracle | $\Omega\!\left(G^2\min\{\rho\Delta,G^2\}/\epsilon^4\right)$; tight in the small-gap regime | Public preprint [(Li and Pan, 2026)](https://arxiv.org/abs/2608.03246v1); human-verified and formally verified in Lean |
| [Lower bounds for stepsize-based acceleration of gradient descent](stepsize-accelerated-gd-lower-bound/) | Smooth convex GD with predetermined stepsize schedules; last iterate | Initial $\Omega(T^{-p})$ for every $p>1.9319$; subsequently strengthened to exponents $1.6342$ and $1.450$ | Public preprint [(Ma and Chen, 2026)](https://arxiv.org/abs/2608.10418); subsequent improvements recorded |
| [Tight lower bound for nonconvex--PL minimax optimization](nonconvex-pl-minimax-lower-bound/) | Deterministic first-order NC--PL minimax optimization | $\Omega(\ell\Delta\kappa/\epsilon^2)$ oracle calls | Public preprint [(Pan and Li, 2026)](https://arxiv.org/abs/2608.26799) |
| [Point convergence of Nesterov's accelerated gradient method](nag-point-convergence/) | Smooth convex minimization with classical NAG at the critical acceleration schedule | $x_k\to x_\infty$, $y_k\to x_\infty$, with $x_\infty\in\arg\min f$ | Public preprint [(Jang and Ryu, 2026)](https://arxiv.org/abs/2510.23513); AI-assisted proof |

## Open problems not yet solved by AI

The following problems are recorded as open research questions. They have not been solved by the AI-assisted proof searches documented in this repository.

| Open problem | Setting | Target | Status |
| --- | --- | --- | --- |
| [Fully first-order stochastic bilevel optimization](../open-problems/stochastic-bilevel/) | Stochastic bilevel; globally unbiased first-order oracle | $\Omega(\epsilon^{-6})$ or $\Omega(\epsilon^{-4})$, depending on stochastic smoothness | **Open; not solved by AI** |
| [Finite-sum nonconvex optimization](../open-problems/finite-sum-nonconvex/) | Individually smooth finite sum | $\Omega(n^\delta\epsilon^{-2})$, ideally $\delta=1/2$ | **Open; not solved by AI** |
| [Nonconvex--concave minimax optimization](../open-problems/nonconvex-concave-minimax/) | Smooth NC--C minimax | $\Omega(\epsilon^{-2-\delta})$, ideally $\Omega(\epsilon^{-3})$ | **Open; not solved by AI** |
| [Minimax optimization under two-sided PL conditions](../open-problems/pl-minimax/) | Deterministic two-sided PL--PL minimax | Match the $\widetilde O(\kappa_x\kappa_y)$ upper bound | **Open; not solved by AI** |
| [Zero-order nonsmooth nonconvex stochastic optimization](../open-problems/zeroth-order-nonsmooth-nonconvex/) | Noisy function-value oracle; $(\delta,\epsilon)$ stationarity | $\Omega(d\delta^{-1}\epsilon^{-3})$ | **Open; not solved by AI** |
| [Deterministic first-order nonsmooth nonconvex optimization](../open-problems/deterministic-nonsmooth-nonconvex/) | Noiseless first-order oracle; $(\delta,\epsilon)$ stationarity | $\Omega(\delta^{-1}\epsilon^{-3})$ | **Open; not solved by AI** |
| [Stochastic bandit convex optimization](../open-problems/bandit-convex-regret/) | Lipschitz losses; bandit feedback | Close $d^{4/3}$ versus $d^{3/2}$ regret gap | **Open; not solved by AI** |
| [Exact-value zeroth-order smooth convex optimization](../open-problems/zeroth-order-smooth-convex/) | Smooth convex; exact function values | $\Omega(d\epsilon^{-1/2})$ in the normalized setting | **Open; not solved by AI** |

See [`open-problems/`](../open-problems/) for precise definitions, oracle models, solution criteria, known bounds, and references.

## Starting a new project

New work should begin from [the project template](_template/). See the repository-level [contribution guide](../CONTRIBUTING.md) for the verification and attribution checklist.

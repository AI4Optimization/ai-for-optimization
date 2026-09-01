# AI Optimization Theory

An organized record of new optimization-theory bounds discovered with AI assistance and checked by human researchers.

The repository is organized by project rather than by model or chat. Each project records the mathematical claim, assumptions, oracle model, proof status, provenance, and the best available write-up. AI output is treated as proof-search material: a result is listed as proved only after verification.

## Projects

| Project | Setting | Bound | Status |
| --- | --- | --- | --- |
| [Optimal upper bound for nonconvex-strongly-concave minimax optimization](projects/nc-sc-minimax-log-factors/) | Deterministic first-order nonconvex-strongly-concave minimax optimization | Main term $O(\sqrt{\kappa}L\Delta/\epsilon^2)$, plus one-time logarithmic costs | Verified draft; cleanup needed |
| [Halpern acceleration for high-order monotone VIs](projects/halpern-high-order-mvi/) | $p$th-order methods for smooth monotone variational inequalities | $\widetilde O_p\!\left(1+(L_pR^p/\epsilon)^{1/p}\right)$ oracle calls | Public preprint |
| [Tight lower bounds for nonconvex-quadratic bilevel optimization](projects/bilevel-condition-number-lower-bound/) | Deterministic nonconvex--quadratic bilevel optimization | $\Omega(\kappa_y^{5/2}L_1\Delta/\epsilon^2)$ first-order/HVP oracle calls | Public preprint |
| [Tight lower bounds for highly-smooth non-convex optimization](projects/highly-smooth-nc-lower-bound/) | Deterministic first-order nonconvex optimization under higher-order smoothness | $\Omega(\epsilon^{-7/4})$ for $p=2$ and $\Omega(\epsilon^{-5/3})$ for $p\geq3$, with full parameter dependence | Public preprint, first discovered in [arXiv:2606.05438](https://arxiv.org/abs/2606.05438). |
| [Tight lower bound for discrete minimax optimization](projects/dmo-tight-lower-bound/) | Deterministic first-order discrete minimax optimization | $\Omega(N\Delta L/\epsilon^2)$ component-oracle calls | Verified draft; not yet written up |

## Open problems not yet solved by AI

The following problems are recorded as open research questions. They have not been solved by the AI-assisted proof searches documented in this repository.

| Open problem | Setting and conjectured bound | Main unresolved step | Source | Status |
| --- | --- | --- | --- | --- |
| Tight lower bound for fully first-order stochastic bilevel optimization | For standard globally unbiased stochastic first-order oracles ($r=\infty$), prove that finding an $\epsilon$-stationary point still requires $\Omega(\epsilon^{-6})$ oracle calls without stochastic smoothness and $\Omega(\epsilon^{-4})$ with stochastic smoothness. | Construct a globally valid hard instance in which $g(x,\cdot)$ is strongly convex for every $(x,y)$ and $\|\nabla_x g(x,y)\|_\infty$ remains globally of the same order as $\|\nabla_x g(x,y^*(x))\|_\infty$. Existing lower bounds establish these rates only for a $y^*(x)$-aware oracle with reliability radius $r_\epsilon=\Theta(\epsilon)$. | [Kwon, Kwon, and Lyu, Conjecture 1](https://arxiv.org/abs/2402.07101) | **Open; not solved by AI** |

## Repository conventions

Every project should contain a `README.md` with:

- a precise statement of the bound and its assumptions;
- the solution criterion and oracle-cost convention;
- a status label and verification record;
- links to the original AI trace and any cleaned manuscript;
- known limitations, open steps, and dependencies on prior results.

Status labels used here are:

- **exploration** - an unverified idea or partial proof;
- **candidate proof** - a complete-looking argument awaiting verification;
- **verified draft** - checked for correctness but not yet publication-ready;
- **clean write-up** - organized as a readable manuscript;
- **public preprint / published** - externally available scholarly version.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the project checklist and [projects/_template](projects/_template/) for a reusable skeleton.

## Scope and caution

The repository documents research results and their provenance; it is not itself a peer-review venue. Complexity claims are meaningful only together with their assumptions, solution criterion, allowed primitive operations, and hidden logarithmic or parameter-dependent factors.


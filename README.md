# AI Optimization Theory

An organized record of open problems and new bounds in optimization theory that may be solved with AI assistance and checked by human researchers.

The repository is organized by project rather than by model or chat. Each project records the mathematical claim, assumptions, oracle model, proof status, provenance, and the best available write-up. AI output is treated as proof-search material: a result is listed as proved only after verification.

## Cite this repository

A repository-level BibTeX entry is provided early so that problem curators, AI contributors, verifiers, and maintainers can receive timely credit. Update the access date to the version you used:

```bibtex
@misc{zhang2026aioptimizationtheory,
  author       = {Zhang, Jingzhao and {AI Optimization Theory Contributors}},
  title        = {AI Optimization Theory: Open Problems and AI-Assisted Bounds},
  year         = {2026},
  howpublished = {GitHub repository},
  url          = {https://github.com/ZhangJingzhao/ai-optimization-theory},
  note         = {Accessed: YYYY-MM-DD}
}
```

The same entry is available as [`CITATION.bib`](CITATION.bib). When citing a particular result, please also cite its project README, original contributor, and associated paper or AI-response record.

## Background and curation criteria

This repository lists research-level open problems in optimization that may be solvable by AI. The organizers filter both proposed problems and claimed AI solutions according to three principles:

1. **Established setup.** A problem must concern an existing, interesting, and well-studied optimization setting with an open gap between upper and lower bounds. The benchmark is not intended for manufacturing new setups solely to create solvable questions.
2. **Standalone significance.** Closing or materially improving the stated gap should, through the improved bound alone, be capable of supporting a top-conference- or journal-level research contribution.
3. **Sanity-checked solutions.** Before a claimed AI response or clean write-up is listed as likely correct, the organizers check that the rate is significant, addresses the original problem, and does not obtain the improvement by adding new assumptions or changing the oracle or solution model. This check is a research sanity check, not a substitute for a full proof audit or peer review.

## Purpose

The repository is intended to serve several complementary roles:

1. **A home for standalone theory results.** A clean write-up should be assessable and citable for its mathematical result, independently of how the proof was discovered.
2. **A research benchmark for AI.** The open-problem list provides a changing but documented benchmark for tracking progress in AI systems' ability to solve research-level optimization problems.
3. **A path from promising AI output to papers.** An AI response that is likely correct but not yet cleaned up is open for the community to claim, verify fully, and develop into a paper. Any resulting work must properly attribute the original contributor who released the initial AI response, as well as subsequent contributors.
4. **Timely contribution records.** Commit history and maintenance records provide a flexible, timely way to document contributions to mathematical theory in an AI-assisted research era.

## Projects

| Project | Setting | Bound | Status |
| --- | --- | --- | --- |
| [Optimal upper bound for nonconvex-strongly-concave minimax optimization](projects/nc-sc-minimax-log-factors/) | Deterministic first-order nonconvex-strongly-concave minimax optimization | Main term $O(\sqrt{\kappa}L\Delta/\epsilon^2)$, plus one-time logarithmic costs | Verified draft; cleanup needed |
| [Tight lower bound for stochastic nonconvex-strongly-concave minimax optimization](projects/stochastic-nc-sc-tight-lower-bound/) | Bounded-variance stochastic first-order NC-SC minimax optimization for zero-respecting algorithms | $\Omega\!\left(L\Delta[\sqrt{\kappa}/\epsilon^2+\kappa\sigma^2/\epsilon^4]\right)$ oracle calls | Verified draft; cleanup needed |
| [Tight lower bound for the nonconvex Universal Heavy Ball method](projects/universal-heavy-ball-lower-bound/) | Deterministic first-order nonconvex optimization with $L$-Lipschitz gradients and $\gamma$-Hölder Hessians | $\Omega\!\left(\epsilon^{-(4+3\gamma)/(2+2\gamma)}\right)$ in the normalized regime, simultaneously for every $\gamma\in[0,1]$ | Verified draft; cleanup needed; based on [(Chen et al., 2026, Sec. 3.3)](https://arxiv.org/abs/2511.22331) |
| [Halpern acceleration for high-order monotone VIs](projects/halpern-high-order-mvi/) | $p$th-order methods for smooth monotone variational inequalities | $\widetilde O_p\!\left(1+(L_pR^p/\epsilon)^{1/p}\right)$ oracle calls | Public preprint [(Chen et al., 2026)](https://arxiv.org/abs/2608.08463) |
| [Tight lower bounds for nonconvex-quadratic bilevel optimization](projects/bilevel-condition-number-lower-bound/) | Deterministic nonconvex--quadratic bilevel optimization | $\Omega(\kappa_y^{5/2}L_1\Delta/\epsilon^2)$ first-order/HVP oracle calls | Public preprint [(Chen et al., 2026)](https://arxiv.org/abs/2511.22331), independently discovered by Kaiyi Ji |
| [Tight lower bounds for highly-smooth non-convex optimization](projects/highly-smooth-nc-lower-bound/) | Deterministic first-order nonconvex optimization under higher-order smoothness | $\Omega(\epsilon^{-7/4})$ for $p=2$ and $\Omega(\epsilon^{-5/3})$ for $p\geq3$, with full parameter dependence | Public preprint [(Chen et al., 2026, Sec 3.3)](https://arxiv.org/abs/2511.22331), first discovered in [Zhou 2026](https://arxiv.org/abs/2606.05438). |
| [Tight lower bound for discrete minimax optimization](projects/dmo-tight-lower-bound/) | Deterministic first-order discrete minimax optimization | $\Omega(N\Delta L/\epsilon^2)$ component-oracle calls | Verified draft; not yet written up |

## Open problems not yet solved by AI

The following problems are recorded as open research questions. They have not been solved by the AI-assisted proof searches documented in this repository.

| Open problem | Setting and target | Sources | Status |
| --- | --- | --- | --- |
| Tight lower bound for fully first-order stochastic bilevel optimization | For standard globally unbiased stochastic first-order oracles ($r=\infty$), prove that finding an $\epsilon$-stationary point still requires $\Omega(\epsilon^{-6})$ oracle calls without stochastic smoothness and $\Omega(\epsilon^{-4})$ with stochastic smoothness. Existing lower bounds establish these rates only for a $y^*(x)$-aware oracle with reliability radius $r_\epsilon=\Theta(\epsilon)$. | [Kwon, Kwon, and Lyu, Conjecture 1](https://arxiv.org/abs/2402.07101) | **Open; not solved by AI** |
| Tight complexity bound for finite-sum nonconvex optimization | Under individual component smoothness, SPIDER (Fang et. al.) gives $O(\sqrt n \epsilon^{-2})$ incremental gradient complexity, whereas the best applicable lower bound has no polynomial dependence on $n$: $\Omega(\epsilon^{-2})$. Prove a matching lower bound, or any nontrivial $\Omega(n^\delta\epsilon^{-2})$ bound for some $0<\delta\leq1/2$. | [Fang et al., NeurIPS 2018](https://arxiv.org/abs/1807.01695); [Zhou and Gu, ICML 2019](https://proceedings.mlr.press/v97/zhou19b.html) | **Open; not solved by AI** |
| Tight complexity bound for nonconvex--concave minimax optimization | Lin, Jin, and Jordan studied five regimes: C--C, SC--C, SC--SC, NC--SC, and NC--C. Tight lower bounds are known for the first four regimes, while NC--C remains open. Prove the matching $\Omega(\epsilon^{-3})$ lower bound, or any nontrivial $\Omega(\epsilon^{-2-\delta})$ bound for some $0<\delta\leq1$. | [Lin, Jin, and Jordan, COLT 2020](https://arxiv.org/abs/2002.02417); [Zhang, Hong, and Zhang, Mathematical Programming](https://arxiv.org/abs/1912.07481); [Ouyang and Xu, Mathematical Programming](https://arxiv.org/abs/1808.02901); [Li et al., NeurIPS 2021](https://arxiv.org/abs/2104.08708); [Zhang et al., UAI 2021](https://arxiv.org/abs/2103.15888) | **Open; not solved by AI** |
| Tight complexity bounds for minimax optimization under PL conditions | In the deterministic (noiseless) setting, the upper bound for nonconvex--PL problems is $O(\kappa_y\epsilon^{-2})$, while the corresponding PL--PL upper bound is $\widetilde O(\kappa_x\kappa_y)$. Matching lower bounds were sought for both settings. Pan and Li (2026) proved the matching lower bound for the one-sided nonconvex--PL case; determine the tight lower bound for the two-sided PL--PL setting. | [Yang et al. (2022)](https://arxiv.org/abs/2112.05604); [Chen, Yao, and Luo (2023)](https://arxiv.org/abs/2307.15868)| **Partially solved: one-sided PL is resolved by [Pan and Li (2026)](https://arxiv.org/abs/2608.26799) ; two-sided PL--PL remains open** |
| Joint tight lower bound for zero-order nonsmooth nonconvex stochastic optimization | Kornowski and Shamir give an algorithm using $O(d\delta^{-1}\epsilon^{-3})$ noisy function evaluations to find a $(\delta,\epsilon)$-stationary point. The dependence on each of $d$, $\delta$, and $\epsilon$ is known to be optimal separately, but no lower bound jointly matching all three parameters is known. Prove an $\Omega(d\delta^{-1}\epsilon^{-3})$ lower bound. | [Kornowski and Shamir, JMLR 2024](https://arxiv.org/abs/2307.04504) | **Open; not solved by AI** |
| Tight complexity bound for deterministic first-order nonsmooth nonconvex optimization | The O2NC framework finds a $(\delta,\epsilon)$-stationary point using $O(\delta^{-1}\epsilon^{-3})$ first-order oracle calls. This rate has a matching lower bound in the stochastic setting. Prove the same $\Omega(\delta^{-1}\epsilon^{-3})$ lower bound for deterministic problems with noiseless gradients. | [Cutkosky, Mehta, and Orabona (2023)](https://arxiv.org/abs/2302.03775) | **Open; not solved by AI** |
| Tight regret bound for stochastic bandit convex optimization | For $1$-Lipschitz convex losses on the $d$-dimensional Euclidean ball and horizons $T\geq d^{10/3}$, the current lower bound is $\Omega(d^{4/3}\sqrt T)$, while the best upper bound is $\widetilde O(d^{3/2}\sqrt T)$ under the corresponding favorable geometry. Close the remaining dimension-dependence gap by proving a stronger lower bound or a better upper bound. | [Rajaraman and Han (2026)](https://arxiv.org/abs/2607.18652); [Fokkema et al. (2024)](https://arxiv.org/abs/2406.06506) | **Open; not solved by AI** |
| Tight lower bound for exact-value zeroth-order smooth convex optimization | Recent near-optimal lower bounds for arbitrary adaptive randomized exact-value algorithms apply to Lipschitz convex functions that may be nonsmooth. For convex objectives with $L$-Lipschitz gradients on the $d$-dimensional Euclidean unit ball, prove an $\Omega(d\epsilon^{-1/2})$ function-value-query lower bound in the normalized smooth setting (equivalently, state and prove the corresponding bound with full $L$, radius, and accuracy dependence). | [Zhang, Zhang, Qi, and Lin (2026)](https://arxiv.org/abs/2607.16558) | **Open; not solved by AI** |

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

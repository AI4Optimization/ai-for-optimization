# AI Optimization Theory

An organized record of new optimization-theory bounds discovered with AI assistance and checked by human researchers.

The repository is organized by project rather than by model or chat. Each project records the mathematical claim, assumptions, oracle model, proof status, provenance, and the best available write-up. AI output is treated as proof-search material: a result is listed as proved only after verification.

## Projects

| Project | Setting | Bound | Status |
| --- | --- | --- | --- |
| [NC-SC minimax without multiplicative logarithms](projects/nc-sc-minimax-log-factors/) | Deterministic first-order nonconvex-strongly-concave minimax optimization | Main term $O(\sqrt{\kappa}L\Delta/\epsilon^2)$, plus one-time logarithmic costs | Verified draft; cleanup needed |
| [Halpern acceleration for high-order monotone VIs](projects/halpern-high-order-mvi/) | $p$th-order methods for smooth monotone variational inequalities | $\widetilde O_p\!\left(1+(L_pR^p/\epsilon)^{1/p}\right)$ oracle calls | Clean write-up; arXiv preprint |
| [Condition-number lower bounds for bilevel optimization](projects/bilevel-condition-number-lower-bound/) | Deterministic nonconvex--quadratic bilevel optimization | $\Omega(\kappa_y^{5/2}L_1\Delta/\epsilon^2)$ first-order/HVP oracle calls | Public preprint |

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


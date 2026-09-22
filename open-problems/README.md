# Open problems

This directory records the open-problem benchmark and preserves resolved questions with links to the resulting projects. Each page fixes the mathematical setting and oracle model before stating the desired bound or its resolution.

Mathematical status, AI provenance, and benchmark eligibility are recorded separately for resolved questions. AI involvement is unknown unless supported by a disclosure; a public solution predating a problem's listing is excluded from benchmark success/failure counts.

| Directory | Question | Status |
| --- | --- | --- |
| [`stochastic-bilevel`](stochastic-bilevel/) | Tight lower bounds for fully first-order stochastic bilevel optimization | Partially resolved: bounded-variance $\epsilon^{-6}$ lower bound by [Gu, Wu, and Yang (2026)](https://arxiv.org/abs/2609.21905); stochastic-smoothness $\epsilon^{-4}$ branch remains open; [project](../projects/stochastic-bilevel-first-order-lower-bound/) |
| [`finite-sum-nonconvex`](finite-sum-nonconvex/) | Polynomial finite-sum dependence in nonconvex lower bounds | Resolved by Peng, Tang, and Jia (2026); author-disclosed AI assistance; solution predates benchmark entry; [project](../projects/finite-sum-nonconvex-tight-complexity/) |
| [`nonconvex-concave-minimax`](nonconvex-concave-minimax/) | Tight deterministic NC--C minimax complexity | Resolved for deterministic methods; [project](../projects/nc-c-minimax-tight-complexity/) records disclosed AI assistance; [related stochastic methods](nonconvex-concave-minimax/#related-stochastic-methods) recorded separately, AI involvement unknown |
| [`pl-minimax`](pl-minimax/) | Tight two-sided PL--PL minimax complexity | Open |
| [`zeroth-order-nonsmooth-nonconvex`](zeroth-order-nonsmooth-nonconvex/) | Joint $d,\delta,\epsilon$ lower bound with noisy values | Open |
| [`deterministic-nonsmooth-nonconvex`](deterministic-nonsmooth-nonconvex/) | Deterministic/noiseless Goldstein-stationarity lower bound | Resolved by the AI-assisted proof of [Kornowski (2026)](https://arxiv.org/abs/2609.17780) |
| [`bandit-convex-regret`](bandit-convex-regret/) | Tight dimension dependence in bandit convex regret | Open |
| [`zeroth-order-smooth-convex`](zeroth-order-smooth-convex/) | Smooth exact-value zeroth-order lower bound | Partially resolved: deterministic bounded-query moderate-accuracy case by [Wu et al. (2026)](https://arxiv.org/abs/2609.18230); randomized algorithms remain open; [project](../projects/zeroth-order-smooth-convex-deterministic-lower-bound/) |
| [`zeroth-order-smooth-nonconvex`](zeroth-order-smooth-nonconvex/) | Smooth nonconvex exact-value zeroth-order lower bound | Open |

An open-problem page should specify the objective class, domain and regularity assumptions, oracle, admissible algorithms, output criterion, cost convention, known upper and lower bounds, and the exact gap to close.

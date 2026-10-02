# Joint lower bounds for zeroth-order nonconvex optimization on Euclidean balls

## Status and attribution

**Public preprint; author-disclosed AI assistance; related bounded-domain progress.** Haihan Zhang, Wendao Wu, Chenheng Zhang, Yanyi Li, Chunyuan Zheng, Cong Fang, Haoxuan Li, and Zhouchen Lin, [*Joint Lower Bounds for Zeroth-Order Nonconvex Optimization on Euclidean Balls*](https://arxiv.org/abs/2610.00275v1), 2026. This repository has compared the v1 statements with the benchmark but has not independently audited the complete proof.

The paper obtains the requested joint dimension and accuracy dependence in a local-gap, bounded-query model. It **does not resolve** the [original stochastic nonsmooth nonconvex benchmark](../../open-problems/zeroth-order-nonsmooth-nonconvex/), which uses a global objective gap and unrestricted queries. Record it as related progress, without counting it as a benchmark solution.

## Setting and oracle

Let $`f(x)=\mathbb E_\xi F(x;\xi)`$, with sample functions defined on all of $`\mathbb R^d`$, $`\mathbb E|F(x_0;\xi)|<\infty`$, and sample-wise Lipschitz moduli satisfying

```math
|F(x;\xi)-F(y;\xi)|\leq L(\xi)\|x-y\|_2,
\qquad \mathbb E L(\xi)^2\leq L_0^2.
```

Queries and the final output must lie in the known ball $`X=B_2^d(x_0,R)`$. The initial gap is local:

```math
f(x_0)-\min_{x\in X}f(x)\leq\Delta.
```

An adaptive randomized algorithm may retain independently drawn sample handles and repeatedly query any retained function. A query returns the exact scalar $`F(x;\xi_h)`$, with no derivatives or information about the hidden sample beyond its values. Each scalar evaluation costs one unit; drawing an unevaluated handle is free and reveals nothing. A common-sample two-point estimate therefore costs two evaluations. Internal computation is unrestricted, and the final output need not be a queried point. The budget bounds the number of evaluations on every transcript.

The Goldstein residual is the ambient residual

```math
\partial_\delta f(x)=\mathrm{cl}\,\mathrm{conv}\,
\bigcup_{\|y-x\|_2\leq\delta}\partial^C f(y),
\qquad G_\delta(f,x)=\mathrm{dist}(0,\partial_\delta f(x)).
```

The neighborhood may extend outside $`X`$; this is not a constrained normal-cone stationarity criterion. Success means $`G_\delta(f,x_{\mathrm{out}})\leq\epsilon`$ with probability at least $`1/2`$, over the algorithm's randomness and sampled functions. Every hard instance is promised to contain an ambient stationary point in $`X`$; its location is unknown to the algorithm.

## Reported lower bounds

**Goldstein stationarity (Corollary 4.2).** There are absolute constants $`c,C>0`$ such that, for positive $`L_0,\Delta,\delta,\epsilon`$ and integer $`d\geq2`$ satisfying

```math
0<\epsilon\leq cL_0,\qquad
\Delta\geq C\delta\epsilon,\qquad
d\geq C\left[1+\log\left(2+\frac{\Delta L_0^2}{\delta\epsilon^3}\right)\right],
```

there is a deterministic radius $`R=\Theta(\Delta/\epsilon)`$ and a family of smooth admissible instances, each containing a stationary point in the ball, for which the worst-case scalar-evaluation complexity is

```math
\Omega\!\left(\frac{dL_0^2\Delta}{\delta\epsilon^3}\right).
```

For every adaptive randomized reusable-handle algorithm below a sufficiently small constant times this budget, some fixed instance has success probability less than $`1/2`$. The constants are absolute; the dimension condition is a parameter restriction, not a hidden logarithmic factor in the evaluation bound. With $`L_0=\Delta=1`$, the rate is $`\Omega(d\delta^{-1}\epsilon^{-3})`$ in the stated regime.

**Smooth core (Theorem 4.1).** For a population objective with globally $`H`$-Lipschitz gradient and target $`\|\nabla f(x_{\mathrm{out}})\|_2\leq\eta`$, the corresponding lower bound is

```math
\Omega\!\left(\frac{dL_0^2H\Delta}{\eta^4}\right),
```

on a constructed ball $`R=\Theta(\Delta/\eta)`$, assuming $`0<\eta\leq c_0L_0`$, $`H\Delta\geq C_0\eta^2`$, and

```math
d\geq C_0\left[1+\log\left(2+\frac{H\Delta L_0^2}{\eta^4}\right)\right].
```

The hard family is $`C^\infty`$ and satisfies the same sample-Lipschitz and local-gap budgets. Lemma 6.4 gives $`\|\nabla f(x)\|_2\leq G_\delta(f,x)+H\delta`$; setting $`H=\epsilon/\delta`$ and $`\eta=2\epsilon`$ yields the Goldstein bound. The smooth core is stochastic and does not resolve the separate [exact-value smooth nonconvex benchmark](../../open-problems/zeroth-order-smooth-nonconvex/).

## Comparison with the benchmark and remaining limits

| Requirement | Original Kornowski--Shamir setting | Zhang et al. v1 lower bound |
| --- | --- | --- |
| Objective gap | $`f(x_0)-\inf_{\mathbb R^d}f\leq\Delta`$ | $`f(x_0)-\min_X f\leq\Delta`$ |
| Queries and output | Unrestricted in $`\mathbb R^d`$ | Restricted to the constructed ball |
| Sample access | Common-sample function evaluations | Arbitrary reuse of retained sample functions |
| Target | Ambient Goldstein stationarity | Same target; stationary point in the ball promised |

The linear carrier in the hard construction makes $`\inf_{\mathbb R^d}f=-\infty`$ (Section 7). Thus the family violates the benchmark's finite global-gap assumption. Enlarging the ball also increases its local gap, so the theorem does not transfer to the original model by allowing more query locations.

Proposition A.1 localizes the known upper bound to a ball with $`R\geq C_0(\Delta/\epsilon+\delta)`$, using $`O(1+dL_0^2\Delta/(\delta\epsilon^3))`$ scalar evaluations. This does not match the lower-bound radius: the Goldstein construction has $`R\leq\Delta/(8\epsilon)`$ (discussion after Proposition 4.3). Without the existence promise, the full local-gap class at such small radii can have no successful output at all. Consequently, the paper establishes an information lower bound on solvable instances, not a tight minimax characterization at a common radius. Both that characterization and the unrestricted global-gap lower bound remain open.

## Proof architecture

- Spatially disjoint informative regions hide successive transverse directions; a terminal region contains a stationary point. The gap permits $`\Theta(H\Delta/\eta^2)`$ stages.
- Each retained sample contains a fixed Gaussian perturbation of each hidden direction. An adaptive projection-posterior argument requires $`\Theta(dL_0^2/\eta^2)`$ scalar observations per stage, including repeated queries to the same sample.
- A shadow transcript suppresses unresolved future regions. A first-disagreement coupling bounds premature visits and arbitrary final outputs, then averages over admissible fixed instances. Multiplying the stage and information costs gives the smooth bound.

## Verification record

- [x] On 2026-10-02, compared the supplied v1 PDF (Sections 3--4 and 7, and Proposition A.1) with the original benchmark and Kornowski--Shamir's Assumption 2 and Theorem 5.
- [x] Recorded the theorem quantifiers, success probability, parameter restrictions, ambient output criterion, and scalar-evaluation accounting.
- [x] Checked the algebraic substitution from the smooth lower bound to the Goldstein rate in Lemma 6.4 and Corollary 4.2.
- [ ] Independent lemma-by-lemma audit of the hard-family estimates, adaptive posterior, shadow coupling, and localized upper bound.
- [ ] Independent human repository verifier(s); none recorded.

The eight authors named above report reviewing and approving the mathematical claims and formal artifacts. This is author-reported verification, not an independent repository review. The preprint status does not imply a verified draft or independent formal verification.

## Provenance and references

- **AI disclosure:** the v1 first-page AI Usage statement attributes nearly the entire research pipeline to the authors' internal GPT-5.6 Sol auto-research system and reports a Lean-backed article audit. It says the full audit and system technical reports will be released later; no public trace or audit artifact is supplied in v1.
- **Timeline:** arXiv records v1 as submitted on 2026-09-24. The benchmark page was first committed on 2026-09-05 ([repository commit](https://github.com/AI4Optimization/ai-for-optimization/commit/494330dc896cedce88ea0ea1960ee105951af40e)). The result postdates listing, but its different domain and gap assumptions prevent counting it as a solution of the original benchmark.
- **Canonical manuscript:** [arXiv:2610.00275v1](https://arxiv.org/abs/2610.00275v1), [PDF](https://arxiv.org/pdf/2610.00275v1). The supplied v1 PDF was used for this assessment because the online full text was unavailable.
- **Comparison baseline:** [Kornowski and Shamir, JMLR 25(122), 2024](https://jmlr.org/papers/v25/23-1159.html), [arXiv full text](https://arxiv.org/html/2307.04504v3).
- **Bibliography:** [references.bib](references.bib).

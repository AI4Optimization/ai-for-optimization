# Optimal polynomial exponents for stepsize-based acceleration of gradient descent

## Status

**Public preprints; optimal polynomial exponents and a sharp fixed-horizon follow-up.** Ye and Liu's AI-assisted lower bounds match the known non-anytime and anytime upper bounds up to subpolynomial factors. The [Jeong--Hong follow-up](#sharp-fixed-horizon-follow-up) removes the fixed-horizon loss for all predetermined real stepsizes, establishing the silver rate up to absolute constant factors; its authors disclose AI assistance with writing and checking. This project records these developments separately from the [earlier lower-bound project](../stepsize-accelerated-gd-lower-bound/). The follow-up has not been independently proof-audited by this repository.

## Result

For the original exponent results, following [arXiv v2](https://arxiv.org/abs/2609.09152v2), consider plain gradient descent

```math
x_k=x_{k-1}-h_k\nabla f(x_{k-1}),\qquad h_k\geq0,
```

and define its normalized worst-case last-iterate error by

```math
\mathcal R_n(H):=
\sup_{d\geq1}\ \sup_{f\in\mathcal F_L(\mathbb R^d)}
\sup_{x_*\in\arg\min f}\ \sup_{x_0\neq x_*}
\frac{f(x_n)-f(x_*)}{(L/2)\|x_0-x_*\|^2},
```

where $\mathcal F_L$ denotes convex $L$-smooth functions with a minimizer and $H=(h_1,\ldots,h_n)$. Set

```math
p_{\mathrm{sil}}=\log_2(1+\sqrt2)\approx1.271553,
\qquad
p_{\mathrm{any}}=\frac{2p_{\mathrm{sil}}}{1+p_{\mathrm{sil}}}\approx1.119545.
```

**Non-anytime (Theorem 1.1).** There is an absolute constant $C>0$ such that, for all sufficiently large $n$ and every predetermined nonnegative $n$-step schedule $H$,

```math
\mathcal R_n(H)\geq
n^{-\left(p_{\mathrm{sil}}+C\sqrt{\frac{\log\log n}{\log n}}\right)}.
```

Together with the $O(n^{-p_{\mathrm{sil}}})$ [silver-schedule upper bound](https://doi.org/10.1007/s10107-024-02164-2), this gives

```math
\inf_{H\in[0,\infty)^n}\mathcal R_n(H)
=n^{-p_{\mathrm{sil}}+o(1)}.
```

**Anytime (Theorem 1.2).** There is an absolute constant $C>0$ such that every predetermined infinite nonnegative schedule $`H=(h_k)_{k\geq1}`$ has infinitely many horizons $n$ with

```math
\mathcal R_n(H_n)\geq
n^{-\left(p_{\mathrm{any}}+C\sqrt{\frac{\log\log n}{\log n}}\right)},
\qquad H_n=(h_1,\ldots,h_n).
```

The [anytime upper bound of Zhang, Lee, Du, and Chen](https://proceedings.mlr.press/v291/zhang25a.html) achieves $O(n^{-p_{\mathrm{any}}})$ at every stopping time. Thus no single infinite nonnegative schedule has a uniform $O(n^{-q})$ guarantee for any $q>p_{\mathrm{any}}$.

## Setting and assumptions

These restrictions describe Ye and Liu's original exponent results. The sharp fixed-horizon follow-up below permits arbitrary real stepsizes.

- **Problem class:** unconstrained convex objectives on $\mathbb R^d$, with an $L$-Lipschitz gradient, $L>0$, and a minimizer; dimension is unrestricted in the worst case.
- **Algorithm and schedule:** plain GD with deterministic nonnegative stepsizes fixed before observing the objective or oracle responses; no momentum or auxiliary iterates.
- **Horizon:** the non-anytime schedule may depend on $n$; an anytime schedule must use the same infinite sequence at every horizon.
- **Initialization and scaling:** the error is normalized by $`(L/2)\|x_0-x_*\|^2`$ as in the paper. At distance $R$, the corresponding unnormalized bounds carry an $LR^2$ factor.
- **Oracle and output:** one exact gradient evaluation per update; the output is $x_n$, assessed by objective error.

## Original proof architecture

1. Build local two-coordinate hard functions whose gradients turn along a circular arc. A Moreau envelope realizes the prescribed trajectory, and the local transfer coefficient approaches one.
2. Select checkpoints and analyze their cost recursively. A weighted splitting inequality cancels the additional checkpoint terms introduced by the new construction.
3. Control the constants while approaching the silver exponent, producing the explicit subpolynomial loss. For anytime schedules, apply a record-time argument to obtain the lower bound at infinitely many horizons.

See Sections 2--4 and Appendices A--C of the paper for the proof.

## Verification record for the original result

- [x] The displayed statements, normalization, nonnegative-step restriction, and horizon quantifiers were cross-checked against arXiv v2, Theorems 1.1--1.2.
- [x] The matching upper bounds were checked against their cited sources.
- [x] The authors' AI-use disclosure and the earlier blog post were located.
- [ ] A separate lemma-by-lemma proof audit by this repository's maintainers is recorded.
- [ ] Human verifier(s) for such an audit are recorded.

This entry records a public preprint and a source-level check; it does not certify a new independent proof verification.

## Strongly convex follow-up

[Liu and Ye (2026)](https://arxiv.org/abs/2609.26873) extend the silver-rate optimality result to smooth strongly convex objectives. For plain GD with predetermined nonnegative stepsizes, condition number $\kappa$, and

```math
p_{\mathrm{sil}}=\log_2(1+\sqrt2),
```

they prove the iteration lower bound

```math
\Omega\!\left(
\kappa^{1/p_{\mathrm{sil}}-o(1)}
\log\frac1\delta
\right)
```

for both relative squared distance and relative function error, uniformly over $0<\delta<1$ and all sufficiently large $\kappa$. This matches the polynomial exponent in $\kappa$ of the strongly convex silver-stepsize upper bound of Altschuler and Parrilo (2025). The follow-up therefore settles the corresponding exponent question for predetermined nonnegative schedules, up to the subpolynomial loss.

## Sharp fixed-horizon follow-up

**Public preprint; source-level check.** Yechan Jeong and Youngjoon Hong, [*Silver rate is sharp for gradient descent*](https://arxiv.org/abs/2611.30100v1), arXiv:2611.30100v1, submitted November 23, 2026.

**Theorem 1.1.** Extend the definition of $`\mathcal R_n(H)`$ above to $`H\in\mathbb R^n`$. There is an absolute constant $`c>0`$ such that, for every $`L>0`$, every integer $`n\geq1`$, and every predetermined real schedule $`H=(h_1,\ldots,h_n)`$,

```math
\mathcal R_n(H)\geq c\,n^{-p_{\mathrm{sil}}},
\qquad p_{\mathrm{sil}}=\log_2(1+\sqrt2).
```

The function class, unrestricted finite dimension, minimizer, and initialization quantifiers are exactly those in the definition above. In particular, the hard instance may depend on the schedule and horizon. The paper's $`R_{n,L}(H)`$ equals this entry's $`\mathcal R_n(H)`$: both divide the last-iterate error by $`(L/2)\|x_0-x_*\|^2`$.

The schedule may depend on $`n`$ and $`L`$, but is fixed independently of the objective, initialization, and oracle responses. Zero and negative steps are allowed, with no bound on their magnitudes or restriction on their ordering. The algorithm remains plain GD, with one exact gradient evaluation per update and last-iterate objective error as its criterion. Schedule selection and scalar/vector arithmetic are not additional gradient-oracle calls.

Combining the lower bound with the silver-type upper bounds gives the paper's equation (1.6):

```math
c\,n^{-p_{\mathrm{sil}}}
\leq \inf_{H\in\mathbb R^n}\mathcal R_n(H)
\leq \inf_{H\in[0,\infty)^n}\mathcal R_n(H)
\leq C\,n^{-p_{\mathrm{sil}}}.
```

Here $`c,C>0`$ are absolute, independent of the horizon, smoothness, schedule, and dimension; there is no hidden logarithmic or subpolynomial loss. The original [Altschuler--Parrilo silver schedule](https://doi.org/10.1007/s10107-024-02164-2) attains the upper bound at $`n=2^k-1`$. [Grimmer, Shu, and Wang](https://arxiv.org/abs/2410.16249v2) construct schedules for every length, providing the all-horizon upper bound used here. These are separately chosen finite-horizon schedules, not one infinite anytime schedule.

This strengthens Ye and Liu's fixed-horizon exponent bound above to a constant-factor match and covers signed schedules. Section 1.2 and Table 1 of the follow-up also credit earlier refinements by Bell and a signed-schedule exponent bound by He and Cheng; the improvement here is removal of the remaining losses.

### Proof architecture of the sharp bound

1. Normalize to $`L=1`$ using Lemma 1.2. A quadratic test converts a bound on the number of large steps into a final-error lower bound (Lemma 2.2).
2. Prove a quantitative splitting inequality whose equality case is the silver proportions (Lemma 3.1), and organize intervals between large steps in a tree (Section 3).
3. Realize prescribed signed-step trajectories by convex Moreau envelopes, joining planar trajectories and consecutive blocks to control products of distance ratios (Sections 4 and 6).
4. Control deviations from the silver proportions and average over thresholds and tree levels (Sections 5 and 7). The resulting large-step count bound (Theorem 2.1) and Lemma 2.2 yield Theorem 1.1 without a subpolynomial loss.

### Verification record for the sharp follow-up

- [x] Theorem 1.1, definition (1.2), and equation (1.6) were cross-checked against arXiv v1, including $`n=1`$, arbitrary real schedules, and the absolute-constant quantifiers.
- [x] The normalization and smoothness scaling in Lemma 1.2 were checked against this entry's definition.
- [x] The fixed-horizon scope, last-iterate output, and one-gradient-per-update accounting were checked.
- [x] The earlier loss and all-horizon upper-bound comparison were checked against the cited statements and sources.
- [x] The AI Use Statement was located on page 53 of v1.
- [ ] A separate lemma-by-lemma audit of Sections 3--7, including imported lemmas, recurrences, constants, and trajectory compatibility, is recorded.
- [ ] Human verifier(s) for an independent proof audit are recorded.

The checked items document a source-level comparison, not independent verification of the full proof. No human proof reviewer is recorded for this follow-up.

## Limitations and open questions

- **Fixed-horizon gap resolved:** the sharp follow-up removes the original subpolynomial loss and the nonnegative-step restriction for convex last-iterate objective error. Optimal leading constants and an exact optimal schedule at each horizon are not determined by its constant-factor result.
- **Anytime quantifiers:** Ye and Liu's anytime lower bound still has a subpolynomial loss and holds at infinitely many horizons, not necessarily every sufficiently large horizon. Jeong and Hong's fixed-horizon result does not sharpen it to a constant-factor match at $`p_{\mathrm{any}}`$. The worst-case function may depend on the horizon.
- **Strong convexity:** the strongly convex follow-up above establishes exponent optimality for nonnegative schedules up to a subpolynomial loss. The sharp convex theorem does not remove that loss or establish its strongly convex analogue for signed schedules.
- **Algorithmic scope:** these results do not settle adaptive stepsizes, randomized schedules, or alternative output criteria.

## Provenance and references

- **Original exponent-result authors:** Yuhan Ye and Kaizhao Liu.
- **Earlier public write-up:** [*The Silver Rate Is (Almost) Tight*](https://yeyuhanyyh.github.io/gd-silver-rate/), posted September 7, 2026, 17:50 GMT-4. Retain this link as the earlier public record.
- **Manuscript:** [*Silver Rate Is (Almost) Optimal for Gradient Descent*](https://arxiv.org/abs/2609.09152v2), arXiv:2609.09152, v2. This entry uses the manuscript's statements and normalization; the blog uses a different constant normalization.
- **Strongly convex follow-up:** Kaizhao Liu and Yuhan Ye, [*Silver Rate Is (Almost) Optimal for Gradient Descent: The Strongly Convex Case*](https://arxiv.org/abs/2609.26873), arXiv:2609.26873.
- **Sharp fixed-horizon follow-up:** Yechan Jeong and Youngjoon Hong, [*Silver rate is sharp for gradient descent*](https://arxiv.org/abs/2611.30100v1), arXiv:2611.30100v1, November 23, 2026.
- **AI contribution to the original exponent result, as reported by Ye and Liu:** the authors proposed bending the local trajectory, then developed the construction and analysis through repeated interactions with ChatGPT-6 Astra / Astra Ultra. See the AI Disclosure in the paper and blog.
- **AI contribution to the sharp follow-up, as reported by Jeong and Hong:** the AI Use Statement on page 53 says AI tools assisted with writing and checking the mathematical statements and proofs. It does not name systems, models, or prompts, link conversation traces, or assign a specific discovery role to AI.
- **Original AI traces:** no standalone conversation transcript is linked in the reviewed sources for either the original exponent result or the sharp follow-up; retain their respective AI disclosures as the available provenance records.
- **Preceding construction:** Jung, Cho, and Yun, [*Stronger Lower Bounds for (Non-)Anytime Acceleration of Gradient Descent*](https://arxiv.org/abs/2609.04032).
- **Bibliography:** [references.bib](references.bib).

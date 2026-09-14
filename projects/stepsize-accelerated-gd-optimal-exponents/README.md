# Optimal polynomial exponents for stepsize-based acceleration of gradient descent

## Status

**Public preprint; AI-assisted proof; optimal polynomial exponents.** Ye and Liu's lower bounds match the known non-anytime and anytime upper bounds up to subpolynomial factors. This project records their silver-exponent result separately from the [earlier lower-bound project](../stepsize-accelerated-gd-lower-bound/).

## Result

Following [arXiv v2](https://arxiv.org/abs/2609.09152v2), consider plain gradient descent

$$
x_k=x_{k-1}-h_k\nabla f(x_{k-1}),\qquad h_k\geq0,
$$

and define its normalized worst-case last-iterate error by

$$
\mathcal R_n(H):=
\sup_{d\geq1}\ \sup_{f\in\mathcal F_L(\mathbb R^d)}
\sup_{x_*\in\arg\min f}\ \sup_{x_0\neq x_*}
\frac{f(x_n)-f(x_*)}{(L/2)\|x_0-x_*\|^2},
$$

where $\mathcal F_L$ denotes convex $L$-smooth functions with a minimizer and $H=(h_1,\ldots,h_n)$. Set

$$
p_{\mathrm{sil}}=\log_2(1+\sqrt2)\approx1.271553,
\qquad
p_{\mathrm{any}}=\frac{2p_{\mathrm{sil}}}{1+p_{\mathrm{sil}}}\approx1.119545.
$$

**Non-anytime (Theorem 1.1).** There is an absolute constant $C>0$ such that, for all sufficiently large $n$ and every predetermined nonnegative $n$-step schedule $H$,

$$
\mathcal R_n(H)\geq
n^{-\left(p_{\mathrm{sil}}+C\sqrt{\frac{\log\log n}{\log n}}\right)}.
$$

Together with the $O(n^{-p_{\mathrm{sil}}})$ [silver-schedule upper bound](https://doi.org/10.1007/s10107-024-02164-2), this gives

$$
\inf_{H\in[0,\infty)^n}\mathcal R_n(H)
=n^{-p_{\mathrm{sil}}+o(1)}.
$$

**Anytime (Theorem 1.2).** There is an absolute constant $C>0$ such that every predetermined infinite nonnegative schedule $H=(h_k)_{k\geq1}$ has infinitely many horizons $n$ with

$$
\mathcal R_n(H_n)\geq
n^{-\left(p_{\mathrm{any}}+C\sqrt{\frac{\log\log n}{\log n}}\right)},
\qquad H_n=(h_1,\ldots,h_n).
$$

The [anytime upper bound of Zhang, Lee, Du, and Chen](https://proceedings.mlr.press/v291/zhang25a.html) achieves $O(n^{-p_{\mathrm{any}}})$ at every stopping time. Thus no single infinite nonnegative schedule has a uniform $O(n^{-q})$ guarantee for any $q>p_{\mathrm{any}}$.

## Setting and assumptions

- **Problem class:** unconstrained convex objectives on $\mathbb R^d$, with an $L$-Lipschitz gradient, $L>0$, and a minimizer; dimension is unrestricted in the worst case.
- **Algorithm and schedule:** plain GD with deterministic nonnegative stepsizes fixed before observing the objective or oracle responses; no momentum or auxiliary iterates.
- **Horizon:** the non-anytime schedule may depend on $n$; an anytime schedule must use the same infinite sequence at every horizon.
- **Initialization and scaling:** the error is normalized by $(L/2)\|x_0-x_*\|^2$ as in the paper. At distance $R$, the corresponding unnormalized bounds carry an $LR^2$ factor.
- **Oracle and output:** one exact gradient evaluation per update; the output is $x_n$, assessed by objective error.

## Proof architecture

1. Build local two-coordinate hard functions whose gradients turn along a circular arc. A Moreau envelope realizes the prescribed trajectory, and the local transfer coefficient approaches one.
2. Select checkpoints and analyze their cost recursively. A weighted splitting inequality cancels the additional checkpoint terms introduced by the new construction.
3. Control the constants while approaching the silver exponent, producing the explicit subpolynomial loss. For anytime schedules, apply a record-time argument to obtain the lower bound at infinitely many horizons.

See Sections 2--4 and Appendices A--C of the paper for the proof.

## Verification record

- [x] The displayed statements, normalization, nonnegative-step restriction, and horizon quantifiers were cross-checked against arXiv v2, Theorems 1.1--1.2.
- [x] The matching upper bounds were checked against their cited sources.
- [x] The authors' AI-use disclosure and the earlier blog post were located.
- [ ] A separate lemma-by-lemma proof audit by this repository's maintainers is recorded.
- [ ] Human verifier(s) for such an audit are recorded.

This entry records a public preprint and a source-level check; it does not certify a new independent proof verification.

## Limitations and open questions

- **Exponent optimality:** the loss $n^{-C\sqrt{\log\log n/\log n}}$ remains. The result does not give a constant-factor matching $\Omega(n^{-p_{\mathrm{sil}}})$ bound; reducing or removing this loss remains open.
- **Sign restriction:** the silver-exponent lower bounds concern nonnegative schedules. Extending them to schedules allowing negative steps remains open.
- **Anytime quantifiers:** the lower bound holds at infinitely many horizons, not necessarily every sufficiently large horizon. The worst-case function may depend on the horizon.
- **Algorithmic scope:** these theorems do not settle adaptive stepsizes, randomized schedules, alternative output criteria, or the corresponding strongly convex problem.

## Provenance and references

- **Authors:** Yuhan Ye and Kaizhao Liu.
- **Earlier public write-up:** [*The Silver Rate Is (Almost) Tight*](https://yeyuhanyyh.github.io/gd-silver-rate/), posted September 7, 2026, 17:50 GMT-4. Retain this link as the earlier public record.
- **Manuscript:** [*Silver Rate Is (Almost) Optimal for Gradient Descent*](https://arxiv.org/abs/2609.09152v2), arXiv:2609.09152, v2. This entry uses the manuscript's statements and normalization; the blog uses a different constant normalization.
- **AI contribution, as reported by the authors:** the authors proposed bending the local trajectory, then developed the construction and analysis through repeated interactions with ChatGPT-6 Astra / Astra Ultra. See the AI Disclosure in the paper and blog.
- **Original AI trace:** no standalone conversation transcript is linked in the reviewed sources; the available record is the authors' AI Disclosure.
- **Preceding construction:** Jung, Cho, and Yun, [*Stronger Lower Bounds for (Non-)Anytime Acceleration of Gradient Descent*](https://arxiv.org/abs/2609.04032).
- **Bibliography:** [references.bib](references.bib).

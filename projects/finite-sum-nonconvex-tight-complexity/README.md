# Tight complexity for finite-sum nonconvex optimization

## Status

**Public preprint; external result; author-disclosed AI assistance.** Peng, Tang, and Jia (2026) resolve the repository's [finite-sum nonconvex problem](../../open-problems/finite-sum-nonconvex/). The theorem and oracle model have been compared with the benchmark; an independent repository proof audit has not been completed.

## Result

Write $L=L_{\max}$ in the paper's notation. [Theorem 3.1 and Corollary 3.2](https://arxiv.org/html/2609.00045v2#S3) give the worst-case randomized incremental first-order oracle (IFO) complexity

$$
\Theta\!\left(n+\frac{\sqrt n\,L\Delta}{\epsilon^2}\right).
$$

More precisely, there are universal constants $c_0,c_1>0$ such that, for every integer $n\geq1024$, every $L,\Delta>0$, and $0<\epsilon^2\leq c_0L\Delta$, every randomized algorithm using at most $c_1(n+\sqrt n\,L\Delta/\epsilon^2)$ calls has a finite-dimensional admissible instance on which its output $\widehat x$ satisfies

$$
\Pr\!\left(\|\nabla F(\widehat x)\|\geq4\epsilon\right)\geq\frac{11}{16}.
$$

This is the fixed-budget statement in Appendix C. Appendix F extends the rate to worst-case expected call budgets with $\mathbb E\|\nabla F(\widehat x)\|\leq\epsilon$. Appendix G.1 covers $1\leq n<1024$ by replication of a single hard function and a change of universal constants. PAGE and SPIDER supply the matching upper bound. All rate constants are universal; no logarithmic factors are suppressed.

The result supplies the original target's missing $\sqrt n$ factor in the accuracy-dependent term, together with the additive $n$ cost.

## Setting and assumptions

- **Objective:** $F(x)=n^{-1}\sum_{i=1}^n f_i(x)$ on $\mathbb R^d$, with $\|\nabla f_i(x)-\nabla f_i(y)\|\leq L\|x-y\|$ for every component and every $x,y$. Neither convexity nor a PL condition is required.
- **Initialization:** $F(x_0)-\inf F\leq\Delta$; translating coordinates gives the paper's $x_0=0$.
- **Oracle and cost:** one query $(i,x)$ returns the exact pair $(f_i(x),\nabla f_i(x))$. Count component calls; internal computation is free. A full gradient costs $n$ calls. The lower bound also applies when only component gradients are returned.
- **Algorithms and output:** both query choices may depend on the full transcript and private randomness. Repeated indices, arbitrary query points, random stopping, and an arbitrary output computed from the transcript are allowed. No span or zero-respecting assumption is used.
- **Dimension and regime:** finite dimension may grow with the parameters and call budget. The tight rate is asserted in the small-accuracy regime above, not for a fixed prescribed dimension or arbitrary large $\epsilon$.

## Verification record

- [x] Compared the v2 nonconvex statements, individual smoothness, oracle, output criterion, and parameter regime with the benchmark on 2026-09-16.
- [x] Checked the source disclosures and the repository entry date.
- [ ] Independent lemma-by-lemma audit, including imported lemmas, constants, and oracle accounting.
- [ ] Repository human reviewer names and sign-off.

The v1 AI Use Statement reports that the authors verified their final manuscript. This is author-reported verification by Yuxing Peng, Zhiqing Tang, and Weijia Jia, not an independent repository review. This entry records only the nonconvex stationarity result; the paper's separate PL results are outside this benchmark question.

## Provenance and benchmark timeline

- **Original work:** Yuxing Peng, Zhiqing Tang, and Weijia Jia, [*Dense Weak Hiding: Closing Complexity Gaps in Nonconvex and PL Finite-Sum Optimization under Individual Smoothness*](https://arxiv.org/abs/2609.00045v2), 2026.
- **AI disclosure:** the [v1 AI Use Statement](https://arxiv.org/html/2609.00045v1) describes language-model assistance with brainstorming, proof-draft review, and editing. The [v2 statement](https://arxiv.org/html/2609.00045v2) reports assistance with developing and writing mathematical proofs and improving presentation. Neither statement identifies specific models or provides prompt/response records.
- **Timeline:** arXiv records v1 submission on August 30, 2026, and v2 on September 13, 2026. The problem page first entered this repository in [commit `494330d`](https://github.com/AI4Optimization/ai-for-optimization/commit/494330dc896cedce88ea0ea1960ee105951af40e), dated September 5, 2026. The nonconvex result was already stated in v1.
- **Benchmark eligibility:** pre-existing public solution. Retain the problem's history, but exclude it from AI success/failure counts for problems open at the time of listing. Its AI-assisted provenance does not change this timing.
- **Repository curation:** Codex compared sources and updated the documentation on 2026-09-16; the mathematical result is credited to the paper's authors.

## Related references

- [Fang et al., *SPIDER: Near-Optimal Non-Convex Optimization via Stochastic Path-Integrated Differential Estimator*, NeurIPS 2018](https://arxiv.org/abs/1807.01695).
- [Li, Bao, Zhang, and Richtarik, *PAGE: A Simple and Optimal Probabilistic Gradient Estimator for Nonconvex Optimization*, ICML 2021](https://proceedings.mlr.press/v139/li21a.html).
- [Zhou and Gu, *Lower Bounds for Smooth Nonconvex Finite-Sum Optimization*, ICML 2019](https://proceedings.mlr.press/v97/zhou19b.html).

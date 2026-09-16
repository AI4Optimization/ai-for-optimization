# Tight complexity bound for finite-sum nonconvex optimization

## Status

**Resolved by external work: Peng, Tang, and Jia (2026).** Their public preprint establishes the matching lower bound under individual smoothness for randomized adaptive incremental first-order algorithms.

**AI provenance:** author-disclosed AI assistance. The preprint's AI Use Statement reports assistance from large language models with mathematical proofs and manuscript preparation; specific models and traces are not disclosed there.

**Benchmark status:** pre-existing public solution. The [v1 preprint](https://arxiv.org/abs/2609.00045v1) was submitted on August 30, 2026, before this page's [first repository commit](https://github.com/AI4Optimization/ai-for-optimization/commit/494330dc896cedce88ea0ea1960ee105951af40e) on September 5, 2026. Retain this page as a historical record and exclude it from counts of AI successes or failures on problems open when listed.

See the [project record](../../projects/finite-sum-nonconvex-tight-complexity/) for the precise result, source disclosures, and verification scope. This status records a public-preprint resolution; an independent repository proof audit has not been completed.

## Problem definition

Minimize $F(x)=n^{-1}\sum_{i=1}^n f_i(x)$ over $x\in\mathbb R^d$, where $F$ may be nonconvex, every component $f_i$ has an $L$-Lipschitz gradient, and $F(x_0)-\inf F\leq\Delta$. The output criterion is $\mathbb E\|\nabla F(x)\|\leq\epsilon$.

## Oracle model

At each adaptive query $(i,x)$, an incremental first-order oracle returns $(f_i(x),\nabla f_i(x))$ or just $\nabla f_i(x)$. Complexity is the number of component-oracle calls. The resolved lower bound covers randomized algorithms choosing both the component and query point from their full history and private randomness, including outputs that were never queried. It holds for the value-and-gradient oracle and therefore also for the gradient-only oracle. No linear-span or zero-respecting restriction is imposed.

## Original gap and resolution

The original target was $\Omega(n^\delta\epsilon^{-2})$ for some $0<\delta\leq1/2$, ideally $\delta=1/2$, with full $L$ and $\Delta$ dependence. The page compared SPIDER's $O(\sqrt n\,\epsilon^{-2})$ accuracy-dependent term with a lower bound lacking polynomial $n$ dependence in that term.

**Peng, Tang, and Jia, Theorem 3.1 and Corollary 3.2.** With the paper's $L_{\max}=L$, for $L,\Delta>0$ and $0<\epsilon^2\leq cL\Delta$, where $c>0$ is universal, the worst-case randomized IFO complexity is

$$
\Theta\!\left(n+\frac{\sqrt n\,L\Delta}{\epsilon^2}\right).
$$

The theorem is stated for $n\geq1024$; Appendix G.1 explains the extension to smaller positive $n$ by adjusting universal constants. Appendix F covers expected gradient norm and expected oracle cost, matching the original output criterion. The matching upper bound comes from PAGE and SPIDER. The bound hides no logarithmic factors, and the worst-case dimension may grow with the parameters and query budget.

## References

- [Peng, Tang, and Jia, *Dense Weak Hiding: Closing Complexity Gaps in Nonconvex and PL Finite-Sum Optimization under Individual Smoothness*, arXiv:2609.00045v2](https://arxiv.org/abs/2609.00045v2)
- [Li, Bao, Zhang, and Richtarik, *PAGE: A Simple and Optimal Probabilistic Gradient Estimator for Nonconvex Optimization*, ICML 2021](https://proceedings.mlr.press/v139/li21a.html)
- [Fang et al., *SPIDER: Near-Optimal Non-Convex Optimization via Stochastic Path-Integrated Differential Estimator*, NeurIPS 2018](https://arxiv.org/abs/1807.01695)
- [Zhou and Gu, *Lower Bounds for Smooth Nonconvex Finite-Sum Optimization*, ICML 2019](https://proceedings.mlr.press/v97/zhou19b.html)

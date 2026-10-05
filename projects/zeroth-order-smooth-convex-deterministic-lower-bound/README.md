# Exact-value lower bounds for smooth convex optimization

## Status and attribution

**Resolved by a subsequent randomized lower bound.** Wu et al. (2026) first established the deterministic bounded-query result below. [Dorn et al. (2026)](https://arxiv.org/abs/2610.00345v1) subsequently proved the matching lower bound for adaptive randomized algorithms with unrestricted queries, resolving the recorded open problem.

The original deterministic paper is Wendao Wu, Haihan Zhang, Chenheng Zhang, Yanyi Li, Chunyuan Zheng, Cong Fang, Haoxuan Li, and Zhouchen Lin, [*Near-Optimal Deterministic Exact-Value Complexity for Smooth Convex Optimization*](https://arxiv.org/abs/2609.18230), 2026. Its authors disclose that an internal GPT-5.6 Sol auto-research system carried out nearly the entire research pipeline and a Lean-backed audit; they state that they reviewed and approved the claims. This repository has not independently audited either complete proof. No AI-use disclosure was located in the reviewed Dorn et al. v1 source.

## Setting and oracle

The objective is globally $L$-smooth and convex on $\mathbb R^d$, with a unique minimizer inside $B_2(R/2)$. An adaptive deterministic algorithm may query only points in $B_2(R)$ and receives exact scalar function values; its output is also in $B_2(R)$. It must return $\hat x$ with $`f(\hat x)-f^*\leq\epsilon`$. The cost is the number of exact-value queries.

## Result

Theorem 3.5 proves

```math
\Omega\!\left(d\min\left\{\sqrt{\frac{LR^2}{\epsilon}},\left(\frac{d}{\log(ed)}\right)^{1/3}\right\}\right)
```

queries. An $O(d\sqrt{LR^2/\epsilon})$ upper bound matches it, up to constants, for $LR^2(\log(ed)/d)^{2/3}\leq\epsilon\leq cLR^2$ with a universal $c>0$. The fixed smooth hard instance uses a Moreau-smoothed chain, exact transcript shielding, and delayed rotations.

## Subsequent randomized resolution

Dorn et al. consider globally $`L`$-smooth convex functions on $`\mathbb R^d`$ with a minimizer in $`\mathbb B_2^d(R)`$. Against adaptive randomized exact-value algorithms with unrestricted queries, they prove—already for quadratics—the lower bound

```math
\Omega\!\left(
d\min\!\left\{d,\sqrt{\frac{LR^2}{\epsilon}}\right\}
\right).
```

It has no logarithmic loss and matches the upper bound in the range $`LR^2/d^2\leq\epsilon\leq LR^2/32`$, giving $`\Theta(d\sqrt{LR^2/\epsilon})`$. This closes the randomized and unrestricted-query gap left by the deterministic result.

## Scope of the earlier result

The Wu et al. theorem itself remains deterministic, saturates at high accuracy, and does not cover queries outside $`B_2(R)`$. The Dorn et al. follow-up removes the randomized and query-domain restrictions in its stated accuracy range.

- [Public result: Wu et al. (2026)](https://arxiv.org/abs/2609.18230)
- [Randomized unrestricted-query resolution: Dorn et al. (2026)](https://arxiv.org/abs/2610.00345v1)

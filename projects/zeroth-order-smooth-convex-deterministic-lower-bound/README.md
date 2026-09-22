# Deterministic exact-value lower bound for smooth convex optimization

## Status and attribution

**Public preprint:** Wendao Wu, Haihan Zhang, Chenheng Zhang, Yanyi Li, Chunyuan Zheng, Cong Fang, Haoxuan Li, and Zhouchen Lin, [*Near-Optimal Deterministic Exact-Value Complexity for Smooth Convex Optimization*](https://arxiv.org/abs/2609.18230), 2026. The authors disclose that an internal GPT-5.6 Sol auto-research system carried out nearly the entire research pipeline and a Lean-backed audit; they state that they reviewed and approved the claims. This repository has not independently audited the proof.

## Setting and oracle

The objective is globally $L$-smooth and convex on $\mathbb R^d$, with a unique minimizer inside $B_2(R/2)$. An adaptive deterministic algorithm may query only points in $B_2(R)$ and receives exact scalar function values; its output is also in $B_2(R)$. It must return $\hat x$ with $f(\hat x)-f^*\leq\epsilon$. The cost is the number of exact-value queries.

## Result

Theorem 3.5 proves

$$
\Omega\!\left(d\min\left\{\sqrt{\frac{LR^2}{\epsilon}},\left(\frac{d}{\log(ed)}\right)^{1/3}\right\}\right)
$$

queries. An $O(d\sqrt{LR^2/\epsilon})$ upper bound matches it, up to constants, for $LR^2(\log(ed)/d)^{2/3}\leq\epsilon\leq cLR^2$ with a universal $c>0$. The fixed smooth hard instance uses a Moreau-smoothed chain, exact transcript shielding, and delayed rotations.

## Remaining limits

This partially resolves the [smooth convex exact-value open problem](../../open-problems/zeroth-order-smooth-convex/): **randomized adaptive algorithms remain open**. The high-accuracy lower bound saturates, and queries outside $B_2(R)$ are not covered. A deterministic resisting construction alone does not yield a randomized lower bound.

- [Public result: Wu et al. (2026)](https://arxiv.org/abs/2609.18230)

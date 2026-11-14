# Near-optimal convex optimization with lazy second-order oracles

## Status and attribution

**AI-assisted public preprint.** Xinliang Zhang, Lesi Chen, Chengchang Liu, and Jingzhao Zhang, [*Near-Optimal Convex Optimization with Lazy Second-Order Oracles*](https://arxiv.org/abs/2610.03222), 2026. The authors state that they proved the lower bound, used it to evaluate AI reasoning, and that ChatGPT 6 Astra recovered the same construction. They also credit ChatGPT 5.6 Pro Sol and ChatGPT 6 Astra with successive improvements to the upper bound. Their [initial AI responses](https://chatgpt.com/share/6aae90a9-3250-83e8-82cb-2e532e8c0ab1) are public. The subsequent [gradient--Hessian tradeoff lower bound](https://arxiv.org/abs/2610.22208) by Wu et al. implies the same $m$-dependence as a corollary, under its logarithmic-dimension and Hessian-budget conditions. This repository has not independently audited either proof.

## Problem and oracle model

Let $`f:\mathbb R^d\to\mathbb R`$ be convex with a Lipschitz-continuous Hessian and an attained minimum. An $`m`$-lazy second-order oracle returns gradients at every iteration and a Hessian once per $`m`$ iterations. One iteration is charged as one gradient-query unit; the lazy schedule means Hessian access is sparse. The target is an $`\epsilon`$-solution satisfying $`f(\hat x)-f^*\leq\epsilon`$.

## Matching query complexity

For the lazy second-order model, the authors prove a lower bound on total iterations of

```math
\Omega\!\left(m+m^{1/7}\epsilon^{-2/7}\right)
```

and construct an algorithm with upper bound

```math
\widetilde O\!\left(m+m^{1/7}\epsilon^{-2/7}\right).
```

This improves the previous upper-bound dependence $`\widetilde O(m+m^{13/21}\epsilon^{-2/7})`$ on the Hessian interval parameter $m$ and is tight up to logarithmic factors. The paper also discusses a weighted cost model assigning cost $m$ to a full second-order query; the project rate above follows its equivalent lazy-oracle formulation.

### Matching lower bound from gradient--Hessian tradeoffs

Wu et al., [*Gradient--Hessian Query Tradeoffs: Matching Lower Bounds in Logarithmic Dimension*](https://arxiv.org/abs/2610.22208), give an independent randomized lower bound for nonconvex optimization with Lipschitz Hessian. For initial gap scale $`T=\Delta\sqrt{L_2}/\epsilon^{3/2}`$, dimension $`d\geq C\log(2+T)`$, and rich-query budget $`h\geq1`$ with $`h+1\leq aT`$, every algorithm needs

```math
\Omega\!\left(\min\left\{Td^{1/3},\frac{T^{3/2}}{\sqrt{h+1}}\right\}\right)
```

ordinary gradient queries. Translating the Hessian budget to a lazy schedule with one Hessian query every $m$ iterations means $`h\asymp T/m`$. The second term then becomes $`T^{3/2}/\sqrt{T/m}=T\sqrt m`$. Thus, in the regime where this term controls the minimum, the result gives the matching lazy-Hessian dependence $`\Omega(m+T\sqrt m)`$ (including the $m$ Hessian-spaced iteration cost), subject to $`d\geq C\log(2+T)`$ and the paper's Hessian-budget range. This records the nonconvex tradeoff in the same parameter $m$; it does not replace the convex lower bound above.

## Algorithmic ideas and provenance

The lower bound uses a block zero-chain that separately accounts for first- and second-order information. The upper bound reduces the problem to cubic proximal subproblems and uses preconditioned accelerated gradient with segment search on an extrapolated objective. The paper's AI Usage section reports that ChatGPT 6 Astra recovered the authors' lower-bound construction after earlier models failed to obtain a nontrivial $m$ dependence, and that ChatGPT 5.6 Pro Sol and ChatGPT 6 Astra developed successive upper bounds before reaching the near-optimal rate.

## Reference

- Xinliang Zhang, Lesi Chen, Chengchang Liu, and Jingzhao Zhang, [*Near-Optimal Convex Optimization with Lazy Second-Order Oracles*](https://arxiv.org/abs/2610.03222), 2026.
- Wendao Wu et al., [*Gradient--Hessian Query Tradeoffs: Matching Lower Bounds in Logarithmic Dimension*](https://arxiv.org/abs/2610.22208), 2026.

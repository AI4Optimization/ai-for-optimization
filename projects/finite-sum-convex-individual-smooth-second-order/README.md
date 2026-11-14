# Near-optimal second-order convex finite-sum optimization under individual smoothness

## Status and attribution

**AI-assisted public preprint.** Xinliang Zhang, Lesi Chen, Zonghan Li, and Jingzhao Zhang, [*Near-Optimal Second-Order Convex Finite-Sum Optimization under Individual Smoothness*](https://arxiv.org/abs/2610.42040), 2026. The paper states that its authors proved the lower bound, while ChatGPT 6 Astra discovered the upper bound. The authors provide a public chat trace and report responsibility for the paper. This repository has not independently audited the proof.

## Problem and oracle model

Consider $`f(x)=n^{-1}\sum_{i=1}^n f_i(x)`$ on $`\mathbb R^d`$, where every component is convex, twice continuously differentiable, and satisfies the paper's individual smoothness assumptions, including Lipschitz Hessians. The goal is an $`\epsilon`$-solution with $`f(\hat x)-f^*\leq\epsilon`$. Complexity counts stochastic second-order component-oracle calls as defined in the paper.

## Matching complexity

The authors prove the lower bound

```math
\Omega\!\left(n+n^{5/7}\epsilon^{-2/7}\right)
```

and give the Taylor-corrected Lazy Newton (A-TLN) method with upper bound

```math
\widetilde O\!\left(n+n^{5/7}\epsilon^{-2/7}\right).
```

Thus individual smoothness and convexity improve on the averaged-smoothness second-order rate $`\widetilde\Theta(n+n^{6/7}\epsilon^{-2/7})`$ of Tsedenov and Kovalev. The match is up to logarithmic factors.

## Main ideas and provenance

The lower bound uses an individual-smoothness construction. For the upper bound, a second-order self-bounding inequality supports Taylor-corrected lazy Newton updates, combined with optimal Monteiro--Svaiter acceleration. The authors' AI Usage statement explicitly attributes the upper-bound discovery to ChatGPT 6 Astra and links the [research conversation](https://chatgpt.com/share/6acef320-0c3c-83ea-bafb-ac1554d1ea4e); the lower bound is attributed to the authors.

## Reference

- Xinliang Zhang, Lesi Chen, Zonghan Li, and Jingzhao Zhang, [*Near-Optimal Second-Order Convex Finite-Sum Optimization under Individual Smoothness*](https://arxiv.org/abs/2610.42040), 2026.

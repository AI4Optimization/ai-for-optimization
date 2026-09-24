# Matching bounds for higher-order nonconvex finite-sum optimization

## Status and attribution

**Public preprint:** Wendao Wu, Haihan Zhang, Chenheng Zhang, Yanyi Li, Chunyuan Zheng, Cong Fang, Haoxuan Li, and Zhouchen Lin, [*Matching Upper and Lower Bounds for Higher-Order Nonconvex Finite-Sum Optimization*](https://arxiv.org/abs/2609.28202), 2026. The authors disclose that nearly the entire research pipeline was carried out by their laboratory's GPT-5.6 Sol-powered auto-research system, which also conducted a Lean-backed article audit. They state that the authors reviewed and approved the mathematical claims and take responsibility for the manuscript. This repository has not independently audited the complete proof.

## Problem setting

Consider

$$
F(x)=\frac{1}{n}\sum_{i=1}^n f_i(x),
$$

with initial gap $F(0)-\inf F\leq\Delta$. For a fixed integer $p\geq2$, every component has an $L_p$-Lipschitz $p$th derivative. The goal is to output $\widehat x$ satisfying $\|\nabla F(\widehat x)\|\leq\epsilon$ with constant success probability.

## Oracle model

One exact component query selects an arbitrary index $i$ and point $x$ and returns the complete $p$-jet

$$
\bigl(f_i(x),\nabla f_i(x),\ldots,\nabla^p f_i(x)\bigr).
$$

Algorithms may be adaptive and randomized, query unbounded points, and use unrestricted internal computation. The lower bound imposes no span or zero-respecting restriction. The upper result also holds under the weaker mean-squared $p$th-derivative increment condition. Complexity counts complete component-jet queries, including initialization and verification calls.

## Tight complexity

For every fixed $p\geq2$, Theorem 3.2 establishes the minimax complexity

$$
\Theta_p\!\left(
n+\Delta L_p^{1/p}n^{1-1/(2p)}\epsilon^{-(p+1)/p}
\right).
$$

The constants depend only on the fixed order $p$, and the worst case ranges over all finite dimensions. The lower bound holds for unrestricted adaptive randomized algorithms. The upper bound succeeds with fixed constant probability and removes the prior fixed-confidence logarithmic loss. For example, the nontrivial terms are $\Delta L_3^{1/3}n^{5/6}\epsilon^{-4/3}$ for $p=3$ and $\Delta L_4^{1/4}n^{7/8}\epsilon^{-5/4}$ for $p=4$.

## Proof and algorithmic ideas

- The lower bound extends dense weak hiding to complete higher-order oracle replies. Flat gates conceal every derivative through order $p$, while a censored-transcript argument covers adaptive indices, arbitrary query points, and private randomness.
- The upper bound uses verified Taylor-residual epochs. Full component jets at a snapshot define Taylor control variates; recursive estimation tracks the residual, and exact function values verify an entire epoch before its progress is accepted.
- A separate construction proves the additive $n$ term throughout the positive-parameter regime.

The result closes the previous gap in the power of $n$ between general-order upper and lower bounds. It concerns higher-order incremental access and is distinct from first-order finite-sum complexity and from full-objective higher-order methods.

## Reference

- [arXiv abstract](https://arxiv.org/abs/2609.28202)
- [PDF](https://arxiv.org/pdf/2609.28202)

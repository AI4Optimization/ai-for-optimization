# Finite-sum NC--SC minimax lower bounds with exact proximal oracles

## Status and attribution

**Concurrent public works.** This project records [Peng, Tang, and Jia (2026)](https://arxiv.org/abs/2611.04806) and [Zhou (2026)](https://arxiv.org/abs/2610.04944) as concurrent results on finite-sum nonconvex--strongly-concave minimax complexity. Zhou proves the rate for randomized zero-respecting incremental first-order methods; Peng, Tang, and Jia match it for a broader adaptive randomized class that can make exact component proximal queries. The arXiv:2611.04806 paper reports a Lean 4 formalization of its lower bounds. This project records the authors' results and has not independently audited the proofs.

## Setting and oracle model

Consider $`\Phi(x)=\max_y F(x,y)`$ with $`F(x,y)=n^{-1}\sum_{i=1}^n f_i(x,y)`$, where the components satisfy the joint mean-squared smoothness and strong concavity assumptions in the cited papers. Write $`\kappa=L/\mu`$ and assume the initialization has primal gap at most $`\Delta`$ and joint gradient norm at most $`\sqrt{2L\Delta}`$ as specified by Peng, Tang, and Jia. The target is an $`\epsilon`$-stationary point of the value function, with expected squared primal gradient at most $`\epsilon^2`$ in Zhou's characterization.

Zhou studies randomized zero-respecting incremental first-order algorithms with exact dual initialization. Peng, Tang, and Jia allow arbitrary adaptive randomized algorithms receiving exact component values, gradients, and exact component proximal responses (global saddle points of regularized component problems). Complexity counts component queries. The lower bounds apply in the small-accuracy regime $`\epsilon^2/(L\Delta)`$ below a universal constant.

## Matching rate and scope

The common rate, up to logarithmic factors for the corresponding upper bounds, is

```math
n+\min\{\sqrt n\,\kappa,\ n^{3/4}\sqrt\kappa\}\,
\frac{L\Delta}{\epsilon^2}.
```

Zhou's zero-respecting result is characterized up to logarithmic factors across $`\kappa\geq1`$. In the intermediate regime $`1\leq\kappa\leq\sqrt n`$, their recursive proximal descent-ascent method reaches $`\widetilde O(n+\sqrt n\,\kappa L\Delta/\epsilon^2)`$ with a fixed query budget; for $`\kappa\geq\sqrt n`$, Catalyst matches the other branch. Peng, Tang, and Jia establish the lower bound against arbitrary adaptive randomized algorithms even when exact proximal access is available, and a component-gradient method attains it up to $`\log^2(2+\kappa)`$.

The latter hard instances use common proximal step sizes across components; a component's proximal response reveals hidden directions only up to the first direction assigned to another component. This addresses the possibility that exact proximal queries circumvent first-order hiding.

Under individual smoothness, Zhou also proves the lower bound $`\Omega(n+\min\{\kappa,\sqrt{n\kappa}\}L\Delta/\epsilon^2)`$. It matches the polynomial upper rate for a bilinear subclass when $`\kappa\geq n`$, while the intermediate-condition-number gap remains open.

## References

- Yuxing Peng, Zhiqing Tang, and Weijia Jia, [*On the Complexity of Finite-Sum Nonconvex-Strongly-Concave Minimax Optimization with Exact Proximal Oracles*](https://arxiv.org/abs/2611.04806), 2026.
- Qihao Zhou, [*Near-Optimal Complexity of Finite-Sum Nonconvex-Strongly-Concave Minimax Optimization*](https://arxiv.org/abs/2610.04944), 2026.

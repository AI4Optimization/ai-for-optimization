# Optimal high-order methods for monotone variational inequalities

## Status

**Public preprint; optimal rate.** The main project result is Xinliang Zhang, Lesi Chen, Linxuan Pan, Chengchang Liu, Junchi Yang, and Jingzhao Zhang, [*Optimal High-Order Methods for Solving Monotone Variational Inequalities*](https://arxiv.org/abs/2609.23557), 2026. The earlier [Halpern-ATM paper](https://arxiv.org/abs/2608.08463) by an overlapping author group is retained below as the **previous short note**, not the project's current best bound.

## Problem and oracle model

Find $x^*\in\mathcal X$ satisfying $0\in F(x^*)+N_{\mathcal X}(x^*)$, where $\mathcal X\subseteq\mathbb R^d$ is nonempty, compact, and convex, $F$ is monotone, and $D^{p-1}F$ is $L_p$-Lipschitz. An order-$p$ oracle returns $F(x),DF(x),\ldots,D^{p-1}F(x)$ at a query point. The output is a last-iterate graph point $u$ with $v\in F(u)+N_{\mathcal X}(u)$ and $\|v\|\leq\epsilon$. The complexity counts these oracle calls; solving the regularized Taylor-model VI is an internal computational primitive, so the bound is not a bound on all arithmetic work.

## Current result

For an integer $p\geq2$, Theorem 3.1 gives

$$
O\!\left(\left(\frac{L_pD^p}{\epsilon}\right)^{2/(3p-1)}\right)
$$

order-$p$ oracle calls, where $D=\|x_0-x^*\|$. Equivalently, Theorem 5.1 gives a last-iterate residual of $O(L_pD^p/T^{(3p-1)/2})$ using $O(T)$ total calls. For $p=2$, the rate is $O(T^{-5/2})$ and the oracle complexity is $O(\epsilon^{-2/5})$ after normalizing $L_2D^2$. The accuracy exponent matches the lower bound cited in the paper, without a multiplicative logarithm.

The method uses an **inexact accelerated Halpern outer iteration**. A projected predictor approximates the next resolvent point, and an adaptive Anchored Tensor Method (ATM) solves each regularized subproblem. The warm-start and amortized analysis keep the total inner oracle cost at $O(T)$.

## Earlier short note and subsequent improvement

The same research line's [short note, arXiv:2608.08463](https://arxiv.org/abs/2608.08463) introduced ATM and a large-step inexact Halpern method. It obtained $\widetilde O(T^{-p})$ for general monotone VIs, including $\widetilde O(T^{-2})$ for $p=2$. This was an intermediate improvement over the older general-MVI rate $O(T^{-(p+1)/2})$, but it was **not** the final optimal result. The new accelerated Halpern method improves the exponent to $(3p-1)/2$ and removes the logarithmic factor in the stated oracle rate.

## AI use and provenance

The new paper's AI-usage statement attributes the short note's intermediate $\widetilde O(T^{-p})$ result to a search using Apex Intelligence's system after the authors posed the problem there. It says subsequent multi-round interactions with ChatGPT 6 Astra led to the accelerated Halpern outer loop and optimal rate. The paper dates the discovery to September 9, 2026 and links the [public discussion](https://chatgpt.com/share/6aae8bce-dc34-83ee-807b-dec17139119a). The short note's own account describes earlier proof-search work with Claude Opus 4.6 and GPT 5.6 Sol, followed by human verification and cleanup; a [shared discussion](https://chatgpt.com/share/6a6c372c-6efc-83e8-a378-c6aa1ea3b527) records part of that earlier process. These disclosures refer to different stages and are not interchangeable.

## References

- [Main paper: *Optimal High-Order Methods for Solving Monotone Variational Inequalities* (2026)](https://arxiv.org/abs/2609.23557)
- [Previous short note: *Halpern Iteration Achieves $\widetilde O(\epsilon^{-1/p})$ $p$th-Order Oracle Complexity for Monotone Variational Inequalities* (2026)](https://arxiv.org/abs/2608.08463)
- Project bibliography: [`references.bib`](references.bib)

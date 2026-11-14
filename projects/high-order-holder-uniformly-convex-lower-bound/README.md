# Tight lower bounds under matched high-order Hölder smoothness and uniform convexity

## Status and attribution

**Public preprint; AI use not stated in the paper.** Cedar Site Bai, [*Tight Lower Bounds under Matched High-Order Hölder Smoothness and Uniform Convexity*](https://arxiv.org/abs/2611.05527), 2026. The arXiv version inspected contains no AI-use declaration; this records absence of a disclosure, not evidence that AI was not used. This repository has not independently audited the proof.

## Problem and oracle model

Minimize a uniformly convex function $`f:\mathbb R^d\to\mathbb R`$ with initial gap $`f(x_0)-f^*=\Delta_0`$. Its $p$th derivative is Hölder continuous of degree $`\nu`$ with parameter $`H`$, and the uniform convexity degree is $`q`$ with parameter $`\sigma`$. The paper studies deterministic algorithms receiving derivatives through order $`p`$ and counts derivative-oracle calls needed to achieve $`f(x)-f^*\leq\epsilon`$.

## Matched-order lower bound

When $`q=p+\nu`$, the paper proves that every deterministic order-$p$ method needs

```math
\Omega\!\left(
\left(\frac{H}{\sigma}\right)^{\!2/[3(p+\nu)-2]}
\log\frac{\Delta_0}{\epsilon}
\right)
```

oracle calls. This matches the corresponding upper bound and resolves the matched-smoothness/uniform-convexity case left open by bounds for the two asymmetric regimes.

## Proof idea and scope

The construction uses multiple scales and phases to preserve earlier oracle replies while maintaining global Hölder smoothness and uniform convexity. It generalizes the classical first-order strongly-convex lower-bound phenomenon to matched high-order regularity. The result concerns deterministic algorithms in the specified derivative oracle model; no randomized lower bound is claimed here.

## Reference

- Cedar Site Bai, [*Tight Lower Bounds under Matched High-Order Hölder Smoothness and Uniform Convexity*](https://arxiv.org/abs/2611.05527), 2026.

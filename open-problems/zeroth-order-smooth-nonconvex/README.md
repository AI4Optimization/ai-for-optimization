# Tight lower bound for exact-value zeroth-order smooth nonconvex optimization

## Status

**Open; not solved by AI.** This question asks whether the classical first-order nonconvex lower bound can be strengthened by the dimension factor intrinsic to zeroth-order gradient recovery.

## Problem definition

Minimize a differentiable, possibly nonconvex function

$$
f:\mathbb R^d\to\mathbb R,
$$

assuming that $f$ is bounded below, its gradient is $L$-Lipschitz, and the initial point satisfies

$$
f(x_0)-\inf_x f(x)\leq\Delta.
$$

The algorithm must return a point $\widehat x$ satisfying

$$
\mathbb E\|\nabla f(\widehat x)\|\leq\epsilon
$$

or, equivalently up to the chosen success convention, $\|\nabla f(\widehat x)\|\leq\epsilon$ with constant probability.

## Oracle model

At each adaptively selected query $x_t\in\mathbb R^d$, an exact-value zeroth-order oracle returns only the scalar $f(x_t)$. It returns no gradient, directional derivative, comparison side information, or noisy auxiliary observation.

Algorithms may be adaptive and randomized, may perform unlimited computation between queries, and may choose the final output independently of the queried points. Complexity counts every scalar function evaluation, including evaluations used in finite differences, line searches, initialization, or stopping tests.

Because an exact real value can contain unbounded information, a valid lower bound must work directly in the exact-value model rather than appeal only to finite-precision or noisy-observation arguments.

## Known baseline

For smooth nonconvex optimization, standard first-order lower bounds give

$$
\Omega\!\left(\frac{L\Delta}{\epsilon^2}\right)
$$

gradient-oracle calls. Zeroth-order methods generally spend order $d$ function evaluations to reconstruct one gradient-scale direction, suggesting an additional dimension factor. However, multiplying a first-order lower bound by $d$ is not automatic because exact function values and adaptive queries define a different information model.

## Open target

Prove that every adaptive randomized exact-value zeroth-order algorithm requires

$$
\Omega\!\left(\frac{dL\Delta}{\epsilon^2}\right)
$$

function evaluations in an appropriate nontrivial parameter regime. Under the normalization $L=\Delta=1$, this is

$$
\Omega(d\epsilon^{-2}).
$$

The statement should specify the necessary relation among $d$, $L$, $\Delta$, and $\epsilon$, together with whether the guarantee is in expectation or with constant success probability.

## Relation to the smooth convex question

The sibling [smooth convex exact-value problem](../zeroth-order-smooth-convex/) asks for an $\Omega(d\epsilon^{-1/2})$ lower bound under convexity and a bounded domain. The present problem drops convexity, uses gradient-norm stationarity instead of objective suboptimality, and targets the characteristic $\epsilon^{-2}$ dependence of smooth nonconvex optimization.

## References

- [Carmon, Duchi, Hinder, and Sidford, *Lower Bounds for Finding Stationary Points I*](https://arxiv.org/abs/1710.11606)
- [Carmon, Duchi, Hinder, and Sidford, *Lower Bounds for Finding Stationary Points II: First-Order Methods*](https://arxiv.org/abs/1711.00841)
- [Related open problem: exact-value zeroth-order smooth convex optimization](../zeroth-order-smooth-convex/)

# Randomized matvec lower bounds for simplex-based matrix games

## Status and attribution

**Public preprint; author-disclosed AI assistance.** Wendao Wu and Cong Fang, [*Randomized Matvec Lower Bounds for Simplex-Based Matrix Games*](https://arxiv.org/abs/2610.02095v1), 2026.

The authors report that nearly the entire research pipeline was carried out by their internal Colombo auto-research system, powered by GPT-5.6 Sol, followed by author review and approval. They also report a Lean-backed article audit whose full report was not public in v1. This repository has checked the theorem-level statements and disclosure but has not independently audited the complete proof.

## Matrix-game geometries

For a matrix $`A\in\mathbb R^{m\times n}`$, consider

```math
\min_{x\in\mathcal X}\max_{y\in\mathcal Y} y^\top A x.
```

The paper treats two normalized geometries:

1. **Ball--simplex:** $`\mathcal X=\mathbb B_2^n`$, $`\mathcal Y=\Delta_m`$, and every row of $`A`$ has Euclidean norm at most one.
2. **Simplex--simplex:** $`\mathcal X=\Delta_n`$, $`\mathcal Y=\Delta_m`$, and $`|A_{ij}|\leq1`$.

The output is a feasible pair $`(x,y)`$ with full saddle-point gap at most $`\epsilon`$:

```math
\max_{y'\in\mathcal Y}(y')^\top A x
-\min_{x'\in\mathcal X}y^\top A x'
\leq\epsilon.
```

## Oracle and algorithm model

One query selects arbitrary real vectors and returns the two-sided products

```math
(Ax,A^\top y).
```

Algorithms may be adaptive and randomized and may output a feasible pair that was never queried. The guarantee must hold with probability at least $`2/3`$ for every admissible matrix. Complexity counts these joint two-sided matvec queries.

## Main lower bounds

For all sufficiently small $`\epsilon`$, the worst-case randomized query complexity is

```math
\Omega\!\left(
\frac{\epsilon^{-2/3}}
{\log^2(1/\epsilon)\,\log\log(1/\epsilon)}
\right)
```

for ball--simplex games, and

```math
\Omega\!\left(
\frac{\epsilon^{-2/3}}
{\log^{7/3}(1/\epsilon)\,\log\log(1/\epsilon)}
\right)
```

for simplex--simplex games. The hard dimensions are respectively of order

```math
\epsilon^{-2/3}
\qquad\text{and}\qquad
\frac{\epsilon^{-2/3}}{\log^{1/3}(1/\epsilon)},
```

and the lower bounds extend to larger dimensions. They match the deterministic upper bounds of Karmarkar, O'Carroll, and Sidford up to logarithmic factors.

## Proof architecture

The proof first establishes randomized linear-system hardness after adaptive two-sided matrix-vector queries. It conditions on the transcript, extracts a fresh Gaussian core, and uses uncertainty in its smallest singular value to prevent an accurate solve. Two reductions then convert small full saddle-point gap into small linear-system residual. The simplex--simplex reduction incurs an additional logarithmic normalization loss.

## Verification record

- [x] Both geometries, matrix normalizations, oracle response, and success criterion checked against arXiv v1.
- [x] Accuracy exponents, logarithmic losses, and hard dimensions checked.
- [x] AI-use disclosure recorded separately from proof verification.
- [ ] Complete proof and reported Lean audit independently checked.
- [ ] Independent human repository verifier recorded.

## References

- [Wu and Fang, arXiv:2610.02095v1](https://arxiv.org/abs/2610.02095v1)
- [PDF](https://arxiv.org/pdf/2610.02095v1)

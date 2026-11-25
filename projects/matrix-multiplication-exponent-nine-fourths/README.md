# The matrix multiplication exponent is nine fourths

## Status

**External public result; source-level summary.** This project records OpenAI's November 24, 2026 preprint, [*The matrix multiplication exponent is nine fourths*](https://github.com/openai/math/tree/main/preprints/The-matrix-multiplication-exponent-is-nine-fourths-November-24-2026). The theorem is attributed to its authors; this repository has not independently audited the proof.

## Result

For every field, the square matrix multiplication exponent is exactly

```math
\omega=\frac94.
```

The upper bound was known. The new lower bound proves that every formal arithmetic circuit multiplying two $n\times n$ matrices requires at least $n^{9/4}/2$ multiplication or division gates for each $n\ge2$. Together these results determine the asymptotic arithmetic complexity of square matrix multiplication over every field.

## Setting and assumptions

- **Problem class:** multiplying two square matrices of order $n$.
- **Algebraic setting:** every field.
- **Model:** formal arithmetic circuits; the stated lower bound counts multiplication or division gates.
- **Criterion:** the exponent $\omega$ is the infimum of exponents achievable with $O(n^{\omega+o(1)})$ arithmetic operations.
- **Result scope:** the new paper establishes the lower bound; it combines with the previously known matching upper bound.

## Why this matters for optimization

Many optimization algorithms reduce each iteration to dense linear algebra. For example, a Newton step solves

```math
\nabla^2 f(x_k)\,p_k=-\nabla f(x_k),
```

where the Hessian is a $d\times d$ matrix. Forming the Hessian, factoring it, and solving the system have costs governed by matrix multiplication and related linear algebra. Under standard algebraic reductions, a matrix multiplication algorithm with exponent $\omega$ yields dense matrix factorization and linear-system solution in $O(d^{\omega+o(1)})$ arithmetic operations. Thus the exponent $9/4$ gives the corresponding algebraic-operation benchmark for a dense exact Newton step, and for any method whose per-iteration cost is dominated by such a solve.

This is a per-iteration arithmetic-cost statement. It does not by itself bound the number of optimization iterations, improve a convergence rate, or imply that practical numerical Newton solvers attain the arithmetic-circuit exponent; conditioning, sparsity, finite precision, and data movement also matter.

## Proof architecture

The lower-bound proof argues that a matrix multiplication exponent below $9/4$ would compress tensor networks sufficiently to contradict a lower bound for testing whether entries in several independent lists are distinct. See the preprint for the full tensor-geometric and circuit-complexity argument.

## Verification record

- [x] The theorem's field-uniform scope, lower-bound gate count, and status of the upper bound were checked against the paper abstract.
- [ ] Full proof independently audited.
- [ ] Human verifier(s) recorded.

## Limitations and open questions

- This page records the result and its optimization relevance; it is not an independent proof audit.
- The exponent concerns asymptotic arithmetic operations, not bit complexity or wall-clock runtime.
- For Newton methods, it informs the dense linear-algebra cost per step, not the iteration complexity needed to reach a target accuracy.

## Provenance and references

- OpenAI, [*The matrix multiplication exponent is nine fourths*](https://github.com/openai/math/tree/main/preprints/The-matrix-multiplication-exponent-is-nine-fourths-November-24-2026), November 24, 2026.
- Earlier upper bound: [*An Upper Bound of 9/4 for the Matrix Multiplication Exponent*](https://github.com/openai/math/blob/main/preprints/Matrix-Multiplication-Nine-Fourths-October-2-2026/paper.pdf).
- Release overview: [OpenAI Math repository](https://github.com/openai/math).

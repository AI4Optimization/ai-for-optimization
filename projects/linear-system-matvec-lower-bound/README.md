# A simple complexity lower bound for solving linear systems

## Status and provenance

**Public preprint; AI-assisted proof, checked by the author.** Shamir (2026) gives a short, mostly self-contained proof of a previously known worst-case matrix-vector complexity lower bound. The note credits Dereziński, Epperly, and Meyer (2026) for the earlier, more general result and inspiration; it does not claim to discover the rate first.

The author discloses conversations with ChatGPT 5.6 Sol: both the author and AI contributed ideas, proof strategies, and drafts. Shamir reports thoroughly revising and checking the final write-up and taking responsibility for it. This repository has not independently audited the proof.

## Problem and oracle model

Given $b$ and an invertible matrix $A$ of condition number at most $\kappa$, find $x$ with relative residual

$$
\|Ax-b\|\leq\epsilon\|b\|.
$$

An adaptive, possibly randomized algorithm observes $b$ and can query a vector $v$, receiving $(Av,A^{\mathsf T}v)$. Computation between queries is unrestricted; complexity counts these joint matrix-vector oracle calls. The dimension is not fixed in advance and may grow with the query budget.

## Main lower bound

For $\kappa$ sufficiently large and $\epsilon$ sufficiently small, any algorithm succeeding with probability at least $2/3$ on every admissible instance requires

$$
T\geq c\kappa\log(1/\epsilon)
$$

queries for a universal constant $c>0$. The lower bound already holds for symmetric matrices with spectrum in $[-\kappa,-1]\cup[1,\kappa]$, even if the diagonal eigenvalue matrix is disclosed beforehand and the oracle additionally returns the query expressed in the hidden eigenbasis. The hard dimension can be of order $T^2$.

The proof combines polynomial approximation hardness with a random orthogonal embedding and Yao's principle to cover randomized algorithms.

## Quadratic-optimization consequence

Applying the result to strongly convex quadratics of the form $f(x)=\frac12\|Ax-b\|^2$ yields the classical randomized first-order lower bound

$$
\Omega\left(\sqrt\kappa\log(1/\epsilon)\right)
$$

for reducing objective error by a relative factor $\epsilon$, where $\kappa$ in this expression is the condition number of the quadratic Hessian. A value-and-gradient oracle call can be simulated using two matrix-vector products. This corollary is not presented as a new complexity rate.

## References

- Ohad Shamir, [*A Simple Complexity Lower Bound for Solving $Ax=b$*](https://arxiv.org/abs/2609.10874), 2026.
- Michał Dereziński, Ethan N. Epperly, and Raphael A. Meyer, *The Matrix-Vector Complexity of $Ax=b$*, COLT 2026, the earlier lower bound discussed in Shamir (2026).

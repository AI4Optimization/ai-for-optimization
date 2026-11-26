# Strongly polynomial-time linear programming

## Status

**External public preprint; author-provided Lean formalization for rational LP and companion geometry.** This entry records OpenAI's November 24, 2026 preprint, [*Strongly polynomial linear programming*](https://github.com/openai/math/blob/main/preprints/Strongly-polynomial-linear-programming-November-24-2026/paper.pdf), and its companion polytope-diameter result. The claims and formalizations are attributed to the authors. This repository has reviewed the published statements and formalization scope, but has not independently audited the proofs or rebuilt the Lean development.

## Result

The authors state a deterministic strongly polynomial-time algorithm for explicitly given linear programs with arbitrary real coefficients, answering Smale's ninth problem. The arithmetic step count is polynomial in the numbers of variables and constraints. For rational input, they additionally establish that every intermediate number has bit length polynomial in the full binary input length.

The same manuscript states a strongly polynomial algorithm for convex quadratic programming; see its [abstract](https://github.com/openai/math/blob/main/preprints/Strongly-polynomial-linear-programming-November-24-2026/build/abstract.tex) and [quadratic-programming section](https://github.com/openai/math/blob/main/preprints/Strongly-polynomial-linear-programming-November-24-2026/build/quadratic.tex). The [companion polytope-diameter paper](https://github.com/openai/math/blob/main/preprints/Superpolynomial-graph-diameter-of-simple-polytopes-November-24-2026/paper.pdf) states a refutation of the polynomial Hirsch conjecture for bounded simple rational polytopes, including superpolynomial distance bounds when moves may cross low-dimensional faces.

## Setting and assumptions

- **Problem class:** general linear programming; related convex quadratic programming and polytope-diameter results are recorded above.
- **Input:** an explicitly given LP with arbitrary real coefficients; rational input has an additional bit-length guarantee.
- **Algorithm:** deterministic arithmetic algorithm.
- **Arithmetic complexity:** step count polynomial in the numbers of variables and constraints, independent of coefficient bit length.
- **Rational bit complexity:** all intermediate numbers have bit length polynomial in the full input length. This guarantee depends on the input encoding length even though the arithmetic step count depends only on the dimensions.
- **LP output:** a strictly complementary optimal primal-dual pair, a feasible point with an improving ray, or a sparse infeasibility certificate, as stated in the [authors' release README](https://github.com/openai/math/blob/main/preprints/Strongly-polynomial-linear-programming-November-24-2026/README.md).

## Proof architecture

The preprint develops an algorithmic solution to the strongly polynomial LP problem. Its companion geometric result constructs bounded simple rational polytopes with superpolynomial graph diameter, including lower bounds for paths constrained to cross faces of subpolynomial dimension. The proof details are in the linked manuscripts.

## Author-provided Lean formalization

The authors' [formalization scope](https://github.com/openai/math/blob/main/lean/docs/380.md) records:

- **Rational LP:** fixed rational RAM programs for feasibility and optimization of $Ax\leq b$, with at least one constraint and one variable. Instruction counts are polynomial in the sum of these dimensions, and stored rationals have bit length polynomial in the input bit length.
- **Certificates:** feasibility returns a feasible point or a sparse Farkas certificate. Optimization returns an infeasibility certificate, primal and dual optima of equal value, or a feasible point and an improving ray. The equal-value certificate is the finite-optimum guarantee stated for the formalization.
- **Companion geometry:** the polynomial Hirsch refutation for simple rational polytopes, superpolynomial distance bounds allowing moves across low-dimensional faces, and separation of vertices with a prescribed objective gap.

These are the documented formalization claims. The arbitrary-real LP statement and convex-QP extension should be assessed separately from this rational-LP scope. Reviewing this scope document is distinct from independently checking the formal statements or running Lean.

## Verification record

- [x] The LP arithmetic bound, rational intermediate bit-length guarantee, and output alternatives were checked against the authors' release README.
- [x] The convex-QP claim was checked against the manuscript abstract and quadratic-programming section.
- [x] The rational-RAM LP and companion geometric formalization scopes were checked against the authors' scope document.
- [ ] Lean development rebuilt and checked locally.
- [ ] Full theorem statements, hypotheses, and proof details independently audited.
- [ ] Human verifier(s) recorded.

## Limitations and open questions

- This project page is a bibliographic and scope record, not an independent proof audit.
- The real-coefficient arithmetic model and rational-input bit-length guarantee are distinct parts of the authors' claim.
- The published formalization scope specifies rational LP and companion geometric results; it does not establish that every claim in the manuscripts has been formalized.

## Provenance and references

- OpenAI, [*Strongly polynomial linear programming*](https://github.com/openai/math/blob/main/preprints/Strongly-polynomial-linear-programming-November-24-2026/paper.pdf), November 24, 2026.
- [Authors' release README](https://github.com/openai/math/blob/main/preprints/Strongly-polynomial-linear-programming-November-24-2026/README.md), including the rational-input guarantee and links to feasibility and optimization proofs.
- [Lean formalization scope for LP and polytope diameter](https://github.com/openai/math/blob/main/lean/docs/380.md).
- Related: [*Superpolynomial graph diameter of simple polytopes*](https://github.com/openai/math/blob/main/preprints/Superpolynomial-graph-diameter-of-simple-polytopes-November-24-2026/paper.pdf).
- Release overview: [OpenAI Math repository](https://github.com/openai/math).

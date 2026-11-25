# Strongly polynomial-time linear programming

## Status

**External public result; source-level summary.** This entry records OpenAI's November 24, 2026 preprint, [*Strongly polynomial linear programming*](https://github.com/openai/math/blob/main/preprints/Strongly-polynomial-linear-programming-November-24-2026/paper.pdf). The result is attributed to the paper's authors. This repository has not independently audited its proof.

## Result

The paper gives a deterministic strongly polynomial-time algorithm for linear programming with arbitrary real coefficients. The number of algorithmic steps is polynomial in the numbers of variables and constraints, rather than depending polynomially on coefficient bit length. This answers Smale's ninth problem. The accompanying work on polytope diameters also refutes the polynomial Hirsch conjecture for bounded simple rational polytopes and strengthens the obstruction for moves across low-dimensional faces.

## Setting and assumptions

- **Problem class:** general linear programming.
- **Input:** an LP with arbitrary real coefficients.
- **Algorithm:** deterministic arithmetic algorithm.
- **Complexity measure:** strongly polynomial step count, polynomial in the number of variables and constraints.
- **Scope note:** the theorem concerns step complexity; it does not claim that all intermediate numbers have polynomial bit length.

## Proof architecture

The preprint develops an algorithmic solution to the strongly polynomial LP problem. Its companion geometric result constructs bounded simple rational polytopes with superpolynomial graph diameter, including lower bounds for paths constrained to cross faces of subpolynomial dimension. The proof details are in the linked manuscripts.

## Verification record

- [x] The high-level result and stated scope were checked against the authors' repository overview and release history.
- [ ] Full theorem statements, hypotheses, and proof details independently audited.
- [ ] Human verifier(s) recorded.

## Limitations and open questions

- This project page is a bibliographic and scope record, not an independent proof audit.
- The result's strongly polynomial step bound does not imply polynomial bit complexity for every exact intermediate quantity.

## Provenance and references

- OpenAI, [*Strongly polynomial linear programming*](https://github.com/openai/math/blob/main/preprints/Strongly-polynomial-linear-programming-November-24-2026/paper.pdf), November 24, 2026.
- Related: [*Superpolynomial graph diameter of simple polytopes*](https://github.com/openai/math/blob/main/preprints/Superpolynomial-graph-diameter-of-simple-polytopes-November-24-2026/paper.pdf).
- Release overview: [OpenAI Math repository](https://github.com/openai/math).

# Optimal deterministic oracle complexity for weakly convex optimization

## Status

**Public preprint; human-verified and formally verified in Lean.** The hard instance was developed through iterative collaboration with GPT-5.6 Sol. The authors report independently checking the argument and taking responsibility for the paper; an accompanying Codex-assisted Lean development formalizes the deterministic lower bound.

## Result

Let $\mathcal F(G,\rho,\Delta)$ be the class of globally $G$-Lipschitz, $\rho$-weakly convex functions $f:\mathbb R^d\to\mathbb R$ satisfying $f(0)-\inf f\leq\Delta$. For sufficiently small $\epsilon$, every deterministic first-order algorithm requires

$$
\Omega\!\left(
\frac{G^2\min\{\rho\Delta,G^2\}}{\epsilon^4}
\right)
$$

oracle calls to find $x$ with $\|\nabla f_{1/(2\rho)}(x)\|\leq\epsilon$. In the small-gap regime $\Delta\leq G^2/\rho$, this becomes

$$
\Omega\!\left(\frac{\rho G^2\Delta}{\epsilon^4}\right),
$$

matching the best deterministic and stochastic first-order upper bounds up to universal constants.

## Setting and assumptions

- **Problem class:** unconstrained minimization of a possibly nonsmooth, globally $G$-Lipschitz, $\rho$-weakly convex function.
- **Initialization:** $x^0=0$ and $f(0)-\inf f\leq\Delta$.
- **Stationarity:** $\|\nabla f_{1/(2\rho)}(x)\|\leq\epsilon$, where $f_{1/(2\rho)}$ is the Moreau envelope.
- **Oracle model:** each query returns the pair $(f(x),\partial f(x))$, including the entire subdifferential set rather than an oracle-selected subgradient.
- **Algorithm class:** arbitrary deterministic adaptive first-order algorithms; the final output may be any deterministic function of the transcript.
- **Accuracy regime:** $\epsilon^2\leq c_0\min\{G^2,\rho\Delta\}$ for a universal constant $c_0>0$.

## Proof architecture

1. Construct a tilted max-affine convex block with a setwise zero-chain property, so even the full subdifferential reveals only the next hidden direction.
2. Couple $M=\Theta(\rho\Delta/\epsilon^2)$ overlapping blocks of length $N=\Theta(G^2/\epsilon^2)$ through a weakly convex relay.
3. Use a diagonal filtration to control interleaved information propagation despite overlap; each query exposes only constantly many new directions.
4. Prove Moreau-envelope stationarity is bounded away from zero throughout the reachable subspace for $\Omega(MN)$ queries.
5. Scale the unnormalized construction to $(G,\rho,\Delta,\epsilon)$ and apply a finite-horizon adversarial rotation to extend the zero-respecting lower bound to all deterministic algorithms.

## Verification record

- [x] The theorem statement and parameter regime are checked against the public preprint.
- [x] The full-subdifferential oracle and Moreau-envelope criterion are explicitly stated.
- [x] The authors report independent human verification.
- [x] An accompanying Lean repository formally verifies the deterministic first-order lower bound.
- [x] The small-gap result matches the known $O(\rho G^2\Delta/\epsilon^4)$ dependence.

## Limitations and open questions

- The lower bound applies to deterministic algorithms; extending it to randomized algorithms remains open.
- In the large-gap regime the bound saturates at $\Omega(G^4/\epsilon^4)$.
- The oracle returns the complete subdifferential. Comparisons with weaker subgradient-selection oracles must preserve this distinction.

## Provenance and references

- **Clean write-up:** Jiajin Li and Siyu Pan, [*Optimal Deterministic Oracle Complexity for Weakly Convex Optimization*](https://arxiv.org/abs/2608.03246v1), 2026.
- **Formal verification:** [Weakly-Convex-Lower-Bound-Lean](https://github.com/SiyuPan04/Weakly-Convex-Lower-Bound-Lean).
- **AI systems used:** GPT-5.6 Sol for the hard-instance development and Codex for the Lean formalization, as reported by the authors.

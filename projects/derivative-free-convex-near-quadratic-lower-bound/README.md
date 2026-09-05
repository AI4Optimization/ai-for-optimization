# Near-quadratic lower bound for derivative-free convex optimization

## Status

**Public preprint; human-verified.** The author reports that the mathematical arguments were developed with GPT 5.6 Sol Pro and subsequently verified by the author. The initial $\widetilde\Omega(d^2)$ proof at a smaller accuracy was also formally verified in Lean; the final $\Theta(d^{-1/2})$-accuracy theorem has not been fully formalized.

## Result

Let $Q_{\mathrm{val}}^{\det}(d,R,L,\epsilon)$ denote the worst-case number of exact function-value queries needed by a deterministic algorithm to minimize a convex $L$-Lipschitz function on the Euclidean ball $B_d(R)$ to objective error at most $\epsilon$. There are universal constants $c,\epsilon_0>0$ and $d_0\in\mathbb N$ such that, for every $d\geq d_0$,

$$
Q_{\mathrm{val}}^{\det}\!\left(d,R,L,\frac{\epsilon_0LR}{\sqrt d}\right)
\geq c\frac{d^2}{\log(d+1)}.
$$

Together with Protasov's exact-value upper bound, this gives

$$
Q_{\mathrm{val}}^{\det}\!\left(d,\frac{\epsilon_0}{\sqrt d}\right)
=\widetilde\Theta(d^2),
$$

closing a polynomial oracle-complexity gap dating to 1996. A mixed-integer lifting gives $\widetilde\Theta(2^n d^2)$ queries for $n$ binary and $d$ continuous variables under the paper's fiberwise Lipschitz assumptions.

## Setting and assumptions

- **Problem class:** minimize $f\in\mathcal F_d(R,L)$, where $f:B_d(R)\to\mathbb R$ is convex, $L$-Lipschitz in Euclidean norm, and normalized by $f(0)=0$.
- **Domain:** $B_d(R)=\{x\in\mathbb R^d:\|x\|_2\leq R\}$.
- **Regularity:** no differentiability, smoothness, strict convexity, strong convexity, polyhedrality, or finite representation is assumed.
- **Oracle model:** a deterministic algorithm adaptively queries $x_t\in B_d(R)$ and receives only the exact real value $f(x_t)$. It receives no gradient, subgradient, separating hyperplane, comparison bit, or stochastic estimate.
- **Algorithm class:** unrestricted deterministic sequential algorithms with unlimited computation, memory, and exact real arithmetic; query and output maps may be discontinuous.
- **Output criterion:** return any $\widehat x\in B_d(R)$ satisfying $f(\widehat x)-\min_{x\in B_d(R)}f(x)\leq\epsilon$ for every admissible objective.
- **Cost convention:** every function evaluation counts, including repeated, batched, line-search, rejected, initialization, and stopping-test evaluations.

## Proof architecture

1. Split $d=2m$ coordinates as $(x,z)$ and use the max-affine hard family
   $$
   f_W(x,z)=\max_{i\in[m]}\{a x_i+\langle w_i,z\rangle\},
   $$
   with each unknown row $w_i$ in a small Euclidean ball.
2. Build an exact resisting oracle that maintains a compact convex uncertainty set for every row while preserving the complete value transcript.
3. Show that fewer than order $m^2/\log m$ queries leave linearly many row sets high-dimensional and with large volume radius.
4. Use Urysohn's inequality and averaging to find a common direction of large aggregate width.
5. Move the surviving rows to opposite extremes to construct two transcript-indistinguishable objectives whose minimizers are separated. A support-function growth inequality then forces objective error $\Omega(d^{-1/2})$ for the common output.
6. Apply a transfer theorem, together with binning, flooring, and radial extension, to obtain the mixed-integer lower bound.

## Verification record

- [x] The theorem statement, normalization, scaling, and oracle model appear in the public preprint.
- [x] The author reports human verification and takes responsibility for the manuscript.
- [x] The initial AI-generated $\widetilde\Omega(d^2)$ proof at accuracy of order $d^{-3}$ was formally verified in Lean.
- [ ] The final improvement to accuracy of order $d^{-1/2}$ has not been fully formalized in Lean.
- [x] The comparison with the classical $O(d^2\log(d+1)\log(LR/\epsilon))$ exact-value upper bound is recorded in the preprint.

## Limitations and open questions

- The lower bound is for deterministic algorithms; it does not establish the same result for randomized exact-value methods.
- The theorem fixes a sufficiently small universal constant multiple of $LR/\sqrt d$, rather than every constant multiple.
- The objectives may be nonsmooth. Smooth exact-value zeroth-order convex optimization remains a separate open problem.
- The final accuracy refinement relies on convex-geometric ingredients that are not included in the current Lean formalization.

## Provenance and references

- **Initial AI trace:** [ChatGPT share](https://chatgpt.com/share/6a55aa50-b484-83ea-85c0-c7e7b4bda41c), producing the initial near-quadratic proof at a smaller accuracy.
- **Accuracy-refinement trace:** [ChatGPT share](https://chatgpt.com/share/6a55ad10-7644-83ea-859e-5483d2e0dff0), recorded in Appendix A of the preprint.
- **Clean write-up:** Phillip Kerger, [*Closing the Oracle-Complexity Gap in Derivative-Free Convex Optimization: A Near-Quadratic Lower Bound from Exact Function Values*](https://arxiv.org/abs/2607.13335), 2026.
- **Formal verification:** [zero-order-bounds-lean-verification](https://github.com/PhillipKerger/zero-order-bounds-lean-verification).
- **Prior upper bound:** V. Yu. Protasov, *Algorithms for approximate calculation of the minimum of a convex function from its values*, Mathematical Notes 59 (1996), 69--74.
- **AI system used:** GPT 5.6 Sol Pro, as reported by the author.

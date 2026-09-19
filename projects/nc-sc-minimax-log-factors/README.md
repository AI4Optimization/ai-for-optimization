# NC-SC minimax complexity without multiplicative logarithms

## Status

**Verified draft; not yet cleaned up.** The available proof is a research discussion rather than a publication-ready manuscript. The source discussion should remain the authority until a clean proof is added here.

## AI use

ChatGPT was used as a proof-search and synthesis system in the [linked research discussion](https://chatgpt.com/share/6a93a36e-05d4-83ee-9116-ef55c43f95d6). It compared the known NC-SC upper and lower bounds, proposed the FOAM-compatible potential, worked out its center-change inequality, and assembled the warm-started inner contraction with the outer descent argument. Human researchers subsequently checked the resulting argument; the names and division of verification work have not yet been recorded in this repository. The exact ChatGPT model used in the shared trace is also not recorded, so no model name is inferred here.

The AI trace is retained as provenance, not as the canonical long-term proof. A clean manuscript still needs to restate and independently check every imported FOAM lemma, constant, and oracle-accounting step.

## Previous best results

- Lin, Jin, and Jordan's [*Near-Optimal Algorithms for Minimax Optimization*](https://arxiv.org/abs/2002.02417) gives, in Appendix Theorem A.7, a deterministic first-order NC-SC guarantee with leading dependence $\sqrt\kappa L\Delta/\epsilon^2$ multiplied by accuracy- and parameter-dependent logarithmic factors (a squared logarithm in that statement).
- Zhang, Yang, Guzmán, Kiyavash, and He's [*The Complexity of Nonconvex-Strongly-Concave Minimax Optimization*](https://arxiv.org/abs/2103.15888) establishes the lower bound
  $$
  \Omega\!\left(\frac{\sqrt\kappa L\Delta}{\epsilon^2}\right)
  $$
  under its stated algorithmic restrictions and gives a nearly matching upper bound. Its warm-start/relative-accuracy analysis removes the earlier repeated polylogarithmic dependence on $1/\epsilon$, but parameter-dependent logarithmic factors remain.
- The strongly-convex-strongly-concave subproblems are solved using ideas from Kovalev and Gasnikov's [*The First Optimal Algorithm for Smooth and Strongly-Convex-Strongly-Concave Minimax Optimization*](https://proceedings.neurips.cc/paper_files/paper/2022/hash/5e2ed801f62102f531d109d7c6e1b62f-Abstract-Conference.html), referred to as FOAM in the proof discussion.

Thus, before the present argument, the optimal polynomial main term was known, and the lower bound had no multiplicative logarithm, but the available general deterministic upper bounds still carried logarithmic overhead.

## Current result

Consider

$$
\Phi(x)=\max_{y\in Y} f(x,y), \qquad \kappa=\frac{L}{\mu},
$$

where $f$ is jointly $L$-smooth, is $\mu$-strongly concave in $y$, and is nonconvex in $x$. Let $\Delta=\Phi(x_0)-\inf_x\Phi(x)$.

The verified draft gives a deterministic first-order method whose dominant complexity for finding $\widehat x$ with

$$
\mathbb E\|\nabla\Phi(\widehat x)\|^2\le \epsilon^2
$$

is

$$
O\!\left(\frac{\sqrt\kappa\,L\Delta}{\epsilon^2}\right),
$$

with no logarithm multiplying the $\epsilon^{-2}$ term. The complete bound in the source discussion also contains one-time initialization and final-refinement costs of the form

$$
O\!\left(
\sqrt\kappa\log(2+\kappa)
+\sqrt\kappa\log\!\left(1+\frac{B_0}{\Delta}\right)
\right),
$$

where $B_0$ is an explicit, gradient-computable initialization bound defined in the source proof.

This matches the known lower-bound main term up to the precise restrictions of the relevant lower-bound model. It does **not** establish a uniformly log-free bound in every parameter regime.

## Proof architecture

The argument uses four ingredients:

1. regularize each outer subproblem into a strongly-convex-strongly-concave saddle problem;
2. track a FOAM-compatible potential that controls primal and dual errors without introducing an additional power of $\kappa$ when the proximal center moves;
3. warm-start a constant-factor inner contraction and absorb its error into a joint outer potential;
4. perform a single final refinement to convert Moreau-envelope stationarity into stationarity of $\Phi$.

The amortized outer analysis removes the logarithm from the leading $\sqrt\kappa L\Delta/\epsilon^2$ term. The remaining $\sqrt\kappa\log(2+\kappa)$ comes from the final stationarity-recovery step, and the other logarithm is an initialization cost.

## Important limitations

- The current proof does not eliminate every additive logarithmic term.
- The final conversion from an approximate proximal point to $\nabla\Phi$ stationarity still requires shrinking the tracked error by a $\kappa$-dependent factor.
- Lower-bound comparisons must retain the algorithm-class restrictions in the cited lower-bound papers.
- Constants, edge cases, and all FOAM lemma mappings should be restated carefully in the cleaned manuscript.

## Subsequent single-loop NC--SC result (Zhang and Xu, 2026)

[Zhang and Xu, arXiv:2609.17973](https://arxiv.org/abs/2609.17973) also study the **nonconvex--strongly-concave (NC--SC)** setting. Their single-loop projected damped-extragradient scheme, preceded by a fixed-center warm start, allows a closed convex primal domain and a compact convex dual domain. For a jointly $L$-smooth objective that is $\mu$-strongly concave in $y$, their Theorems 4.2--4.3 and Corollary 4.2 give both optimization-stationarity and game-stationarity guarantees. Writing $\kappa=L/\mu$ and $\Delta_\phi=\phi(x_0)-\inf\phi$, the warm-started oracle bound is

$$
O\!\left(\sqrt\kappa\left[\frac{L\Delta_\phi}{\epsilon^2}+1+\log\!\left(1+\frac{L\bar H_\mu}{\epsilon^2}\right)\right]\right),
$$

where $\bar H_\mu$ is the initialization quantity defined in their paper. The main $\epsilon^{-2}$ term has no multiplicative logarithm. Their optimization-stationarity output satisfies $\mathbb E\|\nabla\phi_{2L}(z_{\mathrm{out}})\|^2\leq\epsilon^2$ for a Moreau-envelope stationarity measure; a different output rule gives a game-stationarity residual at most $\epsilon$.

This is an independently published NC--SC result, not a write-up of the AI-assisted draft above. In particular, Moreau-envelope stationarity and the draft's $\nabla\Phi$ stationarity are different output criteria; their bounds should not be identified without an additional conversion argument. The separate [SC--SC single-loop project](../sc-sc-single-loop-extragradient/) records Zhang and Xu's other paper, arXiv:2609.20327.

## Next cleanup steps

- [ ] Transcribe the theorem and algorithm with stable notation.
- [ ] State the definition of $B_0$ and the initialization routine precisely.
- [ ] Isolate and prove the center-change lemma for the tracked potential.
- [ ] Map the transformed variables and output iterates to the exact FOAM theorem/lemmas.
- [ ] Compare the draft's $\nabla\Phi$ output criterion carefully with the Moreau-envelope and game-stationarity guarantees in arXiv:2609.17973.
- [ ] Audit constants in the joint-potential descent.
- [ ] Add complete bibliographic entries and exact lower-bound qualifications.
- [ ] Record the names and scope of the human verification.

## Provenance

- [Original AI-assisted proof discussion](https://chatgpt.com/share/6a93a36e-05d4-83ee-9116-ef55c43f95d6)
- Starting point: Lin, Jin, and Jordan, [*Near-Optimal Algorithms for Minimax Optimization*](https://arxiv.org/abs/2002.02417)
- Subsequent NC--SC single-loop result: Minghao Zhang and Zi Xu, [*Matching Multi-Loop Complexities with a Single Loop*](https://arxiv.org/abs/2609.17973), 2026.
- Project bibliography: [`references.bib`](references.bib)

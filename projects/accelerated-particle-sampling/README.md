# High-accuracy sampling with bouncy particle and Zigzag methods

## Status and attribution

**Public preprints; concurrent sampling work with distinct AI disclosures.** This project records:

- Fan Chen, Sinho Chewi, Jianfeng Lu, and Matthew S. Zhang, [*Accelerated High-Accuracy Sampling from a Warm Start via the Proximal Bouncy Particle Sampler*](https://arxiv.org/abs/2609.06905v1), v1, 2026-09-07.
- Jianfeng Lu and Yinchen Luo, [*Windowed thinning and query complexity for the bouncy particle and Zigzag samplers*](https://arxiv.org/abs/2607.28413v2), first submitted 2026-07-30; reviewed version v2, 2026-09-01.

Proximal BPS cites Lu and Luo's work. The papers are recorded together as related concurrent results, with separate attribution, initialization assumptions, and oracle costs. This repository has not independently audited either complete proof. These sampling results do not resolve a currently listed optimization benchmark question.

## Common setting and solution criterion

Sample from a strongly log-concave target on all of $`\mathbb R^d`$:

```math
\mu(dx)=Z^{-1}e^{-V(x)}dx,\qquad
V\in C^2(\mathbb R^d),\qquad
0<\alpha\leq\beta,\qquad
\alpha I\preceq\nabla^2V(x)\preceq\beta I,\qquad
\kappa=\beta/\alpha.
```

Lu and Luo use $`U,m,L`$ in place of $`V,\alpha,\beta`$. The output is a sample whose position law has total-variation distance at most $`\epsilon`$ from $`\mu`$. Query bounds below are **expectations**, not worst-case budgets or high-probability query bounds.

## Reported bounds and oracle costs

Let $`B_\epsilon=d\log\kappa+\log(1/\epsilon)`$ for the windowed-thinning rows.

| Method | Initialization | Expected query bound | Unit |
| --- | --- | --- | --- |
| Proximal BPS; Corollary 4.4 | Supplied order-2 Renyi warm start, $`D_2=O(1)`$ | $`\widetilde O(\sqrt\kappa\,d^{1/4})`$ | Full gradient |
| Windowed BPS; Theorem 3 | Gaussian cold start centered at the known minimizer | $`O(\sqrt\kappa\,dB_\epsilon)`$ | Full gradient |
| Windowed Zigzag; Theorem 4 | Same Gaussian cold start | $`O(\kappa d^{5/4}B_\epsilon)`$ | Coordinate partial derivative |

**Proximal BPS.** For $`\Delta_2\geq1`$, $`D_2(\mu_0\|\mu)\leq\Delta_2`$, and $`0<\epsilon<1/4`$, Corollary 4.4 gives the explicit bound, with absolute constants $`K,c>0`$,

```math
\mathcal L=\Delta_2+\log\frac{Kd\kappa}{\epsilon},\qquad
\eta=\frac{c}{\beta(\sqrt{d\mathcal L}+\mathcal L)},
```

```math
\mathbb E N_{\nabla V}
\leq K\sqrt\kappa\,(d+\mathcal L)^{1/4}\mathcal L^{3/4}
\left(\Delta_2+\log\frac4\epsilon\right)\log(\kappa\mathcal L).
```

Here $`D_2(\nu\|\mu)=\log(1+\chi^2(\nu\|\mu))`$. The displayed $`\widetilde O`$ rate assumes $`\Delta_2=O(1)`$ and hides only logarithms in $`d,\kappa,1/\epsilon`$. Theorem 4.3 and Algorithm 4.2 count all gradient calls for approximate proximal solves, conditional sampling, and event simulation. No function-value, exact proximal, or free restricted-Gaussian oracle is assumed. Producing the warm start is outside this bound. [Manuscript, Sections 4.1--4.3](https://arxiv.org/pdf/2609.06905v1).

**Windowed thinning.** Theorems 3--4 assume known $`m,L,x^\star`$ and start the joint position--velocity process from

```math
\rho_0=\mathcal N(x^\star,L^{-1}I)\otimes\mathcal N(0,I),\qquad
\rho_\infty=\mu\otimes\mathcal N(0,I).
```

For $`0<\epsilon<1/2`$, they give $`\chi^2(\rho_T\|\rho_\infty)\leq4\epsilon^2`$, hence joint and position total-variation error at most $`\epsilon`$. Simulation is exact; accuracy determines the time horizon. BPS uses window length $`(Ld)^{-1/2}`$ and refresh rate $`\sqrt{dm}`$; Zigzag uses $`L^{-1/2}d^{-1/4}`$ and $`\sqrt L`$.

The cost includes anchor gradients and candidate-event queries. For Zigzag, $`d`$ coordinate queries count as one full-gradient equivalent, giving

```math
Q_{\mathrm{eq}}=Q_\partial/d
=O\!\left(\kappa d^{1/4}
\left[d\log\kappa+\log\frac1\epsilon\right]\right).
```

This conversion is an oracle convention, not a wall-clock guarantee; direct Zigzag implementation also costs $`O(d)`$ arithmetic per proposal. The cold-start $`d\log\kappa`$ factor must remain visible. [Manuscript, Theorems 3--4 and Section 3.3](https://arxiv.org/pdf/2607.28413v2).

## Proof architecture and limitations

- Proximal BPS combines auxiliary reflection, conditional half-turn particle motion, and occasional resampling. Discrete hypocoercivity controls convergence; conditional sampling and capped event rates control implementation error.
- Windowed thinning uses anchor gradients and smoothness to bound local event rates, then combines exact thinning, continuous-time mixing, and expected event counts.

The warm-start and cold-start rates are not directly comparable end-to-end. Lu and Luo's general mixing estimates accept finite initial chi-squared divergence, but their stated query theorems use the specific Gaussian cold start. Finding its center $`x^\star`$ is not charged. Neither work establishes matching minimax complexity, and neither expected-cost result should be relabeled as a high-probability cost guarantee.

## AI provenance and verification record

Chen, Chewi, Lu, and Zhang disclose GPT-5.6 Sol assistance in discovering the algorithm and original analysis; the authors then reformulated the argument and wrote the manuscript (AI usage, p. 4).

Lu and Luo attribute the design and analysis approach to themselves, and disclose LLM assistance for drafting, editing, and consistency checks. They also report learning of a separate ChatGPT Pro 5.6 BPS result with a stronger high-probability guarantee, which they exclude from their manuscript (Use of AI tools, p. 5). That disclosure does not upgrade their reported expected-cost theorem.

- [x] On 2026-10-02, checked both accessible PDFs, version dates, main theorem statements, initialization assumptions, oracle units, accuracy metrics, and AI disclosures.
- [x] Distinguished supplied warm-start cost from Gaussian cold-start cost and coordinate queries from full-gradient equivalents.
- [ ] Independent lemma-by-lemma proof audit, including imported mixing results and implementation error bounds.
- [ ] Independent human repository verifier(s); none recorded.
- [ ] Public prompts or original AI traces; no stable trace link recorded here.

The authors retain responsibility for their manuscripts; their disclosures are not independent repository verification or a formal proof audit.

## References

- [Proximal BPS v1 PDF](https://arxiv.org/pdf/2609.06905v1) and [HTML](https://arxiv.org/html/2609.06905v1).
- [Windowed thinning v2 PDF](https://arxiv.org/pdf/2607.28413v2).
- [references.bib](references.bib).

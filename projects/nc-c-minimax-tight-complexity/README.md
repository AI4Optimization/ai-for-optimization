# Tight complexity for nonconvex--concave minimax optimization

## Status

**Public preprints; AI-assisted; author-reported human verification and Lean formalizations.** This project records two works submitted to arXiv on September 13, 2026:

- **Pan, Zheng, and Li (PZL):** [arXiv:2609.14235v1](https://arxiv.org/abs/2609.14235v1), matching deterministic lower and upper bounds without logarithmic factors.
- **Wu, Gu, and Yang (WGY):** [arXiv:2609.14233v1](https://arxiv.org/abs/2609.14233v1), deterministic and stochastic lower bounds for zero-respecting methods.

PZL resolves the repository's [unconstrained-primal NC--C open problem](../../open-problems/nonconvex-concave-minimax/). WGY gives a complementary result with a constrained primal domain and a narrower algorithm class. This repository has not independently audited every proof or rebuilt the Lean developments.

## Result

Use $L$ for joint smoothness, $D_{\mathcal Y}$ for the dual-diameter bound, and $\Delta$ for the initial primal value gap. These correspond to $\ell,D_{\mathcal Y},\Delta$ in PZL and $L,D_{\mathcal Y},\Delta_\Phi$ in WGY.

### Optimal deterministic complexity

PZL, Theorem 3.2: there exist universal constants $c_0,c_1>0$ such that, for every $L,D_{\mathcal Y},\Delta>0$ and

$$
0<\epsilon\leq c_0\min\{LD_{\mathcal Y},\sqrt{L\Delta}\},
$$

every deterministic adaptive first-order method has a finite-dimensional instance requiring at least

$$
c_1\frac{L^2D_{\mathcal Y}\Delta}{\epsilon^3}
$$

joint oracle calls in the worst case to return an $\epsilon$-optimization-stationary point. The hard instance has an unconstrained primal domain and a dual Euclidean ball. Theorem 3.1 first proves the zero-respecting case; Theorem 3.2 extends it to arbitrary deterministic methods. Remark 3.1 covers an arbitrary deterministic output computed from the transcript by appending one query.

PZL, Theorem 3.3: for every $L,D_{\mathcal Y},\Delta>0$, every admissible instance, and every $\epsilon>0$, **Tracked-FOAM** returns such a point using

$$
O\!\left(
\left(\frac{L\Delta}{\epsilon^2}+1\right)
\max\left\{1,\frac{LD_{\mathcal Y}}{\epsilon}\right\}
\right)
$$

calls. Thus the optimal complexity in the lower-bound regime is $\Theta(L^2D_{\mathcal Y}\Delta/\epsilon^3)$. These bounds hide only universal constants, with no logarithmic, dimension, or additional initialization factors.

For comparison, Lin, Jin, and Jordan's Minimax-PPA has a $\widetilde O(\epsilon^{-3})$ guarantee for this envelope criterion, and PZL reports that Perturbed Smoothed FOAM improves the earlier squared logarithm to a single logarithm. These accuracy-only comparisons fix all other parameters. Tracked-FOAM removes the remaining logarithmic overhead.

### Deterministic and stochastic zero-respecting lower bounds

WGY, Theorem 4.1, proves $\Omega(L^2D_{\mathcal Y}\Delta/\epsilon^3)$ for deterministic zero-respecting algorithms in the same accuracy regime, with its own universal constants. Zero-respecting methods can activate only coordinates revealed by previous gradient responses, subject to the allowed projections.

WGY, Theorem 5.5, states that there exist universal constants $c_0,c_d,c_n>0$ such that, for every $L,D_{\mathcal Y},\Delta>0$, $\sigma\geq0$, and $0<\epsilon\leq c_0\min\{LD_{\mathcal Y},\sqrt{L\Delta}\}$, an admissible instance and unbiased stochastic oracle of variance at most $\sigma^2$ force every adaptive stochastic zero-respecting method to use at least

$$
c_d\frac{L^2D_{\mathcal Y}\Delta}{\epsilon^3}
+c_n\frac{L^3D_{\mathcal Y}^2\Delta\sigma^2}{\epsilon^6}
$$

calls to return a point satisfying expected envelope-gradient norm at most $\epsilon$. The deterministic term remains when $\sigma=0$. Corollaries 4.2 and 5.6 replace $\Delta$ by a budget $\mathcal G_0$ on $\max_y f(0,y)-\inf_x f(x,0)$; the two gaps agree on their hard instances. These results use constrained auxiliary primal variables and impose zero-respecting behavior on both queries and final outputs.

WGY compares the noise-dominated $\epsilon^{-6}$ rate with SAPD+ (Zhang, Aybat, and Gürbüzbalaban, 2022). That comparison uses a primal-dual-gap budget and a bounded-variance oracle; it does not supply a stochastic upper bound for unrestricted primal-value-gap instances.

## Setting and assumptions

- **Problem class:** $\min_{x\in\mathcal X}\max_{y\in\mathcal Y}f(x,y)$, jointly $L$-smooth on $\mathcal X\times\mathcal Y$, with $f(x,\cdot)$ concave and no convexity assumption in $x$. No fixed positive dual strong-concavity modulus is assumed.
- **Domains:** nonempty closed convex $\mathcal X$ and compact convex $\mathcal Y$, containing the origin, with $\operatorname{diam}(\mathcal Y)\leq D_{\mathcal Y}$. PZL's lower bound already holds for $\mathcal X=\mathbb R^{d_x}$; its upper bound allows general such $\mathcal X$. WGY uses a product of an unconstrained state space and a ball constraining auxiliary primal variables.
- **Initialization:** $(x^0,y^0)=(0,0)$ and $\Phi(0)-\inf_{\mathcal X}\Phi\leq\Delta$, where $\Phi(x)=\max_y f(x,y)$. No initial dual optimality is required for PZL's upper bound.
- **Stationarity:** write $\varphi=\Phi+\iota_{\mathcal X}$, with $\iota_{\mathcal X}$ zero on $\mathcal X$ and $+\infty$ outside. An output must satisfy $\|\nabla\varphi_{1/(2L)}(x)\|\leq\epsilon$. WGY's stochastic criterion is $\mathbb E\|\nabla\varphi_{1/(2L)}(x)\|\leq\epsilon$, not an assertion about every realization.
- **Oracle:** one feasible query returns $(f,\nabla_x f,\nabla_y f)$. WGY's stochastic oracle returns the exact value and an unbiased joint gradient estimate with $\mathbb E\|\widehat\nabla f-\nabla f\|^2\leq\sigma^2$. No mean-square smoothness of the sample gradients is assumed.
- **Cost:** count joint saddle-oracle calls. Arithmetic and Euclidean projections onto the known domains are free in this accounting. PZL implements its inner solves with first-order queries and projections (Appendix B); exact dual maximization or exact proximal optimization of the unknown objective is not a free primitive.
- **Output:** PZL's upper bound selects an iterate using a computable step-and-error certificate (Algorithm 1); it is not a last-iterate guarantee.
- **Dimension:** the lower bounds range over finite dimensions that can grow with the parameters and query horizon; they are not bounds for a fixed prescribed dimension.

## Proof architecture

1. **PZL lower bound:** modify the dual chain to control its maximizer, and couple it to an outer construction that bounds the connector variables whenever the value gradient is small. Verify smoothness, the initial gap, bounded-dual feasibility, and an obstruction to Moreau-envelope stationarity.
2. **Deterministic extension:** primal and dual orthogonal embeddings preserve the instance class and envelope-gradient norm. A finite-horizon resisting oracle transfers the zero-respecting obstruction to arbitrary deterministic algorithms.
3. **PZL upper bound:** regularize the dual problem and smooth the primal problem. Retain and translate the full accelerated FOAM state between subproblems; a joint Lyapunov descent bound makes a constant error contraction per outer step sufficient. Geometric warm-start initialization also avoids a logarithmic cost.
4. **WGY lower bounds:** use a primal-dual zero-chain with bounded auxiliary primal variables. For the stochastic result, clip the dual chain while preserving its maximizer and value function, then hide successive dual coordinates with Bernoulli masking under the variance budget.

## Verification record

- [x] The v1 theorem statements, domains, stationarity criteria, oracle models, and accuracy regimes were compared with the benchmark on 2026-09-15.
- [x] The arbitrary-deterministic versus zero-respecting distinction and constrained-primal restriction are recorded.
- [x] The parameter scaling and the simplification of Tracked-FOAM's full bound were checked at the theorem-comparison level.
- [x] Both papers' AI disclosures and author-reported human verification are attributed below.
- [ ] Independent lemma-by-lemma proof audit, including imported results and constants.
- [ ] Independent rebuild and paper-to-Lean correspondence audit of the linked formalizations.
- [ ] Repository human reviewer names and sign-off.

The authors report checking their mathematical arguments: **Siyu Pan, Taoli Zheng, and Jiajin Li** for PZL; **Qilong Wu, Zhihao Gu, and Junchi Yang** for WGY. This is author-reported verification, not a separate repository review.

## Limitations and open questions

- Neither preprint establishes the lower bound for unrestricted randomized first-order algorithms.
- WGY's stochastic result retains the constrained-primal and zero-respecting restrictions; it is not a stochastic resolution of the original unconstrained-primal benchmark.
- Optimality of the deterministic rate is asserted only for the positive-parameter, small-accuracy regime above. The full upper bound should be used outside that regime.
- Game stationarity, separate primal/dual gradient costs, and higher-order oracles require separate statements.
- The NC--C class allows individual hard instances to be strongly concave in the dual variable with an instance-dependent modulus. The result does not assume a uniform positive modulus across the class.

## Provenance and references

- **PZL manuscript:** Siyu Pan, Taoli Zheng, and Jiajin Li, [*Optimal Deterministic First-Order Oracle Complexity for Nonconvex-Concave Minimax Optimization*](https://arxiv.org/abs/2609.14235v1), 2026. [Author-linked Lean development](https://github.com/SiyuPan04/ncc-lean).
- **WGY manuscript:** Qilong Wu, Zhihao Gu, and Junchi Yang, [*Lower Bounds for Nonconvex-Concave Minimax Optimization*](https://arxiv.org/abs/2609.14233v1), 2026. [Author-linked Lean development](https://github.com/Wu-Qilong/Lower-Bounds-for-Nonconvex-Concave-Minimax-Optimization).
- **AI systems, PZL disclosure:** GPT-5.5 Pro contributed to the hard-instance construction; GPT-5.6 Sol Ultra helped simplify it, design Algorithm 1, and improve the proof presentation; Codex assisted the Lean formalization.
- **AI systems, WGY disclosure:** the authors supplied their own proof draft, central dual chain, auxiliary-variable constraint, and deterministic scaling argument to GPT-5.6 Sol Ultra. The model helped refine the primal construction and technical arguments. The authors introduced the stochastic dual-chain mechanism; model assistance included parts of the clipping construction. Codex assisted the Lean formalization.
- **Original AI traces:** no prompt/response archive is linked in the reviewed v1 disclosures. The manuscripts and formalizations are the available public records; this curation does not substitute for a trace archive.
- **Earlier upper bounds:** Lin, Jin, and Jordan, [*Near-Optimal Algorithms for Minimax Optimization*](https://arxiv.org/abs/2002.02417), COLT 2020, Appendix A; Li, Nagarajan, Pan, and Zhang, [*Smoothing Meets Perturbation: Unified and Tight Analysis for Nonconvex-Concave Minimax Optimization*](https://arxiv.org/abs/2602.14185), 2026, as cited by PZL.
- **Stochastic comparison:** Zhang, Aybat, and Gürbüzbalaban, *SAPD+: An Accelerated Stochastic Method for Nonconvex-Concave Minimax Problems*, NeurIPS 2022, Theorem 5, as cited by WGY.
- **Repository curation:** Codex performed the source comparison and documentation update on 2026-09-15; it did not originate these mathematical results. [Bibliography](references.bib).

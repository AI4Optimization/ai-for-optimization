# Tight lower bound for stochastic nonconvex-strongly-concave minimax optimization

## Status

**Verified draft; cleanup needed.** The scalar-gate construction and its parameter scaling have been checked at the draft level. A publication-ready proof still needs the fixed-oracle definition, support induction, gate-counting argument, domain constants, and quantifiers written in full detail.

The checked scope is the zero-respecting, bounded-variance stochastic first-order oracle model. This status does not cover unrestricted randomized algorithms, mean-squared-smooth stochastic oracles, finite-sum/component-gradient oracles, or sample gradients required to arise from individually smooth sample functions.

Three independent public preprints posted shortly afterward establish and extend the central linear-$\kappa$ stochastic lower bound under different models. They are recorded in [Concurrent follow-up works](#concurrent-follow-up-works); their publication status does not retroactively turn this AI-assisted draft into their proof.

## Result

For smooth nonconvex--strongly-concave minimax problems with joint smoothness $L$, dual condition number $\kappa=L/\mu$, initial primal gap at most $\Delta$, and an unbiased stochastic first-order oracle with variance at most $\sigma^2$, the construction targets the lower bound

```math
\Omega\!\left(
L\Delta\left[
\frac{\sqrt{\kappa}}{\epsilon^2}
+\frac{\kappa\sigma^2}{\epsilon^4}
\right]
\right).
```

The deterministic term $\Omega(\sqrt\kappa L\Delta/\epsilon^2)$ is known. The new part is the stochastic term

```math
\Omega\!\left(\frac{\kappa L\Delta\sigma^2}{\epsilon^4}\right),
```

which improves the published $\kappa^{1/3}$ dependence and matches the linear $\kappa$ dependence of the SAPD+ upper bound, up to the precise initialization metric and logarithmic overhead.

## Setting and oracle model

- The saddle objective is jointly $L$-smooth, nonconvex in the primal variable, and $\mu$-strongly concave in the dual variable.
- The oracle returns an exact function value and an unbiased stochastic gradient $g(w,\xi)$ satisfying $\mathbb E[g(w,\xi)]=\nabla F(w)$ and $`\mathbb E\|g(w,\xi)-\nabla F(w)\|^2\leq\sigma^2`$.
- Algorithms are zero-respecting with respect to past queries and returned stochastic gradients.
- Stationarity is measured by the projected primal-gradient mapping, following the motivating lower-bound paper.

## Scalar-gate construction

Let $u=(x,z)$ and define

```math
(B_Tu)_i=x_i-\frac12z_{i+1},
\qquad i=1,\ldots,T-1.
```

The rows of $B_T$ have disjoint supports, hence

```math
B_TB_T^\top=\frac54I,
\qquad
\|B_T\|=\frac{\sqrt5}{2}.
```

Starting from the zero-chain block $q_T(u)$ used in the existing NC-SC lower-bound construction, set

```math
\bar F_T(u;y)
=q_T(u)+a\langle B_Tu,y\rangle-\frac\nu2\|y\|^2,
\qquad
\nu=\frac{C_0}{\kappa},
\qquad
a^2=12\nu.
```

Maximizing over $y$ is explicit:

```math
\max_y\bar F_T(u;y)
=q_T(u)+\frac{a^2}{2\nu}\|B_Tu\|^2
=q_T(u)+6\|B_Tu\|^2
=h_T(u).
```

Thus the maximized primal hard function is unchanged even though the dual gradient signal has size only $a=\Theta(\kappa^{-1/2})$. The saddle function has constant joint smoothness and strong concavity $\Theta(\kappa^{-1})$.

After the scaling

```math
F_T(U;Y)=\frac{L\lambda^2}{C_0}
\bar F_T\!\left(\frac U\lambda;\frac Y\lambda\right),
\qquad
\lambda=\Theta\!\left(\frac\epsilon L\right),
```

the gradient in an unrevealed gate coordinate has magnitude

```math
G_\epsilon=O\!\left(\frac\epsilon{\sqrt\kappa}\right).
```

## Fixed stochastic oracle

Order the relevant coordinates as

```math
x_1,y_1,z_2,x_2,y_2,z_3,\ldots,x_{T-1},y_{T-1},z_T,x_T.
```

For a query $w$, let $r(w)$ be its largest nonzero coordinate and $j(w)=r(w)+1$. If $j(w)$ is a $y$-gate coordinate, mask only that incoming coordinate:

```math
[g(w,\xi)]_k=
\begin{cases}
\dfrac{\xi}{p}[\nabla F_T(w)]_k,
& k=j(w)\text{ is a gate},\\[1ex]
[\nabla F_T(w)]_k,
& \text{otherwise},
\end{cases}
\qquad
\xi\sim\operatorname{Bernoulli}(p).
```

Choose

```math
p=\frac{G_\epsilon^2}{G_\epsilon^2+\sigma^2}.
```

The oracle is query-dependent but history-independent, is unbiased, and obeys

```math
\mathbb E\|g(w,\xi)-\nabla F_T(w)\|^2
\leq\left(\frac1p-1\right)G_\epsilon^2
=\sigma^2.
```

Consequently,

```math
\frac1p
=1+\Theta\!\left(\frac{\kappa\sigma^2}{\epsilon^2}\right).
```

## Gate-counting progress lemma

The construction is not a standard probability-$p$ zero-chain: the transition through a $y_i$ gate occurs with probability $p$, while the subsequent $z_{i+1}$ and $x_{i+1}$ transitions are deterministic. Therefore the usual probability-$p$ zero-chain lemma cannot be quoted directly.

Let $D_N$ be the number of distinct $y$-gates crossed in the first $N$ oracle calls. Conditional on the transcript through time $t$,

```math
\mathbb E[D_{t+1}-D_t\mid\mathcal F_t]\leq p,
\qquad
\mathbb E D_N\leq pN.
```

Reaching $z_T$ requires crossing all $T-1$ gates, so

```math
\Pr(z_T\neq0)
\leq\frac{\mathbb E D_N}{T-1}
\leq\frac{pN}{T-1}.
```

For $N\leq(T-1)/(4p)$, the terminal coordinate remains hidden with probability at least $3/4$. The zero-chain hard function then retains a constant stationarity obstruction.

With chain length

```math
T=\Theta\!\left(\frac{L\Delta}{\epsilon^2}\right),
```

the gate cost is

```math
\frac Tp
=\Theta\!\left(
\frac{L\Delta}{\epsilon^2}
+\frac{\kappa L\Delta\sigma^2}{\epsilon^4}
\right).
```

Taking the harder of this stochastic instance and the existing deterministic instance gives the stated combined lower bound.

## Concurrent follow-up works

The following three works independently develop the stochastic NC--SC lower-bound direction. Their assumptions, stationarity criteria, and algorithm classes differ, so the results should not be treated as identical.

### Wu et al. (arXiv:2610.00229)

[Wu et al., *Sharp Fresh-Gradient Complexity of Nonconvex-Strongly-Concave Minimax Optimization*](https://arxiv.org/abs/2610.00229) characterize the fresh-gradient complexity, up to logarithmic factors, on unconstrained Euclidean domains for **arbitrary adaptive randomized algorithms**. Given primal gap $\Delta$, initial dual residual at most $G$, and fixed-budget success probability at least $2/3$, their bound is

```math
\widetilde\Theta\!\left(
\frac{\sqrt\kappa L\Delta}{\epsilon^2}
+\frac{\kappa L\Delta\sigma^2}{\epsilon^4}
+\frac{\kappa^2\sigma^2}{\epsilon^2}
+\sqrt\kappa\log_+\!\frac{G}{\epsilon\sqrt\kappa}
\right).
```

Beyond the shared linear-$\kappa$ global stochastic term, this work identifies a separate $\kappa^2\sigma^2/\epsilon^2$ **statistical refinement cost**, proves that dual initialization contributes only additively through a logarithm, and shows that without any control of the initial dual residual there is no finite dimension-free complexity bound, even with exact gradients. Its lower bounds are not restricted to zero-respecting algorithms.

### Zhou (arXiv:2609.30877)

[Zhou, *Tight Stochastic Condition-Number Dependence in Nonconvex-Strongly-Concave Minimax Optimization*](https://arxiv.org/abs/2609.30877) proves tightness for **zero-respecting algorithms** under the same Moreau-envelope stationarity criterion and primal--dual initialization gap used by SAPD+. In the stated regime $\sigma\geq\epsilon$, the complexity is

```math
\Theta\!\left(\frac{\kappa LG\sigma^2}{\epsilon^4}\right).
```

The hard class permits a bounded dual box and a general unbiased bounded-variance oracle. In addition, the construction yields the combined primal-gradient lower bound

```math
\Omega\!\left(L\Delta\left[\frac{\sqrt\kappa}{\epsilon^2}+\frac{\kappa\sigma^2}{\epsilon^4}\right]\right),
```

and gives a matching primal-gradient comparison under controlled cross derivatives. The author reports using GPT-6 Astra and Claude Science with Opus 5.5 for drafting assistance and states that all proofs were verified by the author.

### Zhang, Wu, and Yang (arXiv:2609.35206)

[Zhang, Wu, and Yang, *Tight Lower Bounds for Stochastic Nonconvex-Strongly-Concave Minimax Optimization*](https://arxiv.org/abs/2609.35206) give lower bounds for zero-respecting algorithms on **fully unconstrained** NC--SC problems. Under bounded variance they prove the same stochastic term

```math
\Omega\!\left(\frac{\kappa L\Delta\sigma^2}{\epsilon^4}\right).
```

Their additional result treats an **averaged-smooth stochastic oracle**, proving the first lower bound of

```math
\Omega\!\left(\frac{\kappa^{3/2}\bar L\Delta\sigma}{\epsilon^3}\right),
```

which matches the corresponding upper bound in $\kappa$ and $\epsilon$. A unified quadratic lifting transfers stochastic nonconvex-minimization hardness to the minimax problem; both bounds also extend to Moreau-envelope stationarity. The paper provides a Lean formalization of key components and discloses ChatGPT assistance in construction search, proof refinement, literature review, and drafting, followed by independent author verification.

## Cleanup required

- Write the coordinate-support induction with exact indexing and oracle-call timing.
- State all domain radii and verify that every unconstrained dual maximizer lies in the chosen compact dual box.
- Track the constants in the smoothness, strong-concavity, gap, and stationarity scaling.
- State the zero-respecting algorithm class and the projected-gradient mapping convention precisely.
- Separate expectation and success-probability formulations of the lower bound.
- Record the human verification procedure and reviewers.

## Provenance and references

- [Original AI-assisted proof discussion](https://chatgpt.com/share/6a96c88b-6124-83e8-8189-f20dd246a922)
- [Li, Tian, Zhang, and Jadbabaie: published NC-SC lower bounds](https://arxiv.org/abs/2104.08708)
- [Zhang, Aybat, and Gürbüzbalaban: SAPD+ upper bound](https://arxiv.org/abs/2205.15084)
- [Arjevani et al.: stochastic zero-chain lower-bound framework](https://arxiv.org/abs/1912.02365)
- [Wu et al.: sharp fresh-gradient complexity, arbitrary randomized algorithms](https://arxiv.org/abs/2610.00229)
- [Zhou: tight SAPD+-matched stochastic condition-number dependence](https://arxiv.org/abs/2609.30877)
- [Zhang, Wu, and Yang: bounded-variance and averaged-smoothness lower bounds](https://arxiv.org/abs/2609.35206)
- Project bibliography: [`references.bib`](references.bib)

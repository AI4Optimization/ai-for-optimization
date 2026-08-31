# Condition-number lower bounds for bilevel optimization

## Status

**Public preprint.** The original AI-assisted proof search has been developed into the human-authored and publicly available paper *On the Condition Number Dependency in Bilevel Optimization* (arXiv:2511.22331). This project records the main first-order lower bound and its provenance; the paper is the canonical proof.

## AI use and provenance

The shared discussion [*LB for BLO in Kappa*](https://chatgpt.com/share/6a9550bf-4cb0-83ea-9481-60a54adc43a7) records the AI-assisted proof-search trace for the condition-number lower bound. The trace is retained as research provenance rather than as the canonical proof. The exact model and the division between AI suggestions and later human repairs are not inferred here beyond what is visible in the public sources.

The result was subsequently written into [Chen, Ji, and Zhang, *On the Condition Number Dependency in Bilevel Optimization*](https://arxiv.org/abs/2511.22331). The current arXiv version is a merge of two concurrent works and contains the cleaned statements, constructions, proofs, extensions, and matching upper bounds.

## Problem and oracle model

Consider the unconstrained bilevel problem

$$
\min_{x\in\mathbb R^{d_x}} F(x)=f(x,y^\ast(x)), y^\ast(x)=\arg\min_{y\in\mathbb R^{d_y}}g(x,y).
$$

For the main lower bound, $f$ is smooth and may be nonconvex, while $g$ is a jointly quadratic function whose Hessian in $y$ is positive definite. The relevant parameters are:

- $L_1$: the common first-order smoothness scale used by the paper's NC--Q function class;
- $\mu_y$: the strong-convexity parameter of $g(x,\cdot)$;
- $\kappa_y=L_1/\mu_y$: the lower-level condition number;
- $\Delta$: an upper bound on $F(0)-\inf_x F(x)$.

Algorithms start from zero and access either the deterministic first-order oracle for $(f,g)$ or the paper's HVP oracle, which additionally returns $\nabla^2_{xy}g(x,y)v$ and $\nabla^2_{yy}g(x,y)v$. On quadratic lower-level instances, HVP queries can be simulated using differences of first-order queries, so the two deterministic algorithm classes have the same lower-bound complexity. The output criterion is an $\epsilon$-stationary point satisfying $\|\nabla F(x)\|\leq\epsilon$.

## Main result

There is a numerical constant $a_0\in(0,1)$ such that, for every $L_1,\Delta>0$ and $\mu_y\in(0,a_0L_1]$, one can construct a smooth nonconvex--quadratic bilevel problem for which every deterministic first-order or HVP-based algorithm requires at least

$$
\Omega\!\left(\kappa_y^{5/2}L_1\Delta\epsilon^{-2}\right)
$$

oracle calls to find an $\epsilon$-stationary point. Suppressing $L_1$ and $\Delta$, this is the $\Omega(\kappa_y^{5/2}\epsilon^{-2})$ lower bound highlighted in the paper.

This improves the $\Omega(\sqrt{\kappa_y}\epsilon^{-2})$ condition-number dependence inherited from nonconvex--strongly-concave minimax lower bounds by a factor of $\kappa_y^2$. For a quadratic lower-level function, the paper also gives a $\widetilde O(\kappa_y^{5/2}\epsilon^{-2})$ upper bound, making the dependence tight up to logarithmic factors.

## Proof architecture

The hard instance combines a nonconvex zero-chain in the outer variable with a nested quadratic chain in the lower-level variable. Its key linear-algebraic component is the tridiagonal matrix

$$
A_n=
\begin{bmatrix}
\omega & -q & & & 0\\
-q & 2 & -1 & & \\
& -1 & 2 & \ddots & \\
& & \ddots & 2 & -q\\
0 & & & -q & \omega
\end{bmatrix},
\qquad
q=\frac1{\sqrt{n-1}},\quad
\omega=\frac{n}{(n-1)^2}.
$$

The construction has two simultaneous properties:

1. $I/(2(n-1)^2)\preceq A_n\preceq5I$, so choosing $n=\Theta(\sqrt{\kappa_y})$ realizes the desired lower-level condition number;
2. the endpoint entries of $A_n^{-1}$ are amplified to order $n^2$: $(A_n^{-1})_{11}=2(n-1)^2/3$ and $(A_n^{-1})_{1n}=(n-1)^2/3$.

The amplified inverse endpoints make the implicit solution $y^*(x)$ stretch the effective outer zero-chain by $\alpha=\Theta(n^2)=\Theta(\kappa_y)$. A zero-respecting algorithm can reveal only one new chain coordinate per oracle call. After rescaling the instance to meet the smoothness and initial-gap constraints, the chain length needed before the gradient can fall below $\epsilon$ yields the $\kappa_y^{5/2}L_1\Delta\epsilon^{-2}$ bound. The paper supplies the resisting-oracle/rotation argument extending the zero-respecting construction to all deterministic algorithms in the stated class.

## Further results in the paper

The same framework also yields:

- $\Omega(\kappa_y^{9/4}\epsilon^{-7/4})$ for second-order-smooth deterministic NC--Q problems;
- $\Omega(\kappa_y^{13/6}\epsilon^{-5/3})$ under arbitrary higher-order smoothness;
- $\Omega(\kappa_y^{3/2}/\sqrt\epsilon)$ and $\Omega(\kappa_y^{3/2}\sqrt{\kappa_x})$ for convex--quadratic and strongly-convex--quadratic bilevel problems;
- stochastic lower bounds of $\Omega(\kappa_y^4\epsilon^{-4})$ for stochastic HVP methods and $\Omega(\kappa_y^{9/2}\epsilon^{-4})$ for stochastic first-order methods.

## Limitations and open questions

- The near-tight deterministic characterization is for a quadratic lower-level function. Closing the condition-number gap for general strongly convex lower-level functions remains open.
- The main theorem is a worst-case oracle lower bound for deterministic first-order and the specified HVP-based algorithm classes; it is not an impossibility result for every conceivable computational model.
- The $\kappa_y$ in the lower bound is the lower-level condition number. The paper distinguishes it from a global condition number $\bar\kappa_y$, which may be larger and appears in general NC--SC upper bounds.
- Higher-order and stochastic statements use their own smoothness and oracle definitions; they should not be read as consequences of the first-order theorem without those additional constructions.


## References

- [Paper and version history (arXiv:2511.22331)](https://arxiv.org/abs/2511.22331)
- [Full HTML](https://arxiv.org/html/2511.22331)
- [Original AI-assisted proof discussion: *LB for BLO in Kappa*](https://chatgpt.com/share/6a9550bf-4cb0-83ea-9481-60a54adc43a7)
- Project bibliography: [`references.bib`](references.bib)

### Citation

```bibtex
@article{chen2025condition,
  title   = {On the Condition Number Dependency in Bilevel Optimization},
  author  = {Chen, Lesi and Ji, Kaiyi and Zhang, Jingzhao},
  journal = {arXiv preprint arXiv:2511.22331},
  year    = {2025}
}
```

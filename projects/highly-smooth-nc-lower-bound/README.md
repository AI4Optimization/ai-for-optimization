# Nested-chain lower bounds for highly-smooth nonconvex optimization

## Status

**Checked; public preprint.** We checked the nested-chain construction developed in the [*Highly-Smooth NC Optimization* discussion](https://chatgpt.com/share/6a954295-d7e8-83ee-9e41-e67c81d533ea). A cleaned version appears in Section 3.3 and Theorem 3.1 of [*On the Condition Number Dependency in Bilevel Optimization*](https://arxiv.org/abs/2511.22331); Section 4.2 then nests this construction with a strongly-convex quadratic lower-level chain to obtain highly-smooth bilevel lower bounds.

This construction is a simpler nested-chain reformulation of the sharp lower-bound mechanism first discovered by Zhou in [*Sharp First-Order Lower Bounds for Higher-Order Smooth Nonconvex Optimization*](https://arxiv.org/abs/2606.05438). Zhou's work introduced the block-chain and first proved the sharp exponents. The present project does not claim priority for those exponents.

## AI use and provenance

The shared ChatGPT discussion records the proof search for replacing the block-chain with a nested quadratic bridge. We retain it as the original AI trace, while the checked paper is the canonical proof. The exact ChatGPT model used in this shared trace is not inferred here.

The chronological and technical relationship is:

1. Zhou first discovered and proved the sharp first-order lower bounds using a block-chain; arXiv:2606.05438 states that its construction was discovered with ChatGPT 5.5 Pro and subsequently verified by the author.
2. The shared *Highly-Smooth NC Optimization* discussion developed a simpler nested-chain route to the same single-level bounds.
3. We checked that route and wrote it into arXiv:2511.22331 as the highly-smooth nested chain in Section 3.3/Theorem 3.1.
4. Section 4.2 of arXiv:2511.22331 uses the checked construction as the outer hard instance for highly-smooth nonconvex--quadratic bilevel optimization.

## Problem and oracle model

Let $p\geq1$. Consider unconstrained minimization of a possibly nonconvex function $f:\mathbb R^d\to\mathbb R$ such that its $q$th derivative is $L_q$-Lipschitz for $q=1,\ldots,p$. The initial point is the origin and

$$
f(0)-\inf_x f(x)\leq\Delta.
$$

A deterministic first-order algorithm observes function values and gradients. Its goal is to return an $\epsilon$-stationary point, $\|\nabla f(x)\|\leq\epsilon$. The dimension is allowed to scale with the required chain length; the stated lower bounds are dimension-free in the sense that they contain no explicit dimension factor.

## Main result

For every integer $p\geq1$ and sufficiently small $\epsilon>0$, there is a $p$th-order smooth nonconvex function on which every deterministic first-order method requires at least

$$
\begin{cases}
\Omega\!\left(\Delta L_1\epsilon^{-2}\right), & p=1,\\[3pt]
\Omega\!\left(\Delta L_1^{1/2}L_2^{1/4}\epsilon^{-7/4}\right), & p=2,\\[3pt]
\Omega\!\left(\Delta L_1^{1/2}L_3^{1/6}\epsilon^{-5/3}\right), & p=3,\\[3pt]
\Omega_p\!\left(
\Delta L_1^{1/2}
\min_{1\leq q\leq p}L_q^{1/(2q)}
\epsilon^{-5/3}
\right), & p\geq4
\end{cases}
$$

first-order oracle calls. Thus the construction recovers the sharp $\epsilon^{-7/4}$ exponent under Lipschitz Hessians and the sharp $\epsilon^{-5/3}$ exponent under third- and higher-order smoothness, matching known upper bounds up to logarithmic factors where applicable.

## Simplified nested-chain construction

Partition the variables into outer scalars $\bar x_1,\ldots,\bar x_{T+1}$ and $T$ inner bridges $\underline{x}^{(i)}\in\mathbb R^m$. Define

$$
\widehat f^{\mathrm{hs\text{-}nc}}_{\nu,r}(x)
=\frac{\nu}{2}(1-\bar x_1)^2
+\frac12\sum_{i=1}^T
\widehat Q_m(\bar x_i,\underline{x}^{(i)},\bar x_{i+1})
+\nu\sum_{i=1}^T\Upsilon_r(\bar x_i),
$$

where

$$
\widehat Q_m(x_-,z,x_+)
=\frac1m(z_1-\theta x_-)^2
+\sum_{j=1}^{m-1}(z_{j+1}-z_j)^2
+\frac1m(z_m-\theta x_+)^2,
\qquad
\nu=\frac{\theta^2}{3m-1}.
$$

The proof uses three structural facts:

1. **Exact reduction.** Minimizing an inner bridge gives
   $$
   \min_z\widehat Q_m(x_-,z,x_+)=\nu(x_--x_+)^2,
   $$
   so partial minimization exactly recovers the classical scalar nonconvex zero-chain, scaled by $\nu$.
2. **Sequential revelation.** A zero-respecting first-order method must traverse all $m$ inner coordinates before information can pass from $\bar x_i$ to $\bar x_{i+1}$.
3. **Stationarity transfer.** Under $\theta\sqrt m\leq1$, the full gradient controls the gradient of the partially minimized outer chain:
   $$
   \|\nabla\widehat f^{\mathrm{hs\text{-}nc}}_{\nu,r}(x)\|
   \geq\frac12\|\nabla F(\bar x)\|.
   $$

After calibrating the bridge length, chain length, nonconvex regularizer, and global scaling against $L_1,\ldots,L_p$, $\Delta$, and $\epsilon$, these facts yield the theorem above.

## Relation to the original block-chain

The block-chain of arXiv:2606.05438 was the first construction to attain the sharp exponents. It couples consecutive blocks through an entry coordinate and a suffix readout, and its analysis tracks Green-kernel response quantities to normalize signal transmission, smoothness, gap, and the gradient certificate.

The nested-chain proof preserves the same essential delayed-revelation idea but packages it as an ordinary quadratic path between two outer scalar coordinates. Partial minimization of that path has an explicit closed form and reduces exactly to a scalar quadratic edge. This removes the need to formulate the hard instance through block entry/readout geometry and gives a shorter route to the same rates. It is therefore best viewed as a simplification of Zhou's first construction, not an independent rediscovery of the lower-bound exponents.

## Use in highly-smooth bilevel optimization

Section 4.2 of arXiv:2511.22331 replaces every scalar coordinate in the nested single-level hard instance by an inverse-endpoint-amplified strongly-convex quadratic lower-level chain. The induced hyper-objective becomes a rescaled copy of the single-level nested chain. With $\alpha=\Theta(\kappa_y)$, Theorem 4.2 obtains

$$
\begin{cases}
\Omega\!\left(\kappa_y^{9/4}\Delta L_1^{1/2}L_2^{1/4}\epsilon^{-7/4}\right), & p=2,\\[3pt]
\Omega\!\left(\kappa_y^{13/6}\Delta L_1^{1/2}L_3^{1/6}\epsilon^{-5/3}\right), & p=3,\\[3pt]
\Omega_p\!\left(
\kappa_y^{13/6}\Delta L_1^{1/2}
\min_{1\leq q\leq p}L_q^{1/(2q)}
\epsilon^{-5/3}
\right), & p\geq4.
\end{cases}
$$

These bounds apply to the paper's deterministic first-order and HVP-based algorithm classes on nonconvex--quadratic bilevel problems.

## Verification record

- [x] Nested-chain exact-reduction identity checked
- [x] Full-gradient to outer-gradient stationarity transfer checked
- [x] Smoothness/gap calibration and final single-level rates checked
- [x] Comparison with the first block-chain result checked against arXiv:2606.05438
- [x] Single-level construction incorporated into arXiv:2511.22331, Section 3.3/Theorem 3.1
- [x] Bilevel extension incorporated into arXiv:2511.22331, Section 4.2/Theorem 4.2
- [ ] Independent reproduction by researchers outside the author team recorded

## Limitations

- The result is a worst-case deterministic first-order oracle lower bound; it does not cover every randomized or higher-order oracle model.
- Sufficiently small $\epsilon$ and a dimension large enough to contain the hard chain are required.
- The phrase “simplified” refers to the construction and proof organization. Priority for the sharp exponents and their first proof belongs to Zhou's block-chain work.
- The bilevel condition-number factors require the additional lower-level construction and assumptions of arXiv:2511.22331; they do not follow from the single-level theorem alone.

## References

- [Original AI-assisted proof discussion: *Highly-Smooth NC Optimization*](https://chatgpt.com/share/6a954295-d7e8-83ee-9e41-e67c81d533ea)
- [Checked nested-chain proof and bilevel extension (arXiv:2511.22331)](https://arxiv.org/abs/2511.22331)
- [First sharp block-chain lower bounds (arXiv:2606.05438)](https://arxiv.org/abs/2606.05438)
- Project bibliography: [`references.bib`](references.bib)


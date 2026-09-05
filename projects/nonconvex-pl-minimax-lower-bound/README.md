# Tight lower bound for nonconvex--PL minimax optimization

## Status

**Public preprint.** Pan and Li (2026) prove a matching deterministic first-order lower bound for the one-sided nonconvex--Polyak--Łojasiewicz minimax setting.

## Result

Consider

$$
\min_{x\in\mathbb R^m}\max_{y\in\mathbb R^n} f(x;y),
\qquad
\Phi(x):=\max_y f(x;y),
$$

where $f$ is jointly $\ell$-smooth, $f(x;\cdot)$ satisfies the $\mu$-PL inequality for every $x$, and $\Phi(0)-\inf_x\Phi(x)\leq\Delta$. Let $\kappa=\ell/\mu$. For $\kappa$ bounded below by a universal constant and $0<\epsilon^2\lesssim\ell\Delta$, every deterministic first-order method requires

$$
\Omega\!\left(\frac{\ell\Delta\kappa}{\epsilon^2}\right)
$$

oracle queries in the worst case to find $x$ satisfying $\|\nabla\Phi(x)\|\leq\epsilon$. This matches the known $O(\ell\Delta\kappa/\epsilon^2)$ upper bound in all principal parameters.

## Setting and assumptions

- **Problem class:** smooth nonconvex--PL minimax optimization; the primal value function may be nonconvex.
- **Smoothness:** $f$ is jointly $\ell$-smooth in $(x,y)$.
- **Dual PL condition:** for every fixed $x$, the maximization problem has a finite attained optimum and
  $$
  \frac12\|\nabla_y f(x;y)\|^2\geq\mu\bigl(\Phi(x)-f(x;y)\bigr).
  $$
- **Condition number:** $\kappa=\ell/\mu$.
- **Initialization:** the primal value-function gap satisfies $\Phi(0)-\inf_x\Phi(x)\leq\Delta$.
- **Oracle model:** a deterministic first-order saddle oracle returns $(f(x;y),\nabla_x f(x;y),\nabla_y f(x;y))$.
- **Output criterion:** find a primal point $x$ with $\|\nabla\Phi(x)\|\leq\epsilon$.
- **Algorithm class:** arbitrary deterministic adaptive first-order methods, not only zero-respecting or linear-span algorithms.

## Proof architecture

1. Construct a scalable length-$N$ weighted dual PL chain with smoothness independent of $N$ and PL modulus of order $1/N$.
2. Use each dual block to delay revelation of one successor primal coordinate while recovering the desired outer term exactly after maximizing over the dual variables.
3. Insert a length-$N=\Theta(\kappa)$ dual block into each of $M=\Theta(\ell\Delta/\epsilon^2)$ links of a nonconvex primal zero-chain.
4. Verify joint smoothness, the dual PL inequality, the initial value-function gap, and the value-function stationarity obstruction.
5. Apply separate primal and dual orthogonal embeddings in a finite-horizon resisting-oracle argument to extend the result to arbitrary deterministic methods.

## Verification record

- [x] The theorem statement and parameter regime are checked against the public preprint.
- [x] The first-order saddle oracle and value-function stationarity criterion are explicitly stated.
- [x] The lower bound covers arbitrary deterministic first-order algorithms.
- [x] The parameter dependence matches the cited upper bound.
- [ ] No independent verification record or formal proof artifact is linked here.

## Limitations and open questions

- The theorem is deterministic; randomized first-order lower bounds require separate treatment.
- It assumes a one-sided PL condition in the dual variable. It does not settle the [two-sided PL--PL open problem](../../open-problems/pl-minimax/).
- The result requires the stated condition-number and accuracy regimes.

## Provenance and references

- **Clean write-up:** Siyu Pan and Jiajin Li, [*Lower Bounds for Nonconvex--PL Minimax Optimization*](https://arxiv.org/abs/2608.26799), 2026.
- **Matching upper bound:** Yang et al., [*Smoothed GDA for nonconvex--PL minimax optimization*](https://arxiv.org/abs/2112.05604), 2022.
- **Related open problem:** [Tight complexity under two-sided PL conditions](../../open-problems/pl-minimax/).

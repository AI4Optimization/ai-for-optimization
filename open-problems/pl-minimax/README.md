# Tight complexity bound for minimax optimization under two-sided PL conditions

## Status

**Resolved.** [OpenReview paper PlfFyV6wbZ](https://openreview.net/forum?id=PlfFyV6wbZ) proves the matching lower bound for the two-sided PL--PL minimax problem. This closes the gap against the $`\widetilde O(\kappa_x\kappa_y)`$ upper bound under the paper's stated first-order oracle and solution criterion. See also the paper's full details at the linked OpenReview record.

## Problem definition

Consider $\min_x\max_y f(x,y)$ for a smooth objective. In the one-sided setting, the maximization problem satisfies a Polyak--Łojasiewicz (PL) inequality in $y$ while the induced primal problem may be nonconvex. In the two-sided setting, the corresponding primal and dual gaps satisfy PL inequalities with condition numbers $\kappa_x$ and $\kappa_y$.

## Oracle model

The setting is deterministic and noiseless. A first-order oracle returns $f(x,y)$ and both partial gradients. Complexity counts joint gradient evaluations. The solution measure and initial-gap normalization should match the cited upper-bound paper; lower bounds must make the dependence on both PL condition numbers explicit.

## Known bounds and open target

The two-sided PL--PL upper bound is $\widetilde O(\kappa_x\kappa_y)$. The linked OpenReview work establishes the matching lower bound and resolves this target. The tight one-sided $\Theta(\ell\Delta\kappa_y/\epsilon^2)$ complexity proved by Pan and Li remains a related result, not the proof of the two-sided claim.

## References

- [Yang et al., one-sided PL upper bound (2022)](https://arxiv.org/abs/2112.05604)
- [Chen, Yao, and Luo, PL--PL upper bound (2023)](https://arxiv.org/abs/2307.15868)
- [Pan and Li, matching one-sided NC--PL lower bounds (2026)](../../projects/nonconvex-pl-minimax-lower-bound/)
- [Matching two-sided PL--PL lower bound (OpenReview)](https://openreview.net/forum?id=PlfFyV6wbZ)

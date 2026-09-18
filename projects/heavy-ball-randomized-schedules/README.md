# Heavy Ball under randomized schedules

## Status

**Public preprint.** He and Zhang (2026) prove that predefined randomized parameter schedules accelerate the Heavy Ball method on general smooth convex objectives.

## Setting

Consider Heavy Ball with zero initial velocity,

$$
x_{k+1}=x_k-\eta_k\nabla f(x_k)+\beta_k(x_k-x_{k-1}),
\qquad x_{-1}=x_0,
$$

where $f$ is convex and $L$-smooth and the initial distance to a minimizer is at most $R$. The parameter schedule is sampled independently of oracle observations: it is randomized but predefined rather than gradient-adaptive. Performance is measured by the last-iterate objective gap.

## Main results

The paper separates two levels of randomization.

### Deterministic time boundaries

When gradient-evaluation times are randomized within intervals whose boundaries remain deterministic, the paper constructs both fixed-time and anytime schedules satisfying

$$
f(x_T)-f(x^\star)
=O\left(\frac{LR^2}{T^{4/3}}\right).
$$

The guarantee is in expectation; the anytime schedule also achieves the same asymptotic rate almost surely.

### Randomized time boundaries

When the interval boundaries are randomized as well, the rate improves to

$$
f(x_T)-f(x^\star)
=O\left(\frac{LR^2}{T^{3/2}}\right)
$$

both in expectation and almost surely.

## Relation to Heavy Ball lower bounds

Ma and Zhang (2026) study deterministic schedules fixed before the objective and prove a lower bound of order $LR^2/(T^{(1+\sqrt5)/2}\log T)$. The later AI-assisted note recorded in the [Heavy Ball lower-bound project](../heavy-ball-logfree-lower-bound/) strengthens that deterministic-schedule lower bound to $\Omega(LR^2/T^{3/2})$.

The $O(LR^2/T^{3/2})$ randomized-boundary upper rate matches the exponent of that subsequent deterministic-schedule lower bound, but the schedule models differ: this project uses predefined randomness, whereas the lower bound fixes a deterministic schedule before choosing the adversarial objective.

## References

- Chang He and Shuzhong Zhang, [*Heavy-Ball Method under Randomized Schedules*](https://arxiv.org/abs/2609.09743), 2026.
- Jianhao Ma and Jingzhao Zhang, [*A Lower Bound for the Heavy-Ball Method on Smooth Convex Functions*](https://arxiv.org/abs/2609.08656), 2026.
- [Repository record of the deterministic-schedule Heavy Ball lower bounds](../heavy-ball-logfree-lower-bound/).

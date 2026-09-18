# Log-free lower bound for Heavy Ball on smooth convex functions

## Status

**AI-assisted technical note; improvement over Ma and Zhang (2026).** The proof is attributed in the note to GPT-6 Astra, prompted by Wenzhi Gao. It builds on the static-chain construction and momentum-removal lemma of Ma and Zhang and strengthens their Heavy Ball lower bound.

## Setting

For a horizon $T$, consider the Heavy Ball iteration

$$
x_{t+1}=x_t-\eta_t\nabla f(x_t)+\beta_t(x_t-x_{t-1}),
\qquad x_{-1}=x_0,
$$

where the schedule is fixed before the adversarial objective is selected and satisfies

$$
\eta_t\geq0,
\qquad 0\leq\beta_t<1.
$$

The schedule may depend on $T$, $L$, and $R$, but may not adapt to observed gradients. The output is the actual last iterate $x_T$.

## Main result

For every such predetermined schedule, there is a differentiable convex $L$-smooth function in dimension at most $T+1$, with a minimizer $x^\star$ and initialization $\|x_0-x^\star\|\leq R$, such that

$$
f(x_T)-f(x^\star)
\geq
c\frac{LR^2}{T^{3/2}}
$$

for a universal constant $c>0$. The hard objective is a scaled and translated static one-sided Huber chain.

## Improvement over Ma and Zhang

Ma and Zhang (2026) proved the lower bound

$$
\Omega\left(
\frac{LR^2}{T^{(1+\sqrt{5})/2}\log T}
\right)
$$

for the same broad class of predetermined nonnegative Heavy Ball schedules. The new note improves the polynomial exponent to $3/2$ and removes the logarithmic loss. It reuses Ma and Zhang's static-chain construction and momentum-removal lemma, while adding a sharp $S_2(N)=O(\sqrt{N})$ local estimate and a compression of every retention block into a single virtual checkpoint.

The result does not cover gradient-adaptive schedules and does not itself prove a matching upper bound. He and Zhang (2026) give an $O(T^{-3/2})$ expected and almost-sure last-iterate upper bound using randomized schedules with randomized time boundaries, which is a different schedule model.

## References

- GPT-6 Astra, prompted by Wenzhi Gao, [*An $\Omega(T^{-3/2})$ lower bound for heavy ball*](https://web.stanford.edu/~gwz/blogs/gpt_1/heavy_ball_logfree_lower_bound.pdf), September 9, 2026.
- Jianhao Ma and Jingzhao Zhang, [*A Lower Bound for the Heavy-Ball Method on Smooth Convex Functions*](https://arxiv.org/abs/2609.08656), 2026.
- Chang He and Shuzhong Zhang, [*Heavy-Ball Method under Randomized Schedules*](https://arxiv.org/abs/2609.09743), 2026.

# Lower bounds for Heavy Ball on smooth convex functions

## Status

**Public preprint by Ma and Zhang (2026), with a subsequent AI-assisted improvement.** Ma and Zhang established the original lower bound recorded here. A later technical note attributed to GPT-6 Astra, prompted by Wenzhi Gao, strengthens their rate using the same static-chain framework and momentum-removal lemma.

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

The schedule may depend on $T$, $L$, and $R$, but may not adapt to observed gradients. The objective is convex and $L$-smooth, the initial distance to a minimizer is at most $R$, and performance is measured at the actual last iterate $x_T$.

## Ma and Zhang lower bound

Ma and Zhang (2026) prove that every such predetermined schedule has a worst-case instance satisfying

$$
f(x_T)-f(x^\star)
\geq
c\frac{LR^2}{T^{(1+\sqrt{5})/2}\log T}
$$

for a universal constant $c>0$. Thus arbitrary nonstationary, horizon-dependent tuning cannot guarantee Nesterov's $O(T^{-2})$ rate for classical Heavy Ball on all smooth convex objectives.

## Subsequent improvement

The later note *An $\Omega(T^{-3/2})$ lower bound for heavy ball* improves the Ma--Zhang result to

$$
f(x_T)-f(x^\star)
\geq
c'\frac{LR^2}{T^{3/2}},
$$

again in dimension at most $T+1$ and for the same class of predetermined schedules. The note is attributed to GPT-6 Astra, prompted by Wenzhi Gao, and explicitly builds on Ma and Zhang's static one-sided Huber chain and momentum-removal lemma.

The improvement adds a sharp $S_2(N)=O(\sqrt{N})$ local estimate and compresses each retention block into one virtual checkpoint, removing the logarithmic loss and improving the polynomial exponent. It does not cover gradient-adaptive schedules and does not itself prove a matching upper bound.

He and Zhang (2026) give an $O(T^{-3/2})$ expected and almost-sure last-iterate upper bound using randomized schedules with randomized time boundaries. That is a different schedule model from a fixed deterministic schedule.

## References

- Jianhao Ma and Jingzhao Zhang, [*A Lower Bound for the Heavy-Ball Method on Smooth Convex Functions*](https://arxiv.org/abs/2609.08656), 2026.
- GPT-6 Astra, prompted by Wenzhi Gao, [*An $\Omega(T^{-3/2})$ lower bound for heavy ball*](https://web.stanford.edu/~gwz/blogs/gpt_1/heavy_ball_logfree_lower_bound.pdf), September 9, 2026. Subsequent improvement of Ma and Zhang.
- Chang He and Shuzhong Zhang, [*Heavy-Ball Method under Randomized Schedules*](https://arxiv.org/abs/2609.09743), 2026.

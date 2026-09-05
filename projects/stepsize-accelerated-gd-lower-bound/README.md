# Lower bounds for stepsize-based acceleration of gradient descent

## Status

**Public preprint; subsequently improved.** Ma and Chen's main proof was developed by GPT-5.6 Sol Pro under the authors' guidance, then reviewed, revised, and formally verified in Lean 4. Two September 2026 papers subsequently strengthened the exponent and broadened the comparison between non-anytime and anytime schedules.

## Original result

For smooth convex $f:\mathbb R^d\to\mathbb R$, plain gradient descent follows

$$
x_{t+1}=x_t-\eta_t\nabla f(x_t).
$$

Fix a horizon $T$ and any predetermined nonnegative schedule $(\eta_0,\ldots,\eta_{T-1})$. Let

$$
p_\star=\sqrt{2+\sqrt3}\approx1.9319.
$$

Ma and Chen prove that, for every $p\in(p_\star,2)$, there is a smooth convex hard instance in dimension at most $T+1$ with $\|x_0-x_\star\|=R$ such that

$$
f(x_T)-f(x_\star)\geq c_pLR^2(T+1)^{-p}.
$$

Thus predetermined stepsizes alone cannot attain the optimal general first-order $O(T^{-2})$ rate.

## Setting and assumptions

- **Problem class:** unconstrained convex objectives with $L$-Lipschitz gradients and at least one minimizer.
- **Algorithm:** plain GD; no momentum or auxiliary iterates.
- **Schedule:** deterministic, nonadaptive, and chosen before the objective and dimension. The original theorem permits arbitrary nonnegative magnitudes and ordering, but fixes the horizon in advance.
- **Initialization:** $\|x_0-x_\star\|=R$.
- **Output criterion:** last-iterate objective error $f(x_T)-f(x_\star)$.
- **Cost convention:** one gradient evaluation per iteration.
- **Non-anytime versus anytime:** a non-anytime schedule may depend on $T$; an anytime result requires one infinite schedule to work uniformly over stopping times.

## Subsequent improvements

| Work | Non-anytime lower-bound exponent | Anytime lower-bound exponent | Additional scope |
| --- | ---: | ---: | --- |
| [Ma and Chen (2026)](https://arxiv.org/abs/2608.10418) | $1.9319$ threshold | — | Predetermined nonnegative stepsizes |
| [Ye and Liu (2026)](https://arxiv.org/abs/2609.02855) | $1.6342$ | $1.2408$ | Extends both results to schedules with negative stepsizes |
| [Jung, Cho, and Yun (2026)](https://arxiv.org/abs/2609.04032) | $1.450$ | $1.184$ | Stronger barriers in both settings |

Here a smaller exponent is a stronger lower bound. The best upper bounds reported by Jung, Cho, and Yun have exponents approximately $1.271$ in the non-anytime setting and $1.119$ in the anytime setting, so both gaps remain open.

## Original proof architecture

1. Normalize the stepsizes and split each into a unit-capped part and a long-step excess.
2. Select long steps and construct an explicit adversarial GD trajectory using orthogonal anchors and block-dependent scales.
3. Realize that trajectory as gradient descent on a smooth convex Moreau support envelope.
4. Remove dependence on temporal ordering with two combinatorial matchings.
5. Use a rank cutoff and Lyapunov mass-growth argument; balancing the two cutoff cases yields $p_\star=\sqrt{2+\sqrt3}$.
6. Restore the $L$ and $R$ scaling.

## Verification record

- [x] The original theorem statement and schedule restrictions are checked against the Ma--Chen preprint.
- [x] The authors report substantial human review, verification, and revision.
- [x] The original proof has an accompanying Lean 4 formalization.
- [x] Later exponents and their anytime/non-anytime scope are checked against the two subsequent preprints.
- [ ] The tight convergence exponents remain unknown.

## Limitations and open questions

- None of the three works closes the gap to the best known upper bounds.
- The original Ma--Chen theorem concerns the last iterate and nonnegative, horizon-dependent schedules; later papers broaden the sign restriction and include anytime barriers.
- Adaptive stepsizes, best-iterate guarantees, and the strongly convex setting require separate analysis.

## Provenance and references

- **Original result:** Jianhao Ma and Yuxin Chen, [*A Lower Bound for Stepsize-Based Acceleration of Gradient Descent*](https://arxiv.org/abs/2608.10418), 2026.
- **First subsequent improvement:** Yuhan Ye and Kaizhao Liu, [*Improved Gradient Descent Lower Bounds Beyond Nesterov*](https://arxiv.org/abs/2609.02855), 2026.
- **Second subsequent improvement:** Minchan Jung, Hanseul Cho, and Chulhee Yun, [*Stronger Lower Bounds for (Non-)Anytime Acceleration of Gradient Descent*](https://arxiv.org/abs/2609.04032), 2026.
- **Formal verification of the original proof:** [gd-lower-bound-lean](https://github.com/jianhaoma/gd-lower-bound-lean).
- **AI systems used in the original work:** GPT-5.6 Sol Pro for the main proof and Codex for Lean 4 formalization, as reported by the authors.

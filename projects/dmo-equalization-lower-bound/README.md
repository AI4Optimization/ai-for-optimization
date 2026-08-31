# Equalization lower bound for discrete minimax optimization

## Status

**Checked; not yet written up.** We have checked the deterministic lower-bound argument developed in the [*LB for DMO* discussion](https://chatgpt.com/share/6a95504d-6904-83ea-b9fe-36b17e67918f), but it has not yet been turned into a paper or a self-contained formal proof. The shared discussion remains the most complete source.

The checked claim is the deterministic $\Omega(N\Delta L\epsilon^{-2})$ component-oracle lower bound. The later stochastic constructions in the same discussion are exploratory and are **not** included in the checked status.

## Result

For $N\geq2$, $L,\Delta>0$, and sufficiently small $\epsilon=O(\sqrt{\Delta L})$, there is an unconstrained discrete minimax problem

$$
\min_{x\in\mathbb R^d,\,w\in\mathbb R^{N-1}}
\Psi(x,w),
\qquad
\Psi(x,w)=\max_{i\in[N]}
\left\{h_i(x)-\rho b_i^\top w\right\},
$$

whose components are $L$-smooth and whose initial gap satisfies

$$
\Psi(0,0)-\inf_{x,w}\Psi(x,w)\leq\Delta,
$$

such that every deterministic incremental first-order algorithm requires

$$
\Omega\!\left(N\Delta L\epsilon^{-2}\right)
$$

component-oracle queries to find a point with $\|\nabla\Psi_L(x,w)\|\leq\epsilon$, where $\Psi_L$ denotes the Moreau envelope under the convention used in the source discussion. For $N=1$, the statement reduces to the classical $\Omega(\Delta L\epsilon^{-2})$ smooth nonconvex lower bound.

The bound matches the $O(N\Delta L\epsilon^{-2})$ deterministic complexity targeted by the motivating DMO upper bound.

## Construction

Start from a deterministic finite-sum hard instance

$$
H(x)=\frac1N\sum_{i=1}^N h_i(x)
$$

for which finding $\|\nabla H(x)\|\leq\epsilon$ requires $\Omega(N\Delta L\epsilon^{-2})$ incremental first-order queries. Use a bounded-gradient version with $\|\nabla h_i(x)\|\leq G$, and shift component constants so that $h_i(0)=H(0)$ for every $i$.

Let $B\in\mathbb R^{N\times(N-1)}$ have orthonormal columns spanning $\mathbf1^\perp$:

$$
B^\top B=I,
\qquad
B^\top\mathbf1=0,
\qquad
BB^\top=I-\frac1N\mathbf1\mathbf1^\top.
$$

Set $b_i=B^\top e_i$ and define

$$
f_i(x,w)=h_i(x)-\rho b_i^\top w,
\qquad
\Psi(x,w)=\max_i f_i(x,w).
$$

The added term is linear, so it does not change component smoothness. It is also public information: querying $f_i$ reveals exactly one finite-sum component value and gradient plus the known vector $-\rho b_i$.

## Proof architecture

### Exact equalization

For every fixed $x$,

$$
\min_w\Psi(x,w)=H(x).
$$

The lower bound follows from max being at least the average. Equality is achieved by taking

$$
w^*(x)=\rho^{-1}B^\top
\left(h_1(x)-H(x),\ldots,h_N(x)-H(x)\right),
$$

which makes every shifted component equal to $H(x)$. Consequently, the augmented max problem has the same infimum and initial gap as the finite-sum problem.

### Removing convex-hull cancellation

At a prox point $(\widehat x,\widehat w)$, a Clarke subgradient of the max has the form

$$
\left(
\sum_{i=1}^N\lambda_i\nabla h_i(\widehat x),
-\rho B^\top\lambda
\right),
\qquad \lambda\in\Delta_N,
$$

with $\lambda$ supported on the active components. The main obstruction in a direct max construction is that an arbitrary convex combination of active gradients may cancel. Here the $w$ block removes that freedom. Since

$$
\|B^\top\lambda\|
=\left\|\lambda-\frac1N\mathbf1\right\|,
$$

small $w$-stationarity forces $\lambda$ to be close to the uniform distribution.

If the full residual is at most $\eta$, then

$$
\left\|\lambda-\frac1N\mathbf1\right\|
\leq\frac{\eta}{\rho}
$$

and, using the bounded component gradients,

$$
\|\nabla H(\widehat x)\|
\leq \eta+G\sqrt N\,\frac{\eta}{\rho}.
$$

Choosing $\rho\geq4G\sqrt N$ makes this at most $5\eta/4$. The Moreau-envelope prox relation and $L$-smoothness of $H$ then transfer stationarity back to the algorithm's output $x$, changing only a numerical constant.

### Oracle simulation

One query to the $i$th DMO component returns

$$
f_i(x,w)=h_i(x)-\rho b_i^\top w,
\qquad
\nabla f_i(x,w)=\left(\nabla h_i(x),-\rho b_i\right).
$$

The linear terms are known. Hence a finite-sum algorithm can simulate the entire transcript of any deterministic DMO algorithm using exactly one finite-sum component query per DMO query. A faster DMO algorithm would therefore contradict the finite-sum lower bound.

## Why the auxiliary variable matters

The $w$ variable is an equalizer in two distinct senses:

1. minimizing over $w$ makes the max objective exactly equal to the finite-sum average;
2. stationarity in $w$ forces the active max weights to be nearly uniform.

The first property preserves function values and the initial gap. The second prevents artificial cancellation inside the convex hull of active gradients. Meanwhile, all hidden zero-chain information remains in the $x$ coordinates.

## Items required for a formal write-up

- State the exact DMO function class, Moreau-envelope normalization, oracle protocol, and quantifiers.
- Supply or cite a finite-sum lower bound with globally bounded component gradients, or give the smooth truncation argument that produces it without changing the rate.
- Track the numerical constants in the prox-to-Clarke and prox-to-output stationarity transfers.
- Verify the admissible regime for $N$, $\Delta$, $L$, and $\epsilon$, including the $N=1$ edge case.
- Record the human verification procedure and reviewers.

## Unchecked stochastic directions

The discussion also proposes a noisy value-equalization gadget and a possible sequential construction targeting a function-value-noise term of order

$$
\Omega\!\left(N\Delta L^3\sigma_F^2\epsilon^{-6}\right).
$$

It further explains why the same uniform-weight reduction does not automatically yield an $N$ factor in the stochastic-gradient-noise term. These ideas remain conjectural proof-search material and should not be cited as established results.

## Provenance and references

- [Original AI-assisted proof discussion: *LB for DMO*](https://chatgpt.com/share/6a95504d-6904-83ea-b9fe-36b17e67918f)
- [Emmenegger, Kyng, and Zehmakan: finite-sum oracle lower bounds](https://proceedings.mlr.press/v151/emmenegger22a.html)
- [Zhou and Gu: lower bounds for smooth nonconvex finite-sum optimization](https://proceedings.mlr.press/v97/zhou19b.html)
- Project bibliography: [`references.bib`](references.bib)


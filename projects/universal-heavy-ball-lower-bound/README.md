# Tight lower bound for the nonconvex Universal Heavy Ball method

## Status

**Verified draft; cleanup needed.** The construction and exponent calculations have been checked at the draft level. The argument is based on the nested-chain construction in [Chen, Ji, and Zhang (2026, Section 3.3)](https://arxiv.org/abs/2511.22331), augmented by a fractional Hölder interpolation lemma for the Hessian of its nonconvex regularizer.

A publication-ready version still needs a fully quantified theorem, explicit numerical constants, a line-by-line verification of the Universal Heavy Ball restart rules under the zero-respecting induction, and a clean treatment of initialization-dependent lower-order terms.

## Result

For $\gamma\in[0,1]$, define the function class

$$
\mathcal F_\gamma(L,H,\Delta)
=\left\{
f:\ f(0)-\inf f\leq\Delta,
\ \operatorname{Lip}(\nabla f)\leq L,
\ H_\gamma(f)\leq H
\right\},
$$

where

$$
H_\gamma(f)
=\sup_{x\neq y}
\frac{\|\nabla^2f(x)-\nabla^2f(y)\|}{\|x-y\|^\gamma}.
$$

For fixed $L,H,\Delta>0$ and sufficiently small $\epsilon$, there is a numerical constant $c>0$ and a function $f\in\mathcal F_\gamma(L,H,\Delta)$ such that Universal Heavy Ball requires at least

$$
c\min\left\{
\frac{\Delta L}{\epsilon^2},
\frac{\Delta\sqrt L\,H^{1/(2+2\gamma)}}
{\epsilon^{(4+3\gamma)/(2+2\gamma)}}
\right\}
$$

gradient evaluations to find $x$ satisfying $\|\nabla f(x)\|\leq\epsilon$.

The admissible small-accuracy regime can be written, up to numerical constants, as

$$
\epsilon^2
\lesssim
\Delta\min\left\{L,(H\epsilon^\gamma)^{1/(1+\gamma)}\right\}.
$$

For $L=H=\Delta=1$, the bound is

$$
\Omega\!\left(
\epsilon^{-(4+3\gamma)/(2+2\gamma)}
\right).
$$

It recovers $\Omega(\epsilon^{-2})$ at $\gamma=0$ and $\Omega(\epsilon^{-7/4})$ at $\gamma=1$, matching the interpolation in the Universal Heavy Ball upper bound for every $\gamma\in(0,1)$.

## Why a single-endpoint lower bound is insufficient

Universal Heavy Ball is independent of the Hölder exponent and its guarantee takes an infimum over all $q\in[0,1]$. A hard instance calibrated only at $q=1$ would not rule out the possibility that another $q$ gives the algorithm a smaller bound.

The construction below controls the entire Hessian Hölder profile simultaneously and makes every branch of that infimum have the same order. This is the main new ingredient beyond the endpoint lower bounds.

## Nested-chain construction

Use the highly-smooth nonconvex nested chain from [Chen et al. (2026, Section 3.3)](https://arxiv.org/abs/2511.22331). Let $\bar x=(\bar x_1,\ldots,\bar x_{T+1})$ be the outer variables and let $x^{(i)}\in\mathbb R^m$ be the inner bridge blocks. Define

$$
Q_m(u,x,v)
=\frac1m(x_1-\theta u)^2
+\sum_{j=1}^{m-1}(x_{j+1}-x_j)^2
+\frac1m(x_m-\theta v)^2,
$$

and

$$
\Phi_{\rho,m,T}(\bar x,x)
=\frac\rho2(1-\bar x_1)^2
+\frac12\sum_{i=1}^T
Q_m(\bar x_i,x^{(i)},\bar x_{i+1})
+\rho\sum_{i=1}^T\Upsilon(\bar x_i),
$$

where $\Upsilon$ is the bounded, globally smooth nonconvex zero-chain regularizer of the source construction. Choose

$$
m=\left\lfloor\frac1{3\rho}\right\rfloor,
\qquad
\theta=\sqrt{\rho(3m-1)}.
$$

The springs-in-series identity gives

$$
\min_{x\in\mathbb R^m}Q_m(u,x,v)
=\rho(u-v)^2.
$$

Consequently, minimizing the inner bridge variables reduces the construction exactly to the standard scalar nonconvex zero-chain, and the source stationarity-transfer inequality relates the full gradient to the gradient of that reduced chain.

## Sequential revelation

Order the variables as

$$
\bar x_1,x_1^{(1)},\ldots,x_m^{(1)},
\bar x_2,x_1^{(2)},\ldots,x_m^{(2)},\ldots,
\bar x_{T+1}.
$$

Under this ordering, $\Phi_{\rho,m,T}$ is a first-order zero-chain. Before $m(T-1)$ sequential gradient queries, a zero-respecting method cannot reveal the terminal outer coordinates. The reduced scalar chain then supplies a constant gradient obstruction, so the full gradient remains bounded away from zero.

For vertical scale $\delta$ and horizontal scale $s$, define

$$
f(z)=\delta s^2\Phi_{\rho,m,T}(z/s),
\qquad
a:=\delta\rho.
$$

Choose $s=16\epsilon/a$ and $\delta=L/8$. The chain length and bridge length scale as

$$
T=\Theta\!\left(\frac{\Delta a}{\epsilon^2}\right),
\qquad
m=\Theta\!\left(\sqrt{\frac La}\right).
$$

Thus the number of hidden gradient queries is

$$
m(T-1)
=\Theta\!\left(
\frac{\Delta\sqrt{La}}{\epsilon^2}
\right).
$$

## Fractional Hölder profile

The quadratic bridges have constant Hessian and therefore disappear from Hessian differences. Only the scaled outer regularizers contribute. Since $\Upsilon''$ is both globally bounded and globally Lipschitz,

$$
|\Upsilon''(u)-\Upsilon''(v)|
\leq C\min\{1,|u-v|\}
\leq C|u-v|^q
$$

for every $q\in[0,1]$. The scaled hard instance therefore satisfies

$$
H_q(f)=\Theta(as^{-q})
=\Theta(a^{1+q}\epsilon^{-q})
\qquad\text{simultaneously for every }q\in[0,1].
$$

The matching lower estimate follows by comparing two points separated by exactly $s$ in one regularized outer coordinate, using the nonzero change of $\Upsilon''$ between the selected scalar inputs.

Substituting this profile into each branch of the Universal Heavy Ball upper bound gives

$$
\Delta\sqrt L\,
H_q(f)^{1/(2+2q)}
\epsilon^{-(4+3q)/(2+2q)}
=\Theta\!\left(
\frac{\Delta\sqrt{La}}{\epsilon^2}
\right)
$$

for every $q\in[0,1]$. Hence the infimum over $q$ cannot escape the hard instance.

To enforce the prescribed $\gamma$-Hölder constant, choose

$$
a=c_0\min\left\{L,(H\epsilon^\gamma)^{1/(1+\gamma)}\right\}
$$

for a sufficiently small numerical constant $c_0$. Substitution into the chain length yields the stated lower bound.

## Applicability to Universal Heavy Ball

Universal Heavy Ball forms iterates and velocities from previous vectors and queried gradients using scalar step sizes; its restart rules select previously generated iterates or averages and reset the velocity. Starting from zero, none of these operations can introduce a coordinate before the zero-chain gradient reveals it. The method is therefore zero-respecting on the construction above.

The same hard family can be extended from this specific method to all deterministic first-order algorithms through the standard resisting-oracle rotation argument, because the function class and Euclidean stationarity criterion are orthogonally invariant.

## Cleanup required

- State the exact Universal Heavy Ball parameter convention, including $\bar\ell$, $\alpha_{\rm HB}$, and $\beta_{\rm HB}$.
- Verify the support induction for every queried iterate and averaged point across both restart mechanisms.
- Track numerical constants in the smoothness budget, gap calibration, stationarity transfer, and floor operations defining $m$ and $T$.
- Separate the theorem for Universal Heavy Ball from the stronger rotated lower bound for arbitrary deterministic first-order methods.
- State the required dimension $d=(m+1)T+1$ and the admissible parameter regimes explicitly.
- Record the human verification procedure and reviewers.

## Provenance and references

- [Original AI-assisted proof discussion](https://chatgpt.com/share/6a97b46e-2dac-83e8-b02e-9d3c3a62b199)
- [Marumo and Takeda: Universal Heavy Ball](https://arxiv.org/abs/2303.01073)
- [Chen, Ji, and Zhang (2026), Section 3.3: nested chain for highly-smooth nonconvex problems](https://arxiv.org/abs/2511.22331)
- Project bibliography: [`references.bib`](references.bib)

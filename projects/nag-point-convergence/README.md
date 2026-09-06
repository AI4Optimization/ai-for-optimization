# Point convergence of Nesterov's accelerated gradient method

## Status

**Public preprint; AI-assisted proof.** Jang and Ryu resolve the longstanding point-convergence question for the classical Nesterov accelerated gradient method in finite-dimensional smooth convex optimization. The authors report extensive human filtering and verification of ChatGPT-generated arguments and take responsibility for the final proof.

## Result

Let $f:\mathbb R^n\to\mathbb R$ be convex and $L$-smooth with $\arg\min f\neq\varnothing$. Consider

$$
\begin{aligned}
x_{k+1}&=y_k-\frac1L\nabla f(y_k),\\
y_{k+1}&=x_{k+1}+\frac{t_k-1}{t_{k+1}}(x_{k+1}-x_k),
\end{aligned}
$$

initialized with $x_0=y_0$, where $t_0=1$, $t_k\to\infty$, and

$$
t_{k+1}^2-t_{k+1}\leq t_k^2.
$$

Then there exists $x_\infty\in\arg\min f$ such that

$$
x_k\to x_\infty,
\qquad
y_k\to x_\infty.
$$

Thus the acceleration of objective values does not come at the cost of iterate convergence for the standard critical NAG schedules, including the classical recursive choice and $t_k=(k+2)/2$.

## Setting and assumptions

- **Problem class:** unconstrained finite-dimensional convex minimization.
- **Regularity:** $f$ is differentiable with an $L$-Lipschitz gradient.
- **Existence:** the minimizer set is nonempty.
- **Oracle model:** the algorithm evaluates $\nabla f(y_k)$ through the standard exact first-order oracle used by NAG.
- **Algorithm:** classical two-sequence NAG with step size $1/L$ and the stated $t_k$ conditions.
- **Convergence criterion:** strong point convergence of both iterate sequences to the same minimizer, rather than only convergence of objective values.
- **Known rate:** the usual estimate $f(x_k)-f_\star=O(t_{k-1}^{-2})$ is used to show all cluster points are minimizers.

## Proof architecture

1. First study the critical Nesterov ODE $\ddot X+(3/t)\dot X+\nabla f(X)=0$.
2. For each minimizer $z$, use the standard energy
   $$
   \mathcal E_z(t)=t^2(f(X)-f_\star)+\frac12\|t\dot X+2(X-z)\|^2.
   $$
3. Compare two possible cluster points $z_1,z_2$. Subtracting $\mathcal E_{z_1}$ and $\mathcal E_{z_2}$ cancels the difficult common terms and yields a scalar linear ODE for the difference of squared distances.
4. Show that this distance difference has a limit; evaluating it along subsequences converging to $z_1$ and $z_2$ forces $z_1=z_2$.
5. Transfer the same idea to discrete time using NAG's equivalent $(x_k,y_k,z_k)$ representation and its standard energy $\mathcal E_k(x_\star)$.
6. Apply a scalar sequence lemma to the difference $\|x_k-x_\star\|^2-\|x_k-\widetilde x_\star\|^2$, obtaining uniqueness of cluster points and hence convergence. Finally, $\|y_k-x_k\|\to0$ gives the same limit for $y_k$.

## Verification record

- [x] The assumptions and point-convergence theorem are checked against arXiv v2.
- [x] Both the continuous-time and discrete-time arguments are presented in the public manuscript.
- [x] The authors describe their human verification and the AI-assisted discovery process.
- [x] A complete prompting example and transcript are included in the paper and linked below.
- [ ] The separate $r\in[1,3)$ extension claimed in an earlier version is invalid and must not be treated as verified.

## Limitations and open questions

- The theorem is finite-dimensional; a concurrent work extends related results to Hilbert spaces and FISTA.
- The result concerns the specified NAG schedules and exact gradients, not arbitrary accelerated methods or noisy oracles.
- For the ODE $\ddot X+(r/t)\dot X+\nabla f(X)=0$, the main theorem handles the critical case $r=3$. The paper explicitly retracts its earlier argument for $r\in[1,3)$; point convergence in that interval remains completely open.
- The authors report that many candidate AI arguments were incorrect, underscoring that the final result depends on careful human verification.

## Provenance and references

- **Clean write-up:** Uijeong Jang and Ernest K. Ryu, [*Point Convergence of Nesterov's Accelerated Gradient Method: An AI-Assisted Proof*](https://arxiv.org/abs/2510.23513), arXiv v2, 2026.
- **Reproduction transcript:** [ChatGPT share](https://chatgpt.com/share/6950b63e-1a58-8009-832b-48288fd60c30), reproduced in Appendix A of the paper.
- **AI system used:** GPT-5 Pro, as reported by the authors.
- **Concurrent work:** Boţ, Fadili, and Nguyen, [*The Iterates of Nesterov's Accelerated Algorithm Converge in the Critical Regimes*](https://arxiv.org/abs/2510.22715), 2025.

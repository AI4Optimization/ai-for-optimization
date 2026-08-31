# Halpern acceleration for high-order monotone variational inequalities

## Status

**Clean write-up; public preprint.** The proof has been organized into the paper linked below. The paper also includes the initial AI-generated algorithm and analysis as an appendix for provenance.

## AI use

The authors shortlisted open optimization problems and submitted them to the Apex Intelligence auto-research platform. As disclosed in the paper, Claude Opus 4.6 first found a proof of the nonaccelerated $O(T^{-(p-1)})$ Anchored Tensor Method rate. After the authors verified that result and conjectured the faster rate, GPT 5.6 Sol found the proof of the $\widetilde O(T^{-p})$ Halpern-accelerated rate. Lesi Chen, Xinliang Zhang, Chengchang Liu, and Jingzhao Zhang then verified the results and developed the cleaned paper. The [shared formalization discussion](https://chatgpt.com/share/6a6c372c-6efc-83e8-a378-c6aa1ea3b527) records part of the repair, comparison, and formal-write-up process.

The public preprint preserves the initial AI-generated algorithm and analysis in Appendix D. The main body is the human-verified, cleaned account.

## Previous best results

- For $p=2$, Monteiro and Svaiter's [Newton Proximal Extragradient method](https://doi.org/10.1137/11083085X) achieved the classical $O(T^{-3/2})$ rate for smooth monotone VIs.
- For general $p\ge2$, Bullins and Lai's [HigherOrderMirrorProx](https://arxiv.org/abs/2007.04528) and subsequent high-order MVI methods achieved $O(T^{-(p+1)/2})$ (or the corresponding $\widetilde O(\epsilon^{-2/(p+1)})$ oracle complexity, depending on the residual/gap convention).
- For the more structured convex-concave minimax subclass, Chen, Liu, Luo, and Zhang obtained a second-order rate equivalent to $\widetilde O(T^{-7/4})$ in [COLT 2025](https://proceedings.mlr.press/v291/chen25a.html); the full high-order development cited by the present paper gives $\widetilde O(T^{-(3p+1)/4})$.

These results left open whether the longstanding $O(T^{-(p+1)/2})$ exponent could be improved for a general monotone VI without using minimax structure.

## Current result

For a monotone variational inequality on a nonempty compact convex set $\mathcal X$, assume that $F$ has a Lipschitz $(p-1)$st derivative with constant $L_p$, where $p\ge 2$, and that the initial distance to a solution is at most $R$.

The Halpern-ATM method returns a last-iterate graph point with residual at most $\epsilon$ using

$$
\widetilde O_p\!\left(
1+\left(\frac{L_pR^p}{\epsilon}\right)^{1/p}
\right)
$$

$p$th-order oracle calls. Equivalently, its convergence rate is $\widetilde O(L_p/T^p)$. For $p=2$, the specialized Halpern-NPE method achieves $\widetilde O(T^{-2})$; for general $p$, the paper first develops an Anchored Tensor Method with rate $O(T^{-(p-1)})$ and then uses it inside an inexact Halpern iteration.

The result improves the previously known general-MVI high-order rate $O(T^{-(p+1)/2})$ for $p\ge2$ and matches the classical first-order extragradient exponent when $p=1$.

## Proof architecture

```text
large-step inexact Halpern iteration
             ↓
approximate resolvent subproblems with warm starts
             ↓
Anchored Tensor Method (ATM), or NPE when p = 2
             ↓
regularized high-order Taylor-model VI steps
```

The Halpern residual decays as $O(1/T)$. Because successive resolvent problems admit increasingly accurate warm starts, the resolvent scale can grow as $\eta=\Theta(T^{p-1}/L_p)$ while the summed subproblem cost remains nearly linear. Substituting this large scale into the residual bound yields the $\widetilde O(T^{-p})$ rate.

## Assumptions and oracle convention

- $\mathcal X\subseteq\mathbb R^d$ is nonempty, compact, and convex.
- $F:\mathcal X\to\mathbb R^d$ is continuous and monotone.
- A solution of $0\in F(x)+N_{\mathcal X}(x)$ exists.
- $D^{p-1}F$ is $L_p$-Lipschitz.
- One $p$th-order oracle query returns $F(x),DF(x),\ldots,D^{p-1}F(x)$.
- The cost convention treats solution of the regularized Taylor-model VI as an internal primitive; this convention is essential when comparing oracle bounds.
- The guarantee concerns a last-iterate residual/graph point, not only an ergodic gap.

## Provenance and references

- [Clean paper (arXiv:2608.08463)](https://arxiv.org/abs/2608.08463)
- [PDF](https://arxiv.org/pdf/2608.08463)
- [AI-assisted proof and formalization discussion](https://chatgpt.com/share/6a6c372c-6efc-83e8-a378-c6aa1ea3b527)
- Project bibliography: [`references.bib`](references.bib)

### Citation

```bibtex
@article{chen2026halpern,
  title   = {Halpern Iteration Achieves $\widetilde{\mathcal O}(\epsilon^{-1/p})$ $p$th-Order Oracle Complexity for Monotone Variational Inequalities},
  author  = {Chen, Lesi and Zhang, Xinliang and Wang, Hengyu and Liu, Chengchang and Chen, Yongchao and Zhang, Jingzhao},
  journal = {arXiv preprint arXiv:2608.08463},
  year    = {2026}
}
```

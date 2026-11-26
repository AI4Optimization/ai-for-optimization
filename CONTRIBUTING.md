# Contributing a bound

Create one directory under `projects/` using a short, descriptive kebab-case name. Start from `projects/_template/README.md` and keep the project self-contained.

Before marking a result as verified, record:

1. the theorem statement, including all quantifiers and edge cases;
2. the function/operator class and domain assumptions;
3. the oracle model and what operations are counted or free;
4. the output criterion (last iterate, average, gradient norm, residual, gap, and so on);
5. every hidden dependence in $O(\cdot)$ or $\widetilde O(\cdot)$;
6. the lower bound or previous best upper bound used for comparison;
7. a lemma-by-lemma verification record and the names of human reviewers;
8. the AI systems and prompts/traces that materially contributed to the result;
9. remaining gaps, restrictions, and failed generalizations.

Prefer a short project README that points to a separate manuscript over pasting a long raw transcript. Preserve raw AI traces by stable link or archival file, but do not present them as the canonical proof.

## Catalog placement and attribution

Add each project to the appropriate section of [`projects/README.md`](projects/README.md):

- **Research projects by repository contributors:** a repository contributor is an author or participated in the original proof search or verification. Use the author list and project provenance to establish this connection; citing a contributor's earlier work is insufficient. Keep independent results and external follow-ups attributed separately within the project.
- **External optimization results:** externally authored optimization or related sampling research, including benchmark resolutions and relevant methods. Record AI involvement only when supported by a disclosure, and distinguish the authors' verification from a repository proof audit.
- **Selected external AI mathematics results:** external AI mathematics work with a direct, substantial connection to foundational optimization questions. State that connection and link the original manuscript and any formalization scope.

Catalog placement, proof status, AI provenance, and benchmark eligibility are separate records. A public solution predating a benchmark entry is excluded from its success/failure counts. For formalized work, state the covered model and hypotheses, and distinguish reviewing the authors' scope statement from rebuilding or auditing the formal proof.

## Math formatting on GitHub

Use fenced `math` blocks for display equations. For inline expressions containing Markdown-sensitive characters, use a dollar sign and a backtick at each end, as in [GitHub's math-formatting documentation](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions):

````markdown
A stationarity criterion is $`\|\nabla f(x)\|\leq\epsilon`$.

```math
\Psi(x,w)=\max_{i\in[N]}\left\{h_i(x)-\rho b_i^\top w\right\}.
```
````

These forms preserve TeX commands such as `\!`, `\{`, `\|`, and matrix row breaks (`\\`), and prevent `*` or `_` from becoming Markdown emphasis. Keep the usual TeX backslashes inside the protected expressions; do not double them to compensate for Markdown escaping. In table cells, use `\lVert` and `\rVert` for norms so that pipe characters do not interfere with column separators.

Use `\mathrm{...}` for named operators, such as `\mathrm{dist}` or `\mathrm{Bernoulli}`. GitHub rejects the `operatorname` macro. Add explicit thin spaces between adjacent operator names, as in `\mathrm{cl}\,\mathrm{conv}`.

## Suggested layout

```text
projects/<project-name>/
├── README.md          # result, assumptions, status, and provenance
├── proof.md           # optional cleaned proof
├── notes/             # optional proof-search notes
└── references.bib     # optional project bibliography
```

## Verification principle

A model's agreement with another model is not independent verification. Verification should check the algebra, logical dependencies, parameter regimes, oracle accounting, and compatibility of imported lemmas with the stated assumptions.


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


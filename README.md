# AI for Optimization

An organized record of open problems and new bounds in optimization theory that may be solved with AI assistance and checked by human researchers.

The repository is organized by project rather than by model or chat. Each project records the mathematical claim, assumptions, oracle model, proof status, provenance, and the best available write-up. AI output is treated as proof-search material: a result is listed as proved only after verification.

## Organizers

Lesi Chen, Jiajin Li, Jianhao Ma, Suvrit Sra, Jingzhao Zhang, Peiyuan Zhang, and Xinliang Zhang.

## Cite this repository

A repository-level BibTeX entry is provided early so that problem curators, AI contributors, verifiers, and maintainers can receive timely credit. Update the access date to the version you used:

```bibtex
@misc{chen2026aiforoptimization,
  author       = {Chen, Lesi and Li, Jiajin and Ma, Jianhao and Sra, Suvrit and Zhang, Jingzhao and Zhang, Peiyuan and Zhang, Xinliang},
  title        = {AI for Optimization: Open Problems and AI-Assisted Bounds},
  year         = {2026},
  howpublished = {GitHub repository},
  url          = {https://github.com/AI4Optimization/ai-for-optimization},
  note         = {Accessed: YYYY-MM-DD}
}
```

The same entry is available as [`CITATION.bib`](CITATION.bib). When citing a particular result, please also cite its project README, original contributor, and associated paper or AI-response record.

## Background and curation criteria

This repository lists research-level open problems in optimization that may be solvable by AI. The organizers filter both proposed problems and claimed AI solutions according to three principles:

1. **Established setup.** A problem must concern an existing, interesting, and well-studied optimization setting with an open gap between upper and lower bounds. The benchmark is not intended for manufacturing new setups solely to create solvable questions.
2. **Standalone significance.** Closing or materially improving the stated gap should, through the improved bound alone, be capable of supporting a top-conference- or journal-level research contribution.
3. **Sanity-checked solutions.** Before a claimed AI response or clean write-up is listed as likely correct, the organizers check that the rate is significant, addresses the original problem, and does not obtain the improvement by adding new assumptions or changing the oracle or solution model. This check is a research sanity check, not a substitute for a full proof audit or peer review.

## Purpose

The repository is intended to serve several complementary roles:

1. **A home for standalone theory results.** A clean write-up should be assessable and citable for its mathematical result, independently of how the proof was discovered.
2. **A research benchmark for AI.** The open-problem list provides a changing but documented benchmark for tracking progress in AI systems' ability to solve research-level optimization problems.
3. **Reevaluating Optimization theory research.** We hope that the success and failure pattern in AI can provide insight so that we can reevaluate novelty and challenges of optimization theory study in AI-era.
4. **A path from promising AI output to papers.** An AI response that is likely correct but not yet cleaned up is open for the community to claim, verify fully, and develop into a paper. Any resulting work must properly attribute the original contributor who released the initial AI response, as well as subsequent contributors.
5. **Timely contribution records.** Commit history and maintenance records provide a flexible, timely way to document contributions to mathematical theory in an AI-assisted research era.

## Project catalog

Browse the [project catalog and open-problem benchmark](projects/README.md) for:

- AI-assisted results with their bounds, status, and detailed project write-ups;
- research-level open problems not yet solved by AI;
- the reusable template for proposing a new project.

## Repository conventions

Every project should contain a `README.md` with:

- a precise statement of the bound and its assumptions;
- the solution criterion and oracle-cost convention;
- a status label and verification record;
- links to the original AI trace and any cleaned manuscript;
- known limitations, open steps, and dependencies on prior results.

Status labels used here are:

- **exploration** - an unverified idea or partial proof;
- **candidate proof** - a complete-looking argument awaiting verification;
- **verified draft** - checked for correctness but not yet publication-ready;
- **clean write-up** - organized as a readable manuscript;
- **public preprint / published** - externally available scholarly version.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the project checklist and [projects/_template](projects/_template/) for a reusable skeleton.

## Scope and caution

The repository documents research results and their provenance; it is not itself a peer-review venue. Complexity claims are meaningful only together with their assumptions, solution criterion, allowed primitive operations, and hidden logarithmic or parameter-dependent factors.

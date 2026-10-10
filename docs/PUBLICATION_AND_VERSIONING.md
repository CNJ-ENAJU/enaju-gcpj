# Publication, research artifacts and documentation versions

## Protecting the publication record

The author reports that the article related to this project **has already been published** and has requested that it not be changed. This documentation update preserves the existing manuscripts, article PDFs/DOCX/HTML, figures, tables, scripts, original execution guide and historical logs as-is.

The repository includes [outputs-cobpit/](../outputs-cobpit/) with several COBPIT-oriented file variants, including files labelled `final` and `final-cego` (blind review). Those filenames are **internal artifact labels**, not independent verification of the publisher's version of record. The journal/conference bibliographic record, DOI or proceedings link has not been established from the tracked files in this update. Cite the publisher's actual publication when its bibliographic information is available.

## What changed on 2026-10-10

**Documentation only:**

- Replaced the repository landing README with an English-facing navigation page and a short Portuguese summary.
- Preserved the previously tracked README under [docs/archive/](archive/README_pre_documentation_2026-10-10.md).
- Added an evidence-linked [workflow guide](RESEARCH_WORKFLOW.md).
- Added a [LangGraph conceptual-parallels note](LANGGRAPH_CONCEPTUAL_PARALLELS.md), explicitly denying LangGraph implementation.
- Added an [evidence and limitations register](EVIDENCE_AND_LIMITATIONS.md).

**Not changed:**

- The article and every tracked `manuscripts/` and `outputs-cobpit/` item.
- Scripts under `scripts/`, the runner files and computational methods.
- Figures or CSV tables under `results/`.
- Existing `PESQUISA.md` and historical logs.
- Dataset records or any scientific finding.

## How to interpret versions

1. **Published article** — the authoritative publication is the publisher's version of record, not an automatically chosen GitHub output variant.
2. **Repository research artifacts** — historical code and output files are available to inspect, subject to the limitations registered [here](EVIDENCE_AND_LIMITATIONS.md).
3. **New explanatory documentation** — these guides are retrospective reading aids and do **not** document fresh calculations, completed human reviews or a corrected article.

This is a documentation intervention, **not a corrigendum, re-analysis or post-publication rewrite**. Any later scientific corrections would require a separate, transparent, appropriately authorized process.

## Research integrity in public communication

It is accurate to use this codebase as an example of structured bibliometric work and to draw *conceptual* lessons about inspectable workflow stages. It is not accurate to imply that LangGraph, agentic orchestration, checkpoints requiring formal human approval or independently verified end-to-end reproduction were part of the original method. This distinction applies to talks, posts and teaching material based on this repository.

# ENAJU-GCPJ | Research workflow and methodological transparency

**Public research repository** for a bibliometric mapping project concerning public-sector capacity development, judicial education and educational innovation.

This page is an entry point for **understanding the workflow**, not a claim that every possible validation was completed. The repository contains R scripts, methodological instructions, selected outputs, manuscripts and files prepared for the III COBPIT. It is maintained here as an inspectable example of how a multi-stage research process was structured.

> **Important distinctions**
>
> - The computational workflow is written primarily in **R**. **LangGraph was not used** in this repository.
> - Nodes, edges, persistent state and review points are discussed in the accompanying guide **only as conceptual parallels** with LangGraph, not as a claim of technical implementation.
> - Source code shows what was **implemented**; instructions show what was **recommended**; neither alone proves that every suggested human review was **performed**.
> - The author reports that the related article has been published. The specific publisher's version/DOI has not been independently established from the repository materials. Existing article files have **not** been edited as part of this documentation update.

## Start here

| Read | Purpose |
| --- | --- |
| [Research workflow](docs/RESEARCH_WORKFLOW.md) | Actual files, processing stages, dependencies and intended outputs |
| [Conceptual parallels with LangGraph](docs/LANGGRAPH_CONCEPTUAL_PARALLELS.md) | Precise analogy, including what the project **did not** implement |
| [Evidence and limitations](docs/EVIDENCE_AND_LIMITATIONS.md) | Traceable sources, observed discrepancies and limits of verification |
| [Publication and versioning](docs/PUBLICATION_AND_VERSIONING.md) | How the existing manuscript and output files are kept separate from updated explanatory documents |
| [Original Portuguese execution guide](PESQUISA.md) | Original instructions; consult alongside the limitations note because parts are historical |
| [Previous README (archived verbatim)](docs/archive/README_pre_documentation_2026-10-10.md) | Historical repository description retained for provenance |

## Workflow at a glance

The visible [runner](run_all.R) describes a sequence of R scripts, grouped here for readability:

| Phase | Repository evidence | Purpose |
| --- | --- | --- |
| Search design and collection | [00–05](scripts/) | Configure four thematic search groups and collect records from scholarly sources |
| Consolidation | [06_merge_deduplicate.R](scripts/06_merge_deduplicate.R) | Standardize source schemas and apply DOI/title-based deduplication |
| Screening and classification | [07_classify_corpora.R](scripts/07_classify_corpora.R) | Apply explicit text-based classification and eligibility rules; generate a PRISMA-style figure |
| Bibliometric analyses | [08–14](scripts/) | Descriptive analysis, research networks, topic modeling, institutional mapping and exploratory maturity index |
| Manuscript preparation | [99_render_article.R](scripts/99_render_article.R) and [COBPIT generator](scripts/generate_cobpit_article.py) | Produce article-format outputs from available results |

This is a **description of the code structure**, not a certificate that the whole pipeline runs end-to-end from a clean environment today.

## What this example can demonstrate

The source files make it possible to inspect where search terms, prioritization rules, deduplication keys, eligibility filters, thematic dictionaries, analytical methods and presentation choices enter the workflow. Intermediate RDS/CSV outputs and logs are designed or referenced, although many raw and processed datasets are **not versioned** in Git.

The project's Portuguese guide [PESQUISA.md](PESQUISA.md) recommends reviewing records without an assigned thematic category, interpreting automatically proposed topic labels and validating estimated country-level index scores. Those recommendations identify meaningful places for intellectual scrutiny; **the repository does not establish that each manual review occurred**.

For an accessible, evidence-linked explanation, see [Conceptual parallels with LangGraph](docs/LANGGRAPH_CONCEPTUAL_PARALLELS.md).

## Boundaries of this repository

- **No LangGraph dependency or graph runtime is documented here.** The analogy concerns workflow design, explicit dependencies and responsible research oversight.
- **Not a fully verified reproducibility package.** Collection requires external scholarly APIs/credentials, and raw/processed datasets are largely excluded from version control.
- **Known documentation/result discrepancies exist.** See [Evidence and limitations](docs/EVIDENCE_AND_LIMITATIONS.md), especially source counts and PRISMA labels, before reusing numerical findings.
- **No article or analytical files were corrected in this documentation update.** Original manuscripts, PDFs, scripts and existing result files remain as they were.

## Files and organization

- [scripts/](scripts/) — original R/Python workflow implementations
- [results/](results/) — selected tracked result figures and tables
- [logs/](logs/) — selected historical execution records
- [manuscripts/](manuscripts/) — manuscript source, references and templates
- [outputs-cobpit/](outputs-cobpit/) — tracked files prepared for COBPIT
- [docs/](docs/) — **new explanatory layer**, separated from the original research artifacts

### Resumo em português

Este repositório permite examinar a estrutura de um fluxo de pesquisa bibliométrica desenvolvido com scripts em R. A aproximação com o LangGraph é **conceitual**: etapas, dependências, dados intermediários e pontos em que o pesquisador deve examinar escolhas metodológicas. **O projeto não utilizou LangGraph.** A documentação acrescentada não altera o artigo publicado nem os resultados e scripts originais.

**Documentation update:** 2026-10-10. This update adds explanatory materials only; see [Publication and versioning](docs/PUBLICATION_AND_VERSIONING.md).

# Research workflow | ENAJU-GCPJ

## Scope and evidence standard

This document describes the workflow **as represented by repository code and instructions**. It deliberately separates:

- **Implemented** — behavior visible in source code;
- **Recommended** — checks or judgments proposed in the contemporaneous [Portuguese execution guide](../PESQUISA.md);
- **Verified execution** — runs or decisions evidenced by a recorded artifact. Merely having a script or output file does not prove that all documented checks were performed.

The focus is bibliometric mapping of institutional capacity development, education in the public sector, judicial education and educational innovation. Four corpora (A–D) and their search expressions are configured in [scripts/00_setup.R](../scripts/00_setup.R).

## Diagram: structure represented by the code

\`\`\`mermaid
flowchart TD
    A["00 — Search definitions and environment"] --> B["01–05 — Collect bibliographic records"]
    B --> C["06 — Normalize, merge and deduplicate"]
    C --> D["07 — Classify and apply eligibility rules"]
    D --> E["08–14 — Bibliometric / thematic analyses"]
    E --> F["99 — Quarto article generation"]
    D -. "Review recommended; execution not confirmed" .-> H["Inspect uncategorized records"]
    E -. "Review recommended; execution not confirmed" .-> I["Interpret LDA labels and index assumptions"]
\`\`\`

The diagram is an explanatory representation of a **sequential R workflow**, not a LangGraph program, event trace, or proof of human checkpoints having been completed.

## Stages and inspectable locations

### 1. Search design and collection

**Implemented sources and configuration:** [00_setup.R](../scripts/00_setup.R) and collection scripts for [Scopus](../scripts/01_collect_scopus.R), [OpenAlex](../scripts/02_collect_openalex.R), [Semantic Scholar](../scripts/03_collect_semantic_scholar.R), [Crossref](../scripts/04_collect_crossref.R) and [SciELO](../scripts/05_collect_scielo.R).

**Inspectable decisions:** thematic corpora and search strings, date bounds and API-specific retrieval logic. The collection scripts were written to save source-specific outputs in unversioned \`data/raw/\` directories. Existence of code for five sources **does not establish** that all five provided records to any particular article version.

**Execution evidence:** [selected logs](../logs/steps/) contain setup and an OpenAlex collection attempt. These selected logs do not independently verify an end-to-end execution of all source collectors.

### 2. Consolidation and duplicate resolution

**Implemented:** [06_merge_deduplicate.R](../scripts/06_merge_deduplicate.R) harmonizes fields from different sources, prioritizes sources and removes duplicates using normalized DOI and title handling. Specifically, the visible code removes exact DOI matches and then applies normalized-title matching to records without DOIs. It should **not** be described as a fully validated fuzzy-matching algorithm.

**Designed outputs:** corpus files and a deduplication report in \`data/processed/\`, which is excluded from version control.

**Research judgment:** different choices for identifier normalization, source priority or record consolidation could affect the retained corpus. The script exposes these choices for inspection; this document does not assert that a separate human adjudication of duplicates took place.

### 3. Thematic classification, eligibility and reporting

**Implemented:** [07_classify_corpora.R](../scripts/07_classify_corpora.R) uses dictionaries of nuclear terms against titles, abstracts and keywords. It assigns the labels \`A\`, \`B\`, \`C\`, \`D\`, \`multi_corpus\` or \`uncategorized\`. The script also marks some records ineligible when the title is absent/too short, the year falls outside the configured period, or the record is marked as retracted, and constructs PRISMA-labelled statistics and a diagram.

**Recommended (not independently verified as performed):** [PESQUISA.md](../PESQUISA.md) recommends examining \`uncategorized\` records before discarding them.

**Important caveat:** the saved \`corpus_eligible\` and the PRISMA counts do not apply the \`uncategorized\` category in exactly the same way. The field labelled \`duplicates\` is also calculated downstream of earlier deduplication, so it cannot safely be taken as a standalone count of actual duplicates removed. See [Evidence and limitations](EVIDENCE_AND_LIMITATIONS.md).

### 4. Bibliometric analysis and interpretation

**Implemented modules:** [08](../scripts/08_bibliometric_analysis.R) descriptive bibliometrics, [09](../scripts/09_cocitation_analysis.R) cocitation and collaboration, [10](../scripts/10_keyword_cooccurrence.R) keyword co-occurrence, [11](../scripts/11_bibliographic_coupling.R) bibliographic coupling, [12](../scripts/12_topic_modeling.R) LDA topic modeling, [13](../scripts/13_institutional_mapping.R) institutional mapping and [14](../scripts/14_maturity_index.R) an exploratory maturity index.

**Recommended (not independently verified as performed):** the original guide calls for manual interpretation of automatically suggested topic labels. The [topic script](../scripts/12_topic_modeling.R) labels its output explicitly as requiring manual review. The guide and [index script](../scripts/14_maturity_index.R) note that country-level scores are estimates/proxies requiring empirical validation.

**Research judgment:** labels, index weights and scores involve conceptual and evidentiary decisions beyond executing an algorithm. The code records some assumptions but is not evidence that validation occurred.

### 5. Manuscript generation and outputs

**Implemented entry points:** [99_render_article.R](../scripts/99_render_article.R) supports Quarto manuscript production from preceding objects; [generate_cobpit_article.py](../scripts/generate_cobpit_article.py) contains a separate COBPIT adaptation procedure.

**Tracked manuscript and presentation materials:** [manuscripts/](../manuscripts/) and [outputs-cobpit/](../outputs-cobpit/). Multiple document variants are present; filename alone does not establish which one matches the publisher's version of record.

**Reproducibility constraint:** [the COBPIT generation script](../scripts/generate_cobpit_article.py) points to a template filename that does not match the template presently tracked in [manuscripts/templates/](../manuscripts/templates/). This documentation update does not fix or run the generator.

## What remains with the researcher

At a minimum, the repository makes the following *classes of decisions* visible for a reader to question: search coverage, inclusion period, duplicate resolution, thematic dictionaries, treatment of ambiguous classifications, bibliometric interpretation, topic naming and the assumptions behind an index. Those are **inspectable decisions**, not a claim that AI made them, that every decision was manually validated, or that an agent autonomously routed the process.

For the LangGraph comparison, see [Conceptual parallels](LANGGRAPH_CONCEPTUAL_PARALLELS.md).

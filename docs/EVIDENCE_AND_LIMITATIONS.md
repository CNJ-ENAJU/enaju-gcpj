# Evidence map and verification limits

**Purpose:** distinguish repository facts from inferences and recommendations before presenting this project as an example of responsible research automation. This is a **documentation audit**, not an amendment to the published article.

**Review date:** 2026-10-10. This note reflects the tracked source and results examined at documentation time. No pipeline re-run, raw-data audit or independent publisher-version reconciliation was performed.

## What is directly supported

| Observation | Inspectable source | Status |
| --- | --- | --- |
| Sequential multi-stage R workflow is defined | [run_all.R](../run_all.R), [scripts/](../scripts/) | **Implemented in code** |
| Four thematic query groups are defined | [00_setup.R](../scripts/00_setup.R) | **Implemented in code** |
| Five scholarly collection adapters exist | [01–05 in scripts/](../scripts/) | **Code exists; contribution to final analytic sample not fully verified** |
| DOI and normalized-title handling for deduplication | [06_merge_deduplicate.R](../scripts/06_merge_deduplicate.R) | **Implemented in code** |
| Text-based thematic classification and eligibility flags | [07_classify_corpora.R](../scripts/07_classify_corpora.R) | **Implemented in code** |
| Suggested human review of uncategorized records | [PESQUISA.md](../PESQUISA.md) | **Documented recommendation; completion not verified** |
| Suggested human interpretation of LDA labels | [12_topic_modeling.R](../scripts/12_topic_modeling.R), [PESQUISA.md](../PESQUISA.md) | **Documented recommendation; completion not verified** |
| Index scores described as estimated proxies needing validation | [14_maturity_index.R](../scripts/14_maturity_index.R) | **Explicit limitation in source** |
| Selected logs and output files are tracked | [logs/](../logs/), [results/](../results/), [outputs-cobpit/](../outputs-cobpit/) | **Artifacts present; completeness not established** |
| LangGraph used to run the research | No LangGraph implementation established in reviewed files | **Do not claim** |
| Full manual adjudication and verified end-to-end execution | Not established by reviewed artifacts | **Do not claim** |

## Reconciliation issues visible in tracked files

The following items should be **flagged, not silently corrected**, because they may concern different processing or manuscript versions. No claim is made that the publisher's version contains these errors.

### 1. Source counts and what “Scopus” means

The tracked [results/tables/corpus_distribution.csv](../results/tables/corpus_distribution.csv) contains 9,394 records in its Scopus column and 16,171 in its OpenAlex column, summing to **25,565 across those column totals**. [results/tables/tab13_gap_analysis_corpus_C.csv](../results/tables/tab13_gap_analysis_corpus_C.csv) also reports **25,565** overall and **4,010** for corpus C. Some [manuscript source wording](../manuscripts/enaju-gcpj-article.qmd) describes **25,565 as Scopus records**.

These labels cannot be reconciled from the tracked processed corpus alone. The CSV columns are *reported counts*, not independently audited numbers of distinct eligible records. **Do not repeat them in a promotional post as a verified end-to-end count** unless reconciled against the actual article version and underlying datasets.

### 2. PRISMA counts and \`uncategorized\` status

In [07_classify_corpora.R](../scripts/07_classify_corpora.R), the file named \`corpus_eligible\` is saved based on title/year/retraction eligibility. The displayed PRISMA \`included\` total additionally subtracts entries classified as \`uncategorized\`; that same removal is **not** applied to the saved \`corpus_eligible\` object.

In addition, \`n_identified <- nrow(corpus_full)\` is evaluated **after** prior deduplication in [06_merge_deduplicate.R](../scripts/06_merge_deduplicate.R), while \`n_duplicates <- n_identified - nrow(eligible_df)\` counts exclusions at the next stage. Consequently, the label “duplicates removed” in the diagram is **not an independently reliable deduplication count**.

This identifies a discrepancy between labels and code paths; it does not demonstrate how the final published article calculated or reported its figures.

### 3. Historic guidance, current structure and template filenames

The [Portuguese guide](../PESQUISA.md) describes an earlier RAP/FGV-oriented workflow and file locations, including \`article/\` paths that are not consistent with the present [manuscripts/](../manuscripts/) and [outputs-cobpit/](../outputs-cobpit/) structure. The previously visible README has been retained in [archive](archive/README_pre_documentation_2026-10-10.md).

The [COBPIT Python generator](../scripts/generate_cobpit_article.py) refers to \`manuscripts/templates/template-tc-cobpit.docx\`, whereas the presently tracked [template folder](../manuscripts/templates/) contains a differently named template. Re-running that generator as written may require file/path reconciliation; it has **not** been run as part of this documentation update.

### 4. Evidence of executed workflows and manual decisions

The checked [logs/steps](../logs/steps/) show a setup and OpenAlex collection activity, but do not establish full execution of each stage or a complete chain of manual review decisions. Publicly available GitHub Actions workflow definitions are not equivalent to verified successful runs. No successful end-to-end GitHub Actions execution was verified during this review.

The repository's [gitignore](../.gitignore) excludes \`data/raw/\`, \`data/processed/\` and \`data/outputs/\`. Full reproduction therefore requires external retrieval, credentials where appropriate, and consistency checks; the tracked result figures and tables alone are not a complete frozen research dataset.

### 5. Estimated maturity index

The [index source](../scripts/14_maturity_index.R) embeds researcher-provided estimated country scores and warns that empirical validation is needed. This should be described as an exploratory or provisional analytical construct, **not a validated cross-country ranking**.

## Appropriate public use now

This repository can be cited to **show a real, inspectable architecture of a staged R bibliometric workflow**, with code for data collection, deduplication, classification, analysis and rendering, and with methodological decisions that a researcher ought to supervise.

It **cannot currently be cited as proof** that a LangGraph system was used, that every manual inspection was carried out, that the full pipeline is independently reproducible from Git, or that all numerical results are reconciled. A social-media discussion can focus on the **need for intellectual supervision** without treating this repository as a certified methodological benchmark.

**No original research files were modified to produce this note.**

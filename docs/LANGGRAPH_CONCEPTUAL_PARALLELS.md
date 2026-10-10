# LangGraph concepts and this R pipeline: an analogy, not an implementation

## The premise

The ENAJU-GCPJ repository contains a **multi-stage R research pipeline**. It **does not** contain a demonstrated LangGraph implementation. This guide draws a limited conceptual comparison with ideas that are often discussed in graph-oriented workflow design. It does **not** infer that LangGraph, LLM agents, autonomous decision loops, or a human-in-the-loop runtime were used.

The analogy is useful for explaining why scientific automation should expose *what happened at each stage* and *where a researcher must retain the ability to question methodological assumptions*.

## Evidence-based comparison

| Concept | What is visible in this repository | Boundary of the analogy |
| --- | --- | --- |
| **Nodes: discrete units of work** | [run_all.R](../run_all.R) enumerates individual scripts for collection, deduplication, classification, analysis and rendering. | R scripts are **not** LangGraph nodes. |
| **Edges: dependencies/order** | [run_all.R](../run_all.R) specifies execution order; several scripts read files written by earlier scripts, e.g. [07_classify_corpora.R](../scripts/07_classify_corpora.R) reads `corpus_full.rds`. | This is sequential orchestration and data dependency, **not** LangGraph graph routing. |
| **State: intermediate representations** | Scripts refer to RDS/CSV objects under `data/raw/` and `data/processed/` and to tracked tables in [results/](../results/). | These are persistent research artifacts, **not** LangGraph's shared graph state. Many intermediates are unversioned. |
| **Persistence and resumption** | The [original guide](../PESQUISA.md) describes caching and stage-by-stage re-execution; scripts reference cached inputs and outputs. | No LangGraph checkpointer or verified fault-tolerant resume semantics are demonstrated. |
| **Observability / audit trail** | Source code, selected [logs](../logs/) and [tables/figures](../results/) provide some process visibility. | Records are partial; no complete provenance/audit log for each research decision is evidenced. |
| **Human review** | The [guide](../PESQUISA.md) explicitly recommends manual examination of uncategorized records, LDA topic labels and estimated index scores. | A *recommendation* is not a documented human approval checkpoint; completion is not verified. |
| **Conditional execution** | The R runner includes error handling; collection code has API-specific fallbacks. | No evidence of a LangGraph-style conditional edge or agent-driven routing of research stages. |

## A concrete example: classification requires interpretation

In [scripts/07_classify_corpora.R](../scripts/07_classify_corpora.R), rules classify bibliographic records using terms found in title, abstract and keywords. The code explicitly provides `uncategorized` and `multi_corpus` outcomes. This makes a methodological issue inspectable: *a lexical match is not the same as a verified conceptual fit*.

The [research guide](../PESQUISA.md) recommends examining `uncategorized` records before exclusion. It does **not** provide a complete signed decision record showing that such a review occurred. The distinction matters: workflow design can **invite** critical review, but the presence of a review instruction is not evidence of its execution.

A second example appears in [scripts/12_topic_modeling.R](../scripts/12_topic_modeling.R), which writes suggested labels and explicitly says they should be reviewed manually. This illustrates how computational output and substantive interpretation are different operations; it does not demonstrate that a manual review was completed.

## What can accurately be said in a public post

> In an R-based bibliometric mapping project, I organized data collection, deduplication, classification, and analysis into explicit stages. Looking back at that work, I recognize conceptual parallels with nodes, edges, persistent state, and review points discussed in LangGraph. We did not use LangGraph. The experience illustrates why automation must remain open to methodological inspection, and why researchers need to question what happens between the initial data and the final result.

**Avoid claiming** that the pipeline used LangGraph; that it implemented autonomous agents; that it had formal human-approval gates; that the whole workflow was independently reproduced; or that every reported number and exclusion has been reconciled.

## Responsible framing

This analogy supports a discussion of **researcher responsibility and inspectability**. It does not by itself prove scientific validity, establish an AI contribution log, or show that any specific decision was made by AI. The repository is an example of **structured computational research**, with visible opportunities and limits for methodological oversight.

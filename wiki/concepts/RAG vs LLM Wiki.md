---
type: concept
title: "RAG vs LLM Wiki"
created: 2026-04-08
updated: 2026-04-08
sources: ["wiki/sources/llm-wiki-pattern"]
tags: [rag, knowledge-management, architecture, llm]
---

# RAG vs LLM Wiki

**One-line definition:** The core architectural distinction between re-deriving knowledge at query time (RAG) versus maintaining a pre-compiled synthesis layer (LLM Wiki).

## Explanation

**RAG (Retrieval-Augmented Generation):** Documents are chunked and indexed. At query time, relevant chunks are retrieved and fed to the LLM to generate an answer. Knowledge is re-derived on every question. No accumulation. Examples: NotebookLM, ChatGPT file uploads, most RAG pipelines.

**LLM Wiki:** When a new source arrives, the LLM reads it and integrates the knowledge into the existing wiki — updating entity pages, concept pages, noting contradictions. The synthesis happens once, at ingest time, and compounds. At query time, the LLM reads already-synthesized pages, not raw chunks.

| Dimension | RAG | LLM Wiki |
|-----------|-----|----------|
| When synthesis happens | Query time (every time) | Ingest time (once) |
| Cross-references | Re-derived on demand | Pre-built and maintained |
| Contradictions | Detected per-query | Flagged and tracked persistently |
| Scale ceiling | Embedding infrastructure needed | Index file works to ~100s of sources |
| Human maintenance | Low setup | Active curation of sources |

## Evidence & Examples

Drawn from: [[sources/llm-wiki-pattern]]

## Tensions & Contradictions

RAG has advantages at very large scale (millions of documents) where pre-compiling everything is impractical. LLM Wiki is better suited to personal/team knowledge bases with active curation. These are complementary approaches, not always competing ones.

## Related Concepts

[[LLM Wiki Pattern]], [[Compounding Knowledge Base]]

## Related Entities

[[Obsidian]]

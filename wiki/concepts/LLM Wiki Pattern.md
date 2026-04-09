---
type: concept
title: "LLM Wiki Pattern"
created: 2026-04-08
updated: 2026-04-08
sources: ["wiki/sources/llm-wiki-pattern"]
tags: [knowledge-management, methodology, llm, second-brain]
---

# LLM Wiki Pattern

**One-line definition:** A methodology where an LLM incrementally writes and maintains a persistent wiki from raw sources, rather than re-deriving knowledge at query time.

## Explanation

Instead of uploading documents for RAG retrieval, the LLM **compiles** knowledge into a structured wiki on ingest and keeps it current as new sources arrive. The wiki is the product — a persistent, interlinked collection of summary pages, entity pages, concept pages, and synthesis pages.

Three-layer architecture:
1. **Raw sources** — immutable documents you curate
2. **The wiki** — LLM-maintained markdown files (the synthesis layer)
3. **The schema** — the CLAUDE.md / AGENTS.md configuration that makes the LLM a disciplined maintainer

Three operations:
- **Ingest** — read a source, extract key info, update entity/concept pages, append to log
- **Query** — read the wiki, synthesize an answer, optionally file the result back as a synthesis page
- **Lint** — health-check for orphans, contradictions, stale claims, missing pages

The key property is **compounding**: each ingest makes the wiki richer, and the cross-references are already there when you need them.

## Evidence & Examples

- Drawn from: [[sources/llm-wiki-pattern]]
- Applied in: this vault — `CLAUDE.md` implements the schema, `wiki/` is the maintained layer

## Tensions & Contradictions

None yet. The pattern is new to this vault.

## Related Concepts

[[RAG vs LLM Wiki]], [[Compounding Knowledge Base]], [[Wiki Schema]], [[Memex]]

## Related Entities

[[Obsidian]], [[Vannevar Bush]]

---
type: source
title: "LLM Wiki"
created: 2026-04-08
source_file: "raw/LLM Wiki.md"
tags: [knowledge-management, llm, second-brain, obsidian, methodology]
---

# LLM Wiki

**Author/Origin:** Unknown (idea document, shared as a pattern)  
**Date:** circa 2026  
**Type:** methodology / pattern document

## Summary

LLM Wiki describes a pattern for building personal knowledge bases where an LLM incrementally writes and maintains a persistent wiki, rather than re-deriving knowledge from raw documents at query time (the standard RAG approach). The key insight is that the wiki becomes a **compounding artifact** — richer with every source added and every question asked — because the LLM does all the bookkeeping that humans abandon.

The human's role is curation and direction. The LLM's role is summarizing, cross-referencing, filing, flagging contradictions, and keeping pages current. In practice: Obsidian on one side, LLM agent on the other. The LLM edits the vault; the human browses it in real time.

The document is intentionally abstract — it describes the pattern and leaves domain-specific instantiation to the collaborating LLM agent.

## Key Points

- Standard RAG re-derives knowledge on every query; LLM Wiki compiles it once and keeps it current.
- The wiki sits between raw sources and the user — a maintained synthesis layer.
- The schema (CLAUDE.md / AGENTS.md) is what makes the LLM a disciplined maintainer, not a generic chatbot.
- Three operations: **ingest** (read source, update wiki), **query** (answer from wiki, optionally save result), **lint** (health-check for orphans, contradictions, gaps).
- `index.md` (content-oriented catalog) + `log.md` (chronological append-only record) are the two special navigation files.
- Good answers can be filed back into the wiki as synthesis pages — explorations compound just like ingested sources.
- The Memex analogy: Vannevar Bush's 1945 vision of a personal curated knowledge store with associative trails. LLMs solve the maintenance problem Bush couldn't.

## Entities

[[Vannevar Bush]], [[Obsidian]], [[qmd]], [[Tolkien Gateway]]

## Concepts

[[LLM Wiki Pattern]], [[RAG vs LLM Wiki]], [[Compounding Knowledge Base]], [[Wiki Schema]], [[Memex]]

## Connections

- This document is the founding source for this entire vault — it defines the methodology everything else here follows.
- Contrast with: [[RAG vs LLM Wiki]] — the core architectural distinction.
- The schema described here is implemented in `CLAUDE.md`.

## Notes

Intentionally abstract. Specific folder layout, page formats, and tooling are left to the collaborating LLM. This vault is one instantiation of the pattern.

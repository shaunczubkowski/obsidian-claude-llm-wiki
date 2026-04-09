---
type: entity
title: "Obsidian"
created: 2026-04-08
updated: 2026-04-08
sources: ["wiki/sources/llm-wiki-pattern"]
tags: [tool, note-taking, markdown, knowledge-management]
---

# Obsidian

**Type:** tool  
**One-line summary:** Local-first markdown note-taking app with a graph view, WikiLinks, and a plugin ecosystem — used as the IDE for this LLM Wiki vault.

## Overview

Obsidian is a markdown editor built around a local folder of `.md` files. Key features relevant to the LLM Wiki pattern:
- **WikiLinks** (`[[Page Name]]`) for internal linking — the LLM uses these for all cross-references
- **Graph view** — visualizes the connection structure of the wiki; the best way to see what's connected, what's a hub, what's an orphan
- **Canvas** — visual boards linking notes
- **Dataview plugin** — queries over YAML frontmatter; enables dynamic tables if the LLM adds structured metadata
- **Web Clipper** — browser extension that converts web articles to markdown for the `raw/` folder
- **Sync** — iCloud or Obsidian Sync for cross-device access

In the LLM Wiki workflow: Obsidian is the IDE, the LLM is the programmer, the wiki is the codebase.

## Key Facts

- Files are just markdown — no lock-in, works with git
- The `.obsidian/` folder holds plugin data and settings
- `workspace.json` is managed by Obsidian automatically — do not modify

## Appearances

[[sources/llm-wiki-pattern]]

## Related

[[LLM Wiki Pattern]], [[qmd]]

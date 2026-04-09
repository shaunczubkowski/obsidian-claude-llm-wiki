# Obsidian + Claude LLM Wiki Template

A template for a **persistent, compounding knowledge base** where Claude Code maintains the wiki and you curate the sources.

Instead of re-deriving knowledge every time you ask a question (like RAG), this system builds a structured wiki that grows richer with every source you add. Claude owns the `wiki/` layer — creating pages, maintaining cross-references, and keeping everything consistent. You drop sources into `raw/` and direct the analysis.

## How it works

```
raw/          ← you drop source documents here
wiki/
  sources/    ← Claude creates one summary page per source
  entities/   ← people, companies, tools, projects
  concepts/   ← ideas, frameworks, theories
  synthesis/  ← saved analyses and query answers
  index.md    ← full catalog of all wiki pages
  log.md      ← append-only operation history
```

Each ingest ends with a `git commit`, so any ingest is reversible with a single `git revert`.

## Prerequisites

- [Obsidian](https://obsidian.md) v1.12.7+ — open this folder as a vault
- [Claude Code](https://claude.ai/code) — run from this directory
- git — required for per-ingest commits and rollback

## Quick start

1. Clone or use this template on GitHub
2. Open the folder as an Obsidian vault
3. Open Claude Code in this directory: `claude`
4. Drop a document into `raw/` — any `.md`, article, transcript, etc.
5. Tell Claude: `ingest raw/<your-file>.md`
6. Claude will discuss key takeaways, build the wiki pages, and commit

A worked example is already in the wiki — the `LLM Wiki methodology` ingest — showing exactly what the output looks like.

## Rollback an ingest

Since every ingest is one git commit:

```bash
git log --oneline          # find the ingest commit
git revert <commit-hash>   # undo it atomically
```

## Workflows

Claude understands three commands:

- **Ingest** — `ingest raw/<file>` — summarize a source and build/update all wiki pages
- **Query** — ask any question — Claude reads the wiki and synthesizes an answer (optionally saved to `wiki/synthesis/`)
- **Lint** — `lint the wiki` — health check: orphan pages, missing links, contradictions, stale claims

Full workflow details are in `CLAUDE.md`.

## Customizing

The `CLAUDE.md` file contains the full agent schema — page formats, workflow steps, naming conventions, and quality rules. Edit it to adjust how Claude structures pages or what it prioritizes.

To rename the vault, rename this folder and update the iCloud path in `CLAUDE.md` if using Obsidian Sync.

## Credits

- **[Andrej Karpathy](https://github.com/karpathy)** — original idea and methodology, documented in [this gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- **[Nate Herk (@nateherk)](https://www.youtube.com/@nateherk)** — practical implementation walkthrough in [this video](https://www.youtube.com/watch?v=sboNwYmH3AY)

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

- [Obsidian](https://obsidian.md) v1.12.7+
- [Claude Code](https://claude.ai/code)
- git _(optional — only needed for per-ingest commits and rollback)_

**Recommended community plugin:** [Terminal](https://github.com/polyipseity/obsidian-terminal) — adds a terminal inside Obsidian so you can run Claude Code without switching to a separate app. Install it via **Settings → Community plugins → Browse → search "Terminal"**.

## Getting started

### Simple (no git required)

1. On this GitHub page, click **Code → Download ZIP**
2. Unzip the file to wherever you keep your notes
3. Open Obsidian → **Open folder as vault** → select the unzipped folder
4. Open a terminal in that folder and run `claude`
5. Drop a document into `raw/` and tell Claude: `ingest raw/<your-file>.md`

### Advanced (with git)

Using git gives you per-ingest commits and one-command rollback.

1. On this GitHub page, click **Use this template → Create a new repository** to get your own copy, then clone it:
   ```bash
   git clone https://github.com/<you>/<your-repo>.git
   cd <your-repo>
   ```
2. Open the folder as an Obsidian vault: **Obsidian → Open folder as vault**
3. Run Claude Code from that directory: `claude`
4. Drop a document into `raw/` and tell Claude: `ingest raw/<your-file>.md`
5. Claude builds the wiki pages and commits — repeat for each source

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

## Contributing

Contributions are welcome. The goal is to keep the template general-purpose and domain-agnostic.

**In scope:**
- Improvements to the `CLAUDE.md` schema (clearer instructions, better page formats, edge case handling)
- README and documentation clarity
- Better or additional example sources in `raw/`

**Out of scope:**
- Changes that make the template opinionated toward a specific topic or domain
- Adding dependencies or required plugins

To contribute: open an issue to discuss the change first, then submit a PR.

## Credits

- **[Andrej Karpathy](https://github.com/karpathy)** — original idea and methodology, documented in [this gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- **[Nate Herk (@nateherk)](https://www.youtube.com/@nateherk)** — practical implementation walkthrough in [this video](https://www.youtube.com/watch?v=sboNwYmH3AY)

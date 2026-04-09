# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

This is an Obsidian vault synced via iCloud. It is a personal knowledge base / notes workspace, not a software project.

## Working with This Vault

- Notes are Markdown (`.md`) files. Obsidian uses `[[WikiLinks]]` for internal links.
- Canvas files use the `.canvas` extension (JSON format).
- `.obsidian/` is gitignored — each user's Obsidian config is personal and generated automatically.

## obsidian-headless Tool (`ob`)

The `ob` CLI (obsidian-headless) handles authentication and account-level operations.

- `ob login` — show authenticated user

## Obsidian CLI (`obsidian`)

The `obsidian` CLI provides full programmatic access to the vault. Obsidian must be running for commands to work. Supports `vault=<name>` option to target a specific vault.

**Notes & Files**
```
obsidian read file=<name>             # Read file contents
obsidian create name=<name> content=<text>  # Create a new note
obsidian append file=<name> content=<text>  # Append to a note
obsidian prepend file=<name> content=<text> # Prepend to a note
obsidian delete file=<name>           # Move to trash
obsidian move file=<name> to=<path>   # Move/rename a file
obsidian rename file=<name> name=<new> # Rename a file
obsidian open file=<name>             # Open file in Obsidian
obsidian files                        # List all files
obsidian search query=<text>          # Search vault
```

**Daily Notes**
```
obsidian daily                        # Open today's daily note
obsidian daily:read                   # Read daily note contents
obsidian daily:append content=<text>  # Append to daily note
obsidian daily:path                   # Get daily note file path
```

**Metadata & Properties**
```
obsidian properties file=<name>       # List file properties
obsidian property:read name=<name> file=<name>   # Read a property
obsidian property:set name=<name> value=<v> file=<name>  # Set a property
obsidian tags                         # List all tags in vault
obsidian tags file=<name>             # Tags for a specific file
```

**Links & Graph**
```
obsidian links file=<name>            # Outgoing links from a file
obsidian backlinks file=<name>        # Backlinks to a file
obsidian orphans                      # Files with no incoming links
obsidian deadends                     # Files with no outgoing links
obsidian unresolved                   # Unresolved wikilinks
```

**Tasks**
```
obsidian tasks                        # List all tasks
obsidian tasks todo                   # Incomplete tasks only
obsidian tasks done                   # Completed tasks only
obsidian task ref=<path:line> toggle  # Toggle a task
```

**Vault Info**
```
obsidian vault                        # Show vault info
obsidian files total                  # File count
obsidian folders                      # List folders
obsidian tags counts                  # Tags with occurrence counts
obsidian recents                      # Recently opened files
```

**Templates**
```
obsidian templates                    # List templates
obsidian template:read name=<name>    # Read a template
```

**Sync & History**
```
obsidian sync:status                  # Show sync status
obsidian history file=<name>          # List file history versions
obsidian history:read file=<name> version=<n>  # Read a past version
```

---

# LLM Wiki Agent Schema

This vault is a **persistent, compounding second brain** maintained by the LLM. You (Claude) own the `wiki/` layer entirely — you create pages, update them, maintain cross-references, and keep everything consistent. The user curates sources and directs analysis. You do the bookkeeping.

## Folder Conventions

```
raw/                    # Source documents — immutable, Shaun writes here
  assets/               # Downloaded images (Obsidian attachment folder)

wiki/                   # LLM-maintained knowledge base — you write here
  index.md              # Catalog of all wiki pages (update on every ingest)
  log.md                # Append-only chronological log of all operations
  sources/              # One summary page per ingested source
  entities/             # Pages for people, places, companies, tools, projects
  concepts/             # Ideas, frameworks, theories, themes, models
  synthesis/            # Analyses, comparisons, answers to queries
```

**Rules:**
- Never modify files under `raw/` — read only.
- Always update `wiki/index.md` and append to `wiki/log.md` after any ingest, query that produces a saved page, or lint pass.
- Use `[[WikiLinks]]` for all internal cross-references — never plain text when linking to a page that exists.
- Prefer editing an existing page over creating a new one for the same entity/concept.

## Page Formats

### Source page — `wiki/sources/<slug>.md`
```markdown
---
type: source
title: "<Full Title>"
created: YYYY-MM-DD
source_file: "raw/<filename>"
tags: [tag1, tag2]
---

# <Title>

**Author/Origin:** ...  
**Date:** ...  
**Type:** article | paper | book | podcast | video | transcript | data

## Summary
2–4 paragraph synthesis of the key content.

## Key Points
- ...
- ...

## Entities
Links to entity pages mentioned: [[Entity Name]], ...

## Concepts
Links to concept pages: [[Concept Name]], ...

## Connections
How this source relates to or contradicts other wiki pages. Use [[links]].

## Notes
Anything notable about quality, gaps, or caveats.
```

### Entity page — `wiki/entities/<Name>.md`
```markdown
---
type: entity
title: "<Name>"
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: ["wiki/sources/slug1", "wiki/sources/slug2"]
tags: [person|company|tool|place|project, ...]
---

# <Name>

**Type:** person | company | tool | place | project  
**One-line summary:** ...

## Overview
Synthesized description drawn from all sources seen so far.

## Key Facts
- ...

## Appearances
Sources that mention this entity: [[source-slug]], ...

## Related
Cross-links to related entities and concepts.
```

### Concept page — `wiki/concepts/<Name>.md`
```markdown
---
type: concept
title: "<Name>"
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: ["wiki/sources/slug1"]
tags: [...]
---

# <Name>

**One-line definition:** ...

## Explanation
Full explanation synthesized from sources.

## Evidence & Examples
Drawn from: [[source-slug]], ...

## Tensions & Contradictions
Note any sources that conflict with each other here.

## Related Concepts
[[Concept A]], [[Concept B]], ...

## Related Entities
[[Entity Name]], ...
```

### Synthesis page — `wiki/synthesis/<slug>.md`
```markdown
---
type: synthesis
title: "<Query or Analysis Title>"
created: YYYY-MM-DD
sources_consulted: ["wiki/sources/...", ...]
tags: [...]
---

# <Title>

**Type:** comparison | analysis | answer | overview

## Result
The answer, comparison, or analysis.

## Sources
[[source-slug]], ...

## Caveats
Gaps, uncertainties, or things to verify.
```

## Workflows

### Ingest
When the user drops a new source into `raw/` and asks you to process it:

1. **Read** the source file fully.
2. **Discuss** key takeaways briefly before writing (unless Shaun says skip ahead).
3. **Create** `wiki/sources/<slug>.md` — full summary page.
4. **Update** existing entity pages (or create new ones) for all key entities.
5. **Update** existing concept pages (or create new ones) for all key concepts.
6. **Note contradictions** with existing wiki pages explicitly in the relevant pages.
7. **Update** `wiki/index.md` — add the new source and any new entity/concept pages.
8. **Append** to `wiki/log.md` — one entry per ingest (format below).
9. **Commit** — `git add -A && git commit -m "ingest: <title>"` so this ingest is atomically reversible via `git revert`.

A single source typically touches 5–15 wiki pages.

### Query
When the user asks a question:

1. Read `wiki/index.md` to identify relevant pages.
2. Read those pages.
3. Synthesize an answer with `[[citations]]` to source pages.
4. **Ask** whether to save the answer as a `wiki/synthesis/` page.
5. If yes: create the page, update index.md, append to log.md.

### Lint
When the user asks for a wiki health check:

1. Read `wiki/index.md` for a full inventory.
2. Check for: orphan pages (no inbound links), missing cross-references, contradictions between pages, stale claims, concepts mentioned but lacking their own page.
3. Report findings as a structured list.
4. Fix issues Shaun approves.
5. Append a lint entry to `wiki/log.md`.

## Index Format — `wiki/index.md`

```markdown
# Wiki Index

_Last updated: YYYY-MM-DD — N sources, N entities, N concepts, N synthesis_

## Sources
| Page | Summary | Date |
|------|---------|------|
| [[sources/slug]] | One-line summary | YYYY-MM-DD |

## Entities
| Page | Type | Summary |
|------|------|---------|
| [[entities/Name]] | person/company/tool | One-line summary |

## Concepts
| Page | Summary |
|------|---------|
| [[concepts/Name]] | One-line definition |

## Synthesis
| Page | Type | Summary |
|------|------|---------|
| [[synthesis/slug]] | comparison/analysis | One-line summary |
```

## Log Format — `wiki/log.md`

Each entry uses this header so the log is grep-parseable:

```
## [YYYY-MM-DD] <operation> | <title>
```

Operations: `ingest`, `query`, `lint`, `edit`

Example entry:
```markdown
## [2026-04-08] ingest | Article Title

- Created [[sources/article-slug]]
- Updated [[entities/Person Name]] — added background from this source
- Created [[concepts/New Concept]]
- 3 pages updated, 2 created
```

## Naming Conventions

- **Slugs:** lowercase, hyphens, no spaces — e.g. `the-attention-mechanism`
- **Entity pages:** Title Case matching the proper name — e.g. `Geoffrey Hinton`
- **Concept pages:** Title Case short phrase — e.g. `Transformer Architecture`
- **Synthesis pages:** descriptive slug — e.g. `gpt-vs-gemini-comparison`

## On Scope and Quality

- Write for permanence. Wiki pages are read in future sessions with no conversation context.
- Every claim should be traceable to a `[[source]]` link.
- When uncertain, say so in a **Note** or **Caveats** section — don't omit uncertainty.
- Prefer depth on key pages over shallow coverage of many pages.
- If a new source contradicts an existing page, update that page and flag the contradiction explicitly — do not silently overwrite.

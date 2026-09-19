# devtool

Cursor skill for finding **sparse developer-tool and infrastructure
seats**. Score occupancy, not pain. Empty seats are rare; most honest
leftovers are `file_on` a named host.

The skill name is **`devtool-finder`**, not `profinder`. `profinder`
was the parent repo and an older frontmatter `name:`. That label is
wrong here: this repo hunts developer-tool / infrastructure seats, and
[kirank55/profinder#12](https://github.com/kirank55/profinder/pull/12)
already renamed the skill to `devtool-finder` on the `devtool` branch.

## Use it

Open this repo in Cursor. The skill is at
`.cursor/skills/devtool-finder/` and is auto-discovered.

- Ask for a hunt in a **named stack + host** (`Playwright flake triage`,
  `Actions Runner Controller scale-sets`).
- Or type `/devtool-finder`.
- Broad prompts (`give me a SaaS idea`, `something to build`) emit an
  intake card and stop until stack and host are named nouns.

Do not use this skill for vertical-workflow SaaS seats on a named
system of record, or for people-search.

## Layout

```text
.cursor/skills/devtool-finder/
  SKILL.md
  references/          # loaded on demand by step
research/developer-tools.md   # category map; not loaded on a hunt
```

There is no repo-root `SKILL.md`. A root file named `profinder` would
steal discovery from this repo's actual job, the same way a leftover
profinder skill would have stolen [kirank55/niche](https://github.com/kirank55/niche).

## Fail-closed keeps

`as_company` Sparse/Greenfield requires `keep_gate: pass` (literal
quotes, four search classes, no occupied bundle). A tracker bullet
without an emitted candidate card is not a keep.

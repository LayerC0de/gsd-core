---
type: Fixed
pr: 3232
---
**`state add-decision` no longer records a decision against `[Phase ?]` when it could have known the phase** — omitting `--phase` wrote a literal `- [Phase ?]:` entry into STATE.md even though the frontmatter of the file being written carried `current_phase`, and because a decision entry is a permanent record the placeholder persisted, losing that decision's provenance unless a human noticed and hand-edited it. `cmdStateAddDecision` never consulted frontmatter, despite `cmdStatePruneDecisions` already reading `current_phase` behind a scalar guard a few thousand lines away in the same file. That read is now shared, so an omitted `--phase` resolves from frontmatter, an explicit `--phase` still wins, and `?` is retained only when no phase is resolvable anywhere — an unknown phase stays visibly unknown rather than being guessed. (#3231)

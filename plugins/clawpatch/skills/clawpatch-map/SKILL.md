---
name: clawpatch-map
description: Generate or refresh Clawpatch feature maps for a project. Use when the user asks to run clawpatch map, preview mapping with map --dry-run, inspect mapped features, refresh .clawpatch/features, or prepare features for Clawpatch review.
---

# Clawpatch Map

Map a project into Clawpatch feature records.

## Reference

Read `../clawpatch-setup/references/clawpatch.md` when
you need command details, state layout, or safety policy.

## Workflow

1. Start at the project root and inspect:
   - `git status --short`
   - `.clawpatch/config.json`
   - `.clawpatch/project.json`
   - existing `.clawpatch/features/`
2. If Clawpatch is not initialized, use `$clawpatch-setup` first.
3. If the user asks to preview, run `clawpatch map --dry-run`.
4. Otherwise run `clawpatch map`.
5. Summarize:
   - number of features generated or refreshed
   - stale or skipped features, if reported
   - relevant map warnings
   - the recommended next `clawpatch review` command

## Defaults

Treat `.clawpatch/features/` as generated, untracked mapper output. Do not
commit or manually edit feature records unless the user explicitly asks for a
repo policy change.

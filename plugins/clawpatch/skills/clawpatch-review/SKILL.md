---
name: clawpatch-review
description: Run Clawpatch AI code review over mapped project features. Use when the user asks to run clawpatch review, review mapped features, review since a branch or ref, review a feature scope, inspect Clawpatch review findings, or start the review step before reporting/fixing.
---

# Clawpatch Review

Run bounded Clawpatch review over mapped feature records.

## Reference

Read `../clawpatch-setup/references/clawpatch.md` when
you need command details, state layout, or safety policy.

## Workflow

1. Inspect project state:
   - `git status --short`
   - `.clawpatch/config.json`
   - `.clawpatch/features/`
2. Ensure feature records exist. If they are absent, run `$clawpatch-map` first
   unless the user asked for review-only diagnosis.
3. Run `clawpatch review`, preserving user scope such as:
   - `--since <ref>`
   - `--feature <feature-id>`
   - `--kind <kind>`
   - `--limit <n>`
4. Summarize:
   - review run id, if reported
   - number of findings
   - severity/category summary
   - report or findings path
   - recommended `clawpatch report` command

## Safety

Review is read-only for source files. Do not run fix actions from this skill
unless the user explicitly asks to move into `$clawpatch-fix`.

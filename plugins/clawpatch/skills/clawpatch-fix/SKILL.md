---
name: clawpatch-fix
description: Fix Clawpatch findings safely. Use when the user asks to run clawpatch fix, fix a specific Clawpatch finding, fix all open/actionable Clawpatch findings, continue Clawpatch remediation, or repair issues found by a Clawpatch review.
---

# Clawpatch Fix

Apply Clawpatch fixes for explicit findings or for the actionable open queue.

## Reference

Read `../clawpatch-setup/references/clawpatch.md` when
you need command details, state layout, or safety policy.

## Workflow

1. Inspect current state:
   - `git status --short`
   - `clawpatch status --json` when available
   - current report or `.clawpatch/findings/`
2. If the user named findings, run `clawpatch fix --finding <id>` for each one.
3. If no finding was specified, enumerate actionable open findings and fix them
   one at a time.
4. After each fix, inspect the result and record:
   - finding id
   - files changed
   - validation command results
   - patch attempt status
5. Recommend or run `$clawpatch-revalidate` when the fix phase completes.

## Safety

Respect Clawpatch dirty-worktree guards. Do not bypass them unless the user
explicitly asks and accepts the risk.

Do not commit, push, open PRs, or land changes. Do not broaden a fix beyond the
finding unless code evidence proves the failure class requires it.

---
name: clawpatch-automate
description: Run a conservative automated Clawpatch map-review-report-fix-revalidate workflow. Use in Codex automations or interactive sessions when the user wants a full Clawpatch review loop, automated remediation of actionable findings, revalidation, and a final report without committing, pushing, opening PRs, or landing changes.
---

# Clawpatch Automate

Run a conservative Clawpatch review-fix-revalidate loop.

## Reference

Read `../clawpatch-setup/references/clawpatch.md` before
running the automation. Use the real Clawpatch commands, not future-facing
spec-only commands.

## Workflow

1. Run setup checks:
   - verify or install `clawpatch`
   - run `clawpatch doctor`
   - stop on provider/auth/config failures
2. Run mapping:
   - `clawpatch map`
3. Run review:
   - `clawpatch review`
   - preserve user-provided scope such as `--since <ref>`
4. Generate the first report:
   - `clawpatch status --json`
   - `clawpatch report --format markdown`
   - use JSON too when structured selection is needed
5. Fix actionable findings:
   - use `clawpatch fix --finding <id>`
   - process one finding at a time
   - stop on dirty-worktree guards, failed validation, provider failures, or
     uncertain findings
6. Revalidate:
   - `clawpatch revalidate --all`
7. Generate the final report and summarize:
   - fixed findings
   - remaining open findings
   - uncertain findings
   - commands run
   - files changed

## Install Rule

If `clawpatch` is missing, install globally with `pnpm add -g clawpatch` when
`pnpm` is available. Otherwise use `npm install -g clawpatch`.

## Boundaries

Never auto-commit, push, open PRs, land changes, or use spec-only commands such
as `open-pr` or `land`.

For unattended Codex automations, make the final response useful when there is
nothing to do: include the review status, report path, and whether any findings
remain.

---
name: clawpatch-revalidate
description: Revalidate Clawpatch findings after fixes. Use when the user asks to run clawpatch revalidate, validate a fixed Clawpatch finding, recheck all fixed or pending findings, confirm whether Clawpatch fixes resolved findings, or update finding statuses after remediation.
---

# Clawpatch Revalidate

Run Clawpatch's second-pass validation on fixed findings.

## Reference

Read `../clawpatch-setup/references/clawpatch.md` when
you need command details, state layout, or safety policy.

## Workflow

1. Inspect current state:
   - `git status --short`
   - `clawpatch status --json` when available
   - current findings and patch attempts
2. If the user named a finding or patch target, run scoped revalidation for
   that target.
3. If the user did not specify a target, run `clawpatch revalidate --all`.
4. Summarize status transitions:
   - fixed
   - still open
   - false positive
   - uncertain or needs human review
5. Recommend `clawpatch report` for a final readable summary.

## Safety

Revalidation should not edit source files. If validation exposes a new source
change requirement, stop and move back to `$clawpatch-fix`.

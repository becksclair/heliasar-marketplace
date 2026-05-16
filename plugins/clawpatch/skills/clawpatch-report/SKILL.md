---
name: clawpatch-report
description: Generate and render Clawpatch reports. Use when the user asks for clawpatch report output, a formatted inline summary of Clawpatch findings, JSON or Markdown Clawpatch reports, review triage summaries, or a quick readable report after Clawpatch review/fix/revalidate.
---

# Clawpatch Report

Generate a Clawpatch report and render the important findings inline.

## Reference

Read `../clawpatch-setup/references/clawpatch.md` when
you need command details, state layout, or safety policy.

## Workflow

1. Inspect available findings and reports:
   - `clawpatch status --json` when available
   - `.clawpatch/findings/`
   - `.clawpatch/reports/`
2. Run `clawpatch report --format markdown` by default.
3. If structured extraction is needed, also run
   `clawpatch report --format json`.
4. Render a concise inline summary grouped by severity or status.

## Inline Report Format

Prefer this shape:

```markdown
## Clawpatch Report

### Critical
- `finding-id` - Feature name: short finding title.
  Status: open. Confidence: high.
  Evidence: one short sentence.
  Next: `clawpatch fix --finding finding-id`

### High
...
```

Keep the inline report reviewable. Include finding ids, feature names, status,
confidence, evidence summary, and suggested next command. Do not paste giant raw
reports unless the user asks for the full artifact.

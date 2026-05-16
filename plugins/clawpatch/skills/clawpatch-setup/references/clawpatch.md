# Clawpatch Reference

This reference captures the Clawpatch command surface and project-state policy
used by the `clawpatch-*` skills.

## Sources

- https://clawpatch.ai/
- https://github.com/openclaw/clawpatch/blob/main/docs/spec.md
- https://github.com/openclaw/clawpatch/blob/main/docs/initialization.md
- https://github.com/openclaw/clawpatch/blob/main/docs/configuration.md
- https://github.com/openclaw/clawpatch/blob/main/docs/feature-mapping.md
- https://github.com/openclaw/clawpatch/blob/main/docs/code-review.md
- https://github.com/openclaw/clawpatch/blob/main/docs/reporting.md
- https://github.com/openclaw/clawpatch/blob/main/docs/patching.md
- https://github.com/openclaw/clawpatch/blob/main/docs/validation.md
- https://github.com/openclaw/clawpatch/blob/main/docs/safety.md

## Prerequisites

- Node.js 22+
- Git 2.x
- local Codex CLI/provider credentials
- `clawpatch`

If `clawpatch` is missing, install it globally:

```bash
pnpm add -g clawpatch
```

If `pnpm` is unavailable:

```bash
npm install -g clawpatch
```

## Commands

- `clawpatch init`: create project-local state and detect project metadata,
  languages, frameworks, package managers, and likely validation commands.
- `clawpatch doctor`: check setup and provider/tool readiness.
- `clawpatch map`: generate durable feature records.
- `clawpatch map --dry-run`: preview mapping without editing source files.
- `clawpatch status`: inspect current findings and workflow state.
- `clawpatch status --json`: inspect state for automation.
- `clawpatch review`: review mapped features and write findings.
- `clawpatch review --since <ref>`: review changed scope for automation.
- `clawpatch report --format markdown`: generate readable report output.
- `clawpatch report --format json`: generate structured report output.
- `clawpatch fix --finding <findingId>`: apply a finding-scoped fix.
- `clawpatch revalidate --finding <findingId>`: revalidate one finding.
- `clawpatch revalidate --all`: revalidate the pending queue.

Do not use future-facing/spec-only commands such as `open-pr` or `land`.

## Project State

`clawpatch init` writes:

- `.clawpatch/project.json`
- `.clawpatch/config.json`

Feature mapping writes generated records under:

- `.clawpatch/features/`

Review, patching, reporting, and concurrency state use:

- `.clawpatch/runs/`
- `.clawpatch/findings/`
- `.clawpatch/patches/`
- `.clawpatch/reports/`
- `.clawpatch/locks/`

## Git Policy

Track by default:

- `.clawpatch/config.json`
- `.clawpatch/project.json`

Ignore by default:

```gitignore
.clawpatch/features/
.clawpatch/runs/
.clawpatch/findings/
.clawpatch/patches/
.clawpatch/reports/
.clawpatch/locks/
```

Rationale: config and project records are setup contract. Feature maps and
review artifacts are generated/runtime state that can churn and be regenerated.

## Config Commands

Populate `.clawpatch/config.json` with commands the project already uses.
Prefer manifest scripts, CI commands, and local repo guidance over generic
defaults.

Common command keys:

- `format`
- `typecheck`
- `lint`
- `test`

Clawpatch fix validation runs in this order when configured:

1. format
2. typecheck
3. lint
4. test

If a command cannot be discovered, leave it absent and report that gap.

## Safety

- `review`, `status`, `report`, `doctor`, and `map --dry-run` should not edit
  source files.
- `fix` is explicit and finding-scoped.
- `fix` is dirty-worktree guarded by default.
- Clawpatch does not commit, push, open PRs, or land changes.
- The skills must preserve those boundaries unless the user explicitly asks for
  a separate git operation.

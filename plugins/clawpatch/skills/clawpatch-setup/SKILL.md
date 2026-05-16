---
name: clawpatch-setup
description: Set up Clawpatch for a repository or project. Use when the user asks to install Clawpatch, initialize Clawpatch state, add .clawpatch gitignore entries, populate .clawpatch/config.json commands, run clawpatch doctor, or prepare a project for Clawpatch map/review/fix/revalidate workflows.
---

# Clawpatch Setup

Set up Clawpatch as project-local review infrastructure with a tracked setup
contract and ignored generated state.

## Reference

Read `references/clawpatch.md` before changing project files. It contains the
current command surface, state layout, gitignore policy, and safety rules.

## Workflow

1. Inspect the target project first:
   - `git status --short`
   - package/build manifests such as `package.json`, `pnpm-lock.yaml`,
     `bun.lockb`, `package-lock.json`, `pyproject.toml`, `Cargo.toml`,
     `go.mod`, `pom.xml`, `build.gradle`, `Makefile`, or CI configs
   - existing `.clawpatch/config.json`, `.clawpatch/project.json`, and
     `.gitignore`
2. Confirm prerequisites:
   - Node.js 22+
   - Git
   - local Codex CLI/provider readiness
   - `clawpatch`
3. If `clawpatch` is missing, install it globally:
   - prefer `pnpm add -g clawpatch` when `pnpm` is available
   - otherwise use `npm install -g clawpatch`
4. Run `clawpatch init` from the project root unless the user only asked for a
   dry setup plan.
5. Populate `.clawpatch/config.json` with the project's real commands for:
   - `format`
   - `typecheck`
   - `lint`
   - `test`
6. Add the default `.gitignore` entries if absent:

```gitignore
.clawpatch/features/
.clawpatch/runs/
.clawpatch/findings/
.clawpatch/patches/
.clawpatch/reports/
.clawpatch/locks/
```

7. Leave these setup files trackable:
   - `.clawpatch/config.json`
   - `.clawpatch/project.json`
8. Run `clawpatch doctor` and report any remaining setup issue.

## Command Selection

Prefer commands the project already uses in scripts, CI, or docs. Do not invent
heavy whole-repo checks when a project has an established changed-file or
focused validation command.

If a command is unknown, leave it absent rather than adding a fake command. Say
which command could not be discovered and where you looked.

## Safety

Do not commit, push, open PRs, or land changes. Setup may edit `.gitignore` and
`.clawpatch/config.json`; keep those edits explicit in the final summary.

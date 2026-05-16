# Clawpatch

Clawpatch bundles Codex skills for setting up Clawpatch in a repository and
running the feature-map, review, report, fix, revalidate, and conservative
automation workflows.

The plugin uses the local `clawpatch` CLI. If it is missing, `$clawpatch-setup`
and `$clawpatch-automate` prefer installing it globally with `pnpm`, then fall
back to `npm`.

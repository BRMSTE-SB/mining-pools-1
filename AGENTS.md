# AGENTS.md

## Cursor Cloud specific instructions

This repository is a **data repository**, not a runnable application. It holds the
Bitcoin mining pool definitions used by https://mempool.space/mining/pools.

- Source of truth: `pools-v2.json` (array of pool objects: `id`, `name`, `addresses`,
  `tags`, `link`). All content changes go here. `pools.json` is the legacy v1 file.
- See `README.md` for the contribution rules (how to add/rename a pool, slugs, etc.).

### Validate / "test" / "lint"
There is no build step and no package manager. The only tool needed is `jq`
(preinstalled on the VM). The CI workflow `.github/workflows/validate-json.yml`
runs exactly these two checks, which are the full validation suite:

- Duplicate pool-id check: `sh dupes.sh` (exits non-zero if any `id` repeats).
- JSON syntax check: `jq empty pools-v2.json`.

Run the same locally before committing:

```
sh dupes.sh
jq empty pools-v2.json
jq empty pools.json
```

Note: CI only validates `pools-v2.json`; validating `pools.json` too is a good
safety habit if you touch it.

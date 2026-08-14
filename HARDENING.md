<!-- markdownlint-disable -->

# Hardening Report: TryGhost--action-deploy-theme/v1.6.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **TryGhost--action-deploy-theme/v1.6.5** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/test.yml references GitHub Actions using mutable version tags instead of full 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the tag is moved to a different (potentially malicious) commit. Unpinned references: `actions/checkout@v4` (line 10) and `actions/setup-node@v3` (line 11).

Locations:

- `.github/workflows/test.yml:10`
- `.github/workflows/test.yml:11`

### missing-permissions (severity: medium)

Neither .github/workflows/test.yml nor .github/workflows/major.yml declares a top-level `permissions:` block, and no job within either file has a job-level `permissions:` block. Without explicit permissions, workflows inherit the default repository permissions (which may be `write-all` for private repos or broad for public repos), violating the principle of least privilege.

Locations:

- `.github/workflows/test.yml:1`
- `.github/workflows/major.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed test.yml: pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v3 → @3235b876344d2a9aa001b8d1453c930bba69e610 (with tag comments), and added top-level `permissions: {}`. Fixed major.yml: added top-level `permissions: {}` and job-level `permissions: contents: write` for the update-major job (which needs to push a tag update).


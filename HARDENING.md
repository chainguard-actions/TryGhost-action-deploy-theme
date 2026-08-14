<!-- markdownlint-disable -->

# Hardening Report: TryGhost--action-deploy-theme/v1.6.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **TryGhost--action-deploy-theme/v1.6.4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in test.yml use mutable tag refs instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved: `actions/checkout@v3` and `actions/setup-node@v3`.

Locations:

- `.github/workflows/test.yml:13`
- `.github/workflows/test.yml:14`

### missing-permissions (severity: medium)

Neither .github/workflows/major.yml nor .github/workflows/test.yml has a top-level `permissions:` key, and no job in either file defines its own `permissions:` block. Without explicit permissions, workflows run with the default (potentially write) token permissions, violating least-privilege.

Locations:

- `.github/workflows/major.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed test.yml: pinned actions/checkout@v3 → @f43a0e5ff2bd294095638e18286ca9a3d1956744 and actions/setup-node@v3 → @3235b876344d2a9aa001b8d1453c930bba69e610 (both with # v3 comments), and added top-level `permissions: contents: read`. Fixed major.yml: added top-level `permissions: contents: write` (required by the update-majorver action to push updated major version tags).


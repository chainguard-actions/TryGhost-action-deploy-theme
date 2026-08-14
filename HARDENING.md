<!-- markdownlint-disable -->

# Hardening Report: TryGhost--action-deploy-theme/v1.6.6

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **TryGhost--action-deploy-theme/v1.6.6** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in test.yml use mutable version tags instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved. Failing references: `actions/checkout@v4` and `actions/setup-node@v4`.

Locations:

- `.github/workflows/test.yml:13`
- `.github/workflows/test.yml:14`

### missing-permissions (severity: medium)

test.yml has no top-level `permissions:` key and the single job (`lint`) also has no `permissions:` key. The workflow is triggered by `pull_request` events, so the default broad permissions (read on most scopes, write on contents for push) apply. Explicit minimal permissions should be declared.

Locations:

- `.github/workflows/test.yml:1`

### missing-permissions (severity: medium)

major.yml has no top-level `permissions:` key and the single job (`update-major`) also has no `permissions:` key. This workflow runs on tag pushes and calls an external action that updates major version tags, so it likely needs write access to refs — but that should be declared explicitly with minimal scope rather than relying on broad defaults.

Locations:

- `.github/workflows/major.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed test.yml: pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 and actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020 (both with # v4 comments), and added top-level `permissions: contents: read`. Fixed major.yml: added top-level `permissions: contents: write` (required for the update-majorver action to push tag refs). The nowactions/update-majorver reference in major.yml was already pinned to a full SHA so no change was needed there.


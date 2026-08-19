<!-- markdownlint-disable -->

# Hardening Report: onramper--action-deploy-aws-static-site/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **onramper--action-deploy-aws-static-site/v1.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/checkout@v2` (a mutable version tag) in two steps instead of a full 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. Both the `build` job (line 14) and the `test` job (line 20) are affected.

Locations:

- `.github/workflows/test.yml:14`
- `.github/workflows/test.yml:20`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key, and neither the `build` job nor the `test` job defines its own `permissions:` block. Without explicit permissions, the workflow runs with the default (potentially broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/test.yml: (1) Pinned both `actions/checkout@v2` references to the full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` (with `# v2` comment) to prevent silent mutable-tag updates. (2) Added `permissions: {}` at the top level of the workflow to enforce least-privilege token access.


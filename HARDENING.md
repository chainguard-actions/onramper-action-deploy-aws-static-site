<!-- markdownlint-disable -->

# Hardening Report: onramper--action-deploy-aws-static-site/v3.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **onramper--action-deploy-aws-static-site/v3.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references `actions/checkout@v2`, which is pinned to a mutable tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. It should be replaced with the full SHA, e.g. `actions/checkout@ee0669bd1cc54295c223e0bb666b733df41de1c5 # v2`.

Locations:

- `.github/workflows/build-test.yml:10`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the single job (`all`) also has no `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be `write-all`). A minimal permissions block (e.g. `contents: read`) should be added at the top level or per-job level.

Locations:

- `.github/workflows/build-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `actions/checkout@v2` to its full immutable SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with a `# v2` comment for readability. 2. Added a top-level `permissions: contents: write` block — `contents: write` is the minimum required because the 'Publish artifacts' step performs a `git push` to update the v3.1 branch.


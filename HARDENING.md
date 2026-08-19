<!-- markdownlint-disable -->

# Hardening Report: onramper--action-deploy-aws-static-site/v3.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **onramper--action-deploy-aws-static-site/v3.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v2`, which is a mutable tag reference rather than a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. It should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/build-test.yml:10`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/build-test.yml` has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be `write-all`), granting broader access than necessary. A minimal permissions block (e.g. `permissions: contents: read`) should be added.

Locations:

- `.github/workflows/build-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `actions/checkout@v2` to its full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with the original tag preserved as a comment (`# v2`). 2. Added a top-level `permissions: contents: write` block — `contents: write` is the minimum needed because the workflow's 'Publish artifacts' step performs a `git push` back to the repository.


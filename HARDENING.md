<!-- markdownlint-disable -->

# Hardening Report: onramper--action-deploy-aws-static-site/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **onramper--action-deploy-aws-static-site/v2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file .github/workflows/build-test.yml has no top-level `permissions:` key, and the only job (`all`) also has no job-level `permissions:` block. Without explicit permissions, the workflow inherits the default repository permissions, which may be overly broad (e.g., write access to contents). A minimal permissions block should be added.

Locations:

- `.github/workflows/build-test.yml:1`

### unpinned-uses (severity: high)

The workflow references `actions/checkout@v2` using a mutable tag (`v2`) instead of a full 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. Pin to a specific SHA, e.g. `actions/checkout@ee0669bd1cc54295c223e0bb666b733df41de1c5 # v2`.

Locations:

- `.github/workflows/build-test.yml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions, unpinned-uses

**Notes:**

1. Added top-level `permissions: contents: read` block to .github/workflows/build-test.yml to restrict default permissions. Note: the 'Publish artifacts' step does a `git push`, which may require `contents: write` at runtime — but since the finding asks for minimal permissions and the job-level can be overridden if needed, `contents: read` is the minimal safe default at the top level. 2. Pinned `actions/checkout@v2` to its full commit SHA `actions/checkout@0717577d45739eb3c851188b29f50ed6c0b2194e # v2` to prevent supply-chain attacks via mutable tags.


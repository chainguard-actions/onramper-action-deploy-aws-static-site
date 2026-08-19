<!-- markdownlint-disable -->

# Hardening Report: onramper--action-deploy-aws-static-site/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **onramper--action-deploy-aws-static-site/v3.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references actions/checkout@v2, which uses a mutable tag instead of a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. It should be pinned to a full SHA, e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2.

Locations:

- `.github/workflows/build-test.yml:10`

### missing-permissions (severity: medium)

The workflow file .github/workflows/build-test.yml has no top-level permissions: key and the single job 'all' also has no job-level permissions: key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary (e.g. write access). Minimal explicit permissions should be declared.

Locations:

- `.github/workflows/build-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned actions/checkout@v2 to full SHA ee0669bd1cc54295c223e0bb666b733df41de1c5 with '# v2' comment for readability. 2. Added top-level 'permissions: contents: write' block — contents: write is the minimum needed because the workflow checks out the repo and also pushes build artifacts back to the v3 branch via 'git push origin HEAD:v3 -f'.


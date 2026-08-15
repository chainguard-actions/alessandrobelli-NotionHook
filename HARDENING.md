<!-- markdownlint-disable -->

# Hardening Report: alessandrobelli--NotionHook/1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **alessandrobelli--NotionHook/1.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references `alessandrobelli/NotionHook@testing`, where `testing` is a mutable branch name rather than a full 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file, creating a supply-chain risk.

Locations:

- `.github/workflows/main.yml:9`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/main.yml` has no top-level `permissions:` key and the single job `Notion_Hook_job` also has no `permissions:` key. Without explicit permissions, the workflow inherits the default repository permissions (which can be `write-all` for older repositories), granting unnecessarily broad access to the GITHUB_TOKEN. Minimal specific permissions should be declared.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1) Pinned `alessandrobelli/NotionHook@testing` to the full commit SHA `c0af1a795dfda948416e6ea9c6fc1bd716b0cc08` (main branch) — the `testing` branch no longer exists upstream, so `main` was used as the canonical ref. 2) Added `permissions: {}` at the top level of the workflow to explicitly deny all GITHUB_TOKEN permissions, since the workflow only uses repository secrets and requires no token access.


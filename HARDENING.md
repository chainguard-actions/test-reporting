<!-- markdownlint-disable -->

# Hardening Report: phoenix-actions--test-reporting/v14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **phoenix-actions--test-reporting/v14** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable version tags (@v4) instead of pinned full-length commit SHAs. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Affected references: `actions/checkout@v4`, `actions/upload-artifact@v4`.

Locations:

- `.github/workflows/ci.yml:16`
- `.github/workflows/ci.yml:23`
- `.github/workflows/dirty-laundry.yml:14`
- `.github/workflows/test-report.yml:14`

### missing-permissions (severity: medium)

The workflow file `dirty-laundry.yml` has no top-level `permissions:` key and its only job (`build-test`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal explicit `permissions:` block should be added.

Locations:

- `.github/workflows/dirty-laundry.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four unpinned action references by pinning to full commit SHAs: actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 (applied in ci.yml, dirty-laundry.yml, test-report.yml) and actions/upload-artifact@v4 → @ea165f8d65b6e75b540449e92b4886f43607fa02 (applied in ci.yml). Added `permissions: {}` top-level block to dirty-laundry.yml to explicitly restrict token permissions to none, since the workflow only runs npm commands and uses the local action.


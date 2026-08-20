<!-- markdownlint-disable -->

# Hardening Report: phoenix-actions--test-reporting/v13

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **phoenix-actions--test-reporting/v13** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow files reference GitHub Actions using mutable version tags instead of pinned full-length SHA commit hashes. This exposes the workflow to supply-chain attacks if the tag is moved to a different (potentially malicious) commit. Affected references: `actions/checkout@v4` and `actions/upload-artifact@v4`.

Locations:

- `.github/workflows/ci.yml:19`
- `.github/workflows/ci.yml:27`
- `.github/workflows/dirty-laundry.yml:14`
- `.github/workflows/test-report.yml:13`

### missing-permissions (severity: medium)

`dirty-laundry.yml` has no top-level `permissions:` key and its only job (`build-test`) also has no `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad.

Locations:

- `.github/workflows/dirty-laundry.yml:1`

### missing-permissions (severity: medium)

`test-report.yml` has no top-level `permissions:` key and its only job (`report`) also has no `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad.

Locations:

- `.github/workflows/test-report.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three findings across three workflow files:
1. ci.yml: Pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 and actions/upload-artifact@v4 → @ea165f8d65b6e75b540449e92b4886f43607fa02 (already had permissions block).
2. dirty-laundry.yml: Pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 and added top-level `permissions: checks: write`.
3. test-report.yml: Pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 and added top-level `permissions: checks: write`.


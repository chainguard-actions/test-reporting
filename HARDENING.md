<!-- markdownlint-disable -->

# Hardening Report: phoenix-actions--test-reporting/v16

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **phoenix-actions--test-reporting/v16** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable version tags instead of full 40-character SHA commit digests. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. Failing references: actions/checkout@v6 and actions/upload-artifact@v7.

Locations:

- `.github/workflows/ci-report.yml:17`
- `.github/workflows/ci.yml:17`
- `.github/workflows/ci.yml:26`
- `.github/workflows/dirty-laundry-report.yml:17`
- `.github/workflows/dirty-laundry.yml:14`

### missing-permissions (severity: medium)

The workflow file dirty-laundry.yml has no top-level `permissions:` key and its only job (build-test) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default repository token permissions, which may be overly broad (write access to contents, etc.).

Locations:

- `.github/workflows/dirty-laundry.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned all mutable action references to full SHA digests: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 (in ci-report.yml, ci.yml, dirty-laundry-report.yml, dirty-laundry.yml) and actions/upload-artifact@v7 → @043fb46d1a93c77aae656e7c1c64a875d1fc6a0a (in ci.yml). Added minimal `permissions: actions: read` top-level block to dirty-laundry.yml to replace the implicit overly-broad default permissions.


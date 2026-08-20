<!-- markdownlint-disable -->

# Hardening Report: phoenix-actions--test-reporting/v15

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **phoenix-actions--test-reporting/v15** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference external actions using mutable tag-based refs instead of full 40-character SHA commit hashes, making them vulnerable to supply-chain attacks if the tag is moved.

In ci.yml:
- `uses: actions/checkout@v4` (line ~19)
- `uses: actions/upload-artifact@v4` (line ~27)

In dirty-laundry.yml:
- `uses: actions/checkout@v4` (line ~13)

These should be pinned to their full SHA digests, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/ci.yml:19`
- `.github/workflows/ci.yml:27`
- `.github/workflows/dirty-laundry.yml:13`

### missing-permissions (severity: medium)

The workflow file `dirty-laundry.yml` has no top-level `permissions:` key and its only job (`build-test`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or on each job.

Locations:

- `.github/workflows/dirty-laundry.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned all three unpinned action references to full SHA digests: actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 in both ci.yml and dirty-laundry.yml; actions/upload-artifact@v4 → @ea165f8d65b6e75b540449e92b4886f43607fa02 in ci.yml. Added top-level `permissions: contents: read` to dirty-laundry.yml (ci.yml already had a permissions block with actions: read and checks: write).


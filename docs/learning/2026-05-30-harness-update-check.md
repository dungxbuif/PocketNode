# Harness Update Check

Date: 2026-05-30

## Task Summary

Checked whether the installed Harness files, database schema, and Rust CLI
binary in PocketNode needed an update.

## Skills Practiced

- Harness maintenance intake.
- Release checksum verification.
- Installer dry-run review.
- Durable trace and learning-note completion.

## What Was Learned

The safe update check for an installed Harness repo is not just running the
installer. `--merge --dry-run` shows missing files or shim refreshes without
writing, while the prebuilt Rust CLI needs a separate checksum comparison
because merge mode keeps an existing binary.

## Validation Evidence

- Ran `scripts/harness query matrix`.
- Ran `bash /private/tmp/install-harness.sh --directory /Users/dungxbuif/workspace/PocketNode --merge --refresh-agent-shim --dry-run --yes`.
- Compared the installed `scripts/bin/harness-cli` SHA-256 to the latest
  `harness-cli-macos-arm64` release checksum.
- Ran `scripts/harness migrate`, which reported schema version 1 already up to
  date.

## Reusable Guidance

For future Harness update checks, use dry-run merge for files, compare the
platform-specific release checksum for the CLI binary, and only run a real
installer update when the dry run or checksum proves drift.

---
name: remove-background-batch
description: Use when the user points at a folder and wants to process all images in batch.
---

# Remove Background (Batch)

Recursively or non-recursively processes multiple images in a directory. Runs `quick-rmbg` per file, with optional parallelism, and prints a summary of successes and failures.

## When to use

- Directory contains 2+ images to strip backgrounds from
- User wants one-shot processing without looping manually
- Output reporting and skip-logic (existing `-nobg.png` files) is useful

## Inputs to gather

- Directory path — folder containing images
- File glob (optional, default: `*.{jpg,jpeg,png,webp}`)
- Mode — `single` (single-pass, default) or `two-pass`
- Max parallel jobs (optional, default: 1 — set higher for multi-core if GPU supports batching)
- Force flag — skip existing `-nobg.png` siblings or re-process them (default: skip)

## Procedure

1. Verify `quick-rmbg` is on PATH.
2. Expand the glob pattern (or default) within the directory.
3. For each file: check if `<filename>-nobg.png` exists; skip unless `--force` is set.
4. Invoke `quick-rmbg $MODE "$file"` (where `$MODE` is empty or `--two-pass`), optionally in parallel (GNU parallel, xargs, or sequential loop).
5. Capture exit code and any stderr for each file.
6. Print per-file outcome: `<filename> … OK | FAIL <error>`.
7. Print summary: `X succeeded, Y failed, Z skipped`.

## Output / side effects

- Creates `<filename>-nobg.png` for each processed file in the same directory.
- Prints progress and summary to stdout.

## Safety / constraints

- Parallelism can overload GPU memory; default to 1 or ask before raising concurrency.
- Skips are reported; clarify if user wants to force re-process.

---
name: remove-background
description: Use when the user wants to remove the background from a single image file.
---

# Remove Background

Strips the background from a single image and writes the result as `<input>-nobg.png` next to the source file. Wraps the `quick-rmbg` CLI with a PATH check and outcome summary.

## When to use

- User points at a single image and wants the background gone
- First-pass removal before deciding if refinement is needed

## Inputs to gather

- Image path — JPEG, PNG, WebP, BMP, or TIFF file to process

## Procedure

1. Verify `quick-rmbg` is on PATH: `command -v quick-rmbg`. If missing, direct the user to the `install-rembg` skill.
2. Resolve the input path to an absolute path and verify it exists as a regular file.
3. Invoke: `quick-rmbg "$path"` — the CLI writes `<input>-nobg.png` to the same directory.
4. Monitor stdout/stderr for success or rembg error messages (e.g., model download, GPU driver issues).
5. If successful, report the output path and offer next steps (two-pass refinement, batch processing, Dolphin integration).

## Output / side effects

- Creates `<input>-nobg.png` next to the source.
- User sees progress updates and final path.

## Safety / constraints

- First run downloads the default model (~150 MB+); warn if bandwidth/storage is tight.
- GPU acceleration (ROCm/CUDA) is optional; CPU mode is slower but always works.

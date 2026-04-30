---
name: remove-background-two-pass
description: Use when single-pass leaves residue (hair, low-contrast edges) that needs cleanup.
---

# Remove Background (Two-Pass)

Runs background removal twice for cleaner edges and smoother alpha blending. The second pass often removes artifacts the first pass left behind.

## When to use

- Single-pass result has visible halos or stray pixels around fine details (hair, fur, thin branches)
- Default single-pass is too aggressive or too conservative on edge preservation

## Inputs to gather

- Image path — same JPEG/PNG/WebP/BMP/TIFF file to process again (typically the original, or feed the `-nobg.png` from a previous run)

## Procedure

1. Verify `quick-rmbg` is on PATH.
2. Resolve input path to absolute and verify it exists.
3. Invoke: `quick-rmbg --two-pass "$path"` — the CLI appends `-nobg.png` to the filename.
4. Monitor for completion and model-load messages.
5. Report the output path and quality comparison (if user previewed the single-pass version).

## Output / side effects

- Creates `<input>-nobg.png` (overwrites any previous single-pass output).
- Takes 2–3x longer than single-pass.

## Safety / constraints

- Two-pass compounds GPU memory use; may slow down or fail on low-VRAM GPUs.
- Idempotent on re-run (overwrites the previous output).

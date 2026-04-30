---
name: refine-mask-interactive
description: Use when the user wants to iteratively refine a mask until satisfied, re-running on the same image.
---

# Refine Mask (Interactive)

Wraps `quick-rmbg --infinite-hop` to let the user run background removal iteratively on the same image. Each run can use different settings (e.g., model, threshold) to dial in the perfect cutout.

## When to use

- Single or two-pass output is close but not perfect; user wants to tweak and re-run without leaving the workflow
- User wants to experiment with different models or config on a single image
- The upstream CLI's interactive loop is the right tool

## Inputs to gather

- Image path — source image (or previous `-nobg.png`) to refine
- (Optional) Max iterations to suggest or warn after

## Procedure

1. Verify `quick-rmbg` is on PATH.
2. Resolve input path to absolute and verify it exists.
3. Explain: `quick-rmbg --infinite-hop` will run removal, save output, ask if user wants another pass. Type `y` to refine, `n` to exit.
4. Invoke: `quick-rmbg --infinite-hop "$path"` and let the user interact (they control the loop).
5. After exit, report the final output path and iteration count (if the CLI prints it).

## Output / side effects

- Creates or overwrites `<input>-nobg.png` with the user's final choice.
- User drives the iteration loop via prompts.

## Safety / constraints

- This is an interactive CLI; user must stay engaged to answer prompts.
- Each iteration does a full GPU pass; many iterations can drain GPU memory.

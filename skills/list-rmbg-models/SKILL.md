---
name: list-rmbg-models
description: Use when the user wants to know which rembg models are available and which to pick for their use case.
---

# List Rembg Models

Displays available rembg models with descriptions of speed, quality, and best-use scenarios. Mostly a static reference; if available, also shows the output of `rembg list-models`.

## When to use

- User is considering switching models via `configure-rmbg`
- User wants to understand the trade-offs (speed vs. quality) before trying a model

## Inputs to gather

- None — this is a reference skill.

## Procedure

1. Print the built-in model guide (see below).
2. Optionally, run `rembg list-models` (if available on PATH) and append its output.
3. Remind user that model is set in `~/.config/quick-rmbg/config.json` and can be changed via `configure-rmbg`.

## Output / side effects

- Displays a reference table and optional CLI output.
- No files modified.

## Model reference

| Model | Speed | Quality | Best for | Notes |
|-------|-------|---------|----------|-------|
| `u2net` | Good | Good | General use | Default, balanced, well-tested |
| `u2netp` | Fast | Fair | Quick preview, mobile | Smaller/faster, slightly lower quality |
| `u2net_human_seg` | Good | Excellent | People, portraits | Specialized for human subjects |
| `silueta` | Good | Good | Alternative general | Similar to u2net, different training data |
| `isnet-general-use` | Slower | Excellent | High-quality general | Often best quality for varied subjects |
| `birefnet-general` | Slowest | Excellent | Best edges | Newer, slower, often best for fine details (hair, fur) |

## Safety / constraints

- Model selection is for preview/testing; user can revert to default in config if unhappy.
- Slower models require more GPU memory; CPU falls back gracefully.

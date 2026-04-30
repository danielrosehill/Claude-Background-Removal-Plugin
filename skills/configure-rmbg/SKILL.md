---
name: configure-rmbg
description: Use when the user wants to change default model, output naming, or GPU acceleration settings.
---

# Configure Rembg

View or edit `~/.config/quick-rmbg/config.json` to customize the `quick-rmbg` CLI's default behavior (model, output suffix, ROCm gfx_version for GPU).

## When to use

- User wants to switch default model (e.g., from `u2net` to `birefnet-general`)
- GPU acceleration is available and ROCm gfx_version needs tuning
- Output filename suffix should be customized (e.g., `-removed.png` instead of `-nobg.png`)

## Inputs to gather

- Action: `view` (show current config) or `edit` (change a setting)
- If edit: setting name (e.g., `model`, `output_suffix`, `rocm_gfx_version`) and new value

## Procedure

1. Ensure `~/.config/quick-rmbg/` exists: `mkdir -p ~/.config/quick-rmbg`.
2. Read the config file if it exists, or initialize an empty object if missing.
3. For `view`: print current settings (model, output_suffix, rocm_gfx_version if set) in a readable format.
4. For `edit`: 
   - Prompt for or accept the setting and new value.
   - Update the JSON object in memory.
   - Validate JSON before writing (jq or Python json module).
   - Write back to the file: `~/.config/quick-rmbg/config.json`.
5. Confirm the change and show the updated config.

## Output / side effects

- Reads and (optionally) updates `~/.config/quick-rmbg/config.json`.
- Changes apply to all future `quick-rmbg` invocations.

## Safety / constraints

- Invalid JSON will be rejected; no file corruption.
- User must understand what valid model names, output suffixes, and gfx_versions are (refer to `list-rmbg-models` for model names).

---
name: install-rembg
description: Use when quick-rmbg is not found on PATH and needs to be installed or upgraded.
---

# Install Rembg

Installs or upgrades the `quick-rmbg` CLI via `pipx` or `uv tool`, pulling the latest version from the upstream GitHub repository along with `rembg` and `onnxruntime` dependencies.

## When to use

- User tries to use a removal skill but `quick-rmbg` is not on PATH
- User wants to upgrade to a newer version of the CLI
- First-time setup of the plugin

## Inputs to gather

- None — tool selection is automatic (prefer `pipx`, fall back to `uv tool`).

## Procedure

1. Check if `quick-rmbg` already exists: `command -v quick-rmbg`. If found, ask user if they want to upgrade; skip if no.
2. Choose installer:
   - If `pipx` is available: `pipx install git+https://github.com/danielrosehill/Quick-RMBG.git`.
   - Else if `uv tool` is available: `uv tool install git+https://github.com/danielrosehill/Quick-RMBG.git`.
   - Else fail with instructions to install pipx or uv.
3. Monitor for completion (deps: `rembg`, `onnxruntime`).
4. Verify: `quick-rmbg --help`. Exit code 0 = success.
5. Warn: first invocation will download the default model (~150 MB+); bandwidth and storage permitting.
6. Note: GPU acceleration (ROCm/CUDA) is optional. The CLI will auto-detect. Manual config via `configure-rmbg` if needed.

## Output / side effects

- Installs `quick-rmbg` to pipx/uv's bin directory (usually on PATH).
- Downloads ~150 MB+ model on first run; may take 5–10 minutes depending on network.

## Safety / constraints

- Requires `pipx` or `uv` already installed.
- First-run downloads can be slow; warn user.
- GPU dependencies (ROCm/CUDA) must be pre-installed for hardware acceleration; CPU fallback is always available but slower.

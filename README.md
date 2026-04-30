# Background Removal

Remove image backgrounds via [`rembg`](https://github.com/danielgatis/rembg) — single-pass, two-pass cleanup, batch mode, and a KDE Dolphin right-click integration.

Built as a Claude Code wrapper around the [`Quick-RMBG`](https://github.com/danielrosehill/Quick-RMBG) CLI.

## Skills

- `remove-background` — single-pass removal of one image
- `remove-background-two-pass` — two passes for cleaner edges (hair, low-contrast backgrounds)
- `remove-background-batch` — process a directory of images
- `refine-mask-interactive` — iterative cleanup until satisfied
- `install-dolphin-action` — install KDE Dolphin right-click service menu
- `uninstall-dolphin-action` — remove the Dolphin service menu
- `configure-rmbg` — edit `~/.config/quick-rmbg/config.json` (default model, ROCm gfx_version, etc.)
- `install-rembg` — install / upgrade the underlying `quick-rmbg` CLI via pipx or uv
- `list-rmbg-models` — quick reference of available rembg models

## Installation

```bash
claude plugins install background-removal@danielrosehill
```

After install, run the `install-rembg` skill once to put `quick-rmbg` on PATH (heavy first-run: rembg downloads ~150 MB of model weights). On KDE, run `install-dolphin-action` to wire up right-click integration.

## Dependencies

- Python 3.10+, `pipx` or `uv`
- `rembg[cli]` (auto-installed by the install skill)
- KDE Plasma 6 (or 5) for the Dolphin integration — optional

## License

MIT

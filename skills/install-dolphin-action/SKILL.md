---
name: install-dolphin-action
description: Use when the user wants right-click "Remove background" in KDE Dolphin file manager.
---

# Install Dolphin Action

Installs the `quick-rmbg.desktop` service menu so users can right-click on images in Dolphin and remove backgrounds directly.

## When to use

- User runs KDE Plasma and wants Dolphin integration
- "Remove background" should appear in Dolphin's right-click context menu

## Inputs to gather

- None — the plugin provides the `.desktop` file.

## Procedure

1. Verify `quick-rmbg` is on PATH (the `.desktop` will fail if the CLI is missing).
2. Source the `.desktop` file from: `${CLAUDE_PLUGIN_ROOT}/assets/dolphin/quick-rmbg.desktop`.
3. Destination: `~/.local/share/kio/servicemenus/quick-rmbg.desktop`. Create the directory if missing: `mkdir -p ~/.local/share/kio/servicemenus`.
4. Copy the file: `cp "${CLAUDE_PLUGIN_ROOT}/assets/dolphin/quick-rmbg.desktop" ~/.local/share/kio/servicemenus/`.
5. Ensure it is executable: `chmod +x ~/.local/share/kio/servicemenus/quick-rmbg.desktop`.
6. Rebuild the KIO cache:
   - Try `kbuildsycoca6 2>/dev/null || kbuildsycoca5` (one or both may not be present).
   - If neither succeeds, notify user but do not fail; next Dolphin restart will use it.
7. Verify the action was installed by checking the file exists and reporting the path.

## Output / side effects

- Installs the service menu. User must restart Dolphin or log out/in to see the right-click option.
- Idempotent: diffing the file before copy can warn if a different version exists; proceed silently if identical.

## Safety / constraints

- Assumes MIME types: image/png;image/jpeg;image/webp;image/bmp;image/tiff.
- The `.desktop` file depends on `quick-rmbg` being on PATH; warn if not found.

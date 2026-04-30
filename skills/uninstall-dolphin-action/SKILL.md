---
name: uninstall-dolphin-action
description: Use when the user wants to remove the Dolphin right-click "Remove background" action.
---

# Uninstall Dolphin Action

Removes the KDE Dolphin service menu for background removal and rebuilds the KIO cache.

## When to use

- User no longer wants right-click integration in Dolphin
- Cleaning up or switching to a different background-removal solution

## Inputs to gather

- None — uninstall targets the known location.

## Procedure

1. Remove the service menu file: `rm -f ~/.local/share/kio/servicemenus/quick-rmbg.desktop`.
2. Verify removal.
3. Rebuild the KIO cache: `kbuildsycoca6 2>/dev/null || kbuildsycoca5`.
4. Report success (whether or not the file existed before removal).

## Output / side effects

- Deletes the `.desktop` file. User's Dolphin right-click menu no longer includes "Remove background".
- Idempotent: succeeds even if the file is already gone.

## Safety / constraints

- Non-destructive to images or other plugins.

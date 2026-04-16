---
name: usecomputer
description: Control your Windows Host from WSL2 — screenshot, click, type, press key.
version: 1.2.0
author: remorses
license: MIT
platforms: [macos, linux, windows]
metadata:
  hermes:
    tags: [automation, desktop, computer-use, screenshot, mouse, keyboard]
    usage: "Use this skill to control the Windows desktop from your WSL2 environment."
    fallback_for_tools: [browser_navigate]
---

Control your computer's desktop using a native Windows bridge from your WSL2 session.

## Prerequisites

- `usecomputer` installed on Windows (`npm install -g usecomputer` on the Windows host).
- WSL2 environment with Windows interop enabled (default).

## Quick Reference

| Action | Bridge Command |
| --- | --- |
| **Screenshot** | `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer screenshot ./shot.png --json` |
| **Click** | `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer click -x 400 -y 300 --coord-map "MAP"` |
| **Type** | `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer type "text"` |
| **Press Key** | `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer press "win"` |

## Procedure

> [!IMPORTANT]
> **YOU MUST USE THE FULL `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer` COMMAND.**
> This is a bridge that allows you to control the Windows Host from WSL2.
> Do NOT use any other command for desktop interaction.

1. **SEE THE SCREEN**: Capture a screenshot to see the Windows desktop:
   `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer screenshot ./screen.png --json`
2. **EXTRACT DATA**: Get the coordinates and the `coordMap` from the JSON output.
3. **CONTROL HOST**:
   - To click: `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer click -x X -y Y --coord-map "MAP"`
   - To open apps: `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer press "win"` then type the app name.

## Pitfalls

- **Paths**: Always use `./` for screenshot paths to ensure they save in your current WSL directory.
- **Modifiers**: Use `win` (not `meta` or `cmd`) for the Windows key when using this bridge.
- **CoordMap**: You MUST pass the `--coord-map` from the LATEST screenshot.

## Verification

1. Take a screenshot: `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer screenshot ./verify.png --json`
2. Confirm the host window is visible in the captured image.

---
name: usecomputer
description: Control the desktop — screenshot, click, type, scroll via native CLI
version: 1.1.0
author: remorses
license: MIT
platforms: [macos, linux, windows]
metadata:
  hermes:
    tags: [automation, desktop, computer-use, screenshot, mouse, keyboard]
    usage: "Use this skill for all desktop control tasks, including screenshots, mouse clicks, and keyboard input on the host machine."
    fallback_for_tools: [browser_navigate]
---

Control your computer's desktop using native CLI commands for screenshots and input.

## Prerequisites

- usecomputer CLI installed (`npm install -g usecomputer`)
- Desktop session with accessibility permissions (macOS) or X11/XWayland (Linux/WSL2 with `DISPLAY=:0`)

## When to Use

- When you need to interact with local apps or the OS GUI.
- When browser-based automation tools are blocked or insufficient.

## Quick Reference

| Action | Command |
| --- | --- |
| **Screenshot** | `usecomputer screenshot ./shot.png --json` |
| **Click** | `usecomputer click -x 400 -y 300 --coord-map "MAP"` |
| **Type** | `usecomputer type "hello text"` |
| **Press Key** | `usecomputer press "meta+r"` (Use `meta` for Windows key) |
| **Drag** | `usecomputer drag 400,300 600,400 --coord-map "MAP"` |
| **Scroll** | `usecomputer scroll --direction down --amount 5` |

## Procedure

> [!IMPORTANT]
> **YOU MUST USE THE `usecomputer` COMMAND FOR ALL ACTIONS.**
> Do NOT attempt to run Windows apps like `notepad` directly in the terminal.
> ALWAYS start by taking a screenshot to see current screen state.

1. **SEE THE SCREEN**: Run `usecomputer screenshot ./screen.png --json`
2. **GET COORDINATES**: Find the X/Y target and copy the `coordMap` string from the JSON output.
3. **CLICK/DRAG**: Use the coordinates and the `coordMap`: `usecomputer click -x 600 -y 400 --coord-map "MAP"`
4. **TYPE TEXT**: Click the target field first, then: `usecomputer type "your message"`
5. **LAUNCH APPS (Windows)**:
   - Run `usecomputer press "meta+r"` to open the Run dialog.
   - Run `usecomputer type "notepad"` then `usecomputer press "enter"`.
6. **VERIFY**: Always take a new screenshot to confirm your action worked.

## Pitfalls

- **WSL2 Interaction**: You MUST set `export DISPLAY=:0` in your terminal environment to control the Windows host.
- **Safety**: Do NOT click top-left (0-200, 0-200) as this triggers OS menus. 
- **CoordMap**: You MUST pass the `--coord-map` from the LATEST screenshot or clicks will fail.

## Verification

1. Run `usecomputer screenshot ./verify.png --json`
2. Confirm the expected UI state is visible in the captured image.

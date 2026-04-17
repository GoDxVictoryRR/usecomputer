---
name: usecomputer
description: Control your Windows Host from WSL2 — screenshot, click, type, press key, scroll, drag.
version: 2.0.0
author: remorses
license: MIT
platforms: [macos, linux, windows]
metadata:
  hermes:
    tags: [automation, desktop, computer-use, screenshot, mouse, keyboard]
    usage: "MANDATORY: Use ONLY the terminal for this skill. DO NOT USE EXECUTE_CODE OR BROWSER_NAVIGATE."
    fallback_for_tools: [browser_navigate]
---

# MANDATORY: DO NOT USE PYTHON OR BROWSER TOOLS FOR THIS SKILL.

Control your computer's desktop using a native Windows bridge. This tool provides full 1:1 parity with the Anthropic Computer Use standard.

## Procedure

> [!IMPORTANT]
> **YOU MUST USE THE WRAPPER SCRIPT AT THIS EXACT PATH:**
> `/home/hardi/usecomputer-wsl`
>
> 1. **To see the screen**: `/home/hardi/usecomputer-wsl screenshot ./shot.png --json`
> 2. **To click something**: 
>    - Perform step 1 to take a screenshot.
>    - Locate the coordinates in the image or ask the user.
>    - Run: `/home/hardi/usecomputer-wsl click -x <x> -y <y>`

## Quick Reference table for the AI (Full Capabilities)

| Action | Command |
| --- | --- |
| **Screenshot** | `/home/hardi/usecomputer-wsl screenshot ./shot.png --json` |
| **Left Click** | `/home/hardi/usecomputer-wsl click -x 500 -y 500` |
| **Right Click** | `/home/hardi/usecomputer-wsl click -x 500 -y 500 --button right` |
| **Double Click**| `/home/hardi/usecomputer-wsl click -x 500 -y 500 --count 2` |
| **Drag** | `/home/hardi/usecomputer-wsl drag 100,200 500,600` |
| **Scroll** | `/home/hardi/usecomputer-wsl scroll down 5` |
| **Type Text** | `/home/hardi/usecomputer-wsl type "Hello"` |
| **Press Key** | `/home/hardi/usecomputer-wsl press "enter"` (Use "ctrl+escape" for Start) |
| **List Windows**| `/home/hardi/usecomputer-wsl window list --json` |

## Pitfalls

- **NEVER FAKE JSON STRINGS**: Do not pass complex JSON or --coord-map to the click command. Keep it simple.
- **NEVER GUESS COORDINATES**: Do not make up x/y values. If you are unsure, ask the user: "Where is the [button name]? Please give me x/y coordinates."
- **DO NOT USE "win"**: Use "ctrl+escape" for the Start menu.
- **NEVER** use `execute_code` or `python`. Always use the bridge script.
>
> 1. **To see the screen**: `/home/hardi/usecomputer-wsl screenshot ./shot.png --json`
> 2. **To click something**: Perform step 1, find the x/y coordinates of your target, then run:
>    `/home/hardi/usecomputer-wsl click -x <x> -y <y> --coord-map "<coordMap_from_json>"`
> 3. **To open an App (Visual Click)**:
>    - `/home/hardi/usecomputer-wsl press "ctrl+escape"`
>    - `/home/hardi/usecomputer-wsl type "Epic Games Launcher"`
>    - `/home/hardi/usecomputer-wsl screenshot ./search.png --json`
>    - (Find the "Open" button in `search.png` and click it)

## Quick Reference table for the AI

| Action | Command |
| --- | --- |
| **Screenshot** | `/home/hardi/usecomputer-wsl screenshot ./shot.png --json` |
| **Click** | `/home/hardi/usecomputer-wsl click -x 500 -y 500 --coord-map "..."` |
| **Open Start** | `/home/hardi/usecomputer-wsl press "ctrl+escape"` |

## Pitfalls

- **DO NOT USE "win"**: Use "ctrl+escape" for the Start menu.
- **NEVER** use `execute_code`.
- **COORDINATES**: Always use the `--coord-map` returned by the `screenshot` command for accurate clicking.

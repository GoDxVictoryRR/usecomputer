---
name: usecomputer
description: Control your Windows Host from WSL2 — screenshot, click, type, press, scroll, drag, hover, debug-point, system-lists.
version: 2.2.0
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

Control your computer's desktop using a native Windows bridge. This tool provides full 100% parity with the `remorses/usecomputer` standard, executing all commands natively on the host.

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

## Comprehensive Command List (Explicit remorses/usecomputer API Parity)

| Action | Command / Granular Flags Supported |
| :--- | :--- |
| **Screenshot** | `screenshot [path] [--display id] [--window id] [--region <x,y,w,h>] [--annotate] [--json]` |
| **Debug Point**| `debug-point -x <x> -y <y> --output ./debug.png --json` (Validates click target visually) |
| **Click**      | `click -x <x> -y <y> [--button left/right/middle] [--count n] [--modifier shift/cmd/ctrl/alt]` |
| **Hover/Move** | `hover -x <x> -y <y>`  (Or `mouse move -x <x> -y <y>`) |
| **Drag**       | `drag <from_x,y> <to_x,y> [bezier_cp_x,y] [--button left/right/middle]` (Supports curves) |
| **Scroll**     | `scroll <up/down/left/right> [amount] [--at <x,y>]` |
| **Type Text**  | `type "Hello" [--delay ms] | Or via pipe: `cat file \| /home/hardi/usecomputer-wsl type --stdin [--chunk-size n] [--chunk-delay ms] [--max-length n]` |
| **Press Key**  | `press "ctrl+escape"` (Supports combos: "cmd+shift+p", "enter") `[--count n] [--delay ms]` |
| **Inspect Env**| `window list --json`, `display list --json`, `desktop list --windows --json` |
| **Mouse State**| `mouse position --json`, `mouse down [--button right]`, `mouse up` |

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

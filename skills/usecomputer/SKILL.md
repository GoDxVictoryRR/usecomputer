---
name: usecomputer
description: Control your Windows Host from WSL2 — screenshot, click, type, press key.
version: 1.4.0
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

Control your computer's desktop using a native Windows bridge.

## Procedure

> [!IMPORTANT]
> **YOU MUST USE THE WRAPPER SCRIPT IN THE PROJECT ROOT:**
> `./usecomputer-wsl`
>
> 1. To see the screen: `./usecomputer-wsl screenshot ./shot.png --json`
> 2. To open an App (e.g. Epic Games):
>    - `./usecomputer-wsl press "ctrl+escape"`
>    - `./usecomputer-wsl type "Epic Games"`
>    - `./usecomputer-wsl press "enter"`

## Quick Reference table for the AI

| Action | Command |
| --- | --- |
| **Open Start Menu** | `./usecomputer-wsl press "ctrl+escape"` |
| **Launch App** | `./usecomputer-wsl press "ctrl+escape"`, then type name, then press "enter" |

## Pitfalls

- **DO NOT USE "win"**: The "win" key code is unstable. Always use "ctrl+escape" to open the Windows Start menu.
- **NEVER** use `execute_code`.
- **NEVER** use `browser_navigate`.

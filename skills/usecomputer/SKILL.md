---
name: usecomputer
description: Control your Windows Host from WSL2 — screenshot, click, type, press key.
version: 1.3.0
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

Control your computer's desktop using a native Windows bridge from your WSL2 session. 

## Procedure

> [!IMPORTANT]
> **YOU MUST USE THE TERMINAL TOOL WITH THE FULL BRIDGE COMMAND:**
> `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer`
>
> 1. To see the screen: `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer screenshot ./shot.png --json`
> 2. To open an App (e.g. Epic Games):
>    - `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer press "ctrl+escape"`
>    - `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer type "Epic Games"`
>    - `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer press "enter"`

## Quick Reference table for the AI

| Action | Bridge Command |
| --- | --- |
| **Open Start Menu** | `/mnt/c/Windows/system32/cmd.exe /c npx usecomputer press "ctrl+escape"` |
| **Launch App** | `press "ctrl+escape"`, then type name, then press "enter" |

## Pitfalls

- **DO NOT USE "win"**: The "win" key code is unstable. Always use "ctrl+escape" to open the Windows Start menu.
- **NEVER** use `execute_code`. The tool is a CLI binary, not a python library.
- **NEVER** use `browser_navigate`. This is for web, not desktop.

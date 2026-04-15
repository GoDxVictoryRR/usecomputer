---
name: usecomputer
description: Control the desktop — screenshot, click, type, scroll via native CLI
version: 1.0.0
author: remorses
license: MIT
platforms: [macos, linux, windows]
metadata:
  hermes:
    tags: [automation, desktop, computer-use, screenshot, mouse, keyboard]
    fallback_for_tools: [browser_navigate]
---

Control your computer's desktop using native CLI commands for screenshots and input.

## Prerequisites

- usecomputer CLI installed (`npm install -g usecomputer`)
- Desktop session with accessibility permissions (macOS) or X11/XWayland (Linux/WSL2 with `DISPLAY=:0`)

## When to Use

- When you need to interact with local applications or the OS GUI
- When browser-based automation tools are blocked or insufficient
- When you need to take screenshots of specific app windows

## Quick Reference

| Action | Command |
| --- | --- |
| Screenshot | `usecomputer screenshot ./shot.png --json` |
| Click | `usecomputer click -x 400 -y 300 --coord-map "MAP"` |
| Type | `usecomputer type "hello text"` |
| Press Key | `usecomputer press "meta+r"` (Use `meta` for Windows key) |
| Drag | `usecomputer drag 400,300 600,400 --coord-map "MAP"` |
| Scroll | `usecomputer scroll --direction down --amount 5` |

## Procedure

1. Capture a screenshot of the current screen to locate elements: `usecomputer screenshot ./screen.png --json`
2. Extract the `coordMap` value from the JSON output of the screenshot command.
3. Identify the target coordinates on the screenshot image.
4. Perform pointer actions (click/drag) using the coordinates and the `coordMap`: `usecomputer click -x 600 -y 400 --coord-map "MAP"`
5. Type text into active fields using `usecomputer type "your message"`.
6. Use `usecomputer press "enter"` or shortcuts like `usecomputer press "cmd+v"` for keyboard control.
7. Verify the result of your action by taking a fresh screenshot.

## Pitfalls

- Clicking coordinates below 200,200 (like 0-50) can trigger OS menus or close windows.
- Always pass the exact `coordMap` from the most recent screenshot to ensure click accuracy.
- When running from WSL2 to control the Windows host, ensure `DISPLAY=:0` is set in the environment.
- Large text blocks should be piped via stdin if the terminal's argument buffer is small.

## Verification

1. Take a screenshot: `usecomputer screenshot ./verify.png --json`
2. Confirm the expected UI state or application change is visible in the captured image.

---
name: usecomputer
description: Control your Windows Host from WSL2 — screenshot, click, type, press, scroll, drag.
version: 4.0.0
author: remorses
license: MIT
platforms: [macos, linux, windows]
metadata:
  hermes:
    tags: [automation, desktop, computer-use, screenshot, mouse, keyboard]
    usage: "Use ONLY the terminal tool. DO NOT use vision_analyze, browser_navigate, execute_code, or Python."
    fallback_for_tools: [browser_navigate]
---

# usecomputer — Windows Desktop Automation via WSL2

Run all commands through the bridge:
```
/home/hardi/usecomputer-wsl <command> [args]
```

> **CRITICAL**: Do NOT use the `vision_analyze` tool. It will always time out.
> Use `window list --json` to locate windows, and standard UI conventions for button positions.

---

## RECIPE 1: Open an application

```bash
/home/hardi/usecomputer-wsl press "ctrl+escape"
sleep 1
/home/hardi/usecomputer-wsl type "AppName"
sleep 1
/home/hardi/usecomputer-wsl press "enter"
sleep 2
```

## RECIPE 2: Find a window's position on screen

```bash
/home/hardi/usecomputer-wsl window list --json
```

Output tells you:
- `x`, `y` — top-left corner of the window
- `width`, `height` — window size
- `title` — window title

**Calculate button positions from window geometry:**
- Title bar: `x + width/2`, `y + 15`
- Close button (X): `x + width - 20`, `y + 15`
- Center of window: `x + width/2`, `y + height/2`
- Top menu bar (File/Edit): `x + 30`, `y + 40`  (File is ~30px from left)

## RECIPE 3: Click inside a known window

```bash
# Get window info
/home/hardi/usecomputer-wsl window list --json
# Then click relative to window position
# e.g. if window is at x=200, y=100, width=800, height=600:
# File menu is at x=230 (200+30), y=140 (100+40)
/home/hardi/usecomputer-wsl click -x 230 -y 140
```

## RECIPE 4: Type text and save a file

```bash
# Type text
/home/hardi/usecomputer-wsl type "text to type"

# Save with Ctrl+S (saves to existing location)
/home/hardi/usecomputer-wsl press "ctrl+s"
sleep 1

# If file is new (Save As dialog appears), type the full path:
/home/hardi/usecomputer-wsl type "C:\\Users\\hardi\\Desktop\\test.txt"
/home/hardi/usecomputer-wsl press "enter"
```

## RECIPE 5: Close an application

```bash
/home/hardi/usecomputer-wsl press "alt+f4"
sleep 1
# If "Save changes?" dialog appears, press enter to confirm "Don't Save"
# or press tab to navigate to the correct button first
```

## RECIPE 6: Take a screenshot (for your own reference only)

```bash
/home/hardi/usecomputer-wsl screenshot /tmp/shot.png --json
```

> NOTE: Take a screenshot only when you need to verify something or show the user a result.
> Do NOT call `vision_analyze` on it — analyze the JSON metadata returned instead.
> The JSON output already tells you: captureWidth, captureHeight, desktopIndex.

---

## Standard Windows UI Coordinate Conventions

Use these offsets from the values in `window list --json`:

| UI Element | X offset from window.x | Y offset from window.y |
|:---|:---|:---|
| Menu bar (File) | `+30` | `+40` |
| Menu bar (Edit) | `+65` | `+40` |
| Menu bar (View) | `+100` | `+40` |
| Title bar center | `+width/2` | `+15` |
| Close button (X) | `+width-20` | `+15` |
| Text area center | `+width/2` | `+height/2` |
| OK / primary button (dialogs) | `+width-100` | `+height-40` |
| Cancel button (dialogs) | `+width-200` | `+height-40` |

---

## Full Command Reference

| Action | Command |
|:---|:---|
| **Screenshot** | `/home/hardi/usecomputer-wsl screenshot /tmp/shot.png --json` |
| **Left click** | `/home/hardi/usecomputer-wsl click -x <x> -y <y>` |
| **Right click** | `/home/hardi/usecomputer-wsl click -x <x> -y <y> --button right` |
| **Double click** | `/home/hardi/usecomputer-wsl click -x <x> -y <y> --count 2` |
| **Click+modifier** | `/home/hardi/usecomputer-wsl click -x <x> -y <y> --modifier shift` |
| **Type text** | `/home/hardi/usecomputer-wsl type "text"` |
| **Type (stdin)** | `echo "text" \| /home/hardi/usecomputer-wsl type --stdin` |
| **Press key** | `/home/hardi/usecomputer-wsl press "enter"` |
| **Key combo** | `/home/hardi/usecomputer-wsl press "ctrl+s"` |
| **Repeat key** | `/home/hardi/usecomputer-wsl press "down" --count 5` |
| **Scroll** | `/home/hardi/usecomputer-wsl scroll down 3` |
| **Drag** | `/home/hardi/usecomputer-wsl drag 100,200 500,600` |
| **Window list** | `/home/hardi/usecomputer-wsl window list --json` |
| **Mouse pos** | `/home/hardi/usecomputer-wsl mouse position --json` |

---

## ABSOLUTE RULES

1. Use `/home/hardi/usecomputer-wsl` — never call `npx usecomputer` directly
2. Save screenshots to `/tmp/` — never `/mnt/c/temp/` or other paths
3. **NEVER call `vision_analyze`** — it always times out
4. **NEVER press `win`, `win+r`, `ctrl+alt+delete`** — use `ctrl+escape` for Start menu
5. **NEVER guess coordinates blindly** — use `window list --json` to calculate position
6. Windows paths in dialogs use double backslashes: `C:\\Users\\hardi\\Desktop\\test.txt`

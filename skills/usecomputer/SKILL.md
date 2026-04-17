---
name: usecomputer
description: Control your Windows Host from WSL2 — screenshot, click, type, press, scroll, drag.
version: 3.0.0
author: remorses
license: MIT
platforms: [macos, linux, windows]
metadata:
  hermes:
    tags: [automation, desktop, computer-use, screenshot, mouse, keyboard]
    usage: "MANDATORY: Use ONLY the terminal tool. DO NOT use browser_navigate, execute_code, or Python."
    fallback_for_tools: [browser_navigate]
---

# usecomputer — Windows Desktop Automation via WSL2

You control the Windows desktop by running shell commands through this bridge:

```
/home/hardi/usecomputer-wsl <command> [args]
```

---

## STEP-BY-STEP RECIPES

### Recipe 1: Open any application
```bash
/home/hardi/usecomputer-wsl press "ctrl+escape"
sleep 1
/home/hardi/usecomputer-wsl type "Notepad"
sleep 1
/home/hardi/usecomputer-wsl press "enter"
sleep 2
```

### Recipe 2: Take a screenshot and analyze it
```bash
/home/hardi/usecomputer-wsl screenshot /tmp/shot.png --json
# Then analyze /tmp/shot.png using your vision to find coordinates
```

### Recipe 3: Click a button you can see in a screenshot
```bash
# First take a screenshot to find coords
/home/hardi/usecomputer-wsl screenshot /tmp/shot.png --json
# Then click using the x,y you identified from the image
/home/hardi/usecomputer-wsl click -x 800 -y 400
```

### Recipe 4: Type text into a focused window
```bash
/home/hardi/usecomputer-wsl type "Hello World"
# For large text, pipe it:
echo "big text here" | /home/hardi/usecomputer-wsl type --stdin
```

### Recipe 5: Save a file (Ctrl+S or Ctrl+Shift+S)
```bash
/home/hardi/usecomputer-wsl press "ctrl+s"
sleep 1
# If Save As dialog appears, type the filename and press enter
/home/hardi/usecomputer-wsl type "C:\\Users\\hardi\\Desktop\\test.txt"
/home/hardi/usecomputer-wsl press "enter"
```

### Recipe 6: Close an application
```bash
/home/hardi/usecomputer-wsl press "alt+f4"
```

---

## Full Command Reference

| Action | Command |
| :--- | :--- |
| **Screenshot** | `/home/hardi/usecomputer-wsl screenshot /tmp/shot.png --json` |
| **Click (left)** | `/home/hardi/usecomputer-wsl click -x <x> -y <y>` |
| **Right click** | `/home/hardi/usecomputer-wsl click -x <x> -y <y> --button right` |
| **Double click** | `/home/hardi/usecomputer-wsl click -x <x> -y <y> --count 2` |
| **Click+Modifier**| `/home/hardi/usecomputer-wsl click -x <x> -y <y> --modifier shift` |
| **Type text** | `/home/hardi/usecomputer-wsl type "text here"` |
| **Type (stdin)** | `echo "text" \| /home/hardi/usecomputer-wsl type --stdin` |
| **Press key** | `/home/hardi/usecomputer-wsl press "enter"` |
| **Key combo** | `/home/hardi/usecomputer-wsl press "ctrl+s"` |
| **Repeat key** | `/home/hardi/usecomputer-wsl press "down" --count 5` |
| **Scroll** | `/home/hardi/usecomputer-wsl scroll down 3` |
| **Scroll at pos** | `/home/hardi/usecomputer-wsl scroll down 3 --at 960,540` |
| **Drag** | `/home/hardi/usecomputer-wsl drag 100,200 500,600` |
| **Hover** | `/home/hardi/usecomputer-wsl hover -x <x> -y <y>` |
| **Mouse move** | `/home/hardi/usecomputer-wsl mouse move -x <x> -y <y>` |
| **Mouse pos** | `/home/hardi/usecomputer-wsl mouse position --json` |
| **Window list** | `/home/hardi/usecomputer-wsl window list --json` |
| **Display list** | `/home/hardi/usecomputer-wsl display list --json` |
| **Debug click** | `/home/hardi/usecomputer-wsl debug-point -x <x> -y <y> --output /tmp/debug.png` |

---

## STRICT RULES — NEVER BREAK THESE

1. **ALWAYS use `/home/hardi/usecomputer-wsl`** — never call `npx usecomputer` directly
2. **ALWAYS use `/tmp/` for screenshots** — never use `/mnt/c/temp/` or other paths
3. **NEVER use `browser_navigate` or `execute_code` or Python** for this skill
4. **NEVER press `win`, `win+r`, or `ctrl+alt+delete`** — use `ctrl+escape` to open Start
5. **NEVER guess coordinates** — always take a screenshot first and identify the real x,y
6. **NEVER pass `--coord-map`** to click — just use `-x` and `-y` directly
7. **For Windows paths in dialogs** — use backslashes: `C:\\Users\\hardi\\Desktop\\test.txt`

# Guide

## Overview

This repository now keeps the script in a separate source file: [Script.js](./Script.js).

Use the README for the fast path and this guide for a little more detail.

## Requirements

- Discord desktop app or browser session with "The Last Meadow" available
- Access to Developer Tools
- Permission to paste JavaScript into the console

## Setup

### Recommended: auto-update loader

This loader pulls the latest `Script.js` from the repository each time you run it:

```javascript
await fetch("https://cdn.jsdelivr.net/gh/xKhalidAlharbi/The-Last-Meadow-Ultimate-Auto-GUI-auto-farm-discord@main/Script.js")
  .then((response) => response.text())
  .then((code) => (0, eval)(code));
```

Use this when you want the repo version without manually recopying the full script.

### Manual setup

1. Refresh Discord with `Ctrl + R`.
2. Open Developer Tools with `Ctrl + Shift + I` or `F12`.
3. Open the `Console` tab.
4. Open [Script.js](./Script.js).
5. Copy the full file contents.
6. Paste into the console and press `Enter`.
7. Pick a language when the GUI opens.

## Controls

- `Adventure`: starts the Adventure loop.
- `Craft`: opens the craft game and solves the arrow sequence.
- `Battle`: enters battle mode automatically when ready.
- `Auto Heal`: handles the heal game flow.
- `Auto Defence`: helps with the defence sequence while the relevant game is active.
- `Auto Target`: keeps the target centered and clicks it automatically.
- `Wrong Game`: runs the rapid click helper for the alternate click-based game.
- `Adventure (ms)`: lower is faster for the Adventure loop.
- `Craft (ms)`: adjusts the timing used by the Craft loop.

## Updating

- If you use the loader snippet, rerun the snippet after `Ctrl + R`.
- If you use the manual copy method, copy the newest [Script.js](./Script.js) again after changes.
- The script already cleans up its previous GUI instance when loaded again.

## Troubleshooting

- If the GUI does not appear, refresh Discord and run the loader again.
- If buttons stop working after a Discord update, the selectors in [Script.js](./Script.js) may need to be refreshed.
- If a feature waits without acting, check whether the game is on the correct screen and not on a cooldown or out-of-resources popup.
- If remote loading fails, fall back to the manual copy method.

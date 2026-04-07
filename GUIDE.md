# Guide

## Overview

This repository now keeps the script in a separate source file: [Script.js](./Script.js).

Use the README for the fast path and this guide for a little more detail.

## Requirements

- Discord desktop app with "The Last Meadow" available
- Desktop Developer Tools enabled
- Permission to paste JavaScript into the console

## Setup

### Enable Discord desktop Developer Tools

If `Ctrl + Shift + I` already opens Developer Tools, skip this section.

1. Fully close Discord, including from the system tray.
2. Press `Win + R`.
3. Paste `%APPDATA%\discord` and press `Enter`.
4. Open `settings.json` in a text editor.
5. Add this setting inside the existing JSON object:

```json
"DANGEROUS_ENABLE_DEVTOOLS_ONLY_ENABLE_IF_YOU_KNOW_WHAT_YOURE_DOING": true
```

If the setting is not the first item in the file, add a comma before it so the JSON stays valid. Example:

```json
{
  "BACKGROUND_COLOR": "#202225",
  "DANGEROUS_ENABLE_DEVTOOLS_ONLY_ENABLE_IF_YOU_KNOW_WHAT_YOURE_DOING": true
}
```

6. Save `settings.json`.
7. Open Discord again.
8. Press `Ctrl + Shift + I`, then open the `Console` tab.

Discord **Developer Mode** in settings is different. It helps copy IDs, but it does not open the JavaScript console.

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
2. Open Developer Tools with `Ctrl + Shift + I`.
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
- `Stop All`: stops all running automation loops at once.
- `Reset Position`: moves the GUI back to the default screen position from the settings panel.
- `Transparency`: fades the GUI so more of the game remains visible.
- `Adventure (ms)`: lower is faster for the Adventure loop.
- `Craft (ms)`: adjusts the timing used by the Craft loop.
- The script remembers language, GUI position, minimized state, and speed slider values in local storage.

## Shortcuts

- `Ctrl + Alt + S`: Stop All
- `Ctrl + Alt + R`: Reset Position
- `Ctrl + Alt + M`: Minimize or expand the GUI
- `Ctrl + Alt + T`: Toggle Transparency Mode

## Console Helpers

- `stopMeadowScript()`: stops the script and removes the GUI.
- `stopMeadowAll()`: stops active automation without removing the GUI.
- `resetMeadowGUIPosition()`: moves the GUI back to its default position.
- `toggleMeadowTransparency()`: toggles Transparency Mode.

## Updating

- If you use the loader snippet, rerun the snippet after `Ctrl + R`.
- If you use the manual copy method, copy the newest [Script.js](./Script.js) again after changes.
- The script already cleans up its previous GUI instance when loaded again.

## Troubleshooting

- If the GUI does not appear, refresh Discord and run the loader again.
- If buttons stop working after a Discord update, the selectors in [Script.js](./Script.js) may need to be refreshed.
- If a feature waits without acting, check whether the game is on the correct screen and not on a cooldown or out-of-resources popup.
- If remote loading fails, fall back to the manual copy method.

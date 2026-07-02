# SFT DELTARUNE Debug Menu

![Mod Type](https://img.shields.io/badge/type-UMT%20CSX%20script-blue)
![Game](https://img.shields.io/badge/game-DELTARUNE-yellow)
![Status](https://img.shields.io/badge/status-beta-orange)
![Distribution](https://img.shields.io/badge/distribution-source%20only-green)

**SFT DELTARUNE Debug Menu** is a source-only UndertaleModTool `.csx` script that injects a custom in-game debugging menu into the currently opened DELTARUNE chapter data file.

The goal is to turn the basic pre-made UMT room selector idea into a bigger menu-driven debugging mod with room warping, player tools, visual/collision tools, sound testing, sprite viewing, runtime info, and object browsing.

> This project is not affiliated with, endorsed by, or sponsored by Toby Fox, 8-4, Fangamer, UndertaleModTool, or the official DELTARUNE team.

---

## Important Distribution Rule

This repo should only contain the `.csx` script source and documentation.

Do **not** upload or distribute:

- DELTARUNE game files
- Modified `data.win` files
- Patched chapter data files
- Extracted official sprites, music, SFX, fonts, rooms, or other assets
- Full game folders

Users should run the script themselves on their own legally obtained copy of the game.

---

## Current Version

**Latest script:** `DELTARUNE_Debug_Menu_v4.csx`

### v4 focus

v4 keeps the working v3 feature set, but adds a UI font/alignment fix for rooms where the debug menu text could appear as broken symbols or scattered characters.

The issue happened because some rooms can leave GameMaker's draw font or text alignment in a weird state before the debug menu's Draw GUI event runs. v4 now creates a readable font and forces left/top text alignment before drawing the menu.

---

## Screenshots

Add your screenshots here after testing.

Recommended paths:

```text
docs/screenshots/main-menu.png
docs/screenshots/room-select.png
docs/screenshots/sound-test.png
docs/screenshots/sprite-viewer.png
docs/screenshots/collision-tools.png
```

Example layout:

```md
![Main Menu](docs/screenshots/main-menu.png)
![Room Select](docs/screenshots/room-select.png)
![Sound Test](docs/screenshots/sound-test.png)
```

---

## Features

### Main Menu

The mod uses a full in-game menu instead of a pile of separate hotkeys.

The only global shortcut is:

| Key | Action |
| --- | --- |
| `F3` | Open or close the debug menu |

Everything else is controlled inside menu categories.

---

### Room Select

The Room Select page lists rooms from the currently patched chapter.

Features:

- Search room names by typing.
- Scroll results with Up and Down.
- Press Enter to warp to the selected room.
- Shows the current room name and room index.
- Works per chapter because the room list is generated from the currently opened data file.

Notes:

- This does not load rooms from other chapters.
- To use the mod on another chapter, run the `.csx` script on that chapter's data file too.
- Some rooms may expect story flags, global variables, or previous setup code. Warping directly into those rooms can sometimes cause odd behavior.

---

### Player / Movement Tools

The Player / Movement category provides basic player testing tools.

Included options:

- Toggle no-clip.
- Increase no-clip movement speed.
- Decrease no-clip movement speed.
- Teleport the player to the mouse position.
- Reload the current room.

No-clip controls while the menu is closed:

| Key | Action |
| --- | --- |
| Arrow keys | Move player |
| `W`, `A`, `S`, `D` | Move player |
| `Shift` | Move faster while no-clipping |

Player detection is generic. The script tries to find common player object names such as `obj_mainchara`, `obj_player`, `obj_kris`, and similar names. This should work in many cases, but some rooms or chapters may use different objects.

---

### Visual / Collision Tools

The Visual / Collision category is for inspecting room structure and object visibility.

Included options:

- Toggle the small info overlay.
- Hide or show background/parallax layers.
- Hide or show floor/tile/ground layers.
- Hide or show wall/front layers.
- Hide or show collision/solid/block objects and layers.
- Hide or show character/NPC-like objects.
- Draw collision boxes for detected collision objects.
- Draw object labels on detected collision objects.
- Draw room bounds.
- Draw a player marker.
- Reset all visual toggles.

How detection works:

The script uses name-based detection. It scans the current chapter's layer and object names for common keywords.

Examples:

| Category | Example keywords |
| --- | --- |
| Backgrounds | `bg`, `back`, `background`, `sky`, `parallax` |
| Floors | `floor`, `ground`, `tile`, `tiles`, `path`, `road` |
| Walls | `wall`, `walls`, `front` |
| Collision | `collision`, `coll`, `solid`, `block`, `mask`, `hitbox` |
| Characters | `npc`, `character`, `kris`, `susie`, `ralsei`, `noelle`, `enemy`, `player` |

Because this is name-based, some layers may not be detected, and some objects may be detected too aggressively. The keyword lists can be tuned inside the `.csx` file.

---

### Sound Test

The Sound Test page lists sounds from the currently patched chapter.

Included options:

- Search audio asset names.
- Filter all audio.
- Filter music-like names such as `mus_*`.
- Filter SFX-like names such as `snd_*` or `sfx_*`.
- Toggle looping for selected audio.
- Stop all audio.
- Play selected music or SFX.

Notes:

- This is different from the hidden built-in sound test.
- It lists audio assets from the current data file only.
- Audio naming differs by chapter, so results depend on the patched chapter.

---

### Sprite / Animation Viewer

The Sprite / Animation Viewer lists sprites from the currently patched chapter and can preview them in-game.

Included options:

- Search sprite names.
- Preview selected sprite.
- Play or pause preview animation.
- Previous frame.
- Next frame.
- Reset frame to 0.
- Shows frame count and sprite size.

Notes:

- Sprites are pulled from the currently patched chapter.
- The mod does not load sprites from other chapter data files at runtime.
- Large sprites may be scaled down to fit the preview area.

---

### Battle / Test Rooms

The Battle / Test Rooms page is intentionally safe and generic.

What it does:

- Searches for room names that look battle/test related.
- Lets you warp to those rooms.

What it does not do yet:

- It does not create a true battle launcher.
- It does not spawn custom battle encounters.
- It does not call chapter-specific battle setup scripts.

Why:

DELTARUNE battle setup can depend on chapter-specific scripts, arguments, variables, encounter IDs, party state, and room setup. A real custom battle launcher needs per-chapter reverse engineering and testing.

This page is still useful for finding rooms with names that suggest battle tests, debug rooms, arenas, enemy tests, or encounters.

---

### Runtime Info

The Runtime Info page shows useful live information and gives a few emergency controls.

Shows:

- Current room name and room ID.
- Room size.
- Mouse room position.
- FPS values.
- Asset counts for rooms, sounds, sprites, and objects.
- Detected player object and position.

Included actions:

- Set game speed to 0.5x.
- Set game speed to 1x / normal.
- Set game speed to 2x.
- Set game speed to 4x.
- Stop all audio.
- Panic reset.

Panic reset does:

- Turns no-clip off.
- Resets game speed to normal.
- Stops audio.
- Re-enables visual layer/object toggles.

---

### Object Browser

The Object Browser lists objects from the currently patched chapter.

Included options:

- Search object names.
- Show selected object's live instance count.
- Press Enter to toggle visibility for live instances of the selected object.

This is useful for quickly finding object names, checking if an object exists in the current room, and hiding/showing certain live objects for debugging.

---

## Controls

### Global

| Key | Action |
| --- | --- |
| `F3` | Open or close debug menu |

### Menu Navigation

| Key | Action |
| --- | --- |
| `Up` | Move selection up |
| `Down` | Move selection down |
| `Enter` | Select item / run highlighted action |
| `Backspace` | Go back, or delete one search character on searchable pages |
| `Esc` | Go back / close menu |
| Typing | Search on searchable pages |

### No-clip Movement

These only matter when no-clip is enabled and the debug menu is closed.

| Key | Action |
| --- | --- |
| Arrow keys | Move player |
| `W`, `A`, `S`, `D` | Move player |
| `Shift` | Move faster |

---

## Installation

### Requirements

- A copy of DELTARUNE installed on your computer.
- UndertaleModTool.
- The script file: `DELTARUNE_Debug_Menu_v4.csx`.
- A backup of the original chapter data file.

UndertaleModTool:

```text
https://github.com/UnderminersTeam/UndertaleModTool
```

### Basic install steps

1. Find the DELTARUNE chapter data file you want to patch.
2. Make a backup of the original file.
3. Open the chapter data file in UndertaleModTool.
4. Run `DELTARUNE_Debug_Menu_v4.csx` from UMT's script runner.
5. Save the modified data file.
6. Launch the game.
7. Press `F3` in-game to open the debug menu.

### Multi-chapter install

This script patches only the data file currently opened in UMT.

To support multiple chapters:

1. Open Chapter 1's data file in UMT.
2. Run the script.
3. Save.
4. Repeat for Chapter 2.
5. Repeat for each other chapter you want to patch.

The room, sound, sprite, and object lists are generated at script import time from the currently opened data file.

---

## Uninstallation

The safest uninstall method is to restore your original backup data file.

Recommended:

1. Close the game.
2. Replace the modified data file with your clean backup.
3. Launch the game again.

Do not rely on deleting only the injected object unless you know exactly what was patched.

---

## Recommended Repository Layout

```text
SFT-DELTARUNE-Debug-Menu/
├─ DELTARUNE_Debug_Menu_v4.csx
├─ README.md
├─ GAMEJOLT_DESCRIPTION.txt
├─ docs/
│  └─ screenshots/
│     ├─ main-menu.png
│     ├─ room-select.png
│     ├─ sound-test.png
│     ├─ sprite-viewer.png
│     └─ collision-tools.png
└─ releases/
   └─ old-versions/
      ├─ DELTARUNE_Debug_Menu_v3.csx
      └─ DELTARUNE_Debug_Menu_Starter_v2.csx
```

Keep official game assets out of the repository.

---

## Suggested GitHub Release Checklist

Before publishing a release:

- Test importing the `.csx` in UMT.
- Test opening the menu with `F3`.
- Test at least one room warp.
- Test Sound Test stop/play.
- Test Sprite Viewer on a small sprite and a large sprite.
- Test Panic Reset.
- Confirm that the release only contains source and documentation.
- Confirm no official game data files are included.
- Add screenshots to the README.
- Mark the release as beta if some features are still experimental.

Suggested release title:

```text
SFT DELTARUNE Debug Menu v4 - UI Font Fix + Menu Debug Tools
```

Suggested release files:

```text
DELTARUNE_Debug_Menu_v4.csx
README.md
GAMEJOLT_DESCRIPTION.txt
```

---

## Troubleshooting

### The menu text is garbled or appears as random symbols

Use v4 or newer.

v4 creates a readable debug menu font and forces text alignment before drawing the UI. This should fix the issue where rooms with unusual draw state cause the menu text to display incorrectly.

If it still happens:

- Make sure you imported v4, not v3.
- Try restarting the game after patching.
- Check that the game folder still has `8bitoperator_jve.ttf` or the font file expected by the script.
- Try changing the `font_add` size or font filename inside the script.

### The menu does not open

Check:

- Did the script import successfully in UMT?
- Did you save the patched data file?
- Are you launching the patched copy?
- Is `F3` being blocked by another program or overlay?
- Did the injected object get added to the first room?

### Room warps crash or softlock

Some rooms are not safe to enter directly.

Possible reasons:

- The room expects a story flag.
- The room expects a cutscene variable.
- The room expects a previous room transition.
- The player object is missing.
- The room is a test/dev room or unused room.

Use backups and avoid saving after warping into strange states unless you know it is safe.

### Sound Test audio keeps playing

Use one of these:

- Sound Test -> Stop all audio
- Runtime Info -> Stop all audio
- Runtime Info -> Panic reset

### Visual toggles hide too much or too little

The layer/object hiding system is name-based.

You can tune the keyword lists near the top of the `.csx` file. Search for the sections that build these lists:

```text
bgLayerNames
floorLayerNames
wallLayerNames
collisionLayerNames
collisionObjectNames
characterObjectNames
```

---

## Known Limitations

- The script must be run separately per chapter.
- It cannot load another chapter's data file while the game is running.
- Room Select can warp into rooms that are not safe to enter directly.
- Battle/Test Rooms is not a full custom battle launcher yet.
- Layer/object hiding is keyword-based and may need tuning.
- Player detection is generic and may miss chapter-specific objects.
- This is a debugging mod, not a polished gameplay mod.

---

## Development Notes

The script creates or reuses a persistent object named:

```text
obj_sft_debugmenu
```

It injects code into that object's events:

| Event | Purpose |
| --- | --- |
| Create | Set up lists, settings, font, and default state |
| Step | Handle menu input, no-clip, search, actions, layer visibility, and room changes |
| Draw | Draw room-space overlays such as collision boxes and player marker |
| Draw GUI | Draw the actual debug menu UI |
| Destroy | Clean up DS lists and the added font |

The script also adds the object instance to the first room in the opened data file so it can persist across rooms.

---

## Roadmap Ideas

Possible future updates:

- Configurable menu theme colors.
- Favorites list for rooms, sounds, sprites, and objects.
- Recently visited rooms list.
- Better player object detection per chapter.
- Per-chapter profiles for collision/object keywords.
- Real battle launcher for each chapter.
- Flag/global variable viewer.
- Save-state helper for debug-only testing.
- Text box/dialogue test page.
- Cutscene state viewer.
- More advanced layer browser.
- Live object inspector with x/y/sprite/visible/depth values.

---

## Credits

Project by sonic Fan Tech.

Built as an expanded debugging script inspired by the pre-made Fancy Room Select script commonly used with UndertaleModTool.

Thanks to:

- UndertaleModTool and its contributors.
- The DELTARUNE modding community.
- Toby Fox and the DELTARUNE team for the original game.

---

## Disclaimer

This is an unofficial fan-made debugging tool.

Use it at your own risk. Debug tools can crash the game, softlock rooms, break progression, or leave the game in strange states. Always keep backups of the original data files and your save files.

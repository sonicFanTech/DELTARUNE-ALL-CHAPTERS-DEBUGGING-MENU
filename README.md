# SFT DELTARUNE Debug Menu

![Mod Type](https://img.shields.io/badge/type-UMT%20CSX%20script-blue)
![Game](https://img.shields.io/badge/game-DELTARUNE-yellow)
![Release](https://img.shields.io/badge/release-v1-brightgreen)
![Distribution](https://img.shields.io/badge/distribution-source%20only-green)
![Status](https://img.shields.io/badge/status-public%20beta-orange)

**SFT DELTARUNE Debug Menu** is an unofficial **UndertaleModTool `.csx` script** that injects a custom in-game debugging menu into the currently opened DELTARUNE chapter data file.

The goal of this project is to take the basic pre-made UMT room selector idea and turn it into a larger, menu-driven debugging tool with room warping, player tools, visual/collision tools, sound testing, sprite viewing, runtime information, and object browsing.

This is the **first public release**, so the public version number is **v1**. Older test builds made during development were private testing builds and are not part of the public release history.

> This project is not affiliated with, endorsed by, or sponsored by Toby Fox, 8-4, Fangamer, UndertaleModTool, or the official DELTARUNE team.

---

## Important Distribution Note

This repository should only contain the `.csx` script source and documentation.

does **not** contain or distribute:

- DELTARUNE game files
- Modified `data.win` files
- Patched chapter data files
- Extracted official sprites
- Extracted official music or SFX
- Extracted official fonts
- Extracted official rooms or maps
- Full game folders
- Any other official game assets

Users should run the script themselves on their own legally obtained copy of DELTARUNE.

---

## Current Version

**Latest public script:** `DELTARUNE_Debug_Menu_v1.csx`

**Public release:** v1  
**Release type:** Public beta / source-only UMT script  
**Main open key:** F3  
**Patches:** The currently opened chapter data file only

### What v1 includes

v1 includes the stable menu-based debug tool set, plus the UI text fix that prevents the debug menu from inheriting broken fonts or text alignment from certain rooms.

The debug menu creates and uses a readable UI font for its own drawing, and it resets the text alignment before drawing the menu. This helps stop the menu text from appearing as scattered symbols, invisible text, or broken spacing in rooms that change GameMaker draw state.

---

## Feature Overview

### Main Debug Menu

Press **F3** in-game to open or close the debug menu.

The menu is category-based, so most features are controlled inside the menu instead of using lots of separate hotkeys.

Main categories:

- Room Select
- Player / Movement
- Visual / Collision
- Sound Test
- Sprite / Animation Viewer
- Battle / Test Rooms
- Runtime Info
- Object Browser

---

## Controls

### Global controls

| Key | Action |
| --- | --- |
| F3 | Open or close the debug menu |
| Up / Down | Move through menu rows |
| Enter | Select highlighted option or run highlighted action |
| Backspace | Go back, or delete one search character on searchable pages |
| Esc | Go back, or close the debug menu |
| Typing | Enter search text on searchable pages |

### No-clip movement controls

When no-clip is enabled and the debug menu is closed:

| Key | Action |
| --- | --- |
| Arrow keys | Move player |
| WASD | Move player |
| Shift | Move faster |

---

## Category Details

### Room Select

The Room Select page lets you search and warp to rooms from the currently patched chapter.

Features:

- Lists room names from the current chapter data
- Search/filter rooms by typing
- Warp to the selected room with Enter
- Shows only rooms available in the chapter you patched

Notes:

- Room warping can crash, softlock, or place you in a broken state if the room expects specific story flags, cutscene variables, spawn setup, or chapter state.
- Always keep backup saves before using room warp tools.

---

### Player / Movement

The Player / Movement page contains tools for moving around rooms and testing collision.

Features:

- Toggle no-clip
- Change no-clip speed
- Teleport the player to the mouse position
- Reload the current room

Notes:

- Player detection is generic. It tries to work across chapters, but unusual rooms or special sequences may use different player/control objects.
- No-clip is meant for exploration and debugging, not normal play.

---

### Visual / Collision

The Visual / Collision page helps inspect room layout and hidden objects.

Features:

- Draw collision boxes
- Draw room bounds
- Draw object labels
- Draw a player marker
- Hide/show detected backgrounds
- Hide/show detected floors
- Hide/show detected walls
- Hide/show detected collision or solid objects
- Hide/show detected character/NPC-like objects

Notes:

- Object and layer detection is name-based.
- Some chapters or rooms may use unexpected object names, so the hide/show categories may need future keyword tuning.
- Hiding important objects can make rooms look broken until you toggle them back on or reload the room.

---

### Sound Test

The Sound Test page lets you search and play audio assets from the currently patched chapter.

Features:

- Lists sounds from the current chapter data
- Search/filter sound names
- Play selected sound
- Loop selected sound
- Stop all audio

Notes:

- This is separate from DELTARUNE's hidden/internal sound test.
- It only lists sounds found in the chapter data file you patched.
- It does not load sounds from other chapters automatically.

---

### Sprite / Animation Viewer

The Sprite / Animation Viewer lets you search and preview sprites from the currently patched chapter.

Features:

- Lists sprites from the current chapter data
- Search/filter sprite names
- Preview selected sprite
- Animate through sprite frames

Notes:

- It only previews sprites present in the currently patched chapter.
- It does not load sprites from other chapters because each chapter has its own data file/assets.

---

### Battle / Test Rooms

The Battle / Test Rooms page is a safe, generic testing page.

Features:

- Searches for rooms with battle/test-like names
- Lets you warp to those rooms

Important limitation:

This is **not** a full custom battle launcher yet.

DELTARUNE battle setup usually depends on chapter-specific scripts, variables, encounter setup, party state, and arguments. A proper battle launcher would need separate per-chapter logic rather than one generic script that blindly works everywhere.

---

### Runtime Info

The Runtime Info page shows useful current game information and global testing controls.

Features:

- Current room name/index
- Mouse position
- Player position when detected
- FPS/current speed info
- Asset counts
- Game speed presets
- Stop all audio
- Panic reset options

---

### Object Browser

The Object Browser page helps inspect object names and live instances.

Features:

- Search object names
- View objects from the current chapter data
- Toggle visibility of live instances of selected objects

Notes:

- This is useful for finding walls, triggers, blockers, NPC objects, room controllers, and other debug targets.
- Turning off the wrong object can break a room until reload.

---

## Multi-Chapter Usage

This script patches **only the chapter data file currently open in UndertaleModTool**.

To use it on multiple chapters:

1. Open the chapter's data file in UndertaleModTool.
2. Run `DELTARUNE_Debug_Menu_v1.csx`.
3. Save a patched copy.
4. Repeat for any other chapter you want to patch.

Each chapter will have its own:

- Room list
- Sound list
- Sprite list
- Object list
- Battle/test room list

The script does not automatically load assets from other chapters.

---

## Installation

### Requirements

- A legal copy of DELTARUNE
- UndertaleModTool
- `DELTARUNE_Debug_Menu_v1.csx`

### Steps

1. Back up your original DELTARUNE data file.
2. Back up your save files if you care about your current progress.
3. Open the chapter data file in UndertaleModTool.
4. Run `DELTARUNE_Debug_Menu_v1.csx` using UMT's script system.
5. Save the patched file as a modded copy.
6. Launch the game.
7. Press **F3** in-game to open the debug menu.

---

## Updating From Private Test Builds

The public release is **v1**.

Earlier builds named during development were private test builds and should be treated as internal prototypes. For public GitHub/GameJolt releases, use:

- `DELTARUNE_Debug_Menu_v1.csx`
- `README.md`
- `GAMEJOLT_DESCRIPTION.txt`
- `RELEASE_NOTES_v1.txt`

Do not upload the older testing files unless you specifically want to archive them as private development history.

---

## Known Limitations

- Room warping can crash or softlock if the target room expects specific variables, flags, cutscene state, spawn data, or chapter progress.
- The battle/test page is a safe room warp helper, not a complete battle launcher.
- Object hiding is name-based and may need tuning for certain chapters.
- Layer hiding may not catch every visual element.
- Player detection is generic and may miss special sequences.
- Some debug options can leave the game in strange states until you reload the room or restart the game.
- This is a debugging tool, not a polished gameplay mod.

---

## Safety Tips

Before using the mod:

- Back up your original game data files.
- Back up your save files.
- Keep a clean unmodified copy of every chapter.
- Test on a copied game folder when possible.
- Do not use important save files while testing room warps or battle/test rooms.

While using the mod:

- Use the panic reset option if the game state becomes weird.
- Reload the room after heavy visual/object hiding tests.
- Restart the game if sound, speed, or object state does not return to normal.

---

## Screenshots

Add screenshots here after you capture them from your own patched copy.

Suggested screenshots:

- Main category menu
- Room Select page
- Visual / Collision overlay
- Sound Test page
- Sprite Viewer page
- Object Browser page

Do not include screenshots that reveal private save data or unreleased/private content.

---

## Credits

Created by **sonic Fan Tech**.

Inspired by the pre-made Fancy Room Select style of UndertaleModTool scripts.

Thanks to:

- UndertaleModTool and its contributors
- DELTARUNE modding/debugging community resources
- Toby Fox and the official DELTARUNE team for the original game

---

## Disclaimer

This is an unofficial fan-made debugging tool.

This project is not affiliated with, endorsed by, or sponsored by Toby Fox, 8-4, Fangamer, UndertaleModTool, or the official DELTARUNE team.

Use at your own risk. Debugging tools can crash the game, break rooms, create invalid game states, or softlock saves.

# KGJ MLB Editor

A browser-based ROM editor for **Ken Griffey Jr. Presents Major League Baseball** (SNES, 1994).

Built by reverse engineering the original binary — no existing documentation, no source code. Every byte offset, encoding scheme, and data structure was derived from scratch by decompiling the original ClickOnce editor and cross-referencing against the ROM directly.

---

## Usage

1. Download `KGJ_Editor.html`
2. Open it in **Chrome** or **Edge** (other browsers should work but are untested)
3. Drag and drop your ROM file onto the load screen, or click to browse
4. Select a team from the sidebar
5. Edit players inline
6. Hit **Save Team** to commit changes to the in-memory ROM
7. Hit **Export ROM** when you are done to download the finished `.smc` file

No installation. No server. Everything runs locally in your browser.

---

## Supported ROM Formats

| Format | Notes |
|--------|-------|
| `.sfc` | Standard headerless format — works directly |
| `.smc` | SMC copier format — 512-byte header auto-detected and handled |

Both the vanilla ROM with original generic player names and hacked ROMs with real player names are supported.

---

## Features

### Editing
- Edit all 28 teams across both leagues and all six divisions
- Full inline editing of every player field — no separate edit mode
- Starters (9 players), Bench (6 players), Pitchers (10 players) per team
- All positions supported: P, C, 1B, 2B, 3B, SS, LF, CF, RF, DH, OF, IF

### Player fields
| Field | Description |
|-------|-------------|
| First initial | Single character |
| Last name | Up to 8 characters |
| Position | Dropdown, all positions |
| Jersey number | 0–99 |
| BAT / POW / SPD / DEF | Ability ratings 1–10 (hitters) |
| SPD / CON / FAT | Ability ratings 1–10 (pitchers) |
| B/T | Bats/throws handedness |
| Body / Face / Legs | Player appearance (raw values) |
| AVG / HR / RBI | Season stats (hitters) |
| L / S / ERA | Season stats (pitchers) |

### Tools
- **Undo/Redo** — up to 30 steps per team session
- **Copy/Paste** — copy any player and paste onto any slot, including across teams
- **Bulk stat adjust** — set a stat to a fixed value across an entire section at once
- **Player search** — search by name across all 28 teams
- **Compare view** — side-by-side stat comparison of any two teams
- **Reorder players** — move players up and down within a section
- **Collapsible sidebar** — hide the team list for more editing space
- **Export CSV** — export the current team roster to a spreadsheet

### File handling
- **Save Team** — writes edits to the in-memory ROM buffer
- **Export ROM** — downloads the finished `.smc` file ready to load in an emulator
- **Revert** — rolls back unsaved changes on the current team
- **Eject** — unloads the ROM and returns to the load screen, with unsaved-changes prompt

---

## What the ratings mean

Based on community research and ~30 years of gameplay observation:

**Batters**
- **BAT** — Contact ability / batting average
- **POW** — Power; drives home run production. POW matters more than BAT for run scoring — a POW 10 with low BAT will still hit missiles
- **SPD** — Baserunning speed. Big jump between 6 and 7
- **DEF** — Covers both fielding range AND throwing arm strength. A high DEF outfielder will gun runners from the warning track; a low DEF outfielder will not

**Pitchers**
- **SPD** — Pitch velocity
- **CON** — Control
- **FAT** — Fatigue rate; how quickly the pitcher tires

Note: ratings above 9 may not function correctly in-game. The game engine appears to cap effective values at 9 regardless of what is stored.

---

## Technical notes

The ROM stores player data in 800-byte team blocks (25 players × 32 bytes each). Player names use a custom encoding (`byte - 0x0B + 'A'`). Stats are packed into nibbles. Batting average and ERA use a two-byte overflow encoding for values above 255.

Team data offsets were derived by decompiling the original ClickOnce editor binary using IL analysis, then verified against the vanilla ROM.

---

## Disclaimer

This tool is a fan project for personal use. Ken Griffey Jr. Presents Major League Baseball is the property of Nintendo / Software Creations. No ROM files are distributed with this project. You must supply your own legally obtained ROM.

---

## License

MIT License — see `LICENSE` for details.

The MIT licence covers the editor code only. It does not grant any rights to the underlying game or its assets.

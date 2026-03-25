# ZORLAC (Fortress of Zorlac: Heritage Siege)

A modern browser reimagining of the 1982 ZX81 game **Fortress of Zorlac**, rebuilt as a fast arcade duel with neon visuals, particle effects, procedural audio, and persistent local high scores.

## Why this exists

This project is inspired by **Fortress of Zorlac** (Paul Carlson, Timex, 1982), preserved on ZX81 Stuff:

- Original page: https://www.zx81stuff.org.uk/zx81/tape/FortressOfZorlac
- Original metadata on that page:
  - Author: Paul Carlson
  - Publisher: Timex
  - Year: 1982
  - Memory: 16K
  - Program name: `ATTACK`

From the original in-game instructions/listing, the core objective was:

- Destroy the alien and blocks of his fortress
- Survive with five ships
- Score more by skill level and firing distance
- Alien guns are indestructible
- Destroying the alien is worth **50x** a fortress block

This remake keeps that spirit while modernizing control feel, presentation, scoring feedback, and pacing.

## Gameplay

You pilot a ship on the left side of the screen and attack a moving fortress/alien target on the right.

- Break rotating wall segments to build combo and score
- Dodge cannon projectiles fired from orbital guns
- Strike the alien core to clear the sector
- Survive all lives for the highest score

Each cleared sector spawns a new fortress with higher pressure.

## Controls

- `W A S D` or Arrow keys: move
- `Space`: fire
- `Esc`: return to main menu

## Difficulty Modes

Menu options map to internal score/aggression multipliers:

- `CADET` -> x1
- `ACE` -> x2
- `SLAUGHTER` -> x4

## Scoring System

### Fortress segment hit

Base formula:

`50 * difficulty * comboMultiplier * proximityMultiplier`

- Combo multiplier ramps with consecutive hits (up to x10)
- Proximity multiplier:
  - x5 in danger zone (very close)
  - x2 in combat range
  - x1 otherwise

### Alien core destruction

Base formula:

`10000 * difficulty * proximityMultiplier`

In practice, aggressive close-range runs produce much larger scores.

## High Scores

High scores are stored in browser `localStorage` under:

- `zorlac_v26_scores`

Behavior:

- Top 10 saved locally
- Top entries shown in menu/game-over archive views
- New qualifying scores can be saved with a 3-character pilot tag

## Run Locally

No build step is required.

1. Clone/download this repo
2. Open [`ZORLAC.html`](./ZORLAC.html) in a modern browser

If your browser blocks some local behaviors, run a tiny local server instead:

```powershell
# from project folder
python -m http.server 8080
```

Then open `http://localhost:8080/ZORLAC.html`.

## Technical Notes

- Single-file implementation: HTML + CSS + JavaScript
- Rendering: `canvas` (1200x750)
- Audio: Web Audio API oscillators (no external sound files)
- Visual feedback: screen shake, hit stop, trail/debris particles, combo/proximity tags

## Known Browser Caveats

- Audio may require a user interaction before playback (browser policy)
- `window.close()` is often blocked outside script-opened tabs; the terminate button may fall back to navigation behavior

## Project Structure

- [`ZORLAC.html`](./ZORLAC.html): complete game (UI, engine, rendering, audio, scoring)

## Credits

- 2026 reimagined version: Luis Cunha
- Original concept and classic game lineage: Paul Carlson / Timex (1982)
- Historical source and preservation: ZX81 Stuff

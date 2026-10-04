# Last updated October 2026

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static GitHub Pages site (`luis-figueroa-ops.github.io`) - no build system, no bundler, no package manager. Every file is raw HTML/CSS/JS deployed directly.

## Development

Open any `.html` file directly in a browser, or serve locally with:
```
python -m http.server 8080
```

No build, lint, or test commands exist. Changes go live by pushing to `main`.

## Architecture

Self-contained HTML pages - all styles and scripts are inline within each file:

- `index.html` - Landing/portfolio page linking to all tools
- `jd-analyzer/index.html` - Job description analyzer; streams Claude responses, supports follow-up chat
- `ai-role-revealer/index.html` - Two-step tool: generates AI insights for a role, then builds copy-ready prompts

### Games

Each game lives in its own folder under `games/`. None need an API key. Games with a landing page
card are linked by the card's `id` (e.g. `index.html#dodge`).

- `games/dodge/index.html` - DODGE: canvas space arcade game - dodge and shoot asteroids, comets,
  and alien craft across 20 levels with boss waves. Web Audio sound, local leaderboard. Card `#dodge`
- `games/stacked/index.html` - STACKED!: canvas block-stacking drop game; speed ramps up each level,
  high score saved locally. Card `#stacked`
- `games/boxing/index.html` - GLASS JAW: first-person canvas boxing game, twenty fighters across five
  styles. Web Audio sound, local leaderboard. Card `#boxing`
- `games/sudoku/index.html` - GRIDLOCK: sudoku game. Generates a new puzzle
  in the browser each game (random solved grid, then removes clues while a solver confirms the
  solution stays unique). Easy/Medium/Hard/Expert = 40/32/27/~24 clues. How to Play screen on every
  visit, notes, hints, undo, 3-mistake limit, timer. Progress and best times are kept in
  `localStorage` (`gridlock-sudoku-save`, `gridlock-sudoku-best`). Card `#sudoku`
- `games/wordsense/index.html` - WordSense landing page that opens the published Claude artifact.
  The artifact source is `games/wordsense/wordsense-artifact.html` (not a site page). Card `#wordsense`

Not linked from the landing page (no card):

- `games/cross-warriors/index.html` - Cross Warriors: pixel-style canvas game - tap to shoot waves of
  demons across 12 levels with boss fights. Back link goes to the site root
- `games/road-rush/index.html` - ROAD RUSH: first-person canvas driving game - dodge traffic, cones,
  and debris on roads that speed up each level. Local leaderboard. Its back link points to
  `#road-rush`, which has no card yet, and it has no icon or manifest files

### Game page conventions

New games should match the existing ones (Dodge, Stacked, Glass Jaw, GRIDLOCK):

- Back link reads `← Back to Tools` and points to `https://luis-figueroa-ops.github.io/#<card-id>`
  so the landing page scrolls back to that game's card
- Landing page card uses `card-top-row` with a `card-qr` image at `images/<game>_qr.png`
  (shown on desktop, hidden on mobile). QR images are 410x410, navy `#1B2A4A` on white,
  error correction M, 10px modules, 4-module margin
- Game folder includes `icon.svg`, `favicon-32.png`, `apple-touch-icon.png` (180),
  `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`, and `manifest.webmanifest` listing
  the three PNG icons. Keep maskable art inside the center 80% circle
- Include the Google Analytics tag (see Analytics below)

## Claude API Usage Patterns

> **Note:** this section is partly out of date. The AI tools (JD Analyzer, AI
> Role Revealer, Prompt Coach, Course Blueprint, WordSense) are now published
> **Claude Artifacts** - the pages under `jd-analyzer/`, `ai-role-revealer/`
> etc. are just landing pages that link to `claude.ai/public/artifacts/...`.
> The artifact source lives in this repo only for WordSense
> (`games/wordsense/wordsense-artifact.html`).

**Preferred pattern for a new AI tool** - call `window.claude.complete(prompt)`
inside the artifact. It runs on the *viewer's* own Claude account (they click
"Allow" once), needs no API key, and lets the artifact be shared **publicly**.
This works ONLY for artifacts published from a **claude.ai chat**
(`claude.ai/public/artifacts/...`) - WordSense, JD Analyzer, AI Role Revealer,
and Prompt Coach all use it. To update one: open a claude.ai chat, paste the
source, ask for a single self-contained HTML artifact that keeps the
`window.claude.complete()` calls, then publish and set "Anyone with the link".

`window.claude.complete()` is NOT available in artifacts published via the
Claude Code Artifact tool (`claude.ai/code/artifact/...`); that runtime only
offers the capability model, and declaring `sample` there blocks public
sharing. Tested 2026-09 - don't retry it.

**Legacy pattern (avoid)** - direct browser calls to
`https://api.anthropic.com/v1/messages` with a user-supplied `x-api-key` plus
`anthropic-dangerous-direct-browser-access: true` and
`anthropic-version: 2023-06-01`. Forces every visitor to bring their own paid
API key.

## Design System

Each tool has its own visual style - do not assume shared CSS variables across files.

- **Landing page & JD Analyzer**: Navy/gold (`#1B2A4A` / `#B8963E`); fonts: Bebas Neue, DM Sans, Share Tech Mono
- **AI Role Revealer**: Dark purple/tech (`#0a0a0f` bg, `#6c63ff` accent, `#43e8c8` secondary); fonts: IBM Plex Mono, Outfit
- **Dodge**: Cyberpunk dark (`#0d0d18` bg, `#00ffe7` accent); fonts: Orbitron, Share Tech Mono
- **Stacked!**: Dark neon (`#050510` bg, `#00ffe7` accent, `#a080ff` secondary); font: Courier New
- **Glass Jaw**: Dark red/gold (`#140a0c` bg, `#ff3b3b` red, `#f5c542` gold); fonts: Bebas Neue, Share Tech Mono
- **Road Rush**: Night drive (`#0a0e17` bg, `#ffb020` amber, `#ff6a3d` orange); fonts: Orbitron, Share Tech Mono
- **Cross Warriors**: Retro pixel (`#000` bg, `#FFD700` gold, `#8B0000` dark red); font: Press Start 2P
- **GRIDLOCK**: Navy/gold like the landing page (`#1B2A4A` / `#B8963E`, bright gold `#D4A53A`); fonts: Bebas Neue, DM Sans, Share Tech Mono

## Analytics

Google Analytics tag `G-YCMXSWXHTN` is included on every page. Keep it when adding new pages.

# Last updated October 2026

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

**Keep this file up to date.** Any change that adds, removes, renames, or moves a page, card, game,
tool, or asset folder must update this file in the same commit, along with the "Last updated" line.

## Project Overview

Static GitHub Pages site (`luis-figueroa-ops.github.io`) - no build system, no bundler, no package manager. Every file is raw HTML/CSS/JS deployed directly.

## Development

Open any `.html` file directly in a browser, or serve locally with:
```
python -m http.server 8080
```

No build, lint, or test commands exist. Changes go live by pushing to `main`.

## Architecture

Self-contained HTML pages - all styles and scripts are inline within each file. Every page lives in
its own folder as `index.html`. Pages linked from the landing page have a card whose `id` is used as
an anchor (e.g. `index.html#dodge`), and each page's back link points to
`https://luis-figueroa-ops.github.io/#<card-id>` so the landing page scrolls back to that card.
Back link text: `← Back to Home` for Beyond the Resume pages, `← Back to Tools` everywhere else.

### Landing page (`index.html`)

- **Header** - logo (`images/Untitled design.png`, also the `og:image` / `twitter:image` link
  preview), name and tagline, LinkedIn link, and the site QR code (`images/luis_portfolio_qr_v4.png`)
- **Intro** - embedded YouTube video (`youtube.com/embed/j3CCO_9RtOk`), intro text, "why I built
  this", and links to `#beyond-the-resume` and LinkedIn

Then these sections in order:

1. **Beyond the Resume** (`#beyond-the-resume`) - cards: `#about-me`, `#i2b-channel-buildout`,
   `#method-in-motion`, `#operations-augmented`
2. **Tools, Projects & Games** - cards: `#read-aloud`, `#course-blueprint`, `#prompt-coach`,
   `#jd-analyzer`, `#ai-role-revealer`, `#ai-automations`, `#build-use-break-fix`, `#dodge`,
   `#stacked`, `#boxing`, `#sudoku`, `#wordsense`
3. **Professional Development** - cards: `#google-ai`, `#google-pm`, `#google-data-analytics`,
   `#google-advanced-data-analytics`, `#reskilling-coursework`
4. **Using the Tools** - "The games run right here", "The AI tools open in Claude", and an AI Notice
5. **Footer** - brand line and LinkedIn link

### Beyond the Resume pages

- `about-me/index.html` - The Approach Behind the Work: how Luis connects strategy, systems, and
  execution. Card `#about-me`
- `i2b-channel-buildout/index.html` - I2B Channel Buildout: nine SOAR-format stories from scaling
  Verizon Business's 8,000+ agent indirect SMB channel. Uses
  `assets/i2b-channel-buildout/quota-relief-automation.pdf`. Card `#i2b-channel-buildout`
- `method-in-motion/index.html` - Method in Motion: screen-recorded tutorials on formulas and
  dashboard builds. PDFs and thumbnails in `assets/skills-in-action/`. Card `#method-in-motion`
- `operations-augmented/index.html` - Operations, Augmented: thought leadership presentations on
  deploying AI through an operations lens. PDFs and thumbnails in `assets/thought-leadership/`.
  Card `#operations-augmented`
- `my-skills-in-action/index.html` - Redirect only (meta refresh) to `/method-in-motion/`. Keep it
  so old links keep working

### Tools and projects

AI tools that open in Claude - each page is a landing page with an "Open in Claude" button linking
to a published `claude.ai/public/artifacts/...` (see Claude API Usage Patterns below):

- `jd-analyzer/index.html` - JD Analyzer: honest ops read of a job description. Card `#jd-analyzer`
- `ai-role-revealer/index.html` - AI Role Revealer: what AI could do for your actual role, then a
  prompt to get it. Card `#ai-role-revealer`
- `prompt-coach/index.html` - Prompt Coach: scores, diagnoses, and rewrites a rough prompt.
  Card `#prompt-coach`
- `learning-tools/course-blueprint/index.html` - 15-Minute Course Blueprint: builds a course roadmap
  and teaches it in 15-minute sessions. Card `#course-blueprint`

Other tools and projects:

- `read-aloud/index.html` - Read Aloud: paste text or open a .txt, .md, or .docx file and hear it
  read aloud with the browser's Web Speech API; keeps the screen awake while reading (Wake Lock).
  Has its own icon set and `manifest.webmanifest`, plus light/dark themes via `data-theme`.
  Card `#read-aloud`
- `ai-automations/index.html` - AI Automations: three Google Apps Script + Gemini API workflows
  (receipt pipeline, research digests, inbox triage) with workflow diagrams stored next to the page.
  Card `#ai-automations`
- `build-use-break-fix/index.html` - Build. Use. Break. Fix.: video walkthrough
  (`build-use-break-fix.mp4`, `poster.jpg`) with the story behind it. Card `#build-use-break-fix`

### Credentials (Professional Development)

Each folder holds an `index.html` plus the certificate files as matching `.pdf` + `.png` pairs:

- `credentials/google-ai/` - Google AI Professional Certificate. Card `#google-ai`
- `credentials/google-pm/` - Google Project Management Professional Certificate. Card `#google-pm`
  - `credentials/google-pm/capstone-project/` - Capstone: Sauce & Spoon Tablet Rollout (project
    documents as PDF + PNG). Linked from the Google PM page; its back link is `../index.html`
    (`← Back to Certificate`)
- `credentials/google-data-analytics/` - Google Data Analytics Professional Certificate.
  Card `#google-data-analytics`
- `credentials/google-advanced-data-analytics/` - Google Advanced Data Analytics Professional
  Certificate. Card `#google-advanced-data-analytics`
- `credentials/reskilling-coursework/` - Verizon Skill Forward courses (Power BI, Python,
  process flowcharts, project management). Card `#reskilling-coursework`

### Other files

- `assets/` - PDFs and thumbnails used by the Beyond the Resume pages (see above)
- `images/` - landing page images: `Untitled design.png` (logo and link preview image - the
  filename is referenced as `Untitled%20design.png`, so don't rename it without updating
  `index.html`), `luis_portfolio_qr_v4.png` (header QR), and `<game>_qr.png` (game card QR codes).
  `images/placeholder.txt` is not referenced by any page
- `videos/placeholder.txt` - empty placeholder folder; no page references it
- `README.md` - one-line repo description

### Games

Each game lives in its own folder under `games/`. None need an API key.

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

Intentionally unlisted - do NOT add a landing page card:

- `games/cross-warriors/index.html` - Cross Warriors: pixel-style canvas game - tap to shoot waves of
  demons across 12 levels with boss fights. Back link goes to the site root

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

- **Landing page, Beyond the Resume pages & credentials pages**: Navy/gold (`#1B2A4A` / `#B8963E`); fonts: Bebas Neue, DM Sans, Share Tech Mono
- **JD Analyzer**: Navy/gold (`#1B2A4A` / `#B8963E`); font: Segoe UI
- **Prompt Coach & Build. Use. Break. Fix.**: Near-black/gold (`#0e0e0e` bg, `#C9A84C` gold); fonts: Bebas Neue, DM Sans, Share Tech Mono
- **AI Automations**: Near-black/teal (`#0e0e0e` bg, `#2DD4BF` accent); fonts: Bebas Neue, DM Sans, Share Tech Mono
- **Course Blueprint**: GitHub-dark/green (`#0d1117` bg, `#4ade80` accent); fonts: Bebas Neue, DM Sans, Share Tech Mono
- **Read Aloud**: Desk-and-paper look (`#1f2a44` desk, `#d4a53a` gold, `#fbf6e9` paper), light/dark themes; serif system fonts (Iowan Old Style, Palatino, Georgia)
- **WordSense landing page**: Light (`#f5f4f0` bg, `#b8860b` gold); system sans-serif fonts
- **AI Role Revealer**: Dark purple/tech (`#0a0a0f` bg, `#6c63ff` accent, `#43e8c8` secondary); fonts: IBM Plex Mono, Outfit
- **Dodge**: Cyberpunk dark (`#0d0d18` bg, `#00ffe7` accent); fonts: Orbitron, Share Tech Mono
- **Stacked!**: Dark neon (`#050510` bg, `#00ffe7` accent, `#a080ff` secondary); font: Courier New
- **Glass Jaw**: Dark red/gold (`#140a0c` bg, `#ff3b3b` red, `#f5c542` gold); fonts: Bebas Neue, Share Tech Mono
- **Cross Warriors**: Retro pixel (`#000` bg, `#FFD700` gold, `#8B0000` dark red); font: Press Start 2P
- **GRIDLOCK**: Navy/gold like the landing page (`#1B2A4A` / `#B8963E`, bright gold `#D4A53A`); fonts: Bebas Neue, DM Sans, Share Tech Mono

## Analytics

Google Analytics tag `G-YCMXSWXHTN` is included on every page. Keep it when adding new pages.

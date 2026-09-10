# Last updated June 2026

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static GitHub Pages site (`luis-figueroa-ops.github.io`) — no build system, no bundler, no package manager. Every file is raw HTML/CSS/JS deployed directly.

## Development

Open any `.html` file directly in a browser, or serve locally with:
```
python -m http.server 8080
```

No build, lint, or test commands exist. Changes go live by pushing to `main`.

## Architecture

Four self-contained HTML pages — all styles and scripts are inline within each file:

- `index.html` — Landing/portfolio page linking to all tools
- `jd-analyzer/index.html` — Job description analyzer; streams Claude responses, supports follow-up chat
- `ai-role-revealer/index.html` — Two-step tool: generates AI insights for a role, then builds copy-ready prompts
- `games/dodge.html` — Canvas-based arcade game; no API key required

## Claude API Usage Patterns

> **Note:** this section is partly out of date. The AI tools (JD Analyzer, AI
> Role Revealer, Prompt Coach, Course Blueprint, WordSense) are now published
> **Claude Artifacts** — the pages under `jd-analyzer/`, `ai-role-revealer/`
> etc. are just landing pages that link to `claude.ai/public/artifacts/...`.
> The artifact source lives in this repo only for WordSense
> (`games/wordsense/wordsense-artifact.html`).

**Preferred pattern for a new AI tool** — call `window.claude.complete(prompt)`
inside the artifact. It runs on the *viewer's* own Claude account (they click
"Allow" once), needs no API key, and — crucially — lets the artifact be shared
**publicly**. Declaring the `sample` capability (`claude.use("sample")`) is more
powerful but restricts sharing to named people only, so avoid it for anything
that needs to be public. Republish artifacts with capabilities cleared (`{}`).

**Legacy pattern (still in older tools)** — direct browser calls to
`https://api.anthropic.com/v1/messages` with a user-supplied `x-api-key` plus
`anthropic-dangerous-direct-browser-access: true` and
`anthropic-version: 2023-06-01`. Avoid for new work; it forces every visitor to
bring their own paid API key.

## Design System

Each tool has its own visual style — do not assume shared CSS variables across files.

- **Landing page & JD Analyzer**: Navy/gold (`#1B2A4A` / `#B8963E`); fonts: Bebas Neue, DM Sans, Share Tech Mono
- **AI Role Revealer**: Dark purple/tech (`#0a0a0f` bg, `#6c63ff` accent, `#43e8c8` secondary); fonts: IBM Plex Mono, Outfit
- **Dodge**: Cyberpunk dark (`#0d0d18` bg, `#00ffe7` accent); fonts: Orbitron, Share Tech Mono

## Analytics

Google Analytics tag `G-YCMXSWXHTN` is included on every page. Keep it when adding new pages.

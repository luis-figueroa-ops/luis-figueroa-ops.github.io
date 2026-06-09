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

Both AI tools call `https://api.anthropic.com/v1/messages` directly from the browser using a user-supplied API key. The key is never stored — it lives only in the browser session.

Required headers for direct browser access:
```js
'anthropic-dangerous-direct-browser-access': 'true'
'anthropic-version': '2023-06-01'
'x-api-key': userApiKey
```

**JD Analyzer** — uses streaming (`stream: true`), model `claude-opus-4-5`, max_tokens 1500. Maintains `conversationHistory` array for multi-turn chat.

**AI Role Revealer** — non-streaming, two separate calls:
- Step 1 (role analysis): `claude-sonnet-4-6`, max_tokens 1000, expects raw JSON with `{"insights": [{title, body}]}`
- Step 2 (prompt builder): `claude-sonnet-4-6`, max_tokens 1000, returns plain text prompt

## Design System

Each tool has its own visual style — do not assume shared CSS variables across files.

- **Landing page & JD Analyzer**: Navy/gold (`#1B2A4A` / `#B8963E`); fonts: Bebas Neue, DM Sans, Share Tech Mono
- **AI Role Revealer**: Dark purple/tech (`#0a0a0f` bg, `#6c63ff` accent, `#43e8c8` secondary); fonts: IBM Plex Mono, Outfit
- **Dodge**: Cyberpunk dark (`#0d0d18` bg, `#00ffe7` accent); fonts: Orbitron, Share Tech Mono

## Analytics

Google Analytics tag `G-YCMXSWXHTN` is included on every page. Keep it when adding new pages.

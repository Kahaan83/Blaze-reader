<div align="center">

<img src="https://img.shields.io/badge/status-beta-orange?style=flat-square" />
<img src="https://img.shields.io/badge/license-MIT-blue?style=flat-square" />
<img src="https://img.shields.io/badge/built%20with-HTML%20%2B%20CSS%20%2B%20JS-informational?style=flat-square" />
<img src="https://img.shields.io/badge/AI-Claude%20Sonnet-blueviolet?style=flat-square&logo=anthropic" />
<img src="https://img.shields.io/badge/deploy-Vercel-black?style=flat-square&logo=vercel" />

<br /><br />

<h1>⚡ Blaze Reader</h1>

<p><strong>A smart, browser-native RSVP speed reader with AI-powered recall checks.</strong><br/>
Read faster. Remember more. No installs. No accounts. No data leaves your browser.</p>

<a href="https://blaze-reader-neon.vercel.app"><strong>→ Try it live</strong></a>

</div>

---

## What is Blaze Reader?

Blaze Reader is a **Rapid Serial Visual Presentation (RSVP)** tool that flashes words or phrases at a configurable speed, helping you tear through text 2–3× faster than traditional reading. Unlike basic RSVP tools, Blaze Reader layers in two cognitive-science-backed features:

- **Focal letter anchoring** — each word is color-highlighted at its optimal recognition point (the ORP), reducing eye saccade overhead and keeping your focus locked.
- **AI-powered active recall** — every ~60 words, Claude pauses your session and fires a comprehension question generated from what you just read. This transforms passive consumption into engaged learning.

It works entirely in the browser. No backend, no login, no tracking.

---

## Features

| Feature | Details |
|---|---|
| **3 input modes** | Paste text · Fetch from URL · Upload PDF |
| **Adaptive pacing** | Speed ramps from 70% → 110% of target WPM over the first 40% of text |
| **Focal letter highlighting** | ORP-based coloring per word; 6 color options |
| **Phrase mode** | Display 3 words at a time for smoother reading rhythm |
| **Punctuation pauses** | Automatic slowdowns at `.`, `!`, `?`, `,`, `;` — configurable |
| **Reading modes** | Focus (full pauses) or Skim (compressed timing) |
| **Active recall** | AI-generated MCQs via Claude Sonnet every 60 words |
| **Live speed control** | Adjust WPM mid-session without stopping |
| **Replay** | Jump back 10 seconds of reading |
| **Session stats** | Avg WPM · Recall checks · Time saved vs normal reading |
| **Lifetime time-saved tracker** | Cumulative time saved across all sessions (localStorage) |
| **PDF extraction** | Client-side via PDF.js — no upload to any server |
| **URL fetching** | Strips nav/footer/ads, extracts main article body |
| **Zero-dependency deploy** | Single `.html` file, deployable anywhere |

---

## How It Works

```
Input text (paste / URL / PDF)
        ↓
Tokenize into words or 3-word phrases
        ↓
Flash each token at calculated interval
  ├── Base delay: 60,000 ms / current WPM
  ├── Punctuation multiplier (1.5×–2.4×)
  ├── Long-word multiplier (1.15×)
  └── Skim mode compressor (0.7×)
        ↓
Every 60 tokens → pause + trigger recall
  └── POST to Claude Sonnet API
        └── Returns MCQ (question + 4 options + explanation)
        ↓
Session complete → stats summary
```

The focal letter index is calculated by character length:

| Word length | Focal position |
|---|---|
| ≤ 1 char | Index 0 |
| 2–5 chars | Index 1 |
| 6–9 chars | Index 2 |
| 10+ chars | Index 3 |

---

## Getting Started

### Use the live version
Head to [blaze-reader-neon.vercel.app](https://blaze-reader-neon.vercel.app) — no setup needed.

### Run locally
```bash
git clone https://github.com/Kahaan83/Blaze-reader.git
cd Blaze-reader
# Open in browser — no build step required
open blaze-reader.html
```

> **Note:** Active recall requires an Anthropic API key. The app currently calls the API directly from the browser. For production use, route requests through a backend proxy to keep your key secure.

---

## Tech Stack

- **HTML / CSS / Vanilla JS** — zero frameworks, single file
- **PDF.js** (v3.11.174) — client-side PDF text extraction
- **allorigins.win** — CORS proxy for URL fetching
- **Claude Sonnet (`claude-sonnet-4-6`)** — MCQ generation via Anthropic API
- **Vercel** — static hosting

---

## Roadmap

### v1.0 — Core polish *(current focus)*
- [ ] Secure API key handling via a lightweight backend proxy
- [ ] Keyboard shortcuts (Space = pause, ← = replay, ↑↓ = WPM adjust)
- [ ] Persist settings (WPM, mode, color) across sessions via localStorage
- [ ] Better URL fetch fallback — handle paywalls, JS-rendered pages

### v1.1 — Reader enhancements
- [ ] Chapter/section detection in PDFs with jump-to navigation
- [ ] Bionic reading mode (bold first half of each word)
- [ ] Font size control for the display zone
- [ ] Dark / light theme toggle
- [ ] Mobile-optimized layout and touch controls

### v1.2 — AI features
- [ ] Pre-session summary: Claude summarizes the text before you start
- [ ] Post-session debrief: key points, vocabulary, and a comprehension score
- [ ] Adjustable recall frequency (every 30 / 60 / 100 words)
- [ ] Recall difficulty modes (factual / inference / synthesis)
- [ ] Export recall Q&A as Anki deck or Markdown notes

### v2.0 — Platform
- [ ] PWA / installable app with offline support
- [ ] Reading history and session analytics dashboard
- [ ] Browser extension for reading any webpage in-place
- [ ] Multi-column / two-word phrase display option
- [ ] Shareable reading sessions (same text, synced speed)

---

## Contributing

Pull requests are welcome. For major changes, open an issue first to discuss what you'd like to change.

```bash
# Fork → clone → create a branch
git checkout -b feature/your-feature-name

# Make your changes, then open a PR against main
```

---

## License

[MIT](LICENSE) — Kahaan Shah, 2025

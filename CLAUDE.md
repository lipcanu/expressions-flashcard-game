# Spanish Expressions Card Game

A single-file flashcard quiz to memorise Spanish idiomatic expressions. Opens directly in a browser or on GitHub Pages — no build tools, no npm, no framework.

## Deliverable

One file: `index.html`. All data is embedded inline as a JS array (parsed from `expressions.csv` at build time). No runtime fetches.

## Data source

`expressions.csv` — 58 rows + header, 7 columns:

| column | used in game? |
|---|---|
| `expression` | yes — shown as the question |
| `meaning_en` | **no** — never shown to the player |
| `meaning_es` | yes — the correct answer |
| `example_es` | yes — revealed after the player answers |
| `distractor_1/2/3` | yes — the three wrong options |

One row (`a buenas horas mangas verdes`) uses RFC-4180 quoting. Use Python's `csv` module (not naïve `split(',')`) if re-embedding.

## Game mechanics

- Deck shuffled at the start of each session (Fisher–Yates).
- One card at a time: expression in large text, four answer buttons (1 correct + 3 distractors, shuffled).
- On answer: correct → green button + confetti burst; wrong → dark-red button, correct button highlighted green.
- Example sentence revealed after every answer.
- "Siguiente →" button advances to next card (also triggered by Enter/Space).
- Keyboard shortcuts: 1–4 to pick an answer, Enter/Space to advance or start/restart.
- End screen: final score, motivational message based on % (< 50% / 50–80% / > 80%), "Jugar de nuevo" reshuffles.

## UI / style rules — "warm peach" theme (tweakcn-derived)

- **No emojis anywhere.** Use [Lucide](https://lucide.dev) icons inlined as SVG (no CDN script tag — paste raw SVG markup so the file works fully offline).
- **No app title/header.** Quiz views start directly with the progress bar.
- Font: **Chocolate Classical Sans** 400/700 via Google Fonts (only ships those two weights — never request 800).
- Page background: warm cream `#fbf7ec` (flat, no gradients).
- Card: `#fdfcf6`, `border-radius: 16px`, **1.5px terracotta border** `#e89972`, **hard offset shadow** `3px 3px 0 0 #f5c8b3` (peach, no blur). This stamped/sticker shape is the dominant visual signal — apply to all raised elements.
- **Answer buttons: all share the same white background** with the terracotta border. Number badge `.num` is a cream square (`#fbf3dc` bg, `#e89972` border, terracotta text).
- Correct reveal: green `#2fa84f` (border `#1f7a37`), white text.
- Wrong reveal: dark red `#b8401f` (border `#7a2516`), white text.
- On reveal, the check/x icon is a **small white circle pinned to the top-right corner of the answer**, sitting ~12px outside the bounding box, with a 2px coloured border matching the state (green for correct, dark-red for wrong).
- Primary CTA button (`.btn`): terracotta `#a83626` bg, white text, hard peach shadow. Press state collapses the shadow and translates 2px down/right (stamped-button feel).
- Progress bar: cream `#fbf3dc` track with terracotta border; fill is **cyan `#5CD4E4`** (solid, not gradient).
- Example sentence box: cyan-tinted background `#e8f9fc` with 1.5px `#5CD4E4` border and a thicker 4px `#5CD4E4` left border.
- Stats pill: **white rounded pill, centered, overlapping the top edge of the card** (negative `margin-bottom`, positioned above with `z-index`). Contains a green-filled circle around the check (`#2fa84f`) and a red-filled circle around the X (`#d83b3b`), both with white SVG strokes.
- All transitions 150–250 ms ease-out.
- Mobile-friendly: max-width 520px container, large tap targets.

### Theme tokens (CSS vars in `:root`)

| Var | Value | Use |
|---|---|---|
| `--bg` | `#fbf7ec` | page bg |
| `--card` | `#fdfcf6` | card bg |
| `--ink` | `#1c1b17` | body text |
| `--primary` | `#a83626` | CTA, score, prompt, brand accents |
| `--primary-dark` | `#7a2516` | CTA border |
| `--accent` | `#fbf3dc` | number badge bg, progress track, count chip |
| `--border` | `#e89972` | all 1.5px borders |
| `--shadow-color` | `#f5c8b3` | hard offset shadow |
| `--shadow-hard` | `3px 3px 0 0 var(--shadow-color)` | card / CTA |
| `--shadow-hard-sm` | `2px 2px 0 0 var(--shadow-color)` | answer buttons, stats pill |

## Current quiz UI layout (top → bottom)

```
[progress bar (cyan fill on cream track) ←——] [score: n / 58]
                  [white pill: ✓ count | ✗ count]   ← overlaps card top
[card:
  ¿QUÉ SIGNIFICA?
  <expression text>
  [btn 1] [btn 2] [btn 3] [btn 4]   ← all white, terracotta border
  <example sentence — cyan-bordered, hidden until answered>
  [Siguiente →]
]
```

## Score / progress semantics

- Progress bar fills by 1/58 **as soon as the player answers** (correct or not).
- Score counter shows `(correct + wrong) / 58` — total **answered**, matching the progress bar.
- Stats pill shows running correct and wrong counts with check/x Lucide icons inside coloured circles.

## Tech constraints

- Vanilla HTML + CSS + JS only. No libraries (Google Fonts CSS link is fine).
- All data hardcoded in the `<script>` block as a `const EXPRESSIONS = [...]` array.
- Single `index.html` — no other output files.

## Repository & deployment

- Remote: `git@github.com:lipcanu/expressions-flashcard-game.git` (default branch: `main`)
- Live URL: https://lipcanu.github.io/expressions-flashcard-game/ (GitHub Pages, served from root of `main`)
- **Never push to GitHub without explicit confirmation from Diana.**
- Tracked files: `index.html`, `expressions.csv`, `CLAUDE.md`, `README.md`.

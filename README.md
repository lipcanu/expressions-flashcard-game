# Spanish Expressions Flashcard Game

A single-file flashcard quiz to memorise 58 Spanish idiomatic expressions. Pure HTML/CSS/JS — no build tools, no dependencies.

**Play it:** https://lipcanu.github.io/expressions-flashcard-game/

## How it works

- The deck is shuffled at the start of each session.
- Each card shows an expression in Spanish; pick the correct meaning from four options.
- Answer with mouse or keyboard (`1`–`4` to choose, `Enter`/`Space` to advance).
- An example sentence is revealed after each answer.
- Final score and a motivational message at the end; play again to reshuffle.

## Files

- `index.html` — the entire game (UI, logic, and embedded expression data).
- `expressions.csv` — source data, used at authoring time to regenerate the embedded array.
- `CLAUDE.md` — design spec and theme tokens.

## Running locally

Just open `index.html` in any modern browser. No server required.

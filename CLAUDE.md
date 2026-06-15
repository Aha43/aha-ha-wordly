# Claude Instructions — Wordly Scores

## Context

Arne and Harald play the public daily Wordle game. After each game they text each other their attempt count (not the word). This repo tracks their head-to-head results. A **season** is one calendar month.

## Players

- **Arne** — repo owner
- **Harald** — friend

## File structure

```
README.md              ← TOC, one row per season, latest first
data.json              ← source data for the web page (one entry per game)
index.html             ← GitHub Pages scoreboard (renders data.json, no build step)
scores/
  YYYY-MM.md           ← one file per season
```

The public page lives at https://aha43.github.io/aha-ha-wordly/ and renders
entirely from `data.json` (stats are computed in the browser). `index.html` is
static — never hand-edit scores into it.

## Logging a score

When Arne says something like *"June 3 — Arne 4, Harald 3"*:

1. Open the current month's file in `scores/`.
2. Append a row to the games table (see format below).
3. Update the leader line under the title (see format below).
4. Recompute the stats block at the bottom of that file.
5. Update the matching row in `README.md` (wins, ties, spread, champion).
6. Update the `## Latest` section in `README.md` (see format below).
7. Append the game to the current season's `games` array in `data.json`
   (`{ "date": "Jun 3", "word": "CRANE", "a": 4, "h": 3 }`; use `"X"` for a
   failed solve). The page computes all stats from this, so no stat edits here.
8. Commit with a short message, e.g. `Add Jun 3 — Arne 4 Harald 3`.

When starting a new month, also add a new season object at the end of the
`seasons` array in `data.json` (`{ "month": "YYYY-MM", "title": "Month YYYY",
"games": [] }`).

## Monthly file format

Filename: `scores/YYYY-MM.md`

```markdown
# Month YYYY

**Arne leads on wins** — 1–0 · 1 tie · spread +2

| Date | Word | Arne | Harald | Spread | Winner |
|------|------|:----:|:------:|:------:|--------|
| Jun 1 | CRANE | 3 | 5 | +2 | Arne |
| Jun 2 | LIGHT | 4 | 4 | 0 | Tie |

---

## Stats

| | Arne | Harald |
|---|:---:|:---:|
| **Wins** | 1 | 0 |
| **Ties** | — | 1 |
| **Avg attempts** | 3.5 | 4.5 |
| **Total attempts** | 7 | 9 |
| **Season spread** | +2 (Arne ahead) | |

> Spread per game = Harald − Arne attempts. Season spread = sum of all games.  
> Positive = Arne ahead, negative = Harald ahead. X (failed) counts as 7.
```

## Season leader line format

The first line under the season title shows who is leading at a glance. Refresh
it after every game:

```markdown
**Arne leads on wins** — 5–4 · 3 ties · spread +2
```

- Format: `**[leader] leads on [wins/spread]** — A–H · T ties · spread S`
  (where A–H is Arne wins–Harald wins, T is tie count, S is season spread)
- Leader logic (same as README Latest):
  - More wins → `**[name] leads on wins**`
  - Wins equal and spread ≠ 0 → `**[name] leads on spread**`
  - Wins and spread both equal → `**All square**` (drop the "leads on …" wording)
- Use `1 tie` (singular) when there is exactly one tie.

## Spread definition

- **Per game:** `Harald_attempts − Arne_attempts`
  - Positive → Arne used fewer → Arne wins the game
  - Negative → Harald used fewer → Harald wins the game
  - Zero → Tie
- **Season spread:** sum of all per-game spreads
- Used for tiebreaking when wins are equal

## X (failed game)

A failed attempt (no solve) counts as **7** for all calculations.

## Starting a new month

When the first score of a new month is logged:

1. Create `scores/YYYY-MM.md` from the template above (empty table, zeroed stats).
2. Add a new row at the **top** of the seasons table in `README.md` (latest first).

## README seasons table format

```markdown
| Season | Arne wins | Harald wins | Ties | Season spread | Champion |
|--------|:---------:|:-----------:|:----:|:-------------:|----------|
| [June 2026](scores/2026-06.md) | 1 | 0 | 1 | +2 (Arne) | ongoing |
```

Champion column: `ongoing` during the month, then winner's name (or `Tie`) when the month ends.

## README Latest section format

Always replace the two lines under `## Latest` with fresh values after each game:

```markdown
## Latest

**Mon DD · WORD** — [winner] N, [loser] N → [winner] wins  (or "Tie" for equal attempts)

**Month YYYY:** Arne W – Harald W (T ties) · Spread S · [leader] ahead on [wins/spread]
```

Leader line logic:
- If one player has more wins: "[name] ahead on wins"
- If wins are equal and spread ≠ 0: "[name] ahead on spread"
- If wins and spread are both equal: "All square"

# Claude Instructions — Wordly Scores

## Context

Arne and Harald play the public daily Wordle game. After each game they text each other their attempt count (not the word). This repo tracks their head-to-head results. A **season** is one calendar month.

## Players

- **Arne** — repo owner
- **Harald** — friend

## File structure

```
README.md              ← TOC, one row per season, latest first
scores/
  YYYY-MM.md           ← one file per season
```

## Logging a score

When Arne says something like *"June 3 — Arne 4, Harald 3"*:

1. Open the current month's file in `scores/`.
2. Append a row to the games table (see format below).
3. Recompute the stats block at the bottom of that file.
4. Update the matching row in `README.md` (wins, ties, spread, champion).
5. Update the `## Latest` section in `README.md` (see format below).
6. Commit with a short message, e.g. `Add Jun 3 — Arne 4 Harald 3`.

## Monthly file format

Filename: `scores/YYYY-MM.md`

```markdown
# Month YYYY

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

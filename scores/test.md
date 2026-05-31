# Test Season

> This is a fake season used to verify scoring, stats, and spread calculations.

| Date | Word | Arne | Harald | Spread | Winner |
|------|------|:----:|:------:|:------:|--------|
| T-1 | CRANE | 3 | 5 | +2 | Arne |
| T-2 | LIGHT | 4 | 4 | 0 | Tie |
| T-3 | STOVE | 2 | 3 | +1 | Arne |
| T-4 | BEACH | 5 | 2 | -3 | Harald |
| T-5 | PIANO | X | 4 | -3 | Harald |
| T-6 | JAZZY | 4 | 6 | +2 | Arne |

---

## Stats

| | Arne | Harald |
|---|:---:|:---:|
| **Wins** | 3 | 2 |
| **Ties** | — | 1 |
| **Avg attempts** | 4.17 | 4.00 |
| **Total attempts** | 25 | 24 |
| **Season spread** | −1 (Harald ahead on attempts) | |

> Spread per game = Harald − Arne attempts. Season spread = sum of all games.  
> Positive = Arne ahead, negative = Harald ahead. X (failed) counts as 7.

### Verification

| Game | Harald − Arne | Running spread |
|------|:---:|:---:|
| T-1: CRANE (3 vs 5) | +2 | +2 |
| T-2: LIGHT (4 vs 4) | 0 | +2 |
| T-3: STOVE (2 vs 3) | +1 | +3 |
| T-4: BEACH (5 vs 2) | −3 | 0 |
| T-5: PIANO (X=7 vs 4) | −3 | −3 |
| T-6: JAZZY (4 vs 6) | +2 | −1 |

Arne wins the season (3–2), but Harald edges it on total attempts (24 vs 25).  
Spread tiebreaker would go to Harald — good to know before a real tie happens.

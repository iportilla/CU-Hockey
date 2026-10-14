# CU Boulder club hockey data (for pandas DataFrames)

Scraped on 10/14/2026 from the ACHA and Big Mountain Hockey Conference stats pages. Covers three
University of Colorado club teams:

| Team | Season | League / division | Source |
|---|---|---|---|
| CU Men's D1 | 2024-25 | ACHA MD1 WCHL | [schedule](https://www.achahockey.org/stats/schedule/410/46/all-months/homeaway?league=1&division=36&conference=-1) |
| CU Men's D2 | 2023-24 | ACHA MD2 BMHC | [schedule](https://www.achahockey.org/stats/schedule/339/34/all-months/homeaway?league=1&division=56&conference=-1) |
| CU Women's D1 | 2024-25 | ACHA WD1 WWCHL | [schedule](https://www.achahockey.org/stats/schedule/77/45/all-months/homeaway?division=71&league=1&conference=-1) |
| CU Men's D2 | 2026-27 (**in progress**) | BMHC | [schedule](https://www.bigmountainhockey.com/stats/schedule/339) |

Each team's roster, skater stats and goalie stats come from the same site (`/stats/roster/…`,
`/stats/player-stats/…`). For the current 2026-27 season only the schedule and skater stats were
pulled.

## Files

### Clean, combined files (start here)

| File | Rows | One row per |
|---|---|---|
| `cu_games.csv` | 117 | game (all 4 team-seasons) |
| `cu_skaters.csv` | 120 | player per team-season (goalies appear here too, with 0 points) |
| `cu_goalies.csv` | 9 | goalie per team-season |
| `cu_rosters.csv` | 84 | rostered player (no 2026-27 roster) |

**Keys:** `player_id` is the league's player ID, and it stays the same across seasons. Join on
`["player_id", "season"]` to combine stats with roster details. `game_id` identifies a game.

**`cu_games.csv` columns:** `team`, `season`, `game_id`, `date` (ISO), `day`, `home_away`,
`opponent`, `opponent_division` (MD1/MD2/WD1), `venue`, `cu_goals`, `opp_goals`, `result`
(W / L / OTL / SOL; blank if not yet played), `status` (Final / Final OT / Final SO / Scheduled),
`start_time` (upcoming games only).

**`cu_skaters.csv`:** `gp`, `goals`, `assists`, `points`, `points_per_game`, `pp_goals`,
`sh_goals`, `gw_goals`, `shootout_gw_goals`, `pim` (penalty minutes), plus `rookie` (True/False)
and `pos`.

**`cu_goalies.csv`:** `wins`, `losses`, `ot_losses`, `so_losses`, `goals_against`, `gaa`
(goals-against average), `saves`, `save_pct`, `shutouts`, `minutes`, `so_wins`.

**`cu_rosters.csv`:** `position_group` (Forwards/Defense/Goalies), `height` ("6-1"),
`height_in` (73), `weight_lb`, `shoots` (L/R), `hometown_city`, `hometown_state`.

### `as_scraped/`

One CSV per page, as the site showed it, for cleaning exercises. Things students will run into:

- Scores of `-` for games not yet played (2026-27), so the column loads as text
- Dates with no year (`Fri, Sep 6`) that span two calendar years
- Team names with a prefix (`MD1 University of Colorado`), and CU can be either `Visiting` or `Home`
- `Empty Net` and `Totals` summary rows mixed into the goalie tables
- Rookies marked with `*` in their own column
- Women's roster weights listed as `0` (not given). The clean file uses blanks (NaN)
- Hometowns sometimes end in `, United States` and sometimes don't
- The CU rink appears under two names (`CU Boulder Rec Center Ice Rink (CO)` and
  `University Of Colorado Boulder Recreation Center`), and one venue is literally named
  `z delete duplicate Boss Ice Arena`
- `SH%` is always 0.0 (the league doesn't track shots), so it's dropped from the clean file

## Ideas for exercises

- **Selecting and filtering:** home games only, or players with 10 or more points
- **Sorting:** the top 5 scorers per team, using `sort_values` plus `groupby().head()`
- **New columns:** goal differential, `points / gp`, a W/L flag
- **groupby:** record and goals for/against by team-season, home vs. away, or day of the week.
  Average height by position group
- **merge:** skater stats + roster. Two 2023-24 players (Saul Drantch, Arthur Street) have stats
  but aren't on the roster, which is a good `how="left", indicator=True` example
- **Across seasons:** five players appear in both the 2023-24 and 2026-27 Men's D2 data (for
  example Marius Krasauskas and Kory Diponio). Join on `player_id` to compare
- **Checking against the source:** the game results reproduce the goalie W-L totals (Men's D1
  18-16-1-1). The Men's D1 schedule shows 110 goals for, but the skaters scored 108, because the
  two shootout winners are counted in the game score
- **Missing data:** `weight_lb` is NaN for the women's team. `cu_goals` is NaN for upcoming games
- **Dates:** `pd.read_csv(..., parse_dates=["date"])`, then `.dt.month_name()` and `.dt.day_name()`

## Setup

You need pandas (and matplotlib for the chart in the notebook):

```bash
pip install pandas matplotlib
```

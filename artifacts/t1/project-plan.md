# Project Plan

## Project Goal

Develop a clear and reproducible research workflow for comparing three familiar asset classes represented by illustrative ETFs:

- `SPY` — US equities
- `TLT` — long-term US Treasury bonds
- `GLD` — gold

The comparison will focus on return, volatility, drawdown, and cost characteristics, using the fixed dataset provided in the repository.

## Available Data

The repository provides `data/etf_snapshot.csv` (one row per ETF) plus `data/data_dictionary.md`. The dataset is **synthetic teaching data**: all numeric values are illustrative assumptions, not live or historical market observations.

| Column | Meaning |
|---|---|
| `ticker` | Short identifier for the illustrative ETF |
| `asset_class` | Broad type of asset represented by the ETF |
| `expected_return_pct` | Illustrative annual return assumption (%) |
| `volatility_pct` | Illustrative annual variability assumption (%) |
| `max_drawdown_pct` | Illustrative largest peak-to-trough loss (%) |
| `expense_ratio_pct` | Illustrative annual fund fee (%) |

## Expected Final Deliverable

A concise written plan and, in later steps, a reproducible analysis workflow that documents how `SPY`, `TLT`, and `GLD` compare across the available metrics. The analysis steps themselves are planned work and are not yet completed.

## Three Project Milestones

1. **Project setup (T1):** Create this initial project plan, confirming the goal, data, and constraints.
2. **Exploratory analysis:** Compute and compare summary statistics (return, volatility, drawdown, expense) across the three ETFs and produce a readable comparison.
3. **Verification and review:** Check that the analysis is reproducible, confirm results against the source data, and finalize the write-up for review.

## One Data Limitation

All numeric values in `etf_snapshot.csv` are synthetic teaching assumptions, so results cannot be used as investment advice or as a basis for any real investment decision. The dataset also omits correlations, taxes, transaction costs, liquidity, currency exposure, and investor-specific constraints.

## Next Action

Confirm that this plan matches the repository contents, then save the file with Git. JiuWenSwarm will not commit or push the change; that step belongs to the students during T1.

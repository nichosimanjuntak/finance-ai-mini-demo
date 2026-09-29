# T2 ETF Comparison: SPY, TLT, GLD — Fees and Drawdown

T1 planned a comparison of SPY, TLT, and GLD across cost and risk characteristics; this T2 report upgrades that plan from synthetic snapshot assumptions to the real daily T2 ETF Data Pack and covers the annual-fee and historical-drawdown parts (return analysis stays outside this task).

## Inputs and method

- **Input paths:** `data/t2/fund_info.csv` (fee disclosures), `data/t2/daily_prices.csv` (7,536 daily observations), `data/t2/data_dictionary.md` (field definitions); `artifacts/t1/project-plan.md` used only as context.
- **Preparation date:** 2026-09-25 (T2 ETF Data Pack; historical inputs recorded as downloaded 2026-09-20 from the Yahoo Finance chart API, `adjusted_close` enabled).
- **Fee disclosure dates (per ETF; all re-accessed 2026-09-25 per `fee_accessed_on`):** SPY — fund-information as-of 2026-09-10, fee-specific effective date **not stated**; TLT — current prospectus, specific date **not stated** in the fee panel; GLD — effective date **not stated** in the selected field.
- **Common drawdown period:** 2016-09-01 through 2026-08-31 inclusive (2,512 sessions per ETF). **Frequency:** daily (US market sessions; early closes included, weekends/closures absent). **Adjustment basis:** Yahoo `adjusted_close` (provider split and dividend adjustments).
- **Script:** `artifacts/t2/calculate_drawdown.py`. **Command executed:** `python3 artifacts/t2/calculate_drawdown.py`.
- **Input-check result:** all checks passed — ticker set is exactly {SPY, TLT, GLD}; 7,536 unique ticker/date pairs; dates ascending within each ticker; all `close`/`adjusted_close` positive and finite; 2,512 rows per ETF; common first date 2016-09-01 and last date 2026-08-31; identical date sets across tickers.
- **Calculation method:** for each ticker, over all `adjusted_close` observations, `drawdown_t_pct = (adjusted_close_t / cumulative_high_t - 1) * 100`, where `cumulative_high_t` is the largest adjusted_close from the window start through day t; maximum drawdown is the minimum over the window. On ties, the earliest trough and its earliest corresponding peak were selected; peak is required to be on or before trough. Full precision kept internally; rounded to two decimals only for display.

## 1. Comparison

| Ticker | Annual expense ratio (%) | Maximum drawdown (%) | Peak date | Trough date |
|---|---|---|---|---|
| SPY | 0.0945 | -33.72 | 2020-02-19 | 2020-03-23 |
| TLT | 0.15 | -48.35 | 2020-08-04 | 2023-10-19 |
| GLD | 0.4 | -26.40 | 2026-01-29 | 2026-07-16 |

Fees preserve the disclosed precision from `fund_info.csv` (0.0945%, 0.15%, 0.4%). Maximum drawdowns are displayed to two decimals; full-precision values are SPY -33.717257210811404%, TLT -48.351126073648132%, GLD -26.404517857029663%.

## 2. Observation

The ETF with the smallest drawdown loss (closest to zero) in this 2016-09-01..2026-08-31 period is **GLD at -26.40%**, versus SPY at -33.72% and TLT at -48.35%; comparing the displayed two-decimal results, there are **no ties**. These drawdowns were calculated from the `adjusted_close` series, not read from a precomputed snapshot; drawdowns are non-positive, so closer to zero means a smaller loss magnitude. Limitation: these are daily-close drawdowns within the fixed ten-year window and current fee disclosures — not all-time risk measures or ten-year average fees — and they exclude trading costs such as bid/ask spreads.

## 3. Agent Check

This is the Agent's own self-check; it is not independent verification, and no student has checked the data.

- **Chosen ETF:** SPY (reported peak 2020-02-19, trough 2020-03-23).
- **Source rows re-read from `data/t2/daily_prices.csv`:** 2020-02-19 SPY `close=338.3399963378906`, `adjusted_close=307.6394958496094`; 2020-03-23 SPY `close=222.9499969482422`, `adjusted_close=203.91189575195312`.
- **Check command:** inline Python (standard library only) that re-reads the CSV rows above and recomputes `(trough / peak - 1) * 100`; a second pass recomputes the full series for all three tickers.
- **Actual output:** `(203.91189575195312 / 307.6394958496094 - 1) * 100 = -33.717257210811404%`; peak-before-trough confirmed (`2020-02-19 <= 2020-03-23`); full-series recomputation reproduced SPY -33.717257210811404, TLT -48.351126073648132, GLD -26.404517857029663 with peak-on-or-before-trough order for each.
- **Comparison:** the recomputed value matches the report's full-precision value exactly (displayed -33.72%). The full-series pass confirms the calculation used all dates, `adjusted_close` values, cumulative highs from the window start, and the earliest-trough/earliest-peak tie rule. The observation was checked against all three results: GLD (-26.40%) is closest to zero with no ties.
- **Correction/recheck:** none required; no errors were found.

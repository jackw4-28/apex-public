# apex-public

Trimmed copy of the U.S. SEC Financial Statement Data Sets, 2012 Q1 to 2026 Q3.

Source: https://www.sec.gov/data-research/sec-markets-data/financial-statement-data-sets (public U.S. government data, values as filed by each company).

## What is kept

- Annual and quarterly reports only (forms 10-K and 10-Q).
- Whole-company figures only (rows with a co-registrant or a segment are dropped).
- 43 core financial items (for example Assets, Revenues, NetIncomeLoss).

## Files (folder `sec-trimmed`)

- `sub_<quarter>.csv.gz`: one row per report. Columns: adsh (report id), cik (SEC company number), name, sic, form, period, fy, fp, filed (date the report reached the SEC).
- `num_<quarter>.csv.gz`: one row per reported number. Columns: adsh, tag (item name), ddate (period end), qtrs (number of quarters covered, 0 for a point in time), uom (unit), value.
- `build_log.csv`: counts per quarter from the build.

A quarter here is the quarter in which the SEC received the report, not the company's fiscal quarter.

## Known gaps

- September 2016 holds only a small share of the reports filed that month. August to September 2012 and March 2016 are also thin.
- Not every filer is present in every quarter.
- Nothing has been corrected or restated; numbers are as filed.

## Compact plain-text version (folder `sec-compact`)

Same data, uncompressed and smaller, for tools that can only read plain text.

- `r_<quarter>.csv`: one row per report. Columns: i (row number within the quarter), cik, form, period, fp, filed.
- `v_<quarter>.csv`: one row per number. Columns: i (report row number in the matching r file), t (item code, see `tags.csv`), q (quarters covered, 0 for a point in time), v (value), u (unit; blank means USD).
- Only current-period numbers are kept (the number's period end equals the report's period). The prior-period figures each report repeats for comparison are dropped.

### Wider item list (from 2026-11-21)

`sec-compact` now holds 124 items instead of 43 (see `tags.csv`; the first 43 codes are unchanged). The extra items are the other names companies use for debt, interest, depreciation, costs, capital spending, cash, per-share earnings and dividends. `sec-trimmed` still holds the first 43 items only.

## Company number to ticker candidates (folder `match`)

`cik_ticker_candidates.csv` links SEC company numbers to ticker candidates taken from the leading letters of each report's XBRL file name. Columns: cik, ticker, first and last (dates of the first and last report using that name), last_any (the company's last report in the data), bk (1 if on a list of confirmed bankruptcies). This is a clue, not a verified ticker history: about one company in eight has no candidate, and some candidates are wrong.

`format-test` holds files used to test download speed.

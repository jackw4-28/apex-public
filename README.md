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

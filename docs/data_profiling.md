# Data Profiling

**Date:** 2026-10-28
**Data:** `data/raw/World Important Dates.csv`, 1,096 rows × 12 columns
**Where:** the `Profiling` sheet in `workbook/historical_events_analysis.xlsx`. Every number below comes from a formula on that sheet, so it updates if the data is refreshed.

**Bottom line:** the data is usable, but it needs cleaning before analysis. The main problems are disguised missing values ("Unknown" and space-only cells), 8 duplicate events, and a Year column stored as text with BC dates and an impossible year 0.

## 1. Missing values per column

| Column | Empty | Spaces only | "Unknown" | Total missing | % missing |
|---|---:|---:|---:|---:|---:|
| Date | 0 | 26 | 427 | 453 | 41.3% |
| Month | 0 | 0 | 395 | 395 | 36.0% |
| Important Person/Group Responsible | 0 | 0 | 56 | 56 | 5.1% |
| Place Name | 0 | 0 | 20 | 20 | 1.8% |
| All other 8 columns | 0 | 0 | 0 | 0 | 0% |

- No cell is truly empty (`COUNTBLANK` = 0 everywhere). Missing data is disguised as the word "Unknown", or as 26 Date cells that hold only spaces. A plain blank check would have missed all of it.
- **Year has no missing values**, so every event can be placed on the timeline. Day and month are often missing, so the analysis will work at **year level**, not exact dates.

## 2. Distinct values per column

| Column | Distinct values | What it means |
|---|---:|---|
| Sl. No | 1,096 | Unique for every row, so it works as an ID |
| Name of Incident | 1,030 | 66 rows repeat a name (see duplicates) |
| Year | 330 | Good spread across time |
| Country | 113 | Needs grouping into regions for analysis |
| Type of Event | 402 | Far too detailed to chart; needs grouping into ~8 categories |
| Outcome | 4 | Positive, Negative, Mixed, Ongoing; ready to use |

## 3. Duplicates

- Rule: the same **Name of Incident + Year + Country** appears more than once.
- **16 rows = 8 events entered twice**, e.g. Fukushima Daiichi Nuclear Disaster (Sl. No 305 and 649).
- 7 pairs are identical in date, month, year and country. For *Battle of Điện Biên Phủ*, one copy has a full date (7 May) and the other says "Unknown".
- **Plan:** remove 8 rows and keep the more complete copy, giving **1,088 rows** after cleaning.

## 4. Year column

| Check | Result |
|---|---:|
| Years written with "BC" (e.g. "2600 BC") | 7 |
| Year = 0 (no such year in the calendar) | 2 |
| Years with extra spaces (" 1754 BC ") | 1 |
| Latest year | 2022 |

- The column is **text**, not numbers, because of the "BC" values. It can't be sorted or used in maths until it is converted.
- The 2 rows with year 0 are *Introduction of Buddhism to China* and *Founding of Teotihuacan*. Both need a decision on Day 3.

## 5. Other issues noticed

- **Hyphens were replaced by "Unknown"** inside text in 234 rows, e.g. "IndoUnknownPakistani War of 1971", "GuineaUnknownBissau", and one Date of "23Unknown25". This most likely came from a bad find-and-replace by the dataset author.
- **Sl. No has gaps**: it goes up to 1,151 for 1,096 rows. This is harmless, since it is only an ID.
- A few text cells have leading or trailing spaces (Year 1, Affected Population 2, Important Person 2).

## What Day 3 cleaning will fix

| Issue | Fix |
|---|---|
| Spaces around values | Trim all text columns |
| Space-only Date cells | Treat as "Unknown" |
| "Unknown" inside words | Put the hyphen back ("Indo-Pakistani") |
| 8 duplicate events | Remove, keeping the more complete copy |
| Year stored as text, BC dates | New numeric year column: BC becomes negative (2600 BC → -2600) |
| Year = 0 | Review the 2 events and correct or flag them |

# Cleaning Log

**Date:** 2026-10-29
**Input:** `data/raw/World Important Dates.csv` (1,096 rows × 12 columns)
**Output:** the `Clean_Data` query and sheet in `workbook/historical_events_analysis.xlsx`, exported to `data/cleaned/world_important_events_clean.csv` (**1,088 rows × 13 columns**)

All cleaning happens in **Power Query**. `Clean_Data` is a *Reference* of `Raw_Data`, so the raw import is never changed. Each step below is one entry under Applied Steps. Refreshing the query reruns every step.

## Summary

| # | Step (Applied Steps name) | Problem | Fix | Rows / cells affected |
|---|---|---|---|---:|
| 1 | Trimmed Text | Extra spaces before or after values | `Text.Trim` on all 11 text columns | 31 cells |
| 2 | Replaced Value | Missing values written as the word "Unknown" | Whole cell "Unknown" → `null` | 898 cells |
| 3 | Replaced Value1 | 26 Date cells held only spaces (empty after trimming) | Empty Date → `null` | 26 cells |
| 4 | Replaced Value2 | Hyphens inside words had been replaced by "Unknown" (e.g. "Sino**Unknown**Japanese") | "Unknown" inside text → "-" | 234 rows |
| 5 | Replaced Value3 | Step 4 also changed one real use of the word | "- assailants" → "Unknown assailants" | 1 cell |
| 6 | Removed Duplicates | 8 events were entered twice | Keep first row per Name + Year + Country | 8 rows removed |
| 7 | Added Custom | Year is text, with BC years like "2600 BC" | New `Year_Num` number column, BC years as negatives | 7 BC rows |
| 8 | Added Custom1 → Changed Type | Two events have year 0, which does not exist | Replace with a sourced approximate year, set type to Whole Number | 2 rows |

## Details

### 1–3. Spaces and missing values

- Trimmed cells by column: Date 26, Affected Population 2, Important Person/Group Responsible 2, Year 1.
- "Unknown" → `null` by column: Date 427, Month 395, Important Person/Group Responsible 56, Place Name 20.
- Why `null` and not the text "Unknown": Excel and Power Query count `null` as blank, so `COUNTA`, averages and PivotTables treat it as missing instead of as a real value.

Missing values left after cleaning (all real gaps, not fixable from the data):

| Column | Missing | % of 1,088 |
|---|---:|---:|
| Date | 451 | 41.5% |
| Month | 393 | 36.1% |
| Important Person/Group Responsible | 56 | 5.1% |
| Place Name | 20 | 1.8% |

### 4–5. "Unknown" inside words

The source file had replaced every hyphen with "Unknown", e.g. "Sino**Unknown**Japanese" or "COVID**Unknown**19". This affected 234 rows (Impact 118, Name of Incident 93, Person/Group 53, Affected Population 8, Place Name 8, Type of Event 5, Country 1, Date 1). Putting the hyphen back restores the original text.

The only cell where "Unknown" was a real word is "Unknown assailants" (Important Person/Group Responsible). Step 5 puts it back. After cleaning, that is the only cell in the table that still contains "Unknown".

### 6. Duplicates

Rule: same **Name of Incident + Year + Country**. Power Query keeps the first row and drops later copies.

| Event | Kept (Sl. No) | Removed (Sl. No) |
|---|---:|---:|
| Fukushima Daiichi Nuclear Disaster (2011, Japan) | 305 | 649 |
| Cultural Revolution (1966, China) | 160 | 193 |
| Sydney Opera House Opens (1973, Australia) | 333 | 344 |
| Port Arthur Massacre (1996, Australia) | 337 | 348 |
| Battle of Điện Biên Phủ (1954, Vietnam) | 436 | 474 |
| Discovery of Insulin (1921, Canada) | 730 | 754 |
| Official Languages Act (1969, Canada) | 733 | 757 |
| Establishment of Nunavut (1999, Canada) | 743 | 759 |

For Điện Biên Phủ the kept copy (436) is the more complete one: it has the full date (7 May), and the removed copy had "Unknown". The other 7 pairs were identical in date, month, year and country.

### 7. Year as a number (`Year_Num`)

```
if Text.Contains([Year], "BC")
then -Number.From(Text.Trim(Text.Replace([Year], "BC", "")))
else Number.From([Year])
```

"2600 BC" becomes -2600 and "1947" becomes 1947. Negative years sort and chart in the right order, before year 1. The original `Year` text column is kept for display.

BC events: Indus Valley Civilization (-2600), Stonehenge Completion (-2500), Hammurabi's Code (-1754), Battle of the Ten Kings (-1400), Olmec Civilization (-1400), Phoenician Trade (-1100), Gadir founded (-1100).

Range after cleaning: **-2600 to 2022**.

### 8. Year 0 corrections

The calendar goes from 1 BC straight to 1 AD, so "0" is an error in the source. Instead of deleting the two events, each one was given an approximate year from a public source:

| Sl. No | Event | Was | Now | Source |
|---:|---|---:|---:|---|
| 150 | Introduction of Buddhism to China | 0 | **68** | White Horse Temple founded under Emperor Ming of Han, c. 68 AD ([Wikipedia: History of Chinese Buddhism](https://en.wikipedia.org/wiki/History_of_Chinese_Buddhism)) |
| 1139 | Founding of Teotihuacan | 0 | **-100** | "established around 100 BCE" ([Wikipedia: Teotihuacan](https://en.wikipedia.org/wiki/Teotihuacan)) |

Both are approximate dates. They keep the events in the right century and era.

## Known issues left as they are

- **Date column has 13 values that are not a day of the month:** years (1956, 1998, 1972, 2004, 1904, 1917, 1936), month names (October, March), ranges ("6 and 9", "23-25") and numbers (509, 264). Sl. No: 108, 119, 120, 121, 222, 225, 227, 279, 295, 793, 858, 859, 1038. The analysis works at year level and does not use Date, so these are kept as they are.
- **Country mixes countries, cities and historic names** (e.g. Babylon, Tehran, USSR / Soviet Union, Persia, "Kuwait, Iraq"). This is handled on Day 4 by the country-to-region lookup.
- **Type of Event has 402 distinct values.** This is grouped into broad categories on Day 4.

## Check after cleaning

- Rows: 1,096 → **1,088** (8 duplicates removed). Shown in Excel as "1,088 rows loaded".
- Every row has a whole-number `Year_Num`; no year 0 remains.
- An independent re-run of the same rules in Python on the raw CSV matched the `Clean_Data` sheet cell for cell (0 differences).

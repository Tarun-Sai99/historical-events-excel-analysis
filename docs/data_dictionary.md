# Data Dictionary

**Source:** [World Important Events - Ancient to Modern](https://www.kaggle.com/datasets/saketk511/world-important-events-ancient-to-modern) (Kaggle, by saketk511)
**File:** `data/raw/World Important Dates.csv`
**Size:** 1,096 rows (one row per historical event) × 12 columns
**Grain:** each row is one event. `Sl. No` identifies it.

This describes the data **as downloaded**, before any cleaning. Problems noted here are fixed on Day 3 and recorded in `cleaning_log.md`.

| # | Column | Type in raw file | Meaning | Example | Notes |
|---|--------|------------------|---------|---------|-------|
| 1 | Sl. No | Whole number | Serial number of the event | 1 | Unique for every row, but has gaps (runs 1 to 1151 for 1,096 rows) |
| 2 | Name of Incident | Text | Name of the event | Battle of Panipat | Hyphens were replaced by the word "Unknown" (e.g. "IndoUnknownPakistani War of 1971") |
| 3 | Date | Text | Day of the month the event happened | 21 | "Unknown" in 427 rows; 26 more look blank but contain only spaces |
| 4 | Month | Text | Month name | April | "Unknown" in 395 rows |
| 5 | Year | Text | Year the event happened | 1526, 2600 BC | Stored as text because 7 BCE years are written like "2600 BC"; 2 rows have year 0, which doesn't exist |
| 6 | Country | Text | Country where the event happened | India | 113 distinct values; spellings to be standardised |
| 7 | Type of Event | Text | Kind of event | Battle, Political | 402 distinct values, so too detailed to analyse directly; will be grouped into broad categories |
| 8 | Place Name | Text | City or area within the country | Panipat | "Unknown" in 20 rows; "Nationwide" used for country-wide events |
| 9 | Impact | Text | One-line description of the result | Foundation of the Mughal Empire in India | Free text, used for context only |
| 10 | Affected Population | Text | Who was affected | Northern Indian kingdoms | Free text, not a number |
| 11 | Important Person/Group Responsible | Text | Key person or group | Babur | "Unknown" in 56 rows |
| 12 | Outcome | Text | Overall result | Positive | 4 values: Positive (589), Negative (304), Mixed (202), Ongoing (1) |

## Columns added during cleaning and analysis

These columns are in the `Clean_Data` table (and in `data/cleaned/world_important_events_clean.csv`). `Year_Num` comes from Power Query (Day 3). The other five are Excel formulas (Day 4).

| # | Column | Type | How it is made | Example | Values |
|---|--------|------|----------------|---------|--------|
| 13 | Year_Num | Whole number | Power Query: Year as a number, BC years negative, year-0 rows corrected | -2600, 1947 | -2600 to 2022 |
| 14 | Century | Whole number | `=ROUNDUP([@Year_Num]/100,0)`. Negative means BC | 20 (1947), -26 (2600 BC) | -26 to 21 |
| 15 | Era | Text | `LET` + `IFS` on Year_Num | Contemporary | Ancient (to 499), Medieval (500–1499), Early Modern (1500–1799), Modern (1800–1945), Contemporary (1946+) |
| 16 | Country_Std | Text | `XLOOKUP` of Country in the `country_region` table | Babylon → Iraq | 94 countries (cities and old names mapped to a modern country; USSR kept as its own name) |
| 17 | Region | Text | `XLOOKUP` of Country in the `country_region` table | South Asia | 10 world regions, plus "Multiple Regions" for the one Spain/USA event |
| 18 | Category | Text | `XLOOKUP` of Type of Event in the `event_type_category` table | War & Conflict | 9 categories grouping the 402 event types |

### Lookup tables (`Lookups` sheet, source files in `data/reference/`)

- **country_region.csv**: 113 rows, `Country` → `Country_Standard`, `Region`. Examples: Babylon, Basra, Mosul → Iraq; Tehran, Persia → Iran; Samarkand, Bukhara, Tashkent, Uzbek SSR → Uzbekistan; Malaya, Malacca → Malaysia; England → UK; Soviet Union → USSR. Russia and the USSR are placed in Europe.
- **event_type_category.csv**: 402 rows, `Type of Event` → `Category`. Mixed types go by their main subject (e.g. "Military/Political" → War & Conflict, "Nuclear Test" → War & Conflict, "Space Exploration Disaster" → Disasters & Accidents).

Both lookups use "Not found" as the fallback. After loading, no row shows "Not found".

# Historical Events & Timeline Analysis (Excel)

**Question:** How have major world events been spread across time, regions and categories, from ancient times up to the 21st century?

**Tools:** Microsoft Excel 2021 (Power Query, formulas, PivotTables, charts, slicers)

**Dataset:** [World Important Events - Ancient to Modern](https://www.kaggle.com/datasets/saketk511/world-important-events-ancient-to-modern) by saketk511 on Kaggle. Used for learning purposes.

> Work in progress. This README will be completed as the project is built.

## Project structure

```
data/raw/         original dataset, never edited
data/reference/   lookup tables (country to region, event type to category)
data/cleaned/     cleaned data exported from Excel
workbook/         the Excel workbook
docs/             data dictionary, profiling notes, cleaning log, insights
images/           chart and dashboard screenshots
```

## The data

- **1,096 events** (one row per event) with **12 columns**: name, day, month, year, country, type of event, place, impact, affected population, person or group responsible, and outcome (Positive, Negative, Mixed or Ongoing).
- Covers **2600 BC to 2022 AD** across **113 countries**.
- Imported into Excel with **Power Query** (`Raw_Data` query), so the raw file is never edited and the workbook can be refreshed.
- Every column is described in the [data dictionary](docs/data_dictionary.md).

## Progress

- [x] Day 1: Set up repo and load data
- [x] Day 2: Profile the data
- [x] Day 3: Clean the data
- [ ] Day 4: Add helper columns (century, era, region, category)
- [ ] Day 5: Explore with formulas and PivotTables
- [ ] Day 6: Build charts
- [ ] Day 7: Build interactive dashboard
- [ ] Day 8: Write insights and finish README

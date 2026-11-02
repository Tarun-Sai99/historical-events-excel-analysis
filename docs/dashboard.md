# Dashboard

**Date:** 2026-11-02
**Where:** the `Dashboard` sheet, the first sheet in `workbook/historical_events_analysis.xlsx`.

One page that answers the project question at a glance: how major world events are spread across time, regions and categories.

## Layout

1. **Title and subtitle** (rows 1–2)
2. **Four KPI cards** (rows 4–5)
3. **Five charts** (from row 11): events by era, events by century, events by region, category mix in each era, outcome by category
4. **Three slicers** on the right: **Era**, **Region**, **Category**

## KPI cards

Each card is linked to a PivotTable with `GETPIVOTDATA`, so it changes with the slicers.

| Card | Formula | Value (no filter) |
|---|---|---:|
| Total events | `=GETPIVOTDATA("Events",Analysis!$A$3)` | 1,088 |
| From after 1945 | `=IFERROR(GETPIVOTDATA("% of Events",Analysis!$A$3,"Era","Contemporary"),0)` | 55.4% |
| Top region | `=Analysis!H4` (first row of the region PivotTable, sorted largest first) | Europe |
| Negative outcomes | `=IFERROR(GETPIVOTDATA("Sl. No",Analysis!$K$18,"Outcome","Negative"),0)` | 27.8% |

`IFERROR` shows 0% instead of `#REF!` when a filter leaves no matching events (for example, selecting only the Ancient era leaves no Contemporary events).

## Slicers

- All three slicers are connected to **all five PivotTables** (Slicer → Report Connections). This works because the PivotTables share one pivot cache built on the `Clean_Data` table.
- Clicking a slicer button filters every chart and every KPI card at once. Ctrl+click selects several items. The filter icon in the slicer header clears it.

Example: selecting **Europe** in Region shows 268 events, and the charts show how European events split across eras and categories.

## How to update

If the source data changes: **Data → Refresh All**. Power Query reloads and cleans the CSV, the helper columns recalculate, and all PivotTables, charts and KPI cards update.

# Charts

**Date:** 2026-11-01
**Where:** the `Dashboard` sheet (called `Charts` until Day 7) in `workbook/historical_events_analysis.xlsx`. All five are **PivotCharts** built on the PivotTables in the `Analysis` sheet, so they update when the data is refreshed.

Each chart title states the finding, not just the topic, so a reader gets the point without studying the axes.

| # | Title | Chart type | Source | Why this chart type |
|---|---|---|---|---|
| 1 | Over half of events are from after 1945 | Combo: columns (count) + line (% of events) on a second axis | Pivot 1, events by era | Shows both the size and the share of each era. Counts and percentages need separate axes. |
| 2 | 84% of events come from the last 3 centuries | Clustered column | Pivot 2, events by century | One bar per century, in time order. The jump at the end is the story. Axis title explains that negative = BC. |
| 3 | Europe has 1 in 4 events | Horizontal bar, sorted largest first, with data labels | Pivot 3, events by region | Long region names read better on a horizontal axis. Sorted bars make ranking obvious; labels replace the value axis. |
| 4 | War peaks in the Modern era, politics leads after 1945 | 100% stacked column | Pivot 4, % of each era | Eras have very different sizes (16 to 603 events), so each bar is scaled to 100% to compare the mix fairly. |
| 5 | Disasters are 97% negative, but only 59% of wars are | 100% stacked bar | Pivot 5, % of each category | Compares how each category tends to turn out. Colors carry meaning: green = Positive, red = Negative, grey = Mixed, dark blue = Ongoing. |

## Design choices

- **Field buttons hidden** on all charts, so they look like finished visuals rather than working tools.
- **Legends removed** where there is only one series (charts 2 and 3).
- **Bar charts reversed** (chart 3) so the largest value is at the top, matching how people read a ranking.
- **To build chart 4**, Pivot 4 was flipped so each row is an era (eras in Rows, categories in Columns, % of Row Total). Pivot 5 was moved down to K18 to make room.

# Insights

**Question:** How have major world events been spread across time, regions and categories, from ancient times up to the 21st century?

**Data:** 1,088 events (after cleaning) from the Kaggle "World Important Events" dataset, 2600 BC to 2022.

Every number below comes from the PivotTables in `workbook/historical_events_analysis.xlsx`. Most can be reproduced on the `Dashboard` with the slicers.

## Key findings

### 1. The record leans heavily toward recent history

- **55% of events happened after 1945**, and **84% in the last three centuries** (19th–21st).
- The 20th century alone has **544 events (50%)**. Before the 15th century, no century has more than 12.
- The busiest decade is the **2010s (139 events)**, followed by the 1940s (89), the decade of World War II.

**So what:** this dataset tells us more about how well recent events are documented than about how "eventful" each period was. Any comparison across eras should use percentages, not raw counts.

### 2. Europe dominates, especially before 1800

- **Europe has 268 events (25%)**, the most of any region. South Asia (162) and East Asia (148) follow.
- Before 1800, Europe has **90 of 178 events (51%)**.
- Latin America (52) and Central Asia (25) are the least covered.

*On the dashboard:* select Ancient, Medieval and Early Modern in the Era slicer and look at the region chart.

### 3. What makes the record changes with each era

- **Ancient:** mostly **culture and religion (44%)**, such as civilizations, monuments and the spread of religions.
- **Modern (1800–1945):** **war peaks at 33%** of events, the era of colonial wars and the two World Wars.
- **Contemporary (1946+):** **politics and law lead (28%)**. War drops to 15%, while society, health and disasters grow.
- Half of all War & Conflict events (**119 of 234**) are from the 20th century.

### 4. Africa's story is independence

- **95% of Sub-Saharan African events are from after 1945.**
- **More than half (43 of 79)** are Independence & Nation-Building, the highest share of any region.
- Of the 142 independence events overall, **80 are in the 20th century**, the era of decolonisation.

*On the dashboard:* select Sub-Saharan Africa in the Region slicer and look at the category chart.

### 5. Outcome labels are a point of view, not a fact

- Overall, **54% of events are marked Positive** and **28% Negative**.
- Disasters are **97% Negative**, as expected. But **only 59% of wars** are Negative, because wars that led to independence or victory are often marked Positive.
- Contemporary events are more often Positive (56%) than Modern ones (47%).

**So what:** the Outcome column reflects the dataset author's judgement. It is useful as a rough signal, not as a measure of real impact.

## Limitations

- **Selection bias:** the dataset is a curated list, not a complete record. Counts show what the author chose to include.
- **Missing details:** 41% of events have no day and 36% no month, so the analysis works at year level.
- **My own groupings:** Region and Category come from lookup tables I built (`data/reference/`). Some events could fit more than one category, and a few choices (for example, Russia in Europe) are judgement calls.
- **Two corrected years:** the two "year 0" events were given sourced approximate years (see the [cleaning log](cleaning_log.md)).

## Next steps

- Add a population or GDP measure per region to compare events per capita, not just counts.
- Use the Impact text to tag events by theme (for example, wars that ended in independence).
- Rebuild the dashboard in Power BI to add a year-by-year timeline slider.

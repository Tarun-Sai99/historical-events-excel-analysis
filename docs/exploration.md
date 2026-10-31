# Data Exploration (PivotTables)

**Date:** 2026-10-31
**Where:** the `Analysis` sheet in `workbook/historical_events_analysis.xlsx`. Five PivotTables, all built on the `Clean_Data` table (1,088 events). Right-click any of them → **Refresh** to update after the data changes.

## 1. Events by era (A3)

| Era | Events | % of events |
|---|---:|---:|
| Ancient (to 499) | 16 | 1.5% |
| Medieval (500–1499) | 88 | 8.1% |
| Early Modern (1500–1799) | 74 | 6.8% |
| Modern (1800–1945) | 307 | 28.2% |
| Contemporary (1946+) | 603 | 55.4% |

**Finding:** the dataset leans heavily toward recent history. More than half of all events happened after 1945, and 83.6% after 1800.

## 2. Events by century (E3)

- 26 different centuries, from the 26th century BC to the 21st century AD.
- The 19th, 20th and 21st centuries hold **910 of 1,088 events (84%)**. The 20th century alone has 544 (50%).
- Before the 15th century, no century has more than 12 events.

**Finding:** the timeline is very uneven. Early periods are covered by a few landmark events (Indus Valley, Stonehenge, Hammurabi's Code), not by steady coverage. Charts by century should use this as context, not as a measure of how "eventful" history was.

## 3. Events by region (H3)

| Region | Events |
|---|---:|
| Europe | 268 |
| South Asia | 162 |
| East Asia | 148 |
| North America | 102 |
| Oceania | 86 |
| Southeast Asia | 83 |
| Middle East & North Africa | 82 |
| Sub-Saharan Africa | 79 |
| Latin America | 52 |
| Central Asia | 25 |
| Multiple Regions | 1 |

**Finding:** Europe has about 1 in 4 events (24.6%). Latin America and Central Asia are thinly covered. Oceania (86) has more events than all of Latin America (52), which reflects the dataset author's choices more than world history.

## 4. Category mix in each era (K3, % of each era)

| Category | Ancient | Medieval | Early Modern | Modern | Contemporary |
|---|---:|---:|---:|---:|---:|
| Culture, Religion & Sport | **43.8%** | 22.7% | 13.5% | 1.0% | 6.8% |
| War & Conflict | 18.8% | **26.1%** | 24.3% | **33.2%** | 14.6% |
| Politics & Law | 6.3% | 8.0% | **27.0%** | 21.8% | **28.2%** |
| Independence & Nation-Building | 12.5% | 22.7% | 14.9% | 15.0% | 10.4% |

(Other 5 categories are on the sheet.)

**Findings:**
- Ancient events are mostly **culture and religion** (civilizations, monuments, the spread of religions).
- **War & Conflict peaks in the Modern era (33%)**, the period of colonial wars and the two World Wars.
- In the **Contemporary** era, **Politics & Law** is the biggest category (28%), and war drops to 15%. Disasters, society & health, and diplomacy all grow.

## 5. Outcome by category (S3, % of each category)

| Category | Positive | Negative | Mixed |
|---|---:|---:|---:|
| Culture, Religion & Sport | 84% | 4% | 12% |
| Independence & Nation-Building | 70% | 16% | 14% |
| Science, Technology & Exploration | 67% | 22% | 11% |
| Politics & Law | 62% | 15% | 23% |
| War & Conflict | 21% | **59%** | 21% |
| Disasters & Accidents | 3% | **97%** | 0% |
| **All events** | **54%** | **28%** | **19%** |

**Findings:**
- Overall, more events are marked Positive (54%) than Negative (28%). One event is "Ongoing".
- Disasters are almost always Negative, as expected.
- **Only 59% of wars are marked Negative.** Wars that led to independence or victory are often marked Positive. This shows that the Outcome column reflects the dataset author's point of view, so it should be treated as a rough label, not a measured fact.

## Limits to keep in mind

- The dataset is a **selection** of events, not a complete record. The counts show what the author chose to include, not how much happened.
- Category and Region come from lookup tables built for this project (`data/reference/`). Some events could fit more than one category.

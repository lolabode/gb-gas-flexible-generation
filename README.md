# When Does Great Britain Still Need Gas?

**[View the live dashboard](https://lolabode.github.io/gb-gas-flexible-generation/)** · [Requirements document](requirements.pdf)

An analysis of 312,793 half-hourly readings of Great Britain's electricity generation from January 2009 to November 2026, built to show when the grid still relies on flexible gas generation as wind and solar grow.

## The problem

Gas fell from 44.8% of GB generation in 2009 to 26.7% in 2025, and coal has gone. But annual averages hide when gas is still essential: cold, dark, still evenings when wind and solar cannot meet demand. A planning team at a flexible generation business needs to see the hours, seasons and weather conditions when gas plants are called on.

This is a portfolio project built on real, published data. The stakeholder roles are typical of a flexible generation business such as SSE Thermal. No real individuals are represented.

## Key findings (2025)

| Question | Finding |
|---|---|
| How much electricity does gas still supply? | 26.7% of generation, down from 44.8% in 2009. Wind supplied 29.7%. |
| What happens when the wind drops? | Gas supplied 40.1% in the least windy tenth of half-hours, against 14.5% in the windiest. |
| When is gas needed most? | January (38.3%) and the 7pm to 8pm hour (34.3%). |
| How hard does gas work at its peak? | 27,250 MW at 09:30 on 20 January 2025. |
| How clean is the grid? | 127 gCO₂/kWh on average, against 445 in 2009. |

**What this means:** gas is no longer the backbone of GB electricity, but it is still the backstop. Its value lies in covering calm, dark winter evenings, which is why flexible capacity still matters even as its annual share falls.

## Business questions

1. How has the generation mix changed since 2009, and how much of GB electricity does gas still supply?
2. When is gas needed most: by season, by month and by time of day?
3. How does gas respond when the wind drops?
4. How hard does gas have to work at its peak, and how often does it supply more than half of GB electricity?
5. How does carbon intensity change with the generation mix?
6. Can the data be trusted?

## Dashboard

Built as a Power BI-style report with card visuals, slicers and page tabs. It works on desktop and mobile.

| Page | Shows | Questions |
|---|---|---|
| Overview | Headline cards and the generation mix since 2009 | 1, 5 |
| Gas and Wind | Gas share and output across wind deciles | 3 |
| When Gas Is Needed | Gas share by month and hour, peak output, gas-dominant half-hours | 2, 4 |
| Carbon | Carbon intensity by year and month | 5 |
| Data Quality | Checks run, flagged readings and how each was handled | 6 |

Slicers: year, trend range (defaults to 2009 to 2025, the last full year) and fuel type.

## Data

**Source:** [NESO Historic GB Generation Mix](https://www.neso.energy/data-portal/historic-generation-mix), half-hourly, 1 January 2009 to 4 November 2026.

Fields used: generation by fuel (MW), total generation, fuel shares (%) and carbon intensity (gCO₂/kWh).

## Method

- Shares are calculated from summed MW, never by averaging half-hourly percentages, so busy half-hours count for more than quiet ones.
- Wind means transmission wind plus embedded wind.
- Time-of-day analysis uses UK local time, converted from the UTC timestamps in the source.
- Wind deciles rank every half-hour in the year by wind output and split them into ten equal groups.
- 2026 is a partial year and is labelled as one. Partial months are left off monthly charts.

## Data quality

| Check | Result | Handling |
|---|---|---|
| Missing or duplicate half-hours | None in 312,793 readings | No action |
| Fuels add up to total generation | 48 half-hours differ by up to 3 MW | Rounding; accepted |
| Impossible values | 7 July 2026, two half-hours: gas at 0 MW and zero-carbon share at 104.1% | Flagged and excluded |
| Coal after GB coal closure (September 2024) | 24 half-hours show 5 to 198 MW of coal | Flagged and excluded |

Every flagged reading is listed on the Data Quality page with its reason.

## Tools

Python (pandas) for cleaning, checks and aggregation. HTML, CSS and JavaScript for the dashboard, with charts drawn as SVG.

## Author

Felicia Oyebode · MSc Business Analytics, University of Dundee

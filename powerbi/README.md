Overview

This folder documents the Power BI report developed for the wildfire analysis project. The dashboard was designed to help public authorities explore wildfire activity across the United States from 1992 to 2015, with a particular focus on Alaska.
The report consolidates multiple datasets into a structured model and provides several views ranging from national comparisons to local environmental indicators. The report respects accessibility norms and the color palette used was picked in that sense

The .pbix file is not included, but all screenshots and descriptions below reflect the final version of the report.

Page Structure

The report is organized into thematic pages. Each page is designed to answer a specific set of questions by combining geographic data, aggregated measures, and filters. For storytelling purposes, I decided to "Zoom into Alaska", starting by an overview of the US, then to the most exposed states, to introduce Alaska.




1. Global Overview

This page allows national-level comparison.
It includes:

- Burnt area, fire count, and average duration for the selected year
- A choropleth map showing damage score by state, that indicator summarizes overall severity by combining fire size, duration, and frequency into a synthetic metric. Hovering the mouse over a state shows a gauge with a score out of 100 on the specified period of time filtered (all if none).
- Distribution of fire causes

This page provides the context necessary to see how Alaska compares against the rest of the country during the same period.

2. Detailed Analysis

This page breaks down several metrics by state and by season. It shows:

- Burnt area per state
- Fire count per state
- Burnt area per season
- Fire count per season
- A seasonal breakdown, which is important for understanding the timing and predictability of wildfire activity.

3. Alaska Overview

This page presents summary indicators for the state:

- Total burnt area in acres and km²
- Fire count
- Average fire duration
- Year-over-year trends for burnt area and number of fires
- Again the damage score (Alaska only), the gauge helps compare Alaska to other states or to itself across different years when filtering with the "trends" visual.


4. Fire Causes and Land Ownership

This page focuses on ignition causes and land categorization.
It shows:

- Burnt area per cause
- Fire count by land ownership category (public, private, mixed, other)

This page helps identify which causes are dominant and whether they are associated with specific land categories. It was mostly interesting to gauge "Fire Awareness campaigns" relevancy and to help direct the efforts (public or private mainly).

5. Fire Locations, Communities and Infrastructure

This page provides a geographical view of Alaska.
It includes:

- A comparison of fire locations with rescue station locations
- A map of population distribution
- A view showing the distribution of indigenous tribes by borough

The purpose of this page is to identify underserved regions, detect mismatches between fire frequency and available infrastructure, and highlight population exposure.

6. Environment Analysis

This page links wildfire data with environmental indicators from Alaska.
It includes:

- A map of environmental indicators per borough
- Estimated CO₂ emissions per year for the entire period

The CO₂ emission trend is helpful for identifying crisis years and major environmental events, as well as tracking future performance in the effort to reduce wild fire impact on environment (can serve as a benchmark)

7. Weather Impact

This page overlays weather patterns with wildfire activity.
It includes:

- A vulnerability index, plotted by season and year
- A comparison of lightning-induced fires by season
- This page demonstrates how much Alaska’s fires are tied to weather and lightning activity

Data Model

The data model follows a straightforward structure centered on the Fires Cleaned fact table. The remaining tables act as lookup tables or provide additional context for mapping, environmental indicators, or derived aggregations.

A full diagram of the model is available in the model.png screenshot.

The report includes pages for definitions, key DAX formulas used and external sources.

Here is a transcripted version :

Key DAX formulas

⚙️Average Fire Duration (H) =
DATEDIFF('Fires Cleaned'[DISCOVERY_DATE], 'Fires Cleaned'[CONT_DATE], DAY) * 24

⚙️Season =
SWITCH(
    TRUE(),
    'Fires Full Date'[Month] IN {12, 1, 2}, "Winter",
    'Fires Full Date'[Month] IN {3, 4, 5}, "Spring",
    'Fires Full Date'[Month] IN {6, 7, 8}, "Summer",
    'Fires Full Date'[Month] IN {9, 10, 11}, "Fall")

⚙️Damage Score (Log) =
LOG(
    0.5 * [FireSizeScore] +
    0.3 * [DurationScore] +
    0.2 * [FireCountScore])

⚙️Vulnerability Index =
([Avg Temperature Anomaly] * 0.6) +
([Precipitation Deficit] * 0.4)

⚙️CO2 Emissions (t) =
[Average Fire Duration (H)] * 45

⚙️Lightning Risk Global =
CALCULATE(
    COUNTROWS('Fires Cleaned'),
    'Fires Cleaned'[Cause Grouped] = "Lightning")

Data Model Structure

The report relies on a star-schema-like structure centered around the Fires Cleaned fact table. The other tables serve as lookup or enrichment tables. The model was designed intentionally to avoid circular dependencies and to keep the relationships predictable.

Fact table:

Fires Cleaned
This table contains the cleaned and enriched wildfire records used by most visuals. It includes discovery dates, containment dates, fire size, coordinates, grouped causes, county codes, and other derived fields.

Dimension and supporting tables:

Fires Full Date
Calendar table used to slice the data by day, month, year, and custom date keys.

Fire Cause
Lookup table mapping cause labels to cause codes.

Fire Size
Classification table used for grouping fires into standard size categories.

Fire States
Mapping between state codes and state names.

States Area
Surface area per state, useful for normalized comparisons.

Fires Geoloc
Geographic reference table holding latitude, longitude, county, and shape identifiers.

Fire Alaska Good
Cleaned and filtered geographic table for Alaska-specific mapping.

Alaska Meteo
Weather indicators such as temperature and precipitation, with seasonal grouping.

Fire Measures
Table containing precomputed DAX measures (or placeholders for them).

The relationships are mostly one-to-many, always flowing from dimensions toward the fact table. Dates follow a many-to-one relation from Fires Cleaned toward Fires Full Date to ensure consistent time intelligence.
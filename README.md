# Global Earthquake Analysis | 2000–2025

[View Interactive Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiYWFhMGNmYTItM2FlOS00NGI3LTkyNGYtYWRlNTgwMGIyMTlmIiwidCI6Ijc1YzJlNGQ0LWQwNGMtNGNlOS1hMGVhLWM5NzViZGM0MTdlYiIsImMiOjF9&embedImagePlaceholder=true)

## Project Overview

This project presents an analysis of **46,462 earthquakes** recorded worldwide between **2000 and 2025**, with a magnitude of at least **5.0**.

The project combines **SQL Server, QGIS and Power BI** to explore earthquake activity from temporal, geographic and magnitude-related perspectives.

The main goal of the analysis was to investigate:

- how earthquake activity changed over time,
- where earthquakes were concentrated geographically,
- which countries and continents recorded the highest activity,
- how earthquakes differ by magnitude and depth,
- how many events occurred onshore and offshore,
- where the strongest and deepest earthquakes occurred,
- how earthquake activity in Europe compares with the global pattern.

The final report consists of **five pages**, moving from a global overview to temporal, geographic and regional analysis.


## Data Source

The source data comes from the **USGS Earthquake Catalog**.

The analysis covers:

- period: **2000–2025**
- minimum magnitude: **5.0**
- event type: **earthquake**
- geographic scope: **worldwide**

The original data was downloaded in several CSV files and contained information such as earthquake ID, date and time, coordinates, magnitude, depth, place description and event status.


## Data Preparation

The raw CSV files were first loaded into **SQL Server**, where the data was consolidated and validated.

The validation process included checking:

- total and unique earthquake records,
- duplicated IDs,
- date and magnitude ranges,
- missing values,
- unusual depth values,
- yearly and monthly earthquake counts.

After validation, the dataset contained **46,462 unique earthquake records**.

The data was then prepared for reporting in **Power Query**, where relevant fields were selected, data types were standardized and supporting analytical columns were created.


## Geographic Preparation in QGIS

The USGS dataset contains geographic coordinates, but it does not provide a complete analytical hierarchy such as:

`Continent → Subregion → Country`

For this reason, **QGIS** was used to enrich the earthquake data with geographic information.

Earthquake coordinates were spatially joined with Natural Earth geographic layers to assign:

- country,
- continent,
- region,
- subregion,
- geographic code.

Earthquakes outside country boundaries were classified as **Offshore**.

Additional adjustments were made for Russia so that earthquakes could be correctly assigned to either the European or Asian part of the country.

Australia and Oceania were also combined into one reporting category:

`Australia & Oceania`


## Why QGIS Was Used for the Global Map

The original plan was to display all earthquake points directly in Power BI.

However, rendering more than **46,000 geographic points** caused significant performance issues and made the report unstable.

Instead of reducing the dataset, the full earthquake distribution was prepared in **QGIS**.

The final map distinguishes between:

- **Onshore earthquakes**
- **Offshore earthquakes**

and includes country boundaries for geographic context.

The map was exported in high resolution and added to Power BI. A separate full-screen map page was created so users can explore the complete spatial distribution without affecting report performance.


## Data Model

The Power BI report uses a fact-and-dimension model.

The main fact table is:

`fEarthquakes`

Supporting dimensions include:

- `dCalendar`
- `dGeography`
- `dMagnitudeClass`

The model allows earthquake activity to be analysed across time, geography, magnitude classes and depth categories.

Magnitude classes were defined as:

- **Moderate** – 5.0–5.9
- **Strong** – 6.0–6.9
- **Major** – 7.0–7.9
- **Great** – 8.0+

Earthquakes were also divided into three depth categories:

- **Shallow** – below 70 km
- **Intermediate** – 70–299.9 km
- **Deep** – 300 km or more


## DAX Measures

DAX measures were created to support dynamic analysis throughout the report.

They include calculations for:

- total earthquakes,
- average and maximum magnitude,
- average depth,
- magnitude 7.0+ events,
- onshore and offshore activity,
- year-over-year change,
- geographic rankings,
- continent activity share,
- peak earthquake year,
- most active country,
- strongest and deepest earthquakes.

The measures react dynamically to filters and geographic hierarchy levels.


# Dashboard Pages

## 1. Overview

The Overview page provides a high-level summary of the dataset.

The main KPIs include:

- **Total Earthquakes**
- **Max Onshore Magnitude**
- **Max Offshore Magnitude**
- **Avg Magnitude**
- **Magnitude 7.0+ Events**
- **Avg Depth (km)**

The page also compares earthquakes by magnitude class and depth, shows the share of onshore and offshore events and provides detailed earthquake records.

![Overview](screenshots/01_overview.png)


## 2. Temporal Analysis

This page focuses on how earthquake activity changed between **2000 and 2025**.

It includes:

- the most active year,
- the number of earthquakes recorded in the peak year,
- the year with the highest number of magnitude 7.0+ earthquakes,
- the largest annual increase in earthquake activity,
- annual earthquake trends,
- year-over-year change,
- a monthly and yearly activity heatmap.

The analysis shows that **2011** was the most active year in the dataset, with **2,701 earthquakes**.

![Temporal Analysis](screenshots/02_temporal_analysis.png)


## 3. Geographic Analysis

The Geographic Analysis page compares earthquake activity across continents, subregions and countries.

It includes:

- **Top 10 Countries by Earthquake Activity**
- earthquake activity by continent,
- magnitude 7.0+ earthquakes by continent,
- a hierarchical geographic matrix,
- the global earthquake distribution map.

The hierarchy can be expanded from:

`Continent → Subregion → Country`

The page also provides metrics such as earthquake count, magnitude 7.0+ share, average magnitude, maximum magnitude, average depth and year-over-year change.

![Geographic Analysis](screenshots/03_geographic_analysis.png)


## 4. Global Earthquake Map

This page provides a full-size view of the earthquake distribution prepared in QGIS.

The map distinguishes between:

- **Onshore**
- **Offshore**

earthquakes and includes country boundaries for additional context.

The visualization clearly shows major global earthquake belts, especially around the Pacific, western North and South America, Japan, Indonesia and southern Asia.

![Global Earthquake Map](screenshots/04_global_earthquake_map.png)


## 5. Europe Deep Dive

The final page focuses specifically on earthquake activity in Europe.

It includes:

- total earthquakes,
- most active country,
- average magnitude,
- average depth,
- strongest earthquake,
- deepest earthquake,
- activity by country or subregion,
- deepest earthquakes by country,
- yearly earthquake activity,
- strongest European earthquakes.

A geographic parameter allows users to switch between **Country** and **Subregion** views.

Within the European subset, **Iceland** records the highest number of earthquakes, while the deepest earthquake occurred beneath Spain at approximately **610 km**.

![Europe Deep Dive](screenshots/05_europe_deep_dive.png)


## Key Findings

The analysis highlights several patterns:

- The dataset contains **46,462 earthquakes** with magnitude 5.0 or higher.
- Approximately **81% of the events are classified as offshore**.
- The strongest offshore earthquake reached magnitude **9.1**.
- The strongest onshore earthquake reached magnitude **8.0**.
- Most earthquakes belong to the **Moderate magnitude class (5.0–5.9)**.
- Most earthquakes are classified as **Shallow**.
- **2011** was the most active year, with **2,701 earthquakes**.
- Asia records the highest number of onshore earthquakes among the continents.
- Earthquake activity is strongly concentrated along major global seismic zones.
- In Europe, **Iceland** is the most active country in the dataset.
- The deepest European earthquake occurred beneath Spain at approximately **610 km**.


## Tools & Technologies

- **SQL Server**
- **SQL**
- **Power BI**
- **Power Query**
- **DAX**
- **QGIS**
- **CSV**
- **USGS Earthquake Catalog**
- **Natural Earth geographic data**

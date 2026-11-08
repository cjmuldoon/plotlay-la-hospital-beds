# The data

Made from HHS and U.S. Census Bureau data (public domain), see [`../NOTICE`](../NOTICE); our tables and shapes are CC BY 4.0.

- `tables/hospitals.csv`: one row per hospital (86). `hospital_pk` (CMS number), `name`, `type`, `city`, `beds_2023_24` and `icu_beds_2023_24` (the median week of 2023 and 2024), `occupancy_surge` (inpatient beds in use, 13 Dec 2020 to 31 Jan 2021, %), `icu_occupancy_surge`, `occupancy_2023_24`, `weeks_90` (weeks 90% full or fuller), `weeks_reported`, `lat`, `lng` (HHS's geocoded address).
- `tables/hospital_weeks.csv`: one row per hospital and week, 7 June 2020 to 21 April 2024 (`week` is the Sunday it starts). `beds`, `beds_used`, `occupancy` (%), `covid_patients` (confirmed and suspected), `icu_beds`, `icu_used`, `icu_occupancy` (staffed adult ICU). 7-day averages; blank where HHS suppressed a small count or the hospital did not report.
- `tables/county_weeks.csv`: the county each week: hospitals reporting, beds, beds in use, COVID-19 patients, ICU, and the shares.
- `tables/tract_access.csv`: one row per census tract (2,495). `geoid`, `population` (ACS 2018-22), `land_m2`, `nearest_km` (straight line to the nearest general hospital), `band`, `nearest_hospital`, `beds_per_1000_5km`, `_10km`, `_20km`.
- `geometry/hospitals.*`: each hospital as a disc 1 km across at its address (a symbol, not its grounds), keyed by `hospital_pk`. `geometry/tracts.*`: the 2022 cartographic boundary tracts (clipped to the shoreline), keyed by `geoid`.

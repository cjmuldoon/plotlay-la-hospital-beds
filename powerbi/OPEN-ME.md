# Opening the Power BI report

`LAHospitalBeds.pbip` is a Power BI Project: the report (`LAHospitalBeds.Report`, PBIR format) and the semantic model (`LAHospitalBeds.SemanticModel`, TMDL) saved as text, so the repo can show every change. Power BI Desktop opens it like a `.pbix`.

## What you need

- Power BI Desktop for Windows, a recent version (2026). Projects and the PBIR report format are standard in current versions. If Desktop is older than about mid 2025, turn on **File, Options and settings, Options, Preview features, Power BI Project (.pbip) save option** and **Store reports using enhanced metadata format (PBIR)**, then restart Desktop.
- The repo folder on the Windows machine. In Parallels the Mac home folder is usually shared as `\\Mac\Home`.

## Open it

1. In Windows, go to the repo's `powerbi` folder and double-click `LAHospitalBeds.pbip`, or in Desktop use **File, Open report, Browse reports** with the file type set to *Power BI project files (\*.pbip)*.
2. The visuals are empty the first time. Select **Refresh** on the Home ribbon.
   - By default the data is read from the repo's public copy on GitHub (`DataFolder` is `https://raw.githubusercontent.com/cjmuldoon/plotlay-la-hospital-beds/main/data/`). If Desktop asks how to connect, choose **Anonymous** and then **Connect**.
   - To read the files from disk instead, go to **Home, Transform data, Edit parameters** and set `DataFolder` to the full path of the repo's `data` folder, **ending with a backslash** (for example `\\Mac\Home\plotlay-la-hospital-beds\data\`). Then select **OK** and **Apply changes**.
   - If Desktop warns about privacy levels, choose **Ignore privacy levels** (all the sources are public open data).
3. Check the numbers (below).

If the report was updated while open, close Power BI and reopen the .pbip rather than using Apply external changes. (After Apply external changes one export drew the page at about 57% inside a much larger canvas; a full close and reopen put it right.)

## Check the numbers after Refresh

After **Refresh**:

| Page | Card | Should read |
|---|---|---|
| Week by week | COVID-19 patients, the busiest week | 8,316 |
| Week by week | Staffed adult ICU beds in use, the fullest week | 91.6% |
| Week by week | Hospitals that reported | 86 |
| One week (2021-01-03, as it opens) | Inpatient beds in use | 80.6% |
| One week (2021-01-03) | COVID-19 patients | 8,316 |
| How far to a hospital | People | 9,936,690 |
| How far to a hospital | Within 5 km | 82.9% |
| How far to a hospital | 10 km or more | 258,746 |
| How far to a hospital | Km, the average resident | 3.43 |

On **One week**, pick **2023-03-05** and the inpatient card reads 80.9% with 609 COVID-19 patients.

## The model

- **Hospitals**: one row per hospital (`data/tables/hospitals.csv`): its CMS number, name, type, city, position, beds (the median week of 2023-24) and how full it was in the winter surge and in 2023-24. Measure: `Hospitals`.
- **Weeks**: one row per hospital and week (`hospital_weeks.csv`), 7 June 2020 to 21 April 2024, related to Hospitals by `hospital_pk`. `week` is the text date the slicer shows; `week_date` is the same date as a date, for the line charts. Measures: `Beds in use`, `ICU beds in use` (each the beds in use over the beds, added up first, so a big hospital counts for more), `COVID-19 patients`, `Peak COVID-19 patients`, `Peak ICU beds in use`, `Hospitals reporting`.
- **Tracts**: one row per census tract (`tract_access.csv`): people (ACS 2018-22), the straight-line km to the nearest general hospital, the band, and beds per 1,000 people within 10 km. `band` sorts by `band_order`. Measures: `People`, `Within 5 km`, `People 10 km or more`, `Distance, people-weighted`, `Beds per 1,000 within 10 km`.

## The maps

- **Azure Maps** (page 2, One week). Each hospital at its HHS address point, the bubble sized by its COVID-19 patients in the week picked, capped so the big hospitals do not cover their neighbours. If Desktop asks, allow Azure Maps (**File, Options and settings, Options, Security, Use Azure Maps visual**).
- **Shape Map** (page 4, How far to a hospital). The custom map, `data/geometry/tracts.topojson`, is saved inside the report (`LAHospitalBeds.Report/StaticResources/RegisteredResources/tracts.topojson`, a copy that keeps only each tract's `key`), so the 2,498 tracts draw on open, darker the farther from a general hospital. The Shape Map has no base map of its own, so the file also carries the context: the neighbouring counties (US Census TIGERweb, public domain) in a pale ground tone, with the ocean showing as the map's pale blue background. If the map shows the United States instead (an older Desktop can ignore a saved map): select it, then **Format visual**, **Visual**, **Map settings**, **Map type: Custom map**, **Add map type**, and choose `..\data\geometry\tracts.topojson`. Under **View map keys** the tract numbers (06037...) should be matched. If the Shape Map is not in the Visualizations pane, turn it on in **File, Options and settings, Options, Preview features, Shape map visual** and restart Desktop.

## Save a .pbix too

After the refresh, use **File, Save as** with the type **Power BI file (\*.pbix)** to save `powerbi\LAHospitalBeds.pbix`. It includes the data, so it opens without a refresh.

## Publish (only if you choose to)

Use **Home, Publish**. In the Power BI service, set the semantic model's **Data source credentials** for the GitHub address to **Anonymous**. Scheduled refresh then works with no gateway. **Publish to web** makes a public link, so only use it if you mean the report to be public.

## Shot list for the website and the video

| # | Shot | How | Length |
|---|---|---|---|
| 1 | Week by week | As it opens | still |
| 2 | The surge, hospital by hospital | One week, 2021-01-03 (as it opens) | still |
| 3 | March 2023 | One week, pick 2023-03-05 | still |
| 4 | After the pandemic | The table, sorted by In use, 2023-24 | still |
| 5 | How far to a hospital | As it opens; hover a tract in the Antelope Valley | still |

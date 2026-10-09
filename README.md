# Steam Game Success & Orbital Congestion - Tableau Dashboard Projects

![Tableau](https://img.shields.io/badge/Tableau-Dashboards-E97627?logo=tableau&logoColor=white)
![Data cleaning](https://img.shields.io/badge/Data-Cleaned%20%26%20Audited-2D7BF6)
![QA](https://img.shields.io/badge/QA-90%2F90%20numbers%20verified-2FB36B)
![Status](https://img.shields.io/badge/Status-Complete-blue)

Two end-to-end analytics projects: **data audit and cleaning -> KPI design -> dashboard -> quality assurance -> documentation.**

### Live Dashboard Walkthroughs

**1. Steam Game Success Dashboard**



**2. Orbital Congestion Dashboard**






---

## The two projects

### 1. Video Game Industry: What makes a game succeed on Steam?
Thousands of games launch on Steam every year, but only a few earn strong reviews and large player bases. This dashboard looks for what the winners have in common.

* **Data:** 94,407 Steam products (Steam store + SteamSpy estimates) -> **93,102 games after cleaning**.
* **Success ("Hit"):** at least 50 reviews, 80%+ positive reviews **and** 500,000+ estimated owners (quality + reach together).

| Finding | Result |
|---|---|
| Rated games (50+ reviews) | 31,647 |
| Hits | **1,442 (4.6%)** |
| Hit rate at launch price $40+ vs under $5 | **17.3% vs 1.2%** |
| Hit rate with 16+ languages vs 1 language | **11.9% vs 1.9%** |
| Hit rate for Metascore 85+ | **52.7%** (rated games that have a Metascore, n = 3,681) |
| Multiplayer / cloud saves / controller / achievements | each linked to a higher hit rate, even after controlling for price, genre and year |

### 2. Orbital Congestion: Satellite constellations and space debris risk
Thousands of new satellites are crowding low Earth orbit and raising collision risk. This dashboard shows which operators, countries and altitude bands drive the crowding.

> **Important:** the orbital dataset supplied for this project is a **synthetic sample** (5,000 simulated payloads). The findings demonstrate the method and the dashboard design; they are **not real orbital facts**. The structure matches the real CelesTrak SATCAT, so it can be swapped for real data.

| Finding (sample data) | Result |
|---|---|
| Payloads in low Earth orbit | 86% |
| Share in one 100 km shell (500-600 km) | **53%, about 7x denser than the next shell** |
| Share from four mega-constellations | 50% |
| Tracked debris + rocket bodies, 2010 to 2026 | 16,532 -> 29,919 (**+81%**) |

---

## What makes this more than a set of charts
* **Data audit with every fix logged** - corrupt prices (up to EUR 599,000), mislabelled genres, 1,297 software items hiding in a games file, a placeholder language count, operators "launching" before they existed, invalid orbital inclinations. See [`data/DATA_QUALITY_LOG.md`](data/DATA_QUALITY_LOG.md).
* **A defined success measure** instead of a single vanity metric, applied only to games with enough reviews to be reliable.
* **Robustness check** - a logistic regression on 30,542 rated games showed price, localisation and features stay significant after controls, while the raw "best genre" difference largely disappears (so the genre chart is labelled *raw* and small samples are faded).
* **Full QA** - all 90 numbers shown on the dashboards were recomputed independently from the delivered data (90/90 match), plus an automated layout test of every label. See [`reports/4_QA_Report.docx`](reports/4_QA_Report.docx).

## Repository contents
```
tableau-steam-orbital-dashboards/
|-- README.md
|-- data/
|   |-- steam_games_CLEAN_games.csv.zip     cleaned Steam games (unzip before use)
|   |-- orbital_congestion_CLEAN.xlsx       cleaned orbital workbook (Satellites, Debris_Trend, Band_Lookup, logs)
|   `-- DATA_QUALITY_LOG.md                 every issue found and the fix applied
|-- reports/
|   |-- 1_Project_Report.docx               full project report
|   |-- 2_Why_Tableau_and_Project_Rationale.docx
|   |-- 3_Tableau_Build_Guide.docx          step-by-step guide to build both dashboards in Tableau
|   `-- 4_QA_Report.docx                    number reconciliation, layout test, robustness checks
|-- tableau-kit/
|   |-- Tableau_Calculated_Fields.txt       every calculated field, ready to paste
|   |-- Preferences.tps                     custom Tableau colour palettes
|   |-- Colour_Swatches.png                 all hex codes
|   |-- backgrounds/                        dashboard backgrounds at exact Tableau sizes
|   `-- header-images/                      transparent header banners
|-- dashboards/
|   |-- screenshots/                        overview and filtered states
|   |-- design-references/                  target designs for the Tableau build
|   `-- animated-previews/                  short looping previews (MP4)
`-- docs/                                   GitHub Pages site (live interactive dashboards)
```
> The build guide refers to the kit folders by their original names (`02_Backgrounds`, `04_Colour_Palettes`, ...). In this repository they are `tableau-kit/backgrounds`, `tableau-kit/Preferences.tps`, and so on.

## How to use the Tableau kit
1. Unzip `data/steam_games_CLEAN_games.csv.zip`. Connect Tableau to the CSV and to `orbital_congestion_CLEAN.xlsx`.
2. Copy `tableau-kit/Preferences.tps` into `Documents/My Tableau Repository/` and restart Tableau.
3. Create the calculated fields from `tableau-kit/Tableau_Calculated_Fields.txt`.
4. Follow [`reports/3_Tableau_Build_Guide.docx`](reports/3_Tableau_Build_Guide.docx) for every worksheet, colour and pixel position (Steam 1600 x 1360, Orbital 1600 x 1040).
5. Place the background and header images from `tableau-kit/`.

## Interactive dashboards (HTML)
`docs/steam.html` and `docs/orbital.html` are self-contained pages (no installation): click any bar to cross-filter, hover for tooltips, try **Auto-tour**, switch Steam colour skins, search and sort the Top Hits table, and toggle Orbital night mode. Open them from the live link above, or double-click the files locally.

## Limitations
* Orbital data is synthetic (see above).
* SteamSpy owner counts are estimates in wide buckets; the Hit rule uses the lower bound.
* The Steam snapshot (Oct-Dec 2024) only contains games still listed; 2024 is a partial year.
* Results show **association, not causation** - higher-priced, localised, multiplayer games are usually also better funded.

## Tools
Tableau | Microsoft Excel | Python (pandas, statsmodels) for cleaning and checks | HTML/CSS/JavaScript for the interactive dashboards. AI assistance: Claude (Anthropic) was used for code, documentation and QA support; all analysis choices and numbers were reviewed by the author.

## Data sources and credits
* Steam data: Steam store and SteamSpy, via the open **steam-insights** dataset (snapshot Oct-Dec 2024). Please check the original repository's licence before reusing the raw data.
* Orbital data: synthetic sample structured like the CelesTrak SATCAT.
* Steam and the Steam logo are trademarks of Valve Corporation; used here only to identify the data source.
* Completed as part of my learning journey with **Imarticus Learning**.

## Author
**Your Name** - [LinkedIn](https://www.linkedin.com/in/YOUR-LINKEDIN/) - your.email@example.com

## Licence
Code and documentation: MIT (see [`LICENSE`](LICENSE)). Data files keep the licence terms of their original sources.

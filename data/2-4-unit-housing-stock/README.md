# VanToVault Small Multifamily Housing Stock: Housing Units in 2-4 Unit Buildings, 83 US Metros (ACS 2020-2024)

## What this is

For 83 US metropolitan areas (CBSAs) and their principal cities: how many housing units sit in **2-, 3- and 4-unit buildings** (duplexes, triplexes, fourplexes, triple-deckers), what share of all housing units that is, and how much of that stock is **owner-occupied**. The 83 metros are the ones covered by VanToVault's Foothold screen and down payment assistance survey, so the files join on `cbsa` (or `metro`).

- **Publisher:** VanToVault (vantovault.com). **Creator:** Van to Vault
- **Version:** 1.0.0, 2026-09-27. Values retrieved 2026-09-25.
- **DOI:** https://doi.org/10.5281/zenodo.23003739
- **Licence:** CC BY 4.0

## Files

| File | Rows | Contents |
|---|---|---|
| `data/vantovault-2-4-unit-housing-stock-83-metros-acs-2020-2024.csv` | 83 | One row per metro, sorted by share rank |
| `data/vantovault-2-4-unit-housing-stock-83-metros-acs-2020-2024.json` | 83 | Same records plus a metadata block |
| `DATA-DICTIONARY.md`, `data-dictionary.csv` | 27 | Every column: type, unit, description |
| `datapackage.json` | - | Frictionless Data descriptor (validated with frictionless 5.19.1) |
| `CITATION.cff`, `LICENSE.txt` | - | Citation metadata, CC BY 4.0 notice |

## Source

U.S. Census Bureau, American Community Survey (ACS) 5-year estimates, 2020-2024, dataset `ACSDT5Y2024`:
- **B25024, Units in Structure** (all housing units, occupied and vacant): cells 001 total, 004 two units, 005 three or four units.
- **B25032, Tenure by Units in Structure** (occupied housing units): cells 002 owner-occupied total, 005 and 006 owner-occupied in 2 and 3-4 unit structures, 016 and 017 renter-occupied in 2 and 3-4 unit structures.
- **Geography:** 83 CBSAs (summary level 310) and 82 principal-city places (summary level 160).
- **Retrieval:** `https://data.census.gov/api/access/data/table?id=ACSDT5Y2024.B25024&g=310XX00US{cbsa}` (and `B25032`; `160XX00US{state+place FIPS}` for cities), one geography per request. Every row's B25024 URL is in `source_url`.

Every response was checked before use: header and value counts equal, GEO_ID and NAME as requested, and the component cells summing exactly to the table total (B25024 cells 002-011 = 001; B25032 owner cells 003-012 = 002, renter cells 014-023 = 013, 002 + 013 = 001). The values passed through a summarising web-fetch tool, so these checks are the guard; any value can be re-read at its `source_url`.

## Rounding

Every percent column is the **raw ratio of the two counts on the same row x 100, rounded once to 1 decimal** (half up). An earlier working file (2026-09-25) carried two-decimal shares; formatting those to one decimal differs from this rule by 0.1 in 19 cells (for example Chicago 13.5, not 13.6; Rochester 12.0, not 12.1; Milwaukee 16.0, not 15.9). `rank_by_share` orders the unrounded ratios, which swaps Greensboro and San Antonio (59 and 60) relative to that working file.

## Top 10 metros by share of housing units in 2-4 unit buildings

| Rank | Metro | Share 2-4 | Units in 2-4 unit buildings | All housing units | Owner-occupied share of occupied 2-4 |
|---|---|---|---|---|---|
| 1 | Providence, RI | 23.1% | 169,001 | 730,957 | 28.7% |
| 2 | Buffalo, NY | 21.3% | 115,532 | 541,660 | 26.9% |
| 3 | Boston, MA | 20.1% | 413,851 | 2,059,059 | 34.0% |
| 4 | Worcester, MA | 19.6% | 69,528 | 355,185 | 24.7% |
| 5 | Albany, NY | 19.4% | 81,758 | 422,120 | 19.7% |
| 6 | New York, NY | 17.4% | 1,400,004 | 8,038,666 | 32.8% |
| 7 | Milwaukee, WI | 16.0% | 111,919 | 701,558 | 22.4% |
| 8 | Bridgeport, CT | 14.9% | 56,431 | 377,569 | 27.7% |
| 9 | New Orleans, LA | 14.7% | 68,295 | 465,148 | 16.9% |
| 10 | Hartford, CT | 14.7% | 73,204 | 499,522 | 24.3% |

Across the 83 metros: 7,378,457 of 87,404,584 housing units (8.4%) are in 2-4 unit buildings, and 1,414,235 of 6,571,722 occupied units in those buildings (21.5%) are owner-occupied.

## Validation run for this deposit (2026-09-27)

- `units_2 + units_3_4 = units_2_4`, `owner_occ_2 + owner_occ_3_4 = owner_occ_2_4` and the city equivalent hold on every row.
- Every percent column recomputes from its two counts under the rule above.
- `rank_by_count` matches the order of `units_2_4`; `rank_by_share` matches the order of the unrounded ratio.
- 83 rows, 83 distinct CBSA codes; principal-city columns complete for 82 (Bridgeport blank).

## Limitations

- Housing units, not buildings: a duplex counts as 2 units, a fourplex as 4.
- Margins of error are not carried. Metro totals have small relative MOEs; 3-4 unit cells in small metros and all principal-city cells are noisier. A difference of a point or two of share between neighbouring metros is not meaningful.
- CBSAs follow the July 2023 OMB delineations (OMB Bulletin 23-01) used by the 2020-2024 ACS; some cover different counties from the HUD fair market rent areas of the same name.
- B25024 includes vacant units; B25032 covers occupied units only, so occupied_2_4 is below units_2_4.
- 5-year estimates describe 2020-2024 as a period, not 2024 as a point in time.
- Principal city = one Census place, the first-named city of the CBSA. Consolidated cities are reported as their "balance". Bridgeport city, CT was not retrieved.
- Values were retrieved through a summarising web-fetch tool, one geography per call, and each response was checked (header and value counts equal, GEO_ID and NAME as requested, component cells summing exactly to the table total) before use. Any single value can be re-checked at its source_url.

## Related VanToVault data

Owner-occupant 2-4 unit purchase lending by metro, 2018-2025 (the Duplex Buyers Atlas, from HMDA): https://vantovault.com/library/duplex-buyers-atlas/. Note that HMDA reports the largest metros as metropolitan divisions; add the divisions to compare with a CBSA row here.

## Licence

CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/). The licence covers this compilation; the ACS estimates are published by the U.S. Census Bureau.

## How to cite

> Van to Vault (2026). VanToVault Small Multifamily Housing Stock: Housing Units in 2-4 Unit Buildings, 83 US Metros (ACS 2020-2024) (Version 1.0.0) [Data set]. VanToVault. https://doi.org/10.5281/zenodo.23003739

Please also credit the source: U.S. Census Bureau, American Community Survey 5-year estimates 2020-2024, tables B25024 and B25032.

## Mirrors

Zenodo (DOI above) · GitHub: https://github.com/vantovault-stack/open-housing-data · Hugging Face: https://huggingface.co/datasets/vantovault/2-4-unit-housing-stock-83-metros · Kaggle: https://www.kaggle.com/datasets/vantovault/2-4-unit-housing-stock-83-us-metros · All VanToVault datasets: https://vantovault.com/open-data/

## Changelog

- **1.0.0, 2026-09-27.** First release.

Contact: stephan@vantovault.com

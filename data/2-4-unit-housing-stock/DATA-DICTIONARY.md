# Data dictionary: VanToVault Small Multifamily Housing Stock: Housing Units in 2-4 Unit Buildings, 83 US Metros (ACS 2020-2024)

File: `data/vantovault-2-4-unit-housing-stock-83-metros-acs-2020-2024.csv` (83 rows, one per metro, sorted by rank_by_share). Also in `data-dictionary.csv` and `datapackage.json`.

Counts are housing units, not buildings: a duplex is 2 units, a fourplex 4. Blank = not retrieved (Bridgeport principal-city columns only).

| Column | Type | Unit | Description |
|---|---|---|---|
| `metro` | string |  | Short metro label used across VanToVault datasets (Foothold, DPA survey). |
| `state` | string |  | Two-letter state of the principal city. |
| `cbsa` | string |  | 5-digit Core Based Statistical Area code (July 2023 OMB delineations). Join key. |
| `cbsa_name` | string |  | CBSA name as returned by the Census Bureau. |
| `acs_vintage` | string |  | Always "ACS 5-year 2020-2024 (ACSDT5Y2024)". |
| `total_units` | integer | housing units | B25024_001: all housing units, occupied and vacant. |
| `units_2` | integer | housing units | B25024_004: units in 2-unit structures. |
| `units_3_4` | integer | housing units | B25024_005: units in 3- or 4-unit structures. |
| `units_2_4` | integer | housing units | units_2 + units_3_4. |
| `share_2_4_pct` | number | percent | units_2_4 / total_units x 100, rounded once to 1 decimal. |
| `owner_occ_total` | integer | housing units | B25032_002: owner-occupied housing units, all structure types. |
| `owner_occ_2` | integer | housing units | B25032_005: owner-occupied units in 2-unit structures. |
| `owner_occ_3_4` | integer | housing units | B25032_006: owner-occupied units in 3- or 4-unit structures. |
| `owner_occ_2_4` | integer | housing units | owner_occ_2 + owner_occ_3_4. |
| `owner_occ_share_pct` | number | percent | owner_occ_2_4 / owner_occ_total x 100, rounded once to 1 decimal: the share of all owner-occupied homes that are in a 2-4 unit building. |
| `occupied_2_4` | integer | housing units | owner_occ_2_4 + renter-occupied units in 2-4 unit structures (B25032_016 + B25032_017). |
| `owner_occupancy_rate_2_4_pct` | number | percent | owner_occ_2_4 / occupied_2_4 x 100, rounded once to 1 decimal: the share of occupied 2-4 unit housing that is owner-occupied. |
| `rank_by_share` | integer | rank | 1 = highest units_2_4 / total_units of the 83 (ranked on the unrounded ratio). |
| `rank_by_count` | integer | rank | 1 = largest units_2_4 of the 83. |
| `source_url` | string |  | data.census.gov API URL the B25024 values came from; replace B25024 with B25032 for the tenure values. |
| `city_name` | string |  | Principal city (Census place), the first-named city of the CBSA. Blank for Bridgeport (not retrieved). |
| `city_place_fips` | string |  | 7-digit state + place FIPS code of the principal city. |
| `city_total_units` | integer | housing units | B25024_001 for the principal city. |
| `city_units_2` | integer | housing units | B25024_004 for the principal city. |
| `city_units_3_4` | integer | housing units | B25024_005 for the principal city. |
| `city_units_2_4` | integer | housing units | city_units_2 + city_units_3_4. |
| `city_share_2_4_pct` | number | percent | city_units_2_4 / city_total_units x 100, rounded once to 1 decimal. |

`data/vantovault-2-4-unit-housing-stock-83-metros-acs-2020-2024.json` holds the same 83 records under `records` plus a metadata block (title, version, doi, licence, source, rounding rule, caveats).

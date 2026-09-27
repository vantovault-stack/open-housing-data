# duplex_metros: codebook

**File:** `duplex_metros.csv`, 83 rows (one per US metropolitan area), 18 columns, UTF-8, comma-separated, blank = missing.
**Unit of observation:** a metropolitan area (Core Based Statistical Area, July 2023 OMB delineations).
**Licence:** CC BY 4.0. Built 2026-09-27 by Van to Vault from the sources listed per column.
**Build script:** `build_teaching.py` (in this folder; it reads the ACS deposit CSV, the Atlas metro CSV and VanToVault's metro data layer). `hmda-crosswalk-used.csv` lists, for every metro, exactly which HMDA cells were added up.

The 83 metros are the ones VanToVault's Foothold screen covers: large and mid-size US metros, weighted toward the Northeast and Midwest. They are not a random sample of US metros.

| Column | Type | Description | Source |
|---|---|---|---|
| `metro` | text | Short metro name | VanToVault |
| `state` | text | Two-letter state of the principal city | VanToVault |
| `cbsa` | text | 5-digit CBSA code (join key) | OMB / Census |
| `cbsa_name` | text | CBSA name as published by the Census Bureau | Census ACS |
| `census_region` | text | Census Bureau region of `state`: Northeast, Midwest, South or West. Multi-state metros take the principal city's state. | Census regions, assigned from `state` |
| `total_housing_units` | integer | All housing units, occupied and vacant (B25024_001) | ACS 5-year 2020-2024, table B25024 |
| `units_2_4` | integer | Housing units in 2-, 3- or 4-unit buildings (B25024_004 + B25024_005). Units, not buildings: a duplex is 2 units. | ACS 5-year 2020-2024, table B25024 |
| `share_2_4_pct` | number | `units_2_4 / total_housing_units` x 100, 1 decimal | ACS, computed |
| `owner_occ_rate_2_4_pct` | number | Owner-occupied share of occupied units in 2-4 unit buildings, x 100, 1 decimal | ACS 5-year 2020-2024, table B25032, computed |
| `oo_loans_2024` | integer | Mortgages originated in 2024 to buy a 2-4 unit home as the borrower's principal residence (HMDA: action_taken 1, total_units 2-4, occupancy_type 1, loan_purpose 1, lien_status 1). For metros HMDA reports as metropolitan divisions, the divisions are added. Rounded to a whole loan where an average was used (see `oo_loans_basis`). | FFIEC/CFPB HMDA 2024, via the VanToVault Duplex Buyers Atlas |
| `oo_loans_basis` | text | `2024` = single-year 2024 count. `2022-2024 average` = HMDA-based files publish this metro as a 2022-2024 total (fewer than 50 loans in 2024), divided by 3. `2024 with some divisions as 2022-2024 average` = a mix, per division (Philadelphia, San Francisco, Washington DC). | as above |
| `oo_loans_per_1000_units_2_4` | number | Owner-occupant 2-4 unit purchase loans per 1,000 housing units in 2-4 unit buildings: 2024 loans (unrounded) / `units_2_4` x 1,000, 1 decimal. **Year basis:** loans are HMDA 2024 (or the 2022-2024 annual average where noted); units are ACS 2020-2024. 2024 is the last year of the ACS window and the first HMDA year coded on the same 2023 metro delineations as the ACS table. | computed |
| `median_borrower_income_2024` | integer | Median annual income of the borrowers in `oo_loans_2024`, US dollars (HMDA reports thousands). **Missing for 21 metros:** 13 that HMDA splits into metropolitan divisions (medians cannot be combined across divisions) and 8 published only as three-year totals. | HMDA 2024, via the Atlas |
| `fha_limit_2unit` | integer | FHA forward mortgage limit for a 2-unit property in the metro, calendar year 2026, US dollars. $693,050 is the national floor. | HUD CY2026 FHA limits |
| `foothold_pass` | text | `yes` if the metro is one of the 11 ranked in the Foothold index (buying a 2-4 unit building and living in one unit comes out ahead of renting at the model's rate), else `no`. | VanToVault Foothold index, data layer built 2026-09-23 |
| `dpa_2_4` | text | Down payment assistance an owner-occupant can use on a 2-4 unit purchase: `yes` (program found, 73 metros), `no` (none found, 7), `unconfirmed` (3). Some `yes` programs cap at 2 units. | VanToVault DPA survey (agency program pages), checked 2026 |

## Missing values

| Column | Missing | Why |
|---|---|---|
| `median_borrower_income_2024` | 21 | Not published for multi-division metros or three-year rows (not missing at random: most are the largest metros) |
| all others | 0 | |

## Notes for instructors

- **Metro-level data.** Every variable describes a metro, not a person or a building. Relationships between metros do not show how individual buyers behave (ecological fallacy).
- **Different time windows.** ACS 2020-2024 (a five-year period), HMDA 2024, and FHA limits and the Foothold result from 2026. Stock changes slowly; lending and limits do not.
- **Occupancy is what borrowers stated** when they applied for the loan. HMDA leaves out cash purchases and some small lenders.
- `foothold_pass` comes from a published screening model, not an official statistic. Methodology: https://vantovault.com/library/foothold-score/
- **Related files:** the full HMDA series is DOI 10.5281/zenodo.23003737 and the full ACS table is DOI 10.5281/zenodo.23003739. Both are CC BY 4.0.

## Suggested citation

Van to Vault (2026). duplex_metros: 2-4 unit housing, owner-occupant lending and entry costs in 83 US metros. VanToVault. Built from U.S. Census Bureau ACS 2020-2024 (B25024, B25032), FFIEC/CFPB HMDA 2024, HUD CY2026 FHA limits and VanToVault's Foothold and down payment assistance datasets. CC BY 4.0.

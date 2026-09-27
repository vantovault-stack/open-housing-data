# VanToVault Duplex Buyers Atlas: Owner-Occupant 2-4 Unit Purchase Loans by Metro, 2018-2025

## What this is

A count of **mortgages used to buy a 2-, 3- or 4-unit home that the borrower said they would live in**, for the United States, every year from 2018 to 2025, nationally and for every metropolitan statistical area (MSA) or metropolitan division (MD) in the HMDA data. People who buy a small multi-unit building and live in one unit are often called owner-occupant landlords or house hackers.

- **Publisher:** VanToVault (vantovault.com). **Creator:** Van to Vault
- **Version:** 1.0.1, deposited 2026-09-27. Data unchanged from version 1.0.0 (built 2026-09-16, issued 2026-09-17).
- **DOI:** https://doi.org/10.5281/zenodo.23003737
- **Licence:** CC BY 4.0
- **Human-readable edition:** https://vantovault.com/library/duplex-buyers-atlas/
- **Methodology page:** https://vantovault.com/library/duplex-atlas-methodology/

## Files

| File | Rows | Contents |
|---|---|---|
| `data/atlas-national-2018-2025.csv` | 8 | One row per year, national totals |
| `data/atlas-metro-2018-2025.csv` | 3,313 | One row per MSA/MD code per year, all measures, with suppression flags |
| `data/atlas-metro-2025.csv` | 418 | The 2025 rows of the metro file, same columns |
| `data/atlas-2018-2025.json` | - | Everything above plus the metadata block (filters, suppression rules, known issues) |
| `DATA-DICTIONARY.md`, `data-dictionary.csv` | 78 | Every column of every CSV: type, unit, description |
| `datapackage.json` | - | Frictionless Data descriptor (validated with frictionless 5.19.1) |
| `CITATION.cff` | - | Citation metadata |
| `LICENSE.txt` | - | CC BY 4.0 notice |

All files are UTF-8 without a byte-order mark. Three metro names contain non-ASCII letters (MAYAGÜEZ, SAN GERMÁN, SAN JUAN-BAYAMÓN-CAGUAS).

## Source

Home Mortgage Disclosure Act (HMDA) public loan-level data, published by the Federal Financial Institutions Examination Council (FFIEC) and the Consumer Financial Protection Bureau (CFPB), years 2018-2025.

- HMDA Data Browser: https://ffiec.cfpb.gov/data-browser/
- Data Browser API, nationwide CSV endpoint used to pull each year: `https://ffiec.cfpb.gov/v2/data-browser-api/view/nationwide/csv` (documented at https://ffiec.cfpb.gov/documentation/api/data-browser/, which lists 2018-2025 as valid years; checked 2026-09-27)
- Field definitions: https://ffiec.cfpb.gov/documentation/publications/loan-level-datasets/lar-data-fields
- Each year was pulled with the API filters `actions_taken=1` and `total_units=2,3,4` (the build's recorded source note); the remaining filters below were applied by VanToVault to the loan-level rows. Built 2026-09-16.

## Filters: exactly what is counted

A loan is counted when **all** of these hold in the HMDA record (field definitions quoted from the FFIEC LAR data-fields page):

| HMDA field | Value | Meaning |
|---|---|---|
| `action_taken` | 1 | Loan originated |
| `total_units` | 2, 3 or 4 | "The number of individual dwelling units related to the property" |
| `occupancy_type` | 1 | Principal residence |
| `loan_purpose` | 1 | Home purchase |
| `lien_status` | 1 | Secured by a first lien (excludes second mortgages, including down payment assistance seconds) |

**Investor comparison column.** `investor_loans` uses the same filters with `occupancy_type = 3` (investment property). It is a side-by-side comparison and is not part of `total_loans`.

**Geography.** The geography is HMDA's `derived_msa-md` ("The 5 digit derived MSA (metropolitan statistical area) or MD (metropolitan division) code"). Code `99999` is loans outside any MSA/MD; code `0` (2018-2019 only) is loans with no code reported. Both carry `is_metro = FALSE`.

## National series

| Year | Loans | 2-unit | 3-unit | 4-unit | Conventional % | FHA % | VA % | Median income ($) | Median loan ($) |
|---|---|---|---|---|---|---|---|---|---|
| 2018 | 48,689 | 39,757 | 6,146 | 2,786 | 51.3 | 43.9 | 4.8 | 81,000 | 275,000 |
| 2019 | 51,795 | 42,192 | 6,618 | 2,985 | 51.4 | 43.5 | 5.1 | 83,000 | 285,000 |
| 2020 | 53,204 | 42,643 | 7,311 | 3,250 | 48.4 | 45.6 | 6.0 | 84,000 | 315,000 |
| 2021 | 70,516 | 56,603 | 9,884 | 4,029 | 49.3 | 45.3 | 5.3 | 89,000 | 355,000 |
| 2022 | 56,434 | 46,278 | 7,220 | 2,936 | 53.7 | 40.7 | 5.5 | 101,000 | 375,000 |
| 2023 | 45,004 | 37,036 | 5,501 | 2,467 | 55.2 | 38.8 | 6.0 | 114,000 | 385,000 |
| 2024 | 48,432 | 39,171 | 6,084 | 3,177 | 65.3 | 29.2 | 5.5 | 123,000 | 415,000 |
| 2025 | 46,746 | 38,092 | 5,565 | 3,089 | 64.9 | 28.2 | 7.0 | 127,000 | 425,000 |

## Suppression

1. **Cells of 1-9 loans are blank.** Zeros are kept as `0`. Checked for this deposit: across all 50 count columns of the 3,313 metro rows there is no published value between 1 and 9, and `suppressed_cells` equals the number of blank count cells on every row.
2. **Metro-years with fewer than 50 loans are published as three-year totals** (that year plus the two prior years in the data; 2018 and 2019 have shorter windows). On those rows `basis = three_year_total`, `years_in_basis` lists the years summed, and all medians are blank because medians cannot be added. No rows were dropped.
3. **Flags:** `basis`, `years_in_basis`, `suppressed_core` (a headline count was hidden), `suppressed_detail` (only a demographic, age or LTV cell was hidden; true on most rows), `suppressed_cells`.

**What the suppression does not do.** It is a presentation rule, not statistical disclosure control, and the loan-level HMDA source is itself public. Two consequences a user should know about:
- Percent columns are computed before suppression, so they are present on 275 rows where `total_loans` is blank.
- The three-year totals are rolling. Where a code is on a three-year basis for consecutive years, single-year counts can be recovered by differencing consecutive rows, including some that are below 10.

## Metro definitions and crosswalk

- The key is `cbsa_code`, the HMDA MSA/MD code. **Join on the code, never on `metro_name`:** 14 names are shared by more than one code (for example CLEVELAND is 17410, Cleveland OH, and 17420, Cleveland TN).
- **Metropolitan divisions.** HMDA reports the largest MSAs as their divisions, not as the whole MSA. To get a whole MSA, add its division rows for the same year. In the 2024 and 2025 files, which carry the codes of the July 2023 OMB delineations (OMB Bulletin 23-01; codes such as 17410 and 12054 first appear in 2024), the split MSAs and their divisions are: Boston (14454, 15764, 40484); New York (35004, 35084, 29484, 35614); Chicago (16984, 20994, 29404, 29414); Los Angeles (11244, 31084); San Francisco (36084, 41884, 42034); Philadelphia (15804, 33874, 37964, 48864); Miami (22744, 33124, 48424); Seattle (42644, 45104, 21794); Detroit (19804, 47664); Dallas (19124, 23104); Washington (47764, 11694, 23224); Atlanta (12054, 31924); Tampa (45294, 41304). The division names in this list match the BLS table of metropolitan areas and divisions (bls.gov, read 2026-09-27); the codes are HMDA's own.
- **Codes change across years.** Between the 2023 and 2024 files: Atlanta 12060, Tampa 45300 and Cleveland-Elyria 17460 (2018-2023) became divisions 12054 + 31924, 45294 + 41304, and MSA 17410 (Cleveland, OH); Washington-Arlington-Alexandria division 47894 became 47764 + 11694; New Brunswick-Lakewood 35154 became Lakewood-New Brunswick 29484; Gary 23844 became Lake County-Porter County-Jasper County 29414; Everett 21794 is new in 2024. In 2018 a few codes differ again (for example Dayton 19380, Chicago-Naperville-Arlington Heights 16974, Silver Spring-Frederick-Rockville 43524). County sets can change along with codes, so check that a code held still before building a 2018-2025 trend for one metro.

## Validation run for this deposit (2026-09-27)

- **Unit and loan-type additivity.** On all 189 metro rows with no suppressed headline count, `loans_2unit + loans_3unit + loans_4unit = total_loans` and conventional + FHA + VA + USDA = `total_loans`. Nationally the three unit columns add to `total_loans` in every year.
- **National totals against metro rows.** The national rows count every qualifying loan, including loans in `99999` and `0`, so the national total should equal the sum of all metro-file codes for that year. It cannot be checked by simple addition, because three-year rows hold several years and some cells are blank. Instead each code's single-year count was bounded using only the published cells (single-year rows exact; blanks 1-9; three-year-basis years 0-49; each three-year row equal to the sum of its years). For every year 2018-2025 and for `total_loans`, `loans_2unit`, `loans_3unit` and `loans_4unit`, the national figure falls inside the resulting range. For 2025 `total_loans`: national 46,746; metro range 45,522 to 48,593. No inconsistency was found; an exact match cannot be shown from the published cells.
- **Suppression.** No count cell between 1 and 9; `suppressed_cells` matches the blank count cells on every row; no medians on three-year rows.
- **Files.** The three CSVs are byte-identical to version 1.0.0. `atlas-metro-2025.csv` equals the 2025 rows of the full metro file.

## Limitations

- **Not every purchase.** Cash purchases never appear in HMDA; lenders below HMDA reporting thresholds do not report.
- **Occupancy is what the borrower stated at application.** It is not verified afterwards.
- **Loan amounts are approximate.** The public file discloses loan amounts as the midpoint of $10,000 bands.
- **Rate and income are incomplete.** Partially exempt lenders do not report rates, and some loans report no income. Denominators are in `loans_with_rate_reported` and `loans_with_income_reported`.
- **LTV is combined LTV.** A buyer who also took a down payment assistance second loan can show a higher combined LTV than the first mortgage alone.
- **No finding about fairness or approval odds.** Differences between groups or lenders have many causes (credit, loan size, product mix, where lenders operate). The CFPB cautions that HMDA data alone cannot establish discrimination. This dataset makes no such finding.
- **Timing.** Each year's HMDA data is released the following year, so the latest year is 6-18 months old.
- **Divisions, not whole metros**, for the largest MSAs (see above).

## Licence

CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/). The licence covers this compilation, its structure and its documentation. The HMDA source data is public and produced by the FFIEC and the CFPB.

## How to cite

> Van to Vault (2026). VanToVault Duplex Buyers Atlas: Owner-Occupant 2-4 Unit Purchase Loans by Metro, 2018-2025 (Version 1.0.1) [Data set]. VanToVault. https://doi.org/10.5281/zenodo.23003737

Please also credit the source: FFIEC and CFPB, Home Mortgage Disclosure Act public loan-level data, 2018-2025.

## Mirrors

Zenodo (DOI above, the archival copy) · GitHub: https://github.com/vantovault-stack/open-housing-data · Hugging Face: https://huggingface.co/datasets/vantovault/duplex-buyers-atlas-2018-2025 · Kaggle: https://www.kaggle.com/datasets/vantovault/duplex-buyers-atlas-2018-2025 · Downloads and all VanToVault datasets: https://vantovault.com/open-data/

## Changelog

- **1.0.1, 2026-09-27.** Deposit edition with its own DOI. Title, citation, creator and DOI added to the JSON header; data dictionary, CITATION.cff and licence file added. CSVs unchanged.
- **1.0.0, 2026-09-17.** First release, years 2018-2025.

Contact: stephan@vantovault.com

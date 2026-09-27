# Data dictionary: VanToVault Duplex Buyers Atlas: Owner-Occupant 2-4 Unit Purchase Loans by Metro, 2018-2025

Every column in every CSV. The same content is in `data-dictionary.csv` and, as field schemas, in `datapackage.json`.

Blank cell = suppressed (1-9 loans), or a median withheld on a three-year row. `0` is a true zero. Booleans are written `TRUE` / `FALSE`.

## atlas-national-2018-2025.csv

| Column | Type | Unit | Description |
|---|---|---|---|
| `year` | integer |  | Calendar year of origination. |
| `total_loans` | integer | loans | Qualifying owner-occupant 2-4 unit purchase loans. |
| `loans_2unit` | integer | loans | Loans on 2-unit properties. |
| `loans_3unit` | integer | loans | Loans on 3-unit properties. |
| `loans_4unit` | integer | loans | Loans on 4-unit properties. |
| `conventional_pct` | number | percent | Conventional share of total_loans, percent, 1 decimal. |
| `fha_pct` | number | percent | FHA share of total_loans, percent, 1 decimal. |
| `va_pct` | number | percent | VA share of total_loans, percent, 1 decimal. |
| `median_borrower_income` | integer | US dollars | Median applicant income, US dollars, all qualifying loans nationwide with income reported. |
| `median_loan_amount` | integer | US dollars | Median loan amount, US dollars, computed from HMDA public-file loan amounts (disclosed as the midpoint of $10,000 bands), so approximate. Blank on three_year_total rows. |

## atlas-metro-2018-2025.csv and atlas-metro-2025.csv

| Column | Type | Unit | Description |
|---|---|---|---|
| `cbsa_code` | string |  | CBSA or Metropolitan Division code. Authoritative join key; metro_name is not unique. |
| `metro_name` | string |  | HMDA MSA/MD name as published, UTF-8, uppercase. 14 names are shared by multiple codes. |
| `year` | integer |  | Calendar year of origination. |
| `is_metro` | boolean |  | FALSE for the non-metro buckets (codes 99999 and 0), TRUE otherwise. |
| `basis` | string |  | single_year, or three_year_total when the metro had fewer than 50 loans that year. |
| `years_in_basis` | string |  | Comma-separated years summed into this row. |
| `suppressed_core` | boolean |  | TRUE if a headline count (total, unit, or loan-type) was hidden by the under-10 rule. |
| `suppressed_detail` | boolean |  | TRUE if only a demographic, age or LTV detail cell was hidden. TRUE on most rows. |
| `suppressed_cells` | integer | cells | Number of cells hidden on this row. |
| `total_loans` | integer | loans | Qualifying owner-occupant 2-4 unit purchase loans. |
| `loans_2unit` | integer | loans | Loans on 2-unit properties. |
| `loans_3unit` | integer | loans | Loans on 3-unit properties. |
| `loans_4unit` | integer | loans | Loans on 4-unit properties. |
| `conventional_loans` | integer | loans | HMDA loan_type=1. |
| `fha_loans` | integer | loans | HMDA loan_type=2. |
| `va_loans` | integer | loans | HMDA loan_type=3. |
| `usda_loans` | integer | loans | HMDA loan_type=4 (RHS/FSA); rare on 2-4 units. |
| `conventional_pct` | number | percent | Conventional share of total_loans, percent, 1 decimal. Computed before cell suppression, so it can be present where the count is blank. |
| `fha_pct` | number | percent | FHA share of total_loans, percent, 1 decimal. Computed before cell suppression. |
| `va_pct` | number | percent | VA share of total_loans, percent, 1 decimal. Computed before cell suppression. |
| `usda_pct` | number | percent | USDA (RHS/FSA) share of total_loans, percent, 1 decimal. Computed before cell suppression. |
| `median_borrower_income` | integer | US dollars | Median applicant income relied on in the credit decision, US dollars (HMDA reports thousands; multiplied by 1,000). Loans with no income reported are excluded; base in loans_with_income_reported. Blank on three_year_total rows. |
| `income_p25` | integer | US dollars | 25th percentile applicant income, US dollars. Blank on three_year_total rows. |
| `income_p75` | integer | US dollars | 75th percentile applicant income, US dollars. Blank on three_year_total rows. |
| `median_loan_amount` | integer | US dollars | Median loan amount, US dollars, computed from HMDA public-file loan amounts (disclosed as the midpoint of $10,000 bands), so approximate. Blank on three_year_total rows. |
| `median_interest_rate` | number | percent | Median note rate, percent, among loans with a reported rate (base in loans_with_rate_reported). Partially exempt lenders do not report rates. Blank on three_year_total rows. |
| `loans_with_income_reported` | integer | loans | Denominator behind the income medians. |
| `loans_with_rate_reported` | integer | loans | Denominator behind median_interest_rate. |
| `investor_loans` | integer | loans | Same filters with occupancy_type=3. Comparison only; not part of total_loans. |
| `business_purpose_loans` | integer | loans | Loans flagged business or commercial purpose. |
| `ltv_le80` | integer | loans | Loans with combined LTV 80% or less. |
| `ltv_80_90` | integer | loans | Loans with combined LTV over 80 up to 90%. |
| `ltv_90_95` | integer | loans | Loans with combined LTV over 90 up to 95%. |
| `ltv_95_97` | integer | loans | Loans with combined LTV over 95 up to 97%. |
| `ltv_gt97` | integer | loans | Loans with combined LTV over 97%. |
| `ltv_na` | integer | loans | Loans with combined LTV not reported. |
| `ltv_conv_le80` | integer | loans | Conventional loans with combined LTV 80% or less. |
| `ltv_conv_80_90` | integer | loans | Conventional loans with combined LTV over 80 up to 90%. |
| `ltv_conv_90_95` | integer | loans | Conventional loans with combined LTV over 90 up to 95%. |
| `ltv_conv_95_97` | integer | loans | Conventional loans with combined LTV over 95 up to 97%. |
| `ltv_conv_gt97` | integer | loans | Conventional loans with combined LTV over 97%. |
| `ltv_conv_na` | integer | loans | Conventional loans with combined LTV not reported. |
| `race_white` | integer | loans | Loans by HMDA derived race: white. |
| `race_black_or_african_american` | integer | loans | Loans by HMDA derived race: black or african american. |
| `race_asian` | integer | loans | Loans by HMDA derived race: asian. |
| `race_american_indian_or_alaska_native` | integer | loans | Loans by HMDA derived race: american indian or alaska native. |
| `race_native_hawaiian_or_other_pacific_islander` | integer | loans | Loans by HMDA derived race: native hawaiian or other pacific islander. |
| `race_two_or_more_minority_races` | integer | loans | Loans by HMDA derived race: two or more minority races. |
| `race_joint` | integer | loans | Loans by HMDA derived race: joint. |
| `race_not_available` | integer | loans | Loans by HMDA derived race: not available. |
| `race_free_form_text_only` | integer | loans | Loans by HMDA derived race: free form text only. |
| `eth_hispanic_or_latino` | integer | loans | Loans by HMDA derived ethnicity: hispanic or latino. |
| `eth_not_hispanic_or_latino` | integer | loans | Loans by HMDA derived ethnicity: not hispanic or latino. |
| `eth_joint` | integer | loans | Loans by HMDA derived ethnicity: joint. |
| `eth_not_available` | integer | loans | Loans by HMDA derived ethnicity: not available. |
| `eth_free_form_text_only` | integer | loans | Loans by HMDA derived ethnicity: free form text only. |
| `sex_male` | integer | loans | Loans by HMDA derived sex: male. |
| `sex_female` | integer | loans | Loans by HMDA derived sex: female. |
| `sex_joint` | integer | loans | Loans by HMDA derived sex: joint. |
| `sex_not_available` | integer | loans | Loans by HMDA derived sex: not available. |
| `age_under25` | integer | loans | Loans by applicant age group: under25. |
| `age_25_34` | integer | loans | Loans by applicant age group: 25-34. |
| `age_35_44` | integer | loans | Loans by applicant age group: 35-44. |
| `age_45_54` | integer | loans | Loans by applicant age group: 45-54. |
| `age_55_64` | integer | loans | Loans by applicant age group: 55-64. |
| `age_65_74` | integer | loans | Loans by applicant age group: 65-74. |
| `age_over74` | integer | loans | Loans by applicant age group: over74. |
| `age_not_applicable` | integer | loans | Loans by applicant age group: not-applicable (HMDA code 8888). |

## atlas-2018-2025.json

One object holding the header (name, title, version, issued, license, cite_as, doi, homepage, creator, changelog, source, filters, investor_comparison_filter, years, suppression, units, known_issues, limitations) plus `national` (one object per year, national CSV columns) and `metro` (one object per metro-year, metro CSV columns).
In the JSON, suppressed and null fields are omitted from each object rather than written as null.

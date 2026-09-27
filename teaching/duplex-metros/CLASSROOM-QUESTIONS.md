# duplex_metros: five suggested classroom questions

For introductory statistics. Each question uses only `duplex_metros.csv`. None has a "right" story; each is about the method.

1. **Describing a relationship.** Make a scatterplot of `owner_occ_rate_2_4_pct` (y) against `share_2_4_pct` (x). Describe the form, direction and strength of the relationship and name any unusual metros. Is a straight line a reasonable summary? Would a log scale on x change your answer?

2. **Rates, not counts.** Rank the metros by `oo_loans_2024` and then by `oo_loans_per_1000_units_2_4`. Which metros move the most between the two rankings, and why does the choice of denominator matter? What would change if the denominator were `total_housing_units`?

3. **Comparing groups.** Compare `oo_loans_per_1000_units_2_4` across `census_region` with side-by-side boxplots and summary statistics. Are the conditions for a one-way ANOVA reasonable here? If not, what would you use instead?

4. **Missing data.** `median_borrower_income_2024` is missing for 21 metros. Using `units_2_4` and `total_housing_units`, compare the metros with and without an income value. Is the income variable missing at random? How could a regression of `oo_loans_per_1000_units_2_4` on `median_borrower_income_2024` be affected by dropping these metros?

5. **Categorical association and logistic regression.** Make a two-way table of `dpa_2_4` by `foothold_pass`. Are the expected counts large enough for a chi-square test, or is Fisher's exact test more appropriate? Then fit a logistic regression of `foothold_pass` on `entry_price` and `rent_1br`. With 11 "yes" outcomes among 82 complete rows, what are the limits of this model?

All variables are metro-level. Any conclusion is about metros, not about individual buyers.

# duplex_metros: a teaching table

83 US metropolitan areas, one row each, 18 variables on small multifamily (2-4 unit) housing: how much of it there is and who owns it (Census ACS 2020-2024), how many owner-occupants bought it with a mortgage (HMDA 2024), and what it costs to get in (entry price, one-bedroom rent, FHA 2-unit limit, down payment assistance, a rent-versus-own screen).

- `duplex_metros.csv`: the data
- `CODEBOOK.md`: every variable, its source and year, and missing values
- `CLASSROOM-QUESTIONS.md`: five suggested questions for introductory statistics
- `hmda-crosswalk-used.csv`: the HMDA cells behind each metro's loan count (metropolitan divisions added up where HMDA splits a metro)
- `build_teaching.py`: the script that built the table (reads VanToVault's source files; provenance only)

Licence: CC BY 4.0. Van to Vault (vantovault.com). Full series: HMDA lending, https://doi.org/10.5281/zenodo.23003737; ACS housing stock, https://doi.org/10.5281/zenodo.23003739.

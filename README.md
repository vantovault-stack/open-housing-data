# VanToVault Open Housing Data

Open datasets about buying a two-to-four unit home, living in one unit and renting the others — plus
a neighbourhood-level short-term rental census. All are free to reuse with attribution, all are
archived with permanent DOIs, and all are published because the answers they contain are hard to
find anywhere else.

Maintained by Stephan D. · <vantovault@gmail.com> · https://vantovault.com/open-data/

---

## The datasets

### 1. Foothold Index — where owning beats renting

[`vantovault-foothold-metros.csv`](data/vantovault-foothold-metros.csv) · [`vantovault-foothold-metros.json`](data/vantovault-foothold-metros.json)

A screen of **23,424 two-to-four unit listings across 83 US metro areas**, asking a narrower question
than most affordability rankings: not *where are houses cheap*, but *where can a first-time buyer
with limited savings actually get in and stay in*. Every listing must survive seven absolute tests
before its metro is scored at all.

Figures as published on 2026-08-21, data as of **2026-08-06**, modelled at a **6.66%** mortgage rate.
At that rate 11 of the 83 metros clear the affordability bar.

| Column | Meaning |
|---|---|
| `metro`, `state` | Metro area and state |
| `survivors` | Listings that passed all seven screening tests |
| `thin` | `True` when fewer than 20 listings survived — the figures can move a lot month to month |
| `entry_price_usd` | 25th-percentile surviving listing: the cheap end of what passed |
| `typical_price_usd` | Median surviving listing |
| `kept_per_month_usd` | What stays in your pocket versus renting (can be negative) |
| `keep_ratio` | The same figure as a share of one month's rent; 0 means owning costs the same as renting |
| `rank` | Rank among metros that cleared the bar; `null` if it did not rank |
| `foothold_score` | Weighted score, 0-100 |
| `entry_pillar`, `cashflow_pillar`, `durability_pillar` | The three component scores |
| `fha_limit_2unit_usd`, `fha_limit_3unit_usd`, `fha_limit_4unit_usd` | The HUD CY2026 FHA loan limits the FHA ceiling test was run against. Each listing is tested against the limit for **its own unit count** |
| `fha_limit_basis` | `national floor` where the metro sits at the HUD CY2026 national floor (49 metros), `MSA above-floor` where HUD assigns the MSA a higher limit (34 metros) |

⚠ **Scranton carries null dollar figures** — too few listings survived to publish a number honestly.
Fourteen metros are flagged `thin`. They are shown rather than hidden, with their counts beside them.

### 2. Down Payment Assistance Survey — can you use DPA on a 2-4 unit home?

[`vantovault-dpa-83-metros.csv`](data/vantovault-dpa-83-metros.csv) · [`vantovault-dpa-83-metros.json`](data/vantovault-dpa-83-metros.json)

The same 83 metros, screened for one question that first-time buyers ask constantly and almost no
published source answers: **can an owner-occupant use down payment assistance to buy a two-to-four
unit home?** Programs were checked one at a time, and several state agencies corrected their own
published information in the course of answering.

The `status` field is the important one, and it deliberately splits two things most sources collapse:

| `status` | Meaning |
|---|---|
| `program_found` | A program exists that an owner-occupant can use on a 2-4 unit home |
| `none_found` | Checked, and no 2-4-unit-eligible program was found |
| `unconfirmed` | Eligibility is **not stated** and could not be confirmed — **this is an unknown, not a no** |

Treating `unconfirmed` as a "no" will understate what is available. That distinction is the single
most useful thing in the file for a housing counselor.

### 3. Pittsburgh Short-Term Rental Census — Lawrenceville and Bloomfield (August 2026)

[`vantovault-pittsburgh-str-census-airbnb.csv`](data/vantovault-pittsburgh-str-census-airbnb.csv) ·
[`vantovault-pittsburgh-midterm-furnishedfinder.csv`](data/vantovault-pittsburgh-midterm-furnishedfinder.csv) ·
[`vantovault-pittsburgh-str-census.json`](data/vantovault-pittsburgh-str-census.json) (summary counts + file manifest)

A hand-checked, listing-level count of short-term rentals in four official City of Pittsburgh
neighbourhoods (Lower, Central and Upper Lawrenceville, and Bloomfield), built while City Council's
short-term rental zoning bill (2026-0009) was pending. Every row is a live listing you can open.
Airbnb rows carry room type, capacity, host, review count, coordinates, distance to the nearest
neighbourhood boundary (with an explicit **boundary-uncertainty flag**, because platform pins are
displaced) and three two-night rate windows (mid-September, late-September weekend, December).
The Furnished Finder file covers the 30-day-plus mid-term market, with published asking rent and
minimum stay.

Data as of **2026-08-31**. Method, limits and the neighbourhood tables:
https://vantovault.com/library/pittsburgh-short-term-rental-census/

⚠ Read the limits before quoting: single-search counts undercount (pagination gaps on both
platforms were found and closed by quadrant harvesting); rows flagged `boundary_uncertain_material`
may sit in a neighbouring neighbourhood; zoning-district assignment was tested and deliberately
**not** published because pin displacement makes it unreliable at the parcel scale.

---

## Licence

All datasets here are released under **[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)**.
Use them commercially, modify them, build on them — just credit Van to Vault.

## How to cite

> VanToVault, *Foothold Index: rent versus own screen for two to four unit homes across 83 US metros*, 2026.
> DOI [10.5281/zenodo.22019647](https://doi.org/10.5281/zenodo.22019647)

> VanToVault, *Down payment assistance for two to four unit owner occupied purchase, 83 US metros*, 2026.
> DOI [10.5281/zenodo.22019630](https://doi.org/10.5281/zenodo.22019630)

> VanToVault, *Pittsburgh Short-Term Rental Census: Lawrenceville and Bloomfield (August 2026)*, 2026.
> DOI [10.5281/zenodo.22258181](https://doi.org/10.5281/zenodo.22258181)

A machine-readable `CITATION.cff` is included, so GitHub's "Cite this repository" button works.

## What is in here, and what is not

**Here:** all datasets in CSV and JSON, the full screening methodology
([METHODOLOGY.md](METHODOLOGY.md)), field definitions, thresholds, sources and known limitations —
enough to check the work or re-implement the screen.

**Not here yet: the scoring code.** The published figures are produced by a v7 pipeline whose scoring
lives in a spreadsheet rather than in a single runnable script, and the standalone scripts that exist
are from an earlier version at a different mortgage rate. **Publishing them would ship code that does
not reproduce the numbers in this repository**, which would be worse than publishing nothing. A
runnable implementation that reproduces these files exactly is the intended next addition.

## Corrections

If something here is wrong, tell me and I will fix it and say what changed:
<vantovault@gmail.com>. Corrections already made to these datasets are listed at
https://vantovault.com/open-data/.

## Related

- The Foothold Index, written up in full: https://vantovault.com/library/foothold-score/
- Down payment assistance guide: https://vantovault.com/library/down-payment-assistance-duplex/
- The Pittsburgh census page, with per-neighbourhood tables: https://vantovault.com/library/pittsburgh-short-term-rental-census/
- Charts from this data, free to republish: https://vantovault.com/charts/
- Free calculators built on the same math: https://vantovault.com/tools/

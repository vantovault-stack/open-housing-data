# VanToVault Open Housing Data

Two open datasets about buying a two-to-four unit home, living in one unit and renting the others.
Both are free to reuse with attribution, both are archived with permanent DOIs, and both are
published because the answers they contain are hard to find anywhere else.

Maintained by Stephan D. · <vantovault@gmail.com> · https://vantovault.com/open-data/

---

## The datasets

### 1. Foothold Index — where owning beats renting

[`vantovault-foothold-metros.csv`](vantovault-foothold-metros.csv) · [`vantovault-foothold-metros.json`](vantovault-foothold-metros.json)

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

⚠ **Scranton carries null dollar figures** — too few listings survived to publish a number honestly.
Fourteen metros are flagged `thin`. They are shown rather than hidden, with their counts beside them.

### 2. Down Payment Assistance Survey — can you use DPA on a 2-4 unit home?

[`vantovault-dpa-83-metros.csv`](vantovault-dpa-83-metros.csv) · [`vantovault-dpa-83-metros.json`](vantovault-dpa-83-metros.json)

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

---

## Licence

Both datasets are released under **[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)**.
Use them commercially, modify them, build on them — just credit Van to Vault.

## How to cite

> VanToVault, *Foothold Index: rent versus own screen for two to four unit homes across 83 US metros*, 2026.
> DOI [10.5281/zenodo.22019647](https://doi.org/10.5281/zenodo.22019647)

> VanToVault, *Down payment assistance for two to four unit owner occupied purchase, 83 US metros*, 2026.
> DOI [10.5281/zenodo.22019631](https://doi.org/10.5281/zenodo.22019631)

A machine-readable `CITATION.cff` is included, so GitHub's "Cite this repository" button works.

## What is in here, and what is not

**Here:** both datasets in CSV and JSON, the full screening methodology
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
- Charts from this data, free to republish: https://vantovault.com/charts/
- Free calculators built on the same math: https://vantovault.com/tools/

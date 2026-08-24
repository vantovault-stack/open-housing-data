# Foothold Index — methodology

Everything below describes the published dataset in `data/`, as of **2026-08-06**, modelled at a
**6.66%** mortgage rate (Freddie Mac Primary Mortgage Market Survey, week ending 30 July 2026).

> **Correction, 2026-08-22.** Three statements in section 4 of this document did not match the model
> that produced the data, and are corrected below. The **pillar weights** are 30/30/40, not 40/40/20;
> the published scores reproduce on 30/30/40 for all eleven ranked metros and on 40/40/20 for none.
> **Scoring is percentile** for sixteen of the twenty-one measures, not fixed anchors. And
> **cash-flow measures are computed on the median surviving deal**, not on the entry price. The
> **data files were not affected** — only this description of them. No figure in `data/` changed.

The index ranks US metro areas by how realistic it is for a first-time buyer with little cash to buy
a two-to-four unit building, live in one unit, rent the others, and pay no more than they would to
rent. **23,424 listings** were screened across **83 metros**; **11,495 survived** every test; **11
metros** cleared the affordability bar.

## 1. The seven screening tests

Each test runs on every individual listing, **before** any metro is scored. Every threshold is
absolute rather than relative to the listing's own city — a relative screen keeps the cheapest
quarter of every metro no matter how bad that quarter is.

| Test | A listing fails when | Why the test exists |
|---|---|---|
| **Price floor** | Priced below $60,000 | At that price a 2-4 unit building is a shell, or effectively a land sale |
| **FHA ceiling** | Priced above the metro's FHA limit for a 3.5% deposit | A building a first-time buyer cannot finance is not a first-time buyer deal |
| **Condition floor** | Under $40 per square foot | The price is telling you the building has been written off; gut rehab runs $60-$100+ per sq ft |
| **Yield ceiling** | Gross yield above 25% | Almost always a repair bill wearing a rent number. The one threshold the data confirms outright |
| **Neighborhood crime** | Violent crime above 1.45× the median American city | Anchored on FBI city-level figures, so a bad ZIP cannot pass by being average for its own metro |
| **Abandonment** | More than 8% of homes empty for no ordinary reason | Quality is flat below that level and turns sharply above it |
| **Value trend** | Home values fell more than 15% over five years | A market still falling is not a foothold |

## 2. The metro-level bar

A metro is ranked **only if both** hold:

- its **median surviving deal costs no more than renting plus 10%**, and
- the payment fits inside a **48.5% debt-to-income ceiling**.

Metros that pass the listing tests but fail here are retained in the dataset with `rank: null` — for
example New Orleans and New York fail because the payment is too large for local incomes.

## 3. Definitions that matter

- **Entry price** — the **25th-percentile surviving listing**: the cheap end of what passed every
  test. It is a real asking price on a real building, not an average, and not the cheapest listing.
- **Typical price** — the median surviving listing.
- **Median surviving deal** — the single listing at the middle of the surviving set for a metro. Every
  cash-flow figure published for that metro is this one building's economics, so the numbers describe a
  real address rather than an average of buildings that do not exist together.
- **Kept per month** — what stays in your pocket against renting, for the median surviving deal: the
  rent you no longer pay, plus what tenants pay, less the full payment and a maintenance reserve. It
  can be negative.
- **Keep ratio** — kept-per-month as a share of one month's rent. Zero means owning costs the same
  as renting.
- **Thin** — fewer than 20 surviving listings. Shown, not hidden, with the count beside it.

## 4. Scoring

A weighted score across three pillars, built from **twenty-one measures**. Sixteen are scored by
**percentile** — a metro's score on a measure is how many of the other qualifying metros it beats —
and five are scored against **fixed absolute standards**, because how well a state weathered a
recession is not a question about its neighbours. Scores are clamped 0-100.

Percentile scoring makes very different measures comparable. The trade-off is that a percentile score
describes a metro's position among its peers rather than performance against a fixed target, so
scores can move as metros are added or removed.

| Pillar | Weight | What it measures |
|---|---|---|
| **Entry** | 30% | How hard the metro is to get into |
| **Cash flow** | 30% | The monthly economics once you own |
| **Durability** | 40% | Whether the place is likely to hold up |

Cash-flow measures — kept per month, keep ratio, cash-on-cash, PITI, collected rent, DTI — are
computed on the **median surviving deal**, a single real listing at the middle of what passed the
screen, not on the entry price. Entry price and typical price are separate descriptive statistics
about the surviving set. Deposit months and DPA coverage are computed on the entry price.

## 5. Sources and vintage

| Input | Source |
|---|---|
| Listings | Realtor.com |
| Rents | HUD Small Area Fair Market Rents FY2026 |
| Vacancy, income | US Census American Community Survey 2023 |
| Crime | FBI Table 8 and CrimeGrade |
| Home value trend | Zillow Home Value Index |
| FHA limits | HUD CY2026 |
| Mortgage rate | Freddie Mac PMMS, week ending 30 July 2026 (6.66%) |

## 6. What this cannot tell you

Stated plainly, because a screen that hides its limits is not worth checking:

- **Whether any specific building is a good buy.** This works on asking prices and modelled rents and
  has never seen the inside of anything.
- **Condition**, beyond a crude price-per-square-foot test. In Chicago, Pittsburgh, Grand Rapids and
  several other metros the listing feed carried no square footage, so that test could not run at all.
- **Flood insurance costs.** A separate policy, not modelled in any metro here, and in high-risk
  areas it can add thousands a year.
- **Anything about outcomes.** There is no data anywhere in this model on whether a purchase actually
  went well.
- **Five metros carry only one rent series** rather than two, so their most important input has no
  second source checking it: Bakersfield, Rochester, Scranton, Syracuse and Youngstown.

## 7. The settings are choices

Moving them moves the answer. Lowering the affordability bar admits more metros quickly. Raising the
crime multiplier lets cheaper listings through in rougher neighborhoods, which pulls entry prices
down for the wrong reason. Nothing is hidden: every threshold is printed above.

The rate is the binding constraint, not prices alone. At 6.66%, 11 of 83 metros clear the test. Run
the same 23,424 listings at the 3.125% rate available a few years ago and 27 clear it. The buildings
did not change.

---

## Down Payment Assistance Survey — method in brief

83 metros, one question: can an owner-occupant use down payment assistance to buy a 2-4 unit home?
Each metro's state and local programs were checked individually against published program rules, and
where the rules were silent, the administering agency was contacted directly. Several agencies
corrected their own published information during the survey.

Findings are recorded as `program_found`, `none_found`, or `unconfirmed`. **`unconfirmed` means
eligibility was not stated and could not be confirmed — it is an unknown, not a no.** Collapsing it
into "no" understates what is available; that split is the point of the file.

Full write-up and per-metro sourcing: https://vantovault.com/library/down-payment-assistance-duplex/

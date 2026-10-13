# Changelog: VanToVault Down Payment Assistance Survey (83 metros)

## v4.7, 13 October 2026
Six corrections from an independent audit (Audit 6.0), each checked against the program's own page or document on 12 October 2026 and approved by the owner. Same 83 rows, same columns, same row order. Statuses and the median are unchanged; one amount, six source links and the unit limit of the four FL Assist rows change.

| | v4.6 (10 Oct 2026) | v4.7 (13 Oct 2026) |
|---|---|---|
| program_found | 69 | 69 |
| none_found | 10 | 10 |
| unconfirmed | 4 | 4 |
| rows with a flat dollar maximum | 32 | 32 |
| median flat maximum | $17,500 | $17,500 |
| units_max = 4 (reaches a fourplex) | 44 | 48 |
| units_max = 2 (duplex only) | 21 | 21 |
| units_max = 1 (single-family only, or no unit to rent out) | 10 | 10 |
| units_max null (the program does not say) | 8 | 4 |

What changed:
- Portland ME: `max_assistance_usd` 5000 -> 14000. On a 2-4 unit building MaineHousing's Multi-Unit Advantage applies: "For two units Advantage is $8,000, three units is $11,000, and four units is $14,000." The field carries the largest published figure, as the schema note says; `program_or_finding` names all three amounts. `source_url` moves from a third-party summary (downpaymentscout.com) to MaineHousing's own page, https://www.mainehousing.org/homeloan; `as_of` 2026-07 -> 2026-10-12. The $5,000 and the $14,000 both sit below the 16th value, so the median stays $17,500 over 32.
- Lakeland, Miami, North Port-Sarasota, Orlando (Florida Housing FL Assist): status program_found and $10,000 unchanged. `units_max` and `units_max_fha` null -> 4, `units_basis` unstated -> first_mortgage_doc, `units_read` 2026-10-12. FL Assist's own term sheet still states no property type, but Florida Housing says "Down payment assistance is only available when used with Florida Housing's first mortgage loan." (https://www.floridahousing.org/programs/homebuyer-overview-page), and that first mortgage's lender guide (HTH TBA Lender Guide 8.01.25, p.30, "2-4 UNIT PROPERTIES") says "Borrower(s), must occupy one of the units as their primary residence." This is the same reading already used for PHFA (Allentown, Harrisburg, Scranton) and CHFA (Bridgeport, Hartford). `source_url` of the four rows moves from the first-mortgage lender guide, which never states the FL Assist amount, to the Florida Housing page that does ("Offers up to $10,000 on FHA, VA, USDA and Conventional Loans.").
- Knoxville, Memphis, Nashville (THDA): $15,000 unchanged; it is the cap for an existing home. The note adds THDA's new-construction Payment option: up to $25,000 at 0%, repaid over 15 years (Originating Agents Guide: "The Great Choice Plus Payment New Construction is at a zero percent interest rate, monthly payments amortized over a 15-year term, and the loan amount is up to $25,000.", https://dogvxws799i6n.cloudfront.net/wp-content/uploads/OA-Guide-Current.pdf, read 12 October 2026).
- Allentown, Harrisburg, Scranton (PHFA Keystone Advantage, $6,000) and Pittsburgh (URA, $7,500): amounts unchanged. The note adds PHFA's K-FIT: 5% of the lesser of the price or appraised value, no dollar cap, forgiven over ten years, paired only with the Keystone Home Loan (one or two units), so it can be larger for a buyer who qualifies (https://www.phfa.org/programs/assistance.aspx).
- Rochester: `source_url` https://hcr.ny.gov/achieving-dream-program-0 -> https://hcr.ny.gov/dpal-plus-2026-term-sheet, the SONYMA DPAL Plus 2026 term sheet that states the $30,000 and the 60% AMI limit (the Albany, Buffalo and Syracuse rows already cite it).
- Nine GSFA Platinum rows (Bakersfield, Fresno, Los Angeles, Oxnard, Riverside-San Bernardino, Sacramento, San Diego, San Francisco, San Jose): amount stays "up to 5.5% of the loan". The note no longer says the assistance is "split into a second mortgage plus a gift component", which is not true of Standard, and now names the tiers: 5.5% is the Assist-to-Own tier for employees of GSFA member counties (3.5% deferred 0% second plus a gift of up to 2%, subject to market conditions); Standard is up to 5% as a 15-year amortizing second; Select up to 5% (3.5% second plus up to 1.5% gift) (https://www.gsfahome.org/programs/dpa/platinum.shtml).
- Nothing else changed: every other field of all 83 rows is byte-identical to v4.6. The field-by-field change is in this commit's diff.

## v4.6, 10 October 2026
Adds the unit limit to every row so a tool can read it (Deal Math v8 does). Same 83 rows, same row order, the six existing columns unchanged; five columns appended: `units_max`, `units_max_fha`, `units_basis`, `units_read`, `units_source`.

| | v4.5 (6 Oct 2026) | v4.6 (10 Oct 2026) |
|---|---|---|
| program_found | 69 | 69 |
| none_found | 10 | 10 |
| unconfirmed | 4 | 4 |
| rows with a flat dollar maximum | 32 | 32 |
| median flat maximum | $17,500 | $17,500 |
| units_max = 4 (reaches a fourplex) | - | 44 |
| units_max = 2 (duplex only) | - | 21 |
| units_max = 1 (single-family only, or no unit to rent out) | - | 10 |
| units_max null (the program does not say) | - | 8 |

What changed:
- `units_max` is the largest building, in units, on which an owner-occupant who rents the other units can use the assistance, read from the program's own document, page or written answer and quoted in `units_source` with the date in `units_read`. 29 documents or pages were re-read on 10 October 2026 (SONYMA, MassHousing, CHFA, RIHousing, NYC HomeFirst, Minneapolis ACCESS, FHLBank Des Moines, metroDPA, GSFA Platinum, Florida Housing's TBA lender guide, NIFA, MaineHousing, KHC); the rest carry the dated quotes already in `program_or_finding` or the agency emails of August 2026.
- `units_max_fha` is the same figure except in Milwaukee (2 with a WHEDA FHA first, 4 conventional), New Orleans (2 on FHA or VA, 4 Fannie Mae) and Salt Lake City (2 on FHA or VA, 4 under Freddie Mac HFA Advantage), where the first mortgage sets the limit.
- A program that admits one individually deeded unit of a plex (Virginia, Kansas) or a 1-4 unit that may not be rented (Indiana) is recorded as 1: it gives the buyer nothing to rent out.
- Eight rows carry null: the four unconfirmed rows (Grand Rapids, Louisville, Phoenix, Tucson), and the four Florida metros served by FL Assist (Lakeland, Miami, North Port-Sarasota, Orlando), whose second mortgage's own term sheet (FHFC Master Term Sheet 12.11.24) states no property type; the 2-4 unit language exists only for the first mortgages it attaches to, and that indirect basis is not adopted. Null means the program does not say, which is an unknown, not a no.
- No status, amount, note, source URL or as_of changed.

## v4.5, 6 October 2026
Prompted by a written answer from Virginia DHCD (5 October 2026; see https://vantovault.com/corrections/). Same 83 rows, same columns and row order.

| | v4.4 (5 Oct 2026) | v4.5 (6 Oct 2026) |
|---|---|---|
| program_found | 69 | 69 |
| none_found | 8 | 10 |
| unconfirmed | 6 | 4 |
| rows with a flat dollar maximum | 32 | 32 |
| median flat maximum | $17,500 | $17,500 |

What changed:
- Richmond and Virginia Beach-Norfolk: unconfirmed -> none_found. Asked whether a buyer may purchase a whole duplex, live in one unit and rent the other, DHCD answered in writing (Cheri L. Miles, Program Manager, 5 October 2026): "The first-time homebuyer may purchase one of the units in a duplex, triplex or fourplex. The unit must be individually sold/ deeded. The down payment assistance would be available for the one unit. DPA is not available if the homeowner is purchasing the entire building." as_of 2026-10-06.

## v4.4, 5 October 2026
Prompted by Audit 5.0 finding VTV-142 (5 October 2026; see https://vantovault.com/corrections/). Same 83 rows, same columns and row order. This release also brings this mirror current with the site's v4.3 edition (below), which had not yet been pushed here.

| | v4.3 (4 Oct 2026) | v4.4 (5 Oct 2026) |
|---|---|---|
| program_found | 70 | 69 |
| none_found | 8 | 8 |
| unconfirmed | 5 | 6 |
| rows with a flat dollar maximum | 33 | 32 |
| median flat maximum | $15,000 | $17,500 |

What changed:
- Grand Rapids: program_found ($10,000, MSHDA MI 10K DPA Loan, statewide) -> unconfirmed. MSHDA's MI 10K DPA and MI Home lender-requirement pages do not state two-to-four-unit eligibility, and participating-lender documentation describes single-family, condominium and manufactured homes only (read 5 October 2026); max_assistance_usd 10000 -> null. This aligns the Michigan state guide with the Lansing and Ann Arbor city pages, which already treated unit eligibility as unconfirmed.

## v4.3, 4 October 2026
Prompted by Audit 2.0 (4 October 2026; see https://vantovault.com/corrections/). Same 83 rows, same columns and row order.

| | v4.2 (4 Oct 2026) | v4.3 (4 Oct 2026) |
|---|---|---|
| program_found | 72 | 70 |
| none_found | 8 | 8 |
| unconfirmed | 3 | 5 |
| rows with a flat dollar maximum | 36 | 33 |
| median flat maximum | $17,500 | $15,000 |

What changed:
- El Paso: the City of El Paso First Time Homebuyers Program ($5,000) -> the statewide TDHCA My First Texas Home route (2-5% of the loan, two-unit eligible); the city sheet limits eligible property to one unit in a 2-4-unit building, so it does not cover the whole building; max_assistance_usd 5000 -> null (percentage-based).
- Richmond, Virginia Beach-Norfolk: program_found -> unconfirmed. The Virginia DHCD DPA guideline (rev. October 2024) allows a unit in a duplex/triplex/fourplex only if it is individually deeded and the buyer owns no other units as rentals; an August 2026 email confirms a whole-duplex purchase but not renting the other unit (DHCD re-asked 4 October 2026); max_assistance_usd 40000 -> null.
- Allentown, Harrisburg, Scranton: two-unit eligibility confirmed from PHFA's First Mortgage Programs Overview (March 2026) - Keystone Home Loan / Keystone Government allow one or two units (HFA Preferred one unit); 3-4 units not eligible.

## v4.2, 4 October 2026
Prompted by an independent audit delivered 3 October 2026 (83 findings on the site; see https://vantovault.com/corrections/). Same 83 rows, same columns and row order.

| | v4.1 (24 Sep 2026) | v4.2 (4 Oct 2026) |
|---|---|---|
| program_found | 73 | 72 |
| none_found | 7 | 8 |
| unconfirmed | 3 | 3 |
| rows with a flat dollar maximum | 37 | 36 |
| median flat maximum | $15,000 | $17,500 |

What changed:
- Baltimore: program_found -> none_found. The Maryland Mortgage Program Compliance Manual (section 2.10(F), updated 28 January 2026) lists among ineligible residences "any home a portion of which is to be rented"; max_assistance_usd 6000 -> null.
- Denver: "up to 5%" -> "3% or 4% of the Note amount" as a 30-year deferred second (metroDPA US Bank guide, rev. 10 June 2026, p.6), with the guide's own income limit ($216,000 for FHA/USDA/VA and above-80%-AMI conventional, p.10) and property rule ("one-four units", p.13).
- Salt Lake City (UHC Form 300, rev. 6 July 2026): FHA/VA allows 1-2 unit owner-occupied, HFA Advantage 2-4 units (700 score, 95% LTV); traditional DPA is a 30-year amortizing second at the first rate + 1 point (cap 8%), deferred DPA 3.5% simple interest.
- Knoxville, Memphis, Nashville (THDA Originating Agents Guide): Great Choice Plus Payment option is a 30-year amortizing second at the first-mortgage rate, up to 5% / $15,000; $500,000 acquisition-cost cap; $6,000 / $10,000 forgivable no-payment options.
- Milwaukee (WHEDA): Easy Close is a 10-year amortizing second at the first rate, 6% of the lesser of price or appraisal; conventional 2-4 unit needs 3% borrower funds and six months reserves.
- Houston, McAllen (TSAHC Lender Guidelines 4.2): existing 2-4 unit homes need five years of residential use; non-bond conventional is Fannie-only, LTV under 95%, 3% own funds.
- Baltimore and Denver city pages, six state pages and the DPA guide were corrected on the site the same day.

## v4.1, 24 September 2026
Removes internal working notes from 9 rows of `program_or_finding`: a person's name attached to two research rulings (Atlanta, and eight GSFA California rows, which now read "(13 August 2026)"), and an agency staff member's email address in the Atlanta row. No status, amount, source URL or date changed.

## v4, 24 September 2026
Rebuilt from the source workbook after a full fact check of the site against the agencies' own documents. Same 83 rows, same columns and row order, same status vocabulary.

| | v3 (8 Sep 2026) | v4 (24 Sep 2026) |
|---|---|---|
| program_found | 72 | 73 |
| none_found | 7 | 7 |
| unconfirmed | 4 | 3 |
| rows with a flat dollar maximum | 48 | 37 |
| notes cut at 300 characters | 18 | 0 |
| rows changed | | 53 |

What changed:
- Notes are no longer cut at 300 characters.
- Ohio (7 metros): OHFA assistance is 3% (conventional) or 3.5% (government) of the purchase price, per OHFA's homebuyer page and its 1 July 2026 lender guidelines; the older 2.5%/5% came from a superseded 2022 brochure.
- Texas, Missouri, California and other statewide programs: flat dollar caps that appear in no agency document were replaced with the published percentage.
- Baltimore: $6,000, or 3% to 6% of the first mortgage depending on product.
- Tennessee (Knoxville, Memphis, Nashville): THDA confirmed in writing (14 Aug 2026) that its assistance can be used on a 1-4 unit home the buyer lives in.
- Virginia (Richmond, Virginia Beach-Norfolk): the note now states what the agency's email and its written guideline each say.
- Two-unit limits written into the rows for programs that cap at a duplex (North Carolina, Charleston, Seattle, Pittsburgh, Chicago, Detroit, St. Louis, Kansas City, Oklahoma City, Philadelphia, Salt Lake City and others), in the program's own words.
- Albuquerque, Phoenix and Tucson are unchanged from v3.

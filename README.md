# US Car Sales Dashboard

Interactive Tableau dashboard analysing ~24,000 car sales transactions across
seven US dealer regions, built to answer four business questions: what drives
revenue, where it comes from, how it moves over time, and which buyer
attributes actually predict purchase behaviour.

**[View the live dashboard on Tableau Public →]((Car_sales.twb))

![Dashboard overview](screenshots/dashboard.png)

---

## Key findings

**SUVs overtook Hatchbacks as the highest-selling body style** during the
period, visible as a crossover in the cumulative revenue chart.

**Revenue is concentrated in domestic brands.** Chevrolet, Ford and Dodge
together account for a disproportionate share of the top-10 total, ahead of
premium imports.

**Buyer income does not predict purchase price.** Plotting average annual
income against average sale price by brand produces no meaningful relationship
(near-zero slope, wide vertical dispersion at every price point). This is a
negative result worth stating: income-based segmentation would not work on this
dataset, and the field is likely synthetic.

**Revenue is male-skewed**, with roughly a 79/21 split — the single largest
demographic asymmetry in the data.

---

## What the dashboard shows

| View | Question it answers |
|---|---|
| KPI row | Total revenue, top colour, top transmission, top dealer |
| Monthly sales | How did revenue move month to month? |
| Running sales per body style | How has the product mix shifted? |
| Sales by US region | Which regions perform best? |
| Top 10 brands | Which manufacturers drive revenue? |
| Sales by gender | How is revenue split by buyer gender? |

Filters on income, body style, transmission and dealer apply across every
view. Clicking a brand, region or gender mark filters the rest of the
dashboard.

---

## Technical detail

**Tool:** Tableau Public Desktop
**Data:** 23,906 transactions; 16 fields covering vehicle, dealer, customer
and price attributes

Techniques used:
- Running-sum table calculation along the date axis for cumulative trend
- Top-N filters (Top 1, Top 10 by SUM of sales) driving the KPI cards
- Dashboard filter actions for cross-view interactivity
- Geographic role assignment on dealer region

---

## Data preparation

Three issues were identified and handled before building:

**Encoding defect in `Engine`** — values decoded as `DoubleÂ Overhead
Camshaft`, a mis-read UTF-8 non-breaking space. Cleaned before use.

**`Phone` typed as a numeric measure** — Tableau computed a mean and standard
deviation for it. Recast as a string; it is an identifier, not a quantity.

**Ambiguous city names in `Dealer Region`** — Middletown, Aurora and
Greenville exist in multiple US states, and the dataset carries no state
field. Mapping was therefore ruled out in favour of a ranked bar chart, which
conveys the same comparison without implying false geographic precision.

A single null in `Customer Name` was left in place: the field is an identifier
and is not aggregated anywhere in the workbook.

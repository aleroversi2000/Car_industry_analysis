# US Car Sales Dashboard

Interactive Tableau dashboard analysing ~24,000 car sales transactions across
seven US dealer regions, built to answer four business questions: what drives
revenue, where it comes from, how it moves over time, and which buyer
attributes actually predict purchase behaviour.

**[Download the Tableau workbook (.twb)](Car_sales.twb)**

![Dashboard overview]()

---

## Key findings

**SUVs overtook Hatchbacks as the highest-selling body style** during the
period, visible as a crossover in the cumulative revenue chart.

**Revenue is concentrated in domestic brands.** Chevrolet, Ford and Dodge
together account for a disproportionate share of the top-10 total, ahead of
premium imports.

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

## Data cleaning and preparation

Performed in `Car_sales.ipynb` with pandas.

- **Integrity:** 23,906 rows × 16 columns, zero exact duplicates.
- **Missing values:** one null in `Customer Name`, filled with `'Unknown'`
  rather than dropped — the field is an identifier and never aggregated, so
  discarding the row would have lost 15 valid attributes to fix one.
- **Scope check:** `Dealer_Region` inspected for distinct values, confirming
  seven US locations with no variant spellings.
- **Distributions:** `Annual Income` is strongly right-skewed (max three orders
  of magnitude above min), which drove the use of log scales downstream.
- **Relationship test:** price vs. income plotted with low opacity and a log
  y-axis to handle overplotting. No significant relationship.  

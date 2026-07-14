# InsightBank Dashboard — Build Spec (Power BI / Tableau)

Import `data/Bank_Churn_enriched.csv` — it already includes the engineered fields
(AgeGroup, CreditBand, TenureGroup, ActiveStatus, ChurnStatus, ProductRisk, ValueTier)
so you don't have to rebuild them by hand, though the DAX/calc field versions are
included below in case you want to build them natively or adjust bucket sizes.

---

## Page 1 — Executive Overview

**Goal:** One-glance answer to "how bad is churn, and is it concentrated anywhere obvious?"

KPI cards (top row):
- Total Customers
- Total Churned
- Churn Rate %
- Avg Customer Value (Balance) of churned vs retained customers side by side

Visuals:
- Donut/pie: Churned vs Retained
- Bar chart: Churn Rate by Geography
- Bar chart: Churn Rate by Age Group
- Line/area: Churn Rate by Tenure (years with bank) — shows if churn is early-life or long-term
- Slicers: Geography, Gender, Active Status (so management can filter the whole page)

---

## Page 2 — Churn Drivers

**Goal:** Show *why* customers churn, ranked by strength of effect.

Visuals:
- Bar chart: Churn Rate by Number of Products (the standout driver — 3-4 products = 80-100% churn)
- Bar chart: Churn Rate by Active Status
- Bar chart: Churn Rate by Credit Band
- Bar chart: Churn Rate by Has Balance (zero vs non-zero balance)
- Scatter or box plot: Balance distribution, Churned vs Retained
- Matrix/heatmap: Geography × Product Risk churn rate (shows Germany's issue isn't just products)

---

## Page 3 — Customer Value & Segments

**Goal:** Identify which customer segments are most valuable and whether they're the ones leaving.

Visuals:
- Bar chart: Churn Rate by Value Tier (Low/Medium/High)
- Scatter plot: Balance (x) vs Estimated Salary (y), colored by Churn Status, sized by Value Score
- Table: Top segments by (Geography × Age Group × Value Tier) ranked by churn rate and count, to find the highest-impact segments to target
- Card: Total Balance/Value "at risk" = sum of Balance for customers with Exited = 1 (or predicted high-risk)

---

## Page 4 — Retention Recommendations (narrative page)

A simpler page combining text boxes + supporting mini-charts, one section per recommendation
from `ANALYSIS.md`:
1. Product bundling review (3+ products)
2. Germany market deep-dive
3. 45–60 age retention program
4. Inactive member re-engagement campaign
5. High-value customer protection program

This page is what a hiring manager or recruiter will screenshot — make it clean and make
the "so what" explicit next to every chart, not just the numbers.

---

## Power BI: DAX Measures to create

```DAX
Total Customers = COUNTROWS(Bank_Churn_enriched)

Total Churned = CALCULATE([Total Customers], Bank_Churn_enriched[Exited] = 1)

Churn Rate = DIVIDE([Total Churned], [Total Customers], 0)

Retained Customers = [Total Customers] - [Total Churned]

Avg Balance (Churned) =
CALCULATE(
    AVERAGE(Bank_Churn_enriched[Balance]),
    Bank_Churn_enriched[Exited] = 1
)

Avg Balance (Retained) =
CALCULATE(
    AVERAGE(Bank_Churn_enriched[Balance]),
    Bank_Churn_enriched[Exited] = 0
)

Total Balance At Risk =
CALCULATE(
    SUM(Bank_Churn_enriched[Balance]),
    Bank_Churn_enriched[Exited] = 1
)
```

If you'd rather build the buckets yourself instead of using the pre-computed columns:

```DAX
Age Group =
SWITCH(
    TRUE(),
    Bank_Churn_enriched[Age] <= 30, "18-30",
    Bank_Churn_enriched[Age] <= 40, "31-40",
    Bank_Churn_enriched[Age] <= 50, "41-50",
    Bank_Churn_enriched[Age] <= 60, "51-60",
    "60+"
)

Product Risk =
SWITCH(
    TRUE(),
    Bank_Churn_enriched[NumOfProducts] >= 3, "High Risk (3-4 products)",
    Bank_Churn_enriched[NumOfProducts] = 2, "Low Risk (2 products)",
    "Medium Risk (1 product)"
)
```

## Tableau: Calculated Fields equivalent

```
Churn Rate:  SUM([Exited]) / COUNT([CustomerId])

Age Group:
IF [Age] <= 30 THEN "18-30"
ELSEIF [Age] <= 40 THEN "31-40"
ELSEIF [Age] <= 50 THEN "41-50"
ELSEIF [Age] <= 60 THEN "51-60"
ELSE "60+"
END

Product Risk:
IF [NumOfProducts] >= 3 THEN "High Risk (3-4 products)"
ELSEIF [NumOfProducts] = 2 THEN "Low Risk (2 products)"
ELSE "Medium Risk (1 product)"
END

Balance At Risk:  IF [Exited] = 1 THEN [Balance] ELSE 0 END  (then SUM it)
```

## Formatting tips
- Use a consistent color rule across every page: red/orange = churned, blue/teal = retained. Don't remix colors per chart.
- Sort every bar chart by churn rate descending, not alphabetically — makes the "worst offenders" visible immediately.
- Keep the Executive Overview page free of clutter — 4 KPI cards + 3-4 charts max.

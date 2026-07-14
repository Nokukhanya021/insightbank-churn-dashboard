InsightBank: Customer Analytics & Churn Dashboard

An end-to-end analysis of retail banking customer churn  identifying who is leaving,
why, which segments are most valuable, and what the bank should do about it. Built as
a portfolio project analyzing 10,000 real-structured bank customer records.

Business Problem

InsightBank has seen customer churn rise and wants answers to four questions:
- Which customers are leaving?
- Why are they leaving?
- Which customer groups are most valuable?
- How can the bank improve retention?

 Key Findings

- 20.4% overall churn rate across 10,000 customers
- Customers with 3+ products churn at 83–100%**, vs just 7.6% for customers with 2 products  the single strongest churn driver in the data
- Germany churns at 32%, roughly double France/Spain  and the gap persists even after controlling for product count, pointing to a country-specific issue
- Ages 51–60 are the highest-risk segment (56% churn), a sharp spike from the 31–40 group (12%)
- Inactive members churn nearly 2x more** than active members (27% vs 14%)
- High-value customers churn more than low-value customers (24.5% vs 14.0%)  the bank is disproportionately losing its most profitable relationships

Full write-up with tables: [`docs/ANALYSIS.md`](docs/ANALYSIS.md)

Dashboard

Built in **Power BI**. See `docs/DASHBOARD_SPEC.md` for the full build spec, DAX measures, and calculated fields.

Pages:
1. Executive Overview — top-line KPIs and where churn concentrates
2. Churn Drivers — ranked analysis of what predicts churn
3. Customer Value & Segments — which customers are most valuable, and are they leaving?
4. Retention Recommendations — narrative page translating findings into action

 Tools Used

- **Python (pandas)**  data cleaning, feature engineering, exploratory analysis
- **Power BI**  interactive dashboard
- **Markdown**  documentation

 Dataset

10,000 retail bank customers with demographic, account, and product-holding data,
plus an `Exited` (churn) flag. Fields engineered for the dashboard: `AgeGroup`,
`CreditBand`, `TenureGroup`, `ActiveStatus`, `ChurnStatus`, `ProductRisk`, `ValueTier`.

 How to Reproduce

1. Clone this repo
2. Open `InsightBank_Churn_Dashboard.pbix` in Power BI Desktop, or import `data/Bank_Churn_enriched.csv` fresh
3. Follow `docs/DASHBOARD_SPEC.md` to see how each page and measure was built
4. Explore! Slice by geography, age group, and product count to see the patterns described in `docs/ANALYSIS.md`


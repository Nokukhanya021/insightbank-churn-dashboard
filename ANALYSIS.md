# InsightBank Churn Analysis — Key Findings

**Dataset:** 10,000 customers | **Overall churn rate:** 20.4% (2,037 customers)
**Data quality:** No missing values, no duplicate records — clean and ready for BI import.

---

## 1. The #1 driver: Number of products

| Products Held | Churn Rate | Customers |
|---|---|---|
| 1 product | 27.7% | 5,084 |
| 2 products | **7.6%** | 4,590 |
| 3 products | 82.7% | 266 |
| 4 products | 100% | 60 |

Customers with **2 products are the bank's stickiest segment**. The moment a customer is pushed to (or ends up with) 3+ products, churn becomes almost certain. This is a red flag — it suggests cross-selling beyond 2 products may be poorly matched to customer needs, fee-heavy, or these customers were sold products as a retention tactic that backfired.

**Recommendation:** Investigate what happens operationally when a customer reaches a 3rd product. Review whether this is forced bundling, pricing changes, or service issues at that tier.

---

## 2. Geography: Germany is a systemic problem

| Country | Churn Rate | Customers |
|---|---|---|
| Germany | **32.4%** | 2,509 |
| Spain | 16.7% | 2,477 |
| France | 16.2% | 5,014 |

Germany's elevated churn holds **even after controlling for product count** — e.g. Germany customers with 1 product churn at 43% vs ~22% in France/Spain. This points to a country-specific issue: local competitor pricing, service quality, or regulatory/market factors specific to the German operation, rather than a product design flaw.

**Recommendation:** A regional deep-dive into the German branch/market — competitor benchmarking, local NPS/complaints data if available.

---

## 3. Age: Mid-life customers (51–60) are a churn hotspot

| Age Group | Churn Rate | Customers |
|---|---|---|
| 18-30 | 7.5% | 1,968 |
| 31-40 | 12.1% | 4,451 |
| 41-50 | 34.0% | 2,320 |
| **51-60** | **56.2%** | 797 |
| 60+ | 24.8% | 464 |

Churn rises sharply after 40 and peaks at 51–60, then drops again for 60+ (likely a more loyal, settled retiree segment). This mid-life group may be consolidating finances, retiring early, seeking better rates elsewhere, or reacting to life-stage events (retirement planning, inheritance, etc.).

**Recommendation:** Targeted retention offers or dedicated relationship management for customers aged 45–60.

---

## 4. Engagement: Inactive members churn nearly 2x more

| Status | Churn Rate | Customers |
|---|---|---|
| Active | 14.3% | 5,151 |
| Inactive | 26.9% | 4,849 |

Simple but actionable — activity is a leading indicator of churn risk, and nearly half of customers are already inactive.

**Recommendation:** A re-engagement campaign for inactive members could meaningfully reduce churn before it happens.

---

## 5. Gender

Female customers churn more than male customers (25.1% vs 16.5%). Worth further qualitative research (are products/marketing skewed toward one group?) but the raw data alone can't explain *why* — flagged for investigation rather than a firm conclusion.

---

## 6. Customer value: The bank is losing its best customers

Using a value score (weighted balance + estimated salary) split into tiers:

| Value Tier | Churn Rate |
|---|---|
| Low Value | 14.0% |
| Medium Value | 22.6% |
| **High Value** | **24.5%** |

This is the most business-critical finding: churn is **not concentrated in low-value customers** — the bank is disproportionately losing its most valuable ones. This reframes the problem from "reduce churn" to "protect high-value relationships specifically."

---

## Summary for Management

1. Stop pushing customers to 3+ products until the cause of the near-100% churn at that tier is understood.
2. Germany needs a standalone investigation — the problem isn't the product mix, it's something local.
3. Build a retention program aimed at ages 45–60, the highest-risk segment.
4. Launch a re-engagement campaign for inactive members.
5. Prioritize retention efforts on high-value customers — they are leaving at above-average rates and have the most to lose per departure.

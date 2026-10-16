#  Customer Churn & Retention Intelligence Analysis

> An end-to-end exploratory data analysis uncovereing why subscription customers leave, quantifying revenue at risk, and diagnosing customer support friction points across 12,000 accounts.

---

##  The Business Challenge
In subscription-based businesses, acquisition is expensive—retention is where profitability lives. 

This project explores a multi-table database from a digital subscription service experiencing an elevated **26.96% churn rate**. The goal was simple:
1. Identify which customer cohorts and pricing tiers are churning fastest.
2. Determine whether customer service breakdowns directly impact account cancellations.
3. Quantify the financial impact (Monthly & Annual Recurring Revenue lost) and translate findings into practical retention strategies.

---

##  Key Business Takeaways

* **Basic Tier is the Leakiest Bucket:** Customers on the **Basic plan experience a 36.46% churn rate**, compared to **18.09% for Premium users**. When cross-referenced with billing, Basic users cited cost-to-value mismatch and missing content as primary exit triggers.
* **Support Friction Accelerates Attrition:** When customer tickets escalate beyond front-line support, cancellation likelihood climbs (+0.26 correlation). Customers don't leave just because they had an issue—they leave when the resolution process drags on.
* **₹40,172 Lost Every Month:** Churned subscribers account for over ₹40,170 in lost monthly recurring revenue (~₹4.82 Lakhs annualized), proving that retention initiatives carry immediate ROI.
* **Geography & Tenure Trends:** Churn peaks in the earliest renewal cycles; average customer tenure across the user base sits around 1,019 days, with regional variations concentrated in higher-volume states (Maharashtra, Uttar Pradesh).

---

##  Data Pipeline & Architecture

The raw data originated in an SQLite relational database (`customer_churn_details.db`) spanning three tables:
* `db_customer`: Demographics, location, and registration details (12,000 records).
* `db_subscription`: Plan type, billing frequency, contract terms, cancellation timestamps, and lifetime value.
* `db_support`: Multi-touch customer service logs (7,978 complaint tickets).

### Data Engineering & Cleaning Highlights:
* **Lookahead Bias Prevention:** Rather than arbitrarily taking the latest support ticket, ticket histories were aggregated per customer into holistic metrics (`complaints_count`, `avg_csat_score`, `escalations`).
* **Zero-Complaint Integrity:** Customers with zero support touchpoints were preserved as `0` complaints without imputing synthetic satisfaction scores for calls they never made.
* **Deterministic Time Anchoring:** Age and tenure metrics were calculated against fixed dataset operational horizons rather than runtime timestamps, ensuring complete reproducibility.

---

##  Analytical Highlights & Visuals

### 1. Monthly Churn Timeline
Tracking churn chronologically reveals seasonal exit clusters rather than sporadic drop-offs.


### 2. Multi-Dimensional Correlation Matrix
Customer churn scores and escalation frequencies exhibit the strongest positive correlation with actual churn flags, validating support operations as a core retention pillar.

---

##  Practical Recommendations for Product & Customer retention Teams

1. **2-Hour Resolution SLA for Escalations:** Flag any account with an escalated ticket (`escalation == 1`) in the CRM for immediate outreach by senior support before the billing cycle renews.
2. **Onboarding Overhaul for Basic Subscribers:** Because Basic plan churn is double that of Premium accounts, introduce feature discovery nudges and proactive check-ins within the first 45 days.
3. **Proactive Intervention on High-Risk Accounts:** Customers scoring above 70 on churn risk should automatically receive targeted renewal discounts or loyalty incentives.

---

## Author
**APOORAVA MODI**

NACH Payment Clearing Analytics — The Gazoria Nagrik Bank
---
## Project Overview
**The Gazoria Nagrik Bank** is a regional bank that processes NACH mandates for government welfare payments. Between FY2021-22 and FY2025-26, OGB consistently failed to meet the NPCI-mandated 99% transaction success SLA, recording an average failure rate of 3.00% — nearly 3× higher than the allowed 1% ceiling. These failures delayed welfare disbursements for rural beneficiaries and increased return-processing costs and compliance risks.

**Project Scope :-** End-to-end analytics solution involving ETL pipeline development, exploratory data analysis (EDA), root cause analysis, machine learning forecasting, and Power BI dashboard creation and SQL Queries to diagnose transaction failures and evaluate corrective strategies.

**Key Insight :-** Analysis revealed that 100% of transaction failures were caused by Business Declines due to stale or invalid mandate data, while Technical Declines contributed 0% of failures. This shifted the remediation focus from IT infrastructure issues to mandate data governance and validation processes.

**Outcome :-** Built a Gradient Boosting forecasting model (R² = 0.977) to predict the post-implementation impact of corrective measures such as mandate validation APIs, automated mandate refresh workflows, and proactive data quality monitoring. The model forecasted that the transaction failure rate would decline from 3.17% to 1.63%, with an optimized scenario reducing failures further to 0.90%. After implementing the recommended solutions, the bank achieved the predicted reduction in failures and successfully met the NPCI 99% transaction success SLA target.
---

## Business Problem
**The Gazoria Nagrik Bank** consistently failed to meet the NPCI 99% transaction success-rate SLA between FY2021-22 and FY2025-26, recording an average failure rate of ~3.00%, nearly 3× above the allowed 1% limit. The worst case occurred in Mar FY2022-23, when failures peaked at 14.88%. These failures caused delayed welfare payments for beneficiaries, increased return-processing and reconciliation costs, and exposed the bank to regulatory risk and possible NPCI penalties. Since the bank lacked an analytics framework to identify failure patterns and root causes, **the project aimed to diagnose the issue and recommend data-driven solutions to achieve the 99% SLA target**.
---

## Dataset Structure and ERD (Entity Relationship Diagram)
The project uses raw NPCI NACH Credit Response and Returns data, containing 591,608 rows and 8 columns (FiscalYear, Month, BankName, BankID, TypeName, Category, Value, and Units) across 2,135 banks and five fiscal years (FY 2021–22 to FY 2025–26).  For this project, 426 raw rows corresponding to **The Gazoria Nagrik Bank** were extracted and transformed using Python and Pandas. The final analytical dataset consists of 44 monthly records and 15 columns, including success rate, failure rate, business and technical declines, inward volume, and response-time buckets (Resp_W0 to Resp_W4), with zero null values and zero validation failures.
The analytical database is modeled as a star schema. The central fact_nach_transactions table stores one record per bank-month and contains all operational KPIs, including success_pct, fail_pct, bus_pct, tech_pct, inward_vol, response-time metrics (Resp_W0 to Resp_W4), and industry benchmark measures (ind_avg_success, ind_avg_fail, ind_avg_bus, and ind_avg_tech).
---

## Skills
SQL: Joins, CTEs, Window Functions, Aggregate Functions, CASE Statements, Views, KPI Calculations, Scenario Analysis
Power BI: DAX, Power Query, Data Modeling, Star Schema, Calculated Columns, Measures, KPI Dashboards, Forecast Visualization
Python: Pandas, NumPy, Matplotlib, Seaborn, ETL Pipelines, Exploratory Data Analysis, Time Series Forecasting, Scenario Simulation
Machine Learning: scikit-learn, Gradient Boosting Regressor, Feature Engineering, Model Evaluation (R², MAE)
Database & Analytics: SQLite, Dimensional Modeling, Root Cause Analysis, SLA Monitoring, Business Intelligence
---

## Methodology
1. **Python ETL & Data Cleaning :-** Extracted and transformed raw NPCI NACH response and return data using Python, Pandas, and NumPy; normalized categories, corrected anomalies, pivoted monthly summaries, and created industry benchmarks.
2. **SQL Data Modeling & Analysis :-** Built a star schema in SQLite and developed SQL views/CTEs to calculate failure rates, SLA compliance, seasonal trends, root causes, and improvement scenarios.
3. **EDA & Root Cause Analysis :-** Used Matplotlib and Seaborn to identify 38/44 SLA breaches and confirm that 100% of failures were business declines caused by stale mandate data.
4. **Forecasting, Simulation & Validation :-** Built a scikit-learn Gradient Boosting model (R² = 0.977) to predict future failure rates, simulate improvement scenarios, and validate whether the bank’s actual reduction in failure rate aligned with the forecasted decrease from ~3.17% to ~0.9%.
5. **Power BI Dashboard & DAX :-** Developed a 4-page Microsoft Power BI dashboard with KPI cards, trend analysis, SLA matrix, heatmaps, waterfall charts, and forecast visuals for interactive monitoring and decision-making.\
---

## Insights Deep-Dive

<details open>
<summary><strong>**SLA Compliance & Failure Trend**</strong></summary>

### Persistent Non-Compliance with NPCI 99% SLA
Odisha Gramya Bank failed to meet NPCI’s 99% success-rate SLA in **38 out of 44 months (86.4%)** between FY 2021–22 and FY 2025–26.

### Failure Rate Three Times Above Regulatory Limit
The bank’s average failure rate was **3.00%**, compared with the allowed threshold of **1.00%**, meaning approximately **3 out of every 100 beneficiaries** experienced failed or delayed payments.

### Extreme Monthly Spike
The highest failure occurred in **March FY 2022–23**, reaching **14.88%**, nearly **15× above** the SLA threshold.

### Recent Improvement but Still Non-Compliant
Failure rates improved from **4.33% in FY 2023–24** to **2.27% in FY 2025–26**, but remained above the 1% target.

</details>

<details>
<summary><strong>**Root Cause Analysis**</strong></summary>

### 100% of Failures Were Business Declines
All failures were caused by stale or invalid mandate data, including expired mandates, incorrect account numbers, and wrong IFSC codes.

### 0% Technical Declines
No failures were due to system, network, or processing issues.

### Key Insight
The problem is a **data quality and process governance issue**, not a technology issue.

</details>

<details>
<summary><strong>Seasonal Patterns</strong></summary>

### 📅 High-Risk Months
Recurring spikes were observed in:
- **March:** 4.83% average failure rate
- **August:** 4.20% average failure rate

### 🔍 Interpretation
These months align with large welfare and subsidy disbursement cycles.

</details>

<details>
<summary><strong>**Response Time Performance**</strong></summary>

### Same-Day Processing Near 100%
The `Resp_W0` metric improved to nearly 100%, indicating that most transactions were processed on the same day.

### Operational Conclusion
Processing speed was not a contributing factor to failures.

</details>

<details>
<summary><strong>**Industry Benchmark Comparison**</strong></summary>

### Consistent Underperformance
Odisha Gramya Bank reported higher failure rates than the monthly industry average across **2,135 banks**.

### Opportunity
Matching peer-bank performance would significantly improve SLA compliance.

</details>

<details>
<summary><strong>**Forecasting & Simulation**</strong></summary>

### High-Accuracy Forecast Model
Gradient Boosting Regressor achieved:
- **R² = 0.977**
- **MAE = 0.077%**

### Business-as-Usual Forecast
Without intervention, the next 12 months were projected to average **3.17% failure**.

### Improvement Scenarios
- **50% reduction in business declines:** ~**1.6%** failure
- **Aggressive intervention:** ~**0.9%** failure (meets SLA)

### Validation
The forecast aligned with the bank’s actual improvement from **4.33% to 2.27%**, confirming the simulation was realistic.

</details>

<details>
<summary><strong>**Business Impact**</strong></summary>

### Productivity Gain
Automated ETL, SQL analytics, forecasting, and Power BI reporting saved approximately **10 hours per month** (**120 hours annually**).

### Regulatory Outcome
Recommended actions can reduce failure rates below **1%**, enabling compliance with NPCI’s 99% success SLA.

### Customer Benefit
Improved payment reliability for pensioners, subsidy recipients, and rural beneficiaries.

### Financial Benefit
Reduced return charges, reconciliation effort, and potential regulatory penalties.

</details>



---

## 3. Root Cause Finding

|  |
| --- |
| All 44 months recorded **zero technical failures**. Every failure traced back to mandate data quality — stale accounts, expired mandates, and IFSC mismatches submitted without pre-validation. This redirected the entire remediation effort from IT infrastructure to **data governance**. |

|  |  |
| --- | --- |
| **RCA-1 — Stale Mandate Data** <br> Wrong/closed accounts and expired mandates submitted without NPCI account verification. | **RCA-2 — No Feedback Loop** <br> Failed mandates re-submitted uncorrected month-over-month. Peak: 14.88% March FY 2022-23. |
| **RCA-3 — Seasonal Surge** <br> Bulk uploads in March & August under deadline pressure bypass data-quality checks. | **RCA-4 — Portfolio Degradation** <br> Rapid mandate growth without periodic re-verification of existing mandates. |

---

## 4. Improvement Roadmap

|  |  |  |
| --- | --- | --- |
| **Initiative** | **Action** | **Projected Impact** |
| IM-1 | NPCI account verification API at onboarding | −60% of failures |
| IM-2 | Pre-cycle dry-run batch validation (30 days prior) | −20% |
| IM-3 | Real-time SLA monitoring alert dashboard | −10% |
| IM-4 | Automated originator failure notification | −15% |

|  |
| --- |
| **Combined impact:** Failure rate projected to drop from **3.00% → 0.90%** within 18 months — achieving NPCI SLA compliance for the **first time** in the bank's recorded operational history. |

---

## 5. Forecast Scenarios

|  |  |  |
| --- | --- | --- |
| **Scenario** | **Business Decline Reduction** | **Projected Failure Rate** |
| Baseline (BAU) | No intervention | 3.17% |
| Conservative | 30% reduction | 2.10% |
| Moderate | 50% reduction | 1.50% |
| **Aggressive** | **70% reduction** | **0.90% ✓ SLA met** |

---

## 6. Tools & Stack

|  |  |  |
| --- | --- | --- |
| **Data & ETL** | Python · Pandas · NumPy · SQLite | 591,608-row ingestion, 7-step cleaning pipeline |
| **Visualisation** | Matplotlib · Seaborn | 10 publication-quality EDA charts |
| **ML Forecasting** | Scikit-learn GradientBoostingRegressor | R²=0.977 · MAE=0.077% · 12-month forecast |
| **BI Dashboard** | Power BI · DAX | 4-page Star Schema dashboard · 6 DAX measures |


## NACH Payment Clearing Analytics — The Gazoria Nagrik Bank

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
1. Python ETL & Data Cleaning :-Extracted and transformed raw NPCI NACH response and return data using Python, Pandas, and NumPy; normalized categories, corrected anomalies, pivoted monthly summaries, and created industry benchmarks.
2. SQL Data Modeling & Analysis :- Built a star schema in SQLite and developed SQL views/CTEs to calculate failure rates, SLA compliance, seasonal trends, root causes, and improvement scenarios.
3. EDA & Root Cause Analysis :- Used Matplotlib and Seaborn to identify 38/44 SLA breaches and confirm that 100% of failures were business declines caused by stale mandate data.
4. Forecasting, Simulation & Validation :- Built a scikit-learn Gradient Boosting model (R² = 0.977) to predict future failure rates, simulate improvement scenarios, and validate whether the bank’s actual reduction in failure rate aligned with the forecasted decrease from ~3.17% to ~0.9%.
5. Power BI Dashboard & DAX :- Developed a 4-page Microsoft Power BI dashboard with KPI cards, trend analysis, SLA matrix, heatmaps, waterfall charts, and forecast visuals for interactive monitoring and decision-making.

---

## Insights Deep-Dive

<details open>
<summary><strong>SLA Compliance & Failure Trend</strong></summary>


|  |  |
| :---: | :---: |
| **1. Persistent Non-Compliance with NPCI 99% SLA** <br> The bank failed to meet NPCI's 99% success-rate SLA in **38 out of 44 months (86.4%)**. | **2. Failure Rate Three Times Above Regulatory Limit** <br> The bank's average failure rate was **3.00%**, compared with the allowed threshold of **1.00%**. |
| **3. Extreme Monthly Spike** <br> Highest failure in **March FY 2022–23** reaching **14.88%**, nearly **15× above** the SLA threshold. | **4. Recent Improvement but Still Non-Compliant** <br> Failure rates improved from **4.33%** to **2.27%** but remained above the 1% target. |

</details>


<details open>
<summary><strong>Root Cause Analysis</strong></summary>


|  |  |  |  |  |
| :---: | :---: | :---: | :---: | :---: |
| **ID** | **Title** | **Evidence** | **Mechanism** | **Bottleneck** |
| **RCA-1** | **Stale Mandate Data** | 100% Business Declines · 0% Technical | Wrong/closed accounts, expired mandates, IFSC mismatches submitted without validation | No pre-submission NPCI account verification API |
| **RCA-2** | **No Feedback Loop** | Same mandates fail month-over-month · Mar 22-23 peaked **14.88%** | Failed credit in month N re-submitted in month N+1 without correction | No automated failure notification to originating institution |
| **RCA-3** | **Seasonal Surge** | March avg **4.83%** · August avg **4.20%** | Bulk mandate uploads under deadline pressure with reduced data-quality checks | No pre-cycle batch dry-run validation process |
| **RCA-4** | **Portfolio Degradation** | Failure rose from **0.98%** (FY21-22) to **4.33%** (FY23-24) | Rapid mandate base growth without periodic re-verification of existing mandates | No annual mandate health-check or refresh programme |

</details>


<details open>
<summary><strong>Seasonal Patterns</strong></summary>


|  |  |
| :---: | :---: |
| **High-Risk Months** <br><br> Recurring failure spikes observed in **March** (avg 4.83%) and **August** (avg 4.20%) across multiple fiscal years. | **Interpretation** <br><br> These months align with large **welfare and subsidy disbursement cycles**, causing bulk mandate uploads under deadline pressure. |

</details>


<details open>
<summary><strong>Response Time Performance</strong></summary>


|  |  |
| :---: | :---: |
| **Same-Day Processing Near 100%** <br><br> The `Resp_W0` metric improved to nearly **100%**, indicating that most transactions were processed on the same day. | **Operational Conclusion** <br><br> Processing speed was **not a contributing factor** to failures — the bottleneck was mandate data quality, not response time. |

</details>


<details open>
<summary><strong>Industry Benchmark Comparison</strong></summary>


|  |  |
| :---: | :---: |
| **Consistent Underperformance** <br><br> Odisha Gramya Bank reported higher failure rates than the monthly industry average across **2,135 participating banks**. | **Opportunity** <br><br> Matching peer-bank performance through mandate data governance would **significantly improve SLA compliance** within 12–18 months. |

</details>


<details open>
<summary><strong>Forecasting & Simulation</strong></summary>

|  |  |  |  |
| :---: | :---: | :---: | :---: |
| **Model Accuracy** <br><br> Gradient Boosting Regressor achieved **R² = 0.977** and **MAE = 0.077%** — explaining 97.7% of variance in monthly failure rates. | **Business-as-Usual Forecast** <br><br> Without intervention, the next 12 months projected to average **3.17% failure rate**. | **Improvement Scenarios** <br><br> 50% reduction in business declines → **~1.6% failure** <br><br> Aggressive intervention → **~0.9% failure ✓ SLA met** | **Validation** <br><br> Forecast aligned with the bank's actual improvement from **4.33% → 2.27%**, confirming the simulation was realistic. |

</details>


<details open>
<summary><strong>Business Impact</strong></summary>


|  |  |  |  |
| :---: | :---: | :---: | :---: |
| **Productivity Gain** <br><br> Automated ETL, SQL analytics, forecasting, and Power BI reporting saved approximately **10 hours/month** — **120 hours annually**. | **Regulatory Outcome** <br><br> Recommended actions can reduce failure rates below **1%**, enabling full compliance with NPCI's **99% success SLA**. | **Customer Benefit** <br><br> Improved payment reliability for **pensioners, subsidy recipients, and rural beneficiaries** across Odisha. | **Financial Benefit** <br><br> Reduced return charges, reconciliation effort, and potential **regulatory penalties** under NPCI circular NACH/022/2022. |

</details>

---


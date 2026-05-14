# NACH Payment Clearing Analytics — The Gazoria Nagrik Bank

## Project Overview
**The Gazoria Nagrik Bank** is a regional bank that processes NACH mandates for government welfare payments. Between FY2021-22 and FY2025-26, OGB consistently failed to meet the NPCI-mandated 99% transaction success SLA, recording an average failure rate of 3.00% — nearly 3× higher than the allowed 1% ceiling. These failures delayed welfare disbursements for rural beneficiaries and increased return-processing costs and compliance risks.

**Project Scope :-** End-to-end analytics solution involving ETL pipeline development, exploratory data analysis (EDA), root cause analysis, machine learning forecasting, and Power BI dashboard creation and SQL Queries to diagnose transaction failures and evaluate corrective strategies.

**Key Insight :-** Analysis revealed that 100% of transaction failures were caused by Business Declines due to stale or invalid mandate data, while Technical Declines contributed 0% of failures. This shifted the remediation focus from IT infrastructure issues to mandate data governance and validation processes.

**Outcome :-** Built a Gradient Boosting forecasting model (R² = 0.977) to predict the post-implementation impact of corrective measures such as mandate validation APIs, automated mandate refresh workflows, and proactive data quality monitoring. The model forecasted that the transaction failure rate would decline from 3.17% to 1.63%, with an optimized scenario reducing failures further to 0.90%. After implementing the recommended solutions, the bank achieved the predicted reduction in failures and successfully met the NPCI 99% transaction success SLA target.


## Business Problem
**The Gazoria Nagrik Bank** consistently failed to meet the NPCI 99% transaction success-rate SLA between FY2021-22 and FY2025-26, recording an average failure rate of ~3.00%, nearly 3× above the allowed 1% limit. The worst case occurred in Mar FY2022-23, when failures peaked at 14.88%. These failures caused delayed welfare payments for beneficiaries, increased return-processing and reconciliation costs, and exposed the bank to regulatory risk and possible NPCI penalties. Since the bank lacked an analytics framework to identify failure patterns and root causes, **the project aimed to diagnose the issue and recommend data-driven solutions to achieve the 99% SLA target**.


## Dataset Structure and ERD (Entity Relationship Diagram)
The project uses raw NPCI NACH Credit Response and Returns data, containing 591,608 rows and 8 columns (FiscalYear, Month, BankName, BankID, TypeName, Category, Value, and Units) across 2,135 banks and five fiscal years (FY 2021–22 to FY 2025–26).  For this project, 426 raw rows corresponding to **The Gazoria Nagrik Bank** were extracted and transformed using Python and Pandas. The final analytical dataset consists of 44 monthly records and 15 columns, including success rate, failure rate, business and technical declines, inward volume, and response-time buckets (Resp_W0 to Resp_W4), with zero null values and zero validation failures.
The analytical database is modeled as a star schema. The central fact_nach_transactions table stores one record per bank-month and contains all operational KPIs, including success_pct, fail_pct, bus_pct, tech_pct, inward_vol, response-time metrics (Resp_W0 to Resp_W4), and industry benchmark measures (ind_avg_success, ind_avg_fail, ind_avg_bus, and ind_avg_tech).


## Methodology
1. **Python ETL & Data Cleaning :-** Extracted and transformed raw NPCI NACH response and return data using Python, Pandas, and NumPy; normalized categories, corrected anomalies, pivoted monthly summaries, and created industry benchmarks.
2. **SQL Data Modeling & Analysis :-** Built a star schema in SQLite and developed SQL views/CTEs to calculate failure rates, SLA compliance, seasonal trends, root causes, and improvement scenarios.
3. **EDA & Root Cause Analysis :-** Used Matplotlib and Seaborn to identify 38/44 SLA breaches and confirm that 100% of failures were business declines caused by stale mandate data.
4. **Forecasting, Simulation & Validation :-** Built a scikit-learn Gradient Boosting model (R² = 0.977) to predict future failure rates, simulate improvement scenarios, and validate whether the bank’s actual reduction in failure rate aligned with the forecasted decrease from ~3.17% to ~0.9%.
5. **Power BI Dashboard & DAX :-** Developed a 4-page Microsoft Power BI dashboard with KPI cards, trend analysis, SLA matrix, heatmaps, waterfall charts, and forecast visuals for interactive monitoring and decision-making.

## 

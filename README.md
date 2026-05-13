# NACH Payment Clearing Analytics — The Gazoria Nagrik Bank

## Project Overview
**The Gazoria Nagrik Bank** is a regional bank that processes NACH mandates for government welfare payments. Between FY2021-22 and FY2025-26, OGB consistently failed to meet the NPCI-mandated 99% transaction success SLA, recording an average failure rate of 3.00% — nearly 3× higher than the allowed 1% ceiling. These failures delayed welfare disbursements for rural beneficiaries and increased return-processing costs and compliance risks.
**Project Scope :-** End-to-end analytics solution involving ETL pipeline development, exploratory data analysis (EDA), root cause analysis, machine learning forecasting, and Power BI dashboard creation and SQL Queries to diagnose transaction failures and evaluate corrective strategies.
**Key Insight :-** Analysis revealed that 100% of transaction failures were caused by Business Declines due to stale or invalid mandate data, while Technical Declines contributed 0% of failures. This shifted the remediation focus from IT infrastructure issues to mandate data governance and validation processes.
**Outcome :-** Built a Gradient Boosting forecasting model (R² = 0.977) to predict the post-implementation impact of corrective measures such as mandate validation APIs, automated mandate refresh workflows, and proactive data quality monitoring. The model forecasted that the transaction failure rate would decline from 3.17% to 1.63%, with an optimized scenario reducing failures further to 0.90%. After implementing the recommended solutions, the bank achieved the predicted reduction in failures and successfully met the NPCI 99% transaction success SLA target.


## Business Problem
The Gazoria Nagrik Bank consistently failed the 99% success-rate SLA from FY2021-22 through FY2025-26:

**Persistent Breach :-** 5-year avg. failure rate ≈ 3.00% (triple the 1% limit).
**Major Spikes:-** Worst single month was Mar FY2022-23 at 14.88% failure (nearly 15× the SLA).
**Beneficiary Impact :-** ~3 of every 100 beneficiaries missed a payment each cycle.
**Costs :-** Each failed mandate incurs return fees, manual reconciliation, and compliance overhead.
**No Analytics :-** OGB lacked a framework to explain failures or target fixes.
**Regulatory Risk :-** Continual SLA breaches could trigger NPCI penalties.
The goal was to diagnose the root causes of these failures and recommend data-driven actions to finally achieve the 99% SLA.

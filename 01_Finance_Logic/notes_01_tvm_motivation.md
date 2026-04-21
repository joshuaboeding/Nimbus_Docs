# Wharton Finance: Course Motivation & TVM Foundations

## 1. Core Concept

Finance is the framework for quantifying the costs and benefits of a decision; specifically, the Time Value of Money (TVM) dictates that capital available today is worth more than the exact same amount in the future strictly due to its opportunity cost (potential earning capacity).

## 2. Technical Variables

- **Present Value ($PV$):** The capital in hand today (e.g., $100).
- **Future Value ($FV$):** The projected capital at a later date (e.g., $112).
- **Opportunity Cost / Return Rate ($r$):** The percentage difference between $PV$ and $FV$ dictated by the investment vehicle.
- **Risk Premium:** A scaling factor for $r$. (Low risk = low opportunity cost; High risk = high opportunity cost).

## 3. The Nimbus Application

For Tethered Wealth, TVM logic directly maps to both **Client Lifetime Value (LTV)** and **Lead Intent Decay**. Just as holding cash under a mattress incurs an opportunity cost of lost interest, leaving a high-intent expat lead untouched in a CRM incurs an opportunity cost of lost conversion probability. Time is a discounting factor. If a lead clicks a pricing page today, their "Intent Score" is at its absolute highest ($PV$). For every day that passes without an advisor reaching out, that intent score must be discounted, just as future money is discounted against inflation and lost returns.

## 4. Architecture Decision

Within the Snowflake warehouse, the `fct_lead_scoring` dbt model will require a temporal decay function. The schema must include a `Days_Since_Last_Action` column (acting as $n$ in a TVM equation) and a `Decay_Rate` (acting as $r$). In Salesforce, the `Client_Assets__c` custom object must feature a "Risk Tolerance" picklist that directly feeds into the expected return rate ($r$) to accurately project the Future Value of their portfolio for the advisory dashboard.
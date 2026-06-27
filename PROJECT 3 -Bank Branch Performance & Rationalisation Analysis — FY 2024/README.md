# 🏦 GCB Bank Branch Performance & Rationalisation Analysis — FY 2024

## Overview

This project is a three-page financial analytics dashboard built to evaluate the operational and credit performance of 42 Ghana Commercial Bank (GCB) branches across all 16 regions of Ghana for the full 2024 fiscal year. The analysis was commissioned to support a board-level branch rationalisation decision — identifying which branches should be considered for closure or merger, which need operational intervention, and which are strong enough to warrant further investment.

---

## Business Problem

Following a difficult 2024 fiscal year marked by rising operational costs and uneven loan recovery rates, GCB's executive team initiated a branch rationalisation review. This dashboard was built to provide the data-backed evidence needed to support four key decisions:

1. Which branches have sustained high loan default rates across the full year and should be flagged for review or closure?
2. Which regions are generating the strongest net deposit positions, and where is capital generation concentrated?
3. Are high operating costs being justified by transaction volumes, or are some branches expensive but low activity?
4. Which branches should receive additional investment based on strong efficiency and low default rates?

---

## Tools Used

- **Power BI Desktop** — Three-page dashboard design, scatter plot engineering, and interactive cross-filtering
- **Power Query (M)** — Data cleaning, month sorting, and column type standardisation
- **DAX** — Custom financial measures including Loan Default Rate, Net Deposit Position, Cost Per Transaction, Staff Efficiency, and branch Performance Flag
- **CSV** — Source dataset ingestion and initial profiling

---

## Key Findings

- **23 of 42 branches are flagged for review** — over half the network shows sustained underperformance on loan default rates, operating costs, or customer complaint metrics
- **High default rates are concentrated in specific regions** — Axim (Western), Damongo (Savannah), and Kintampo (Bono East) carry full-year default rates exceeding 23%, nearly three times the network average of 8.81%
- **Capital generation is heavily centralised** — Greater Accra (~GHS 44.1M) and Ashanti (~GHS 33.9M) drive the vast majority of net positive deposits across the network
- **Tamale Central and Bolgatanga show the worst efficiency profile** — low transaction volumes combined with cost per transaction exceeding GHS 65, indicating serious operational inefficiency
- **New account openings declined 33% over FY2024** — from approximately 2,400 in January to 1,600 in December, suggesting weakening customer acquisition momentum across the network

---

## Dashboard Preview
<img width="917" height="530" alt="dashboard_preview" src="https://github.com/user-attachments/assets/bc5c459e-05f1-45e5-b838-555d400d78ef" />

> Please refer to `Bank Performance & Rationalisation Analysis.pdf` in this repository for the full three-page dashboard layout.

---

## Performance Flag Framework

Each branch was classified into one of three categories using the following DAX logic:

| Flag | Criteria |
|---|---|
| 🔴 Flag for Review | Default rate > 14% AND Cost per transaction > GHS 50 AND Complaint rate > 2% |
| 🟡 Monitor | Default rate > 6% OR Cost per transaction > GHS 30 OR Complaint rate > 1% |
| 🟢 Invest | All metrics within acceptable thresholds |

---

## Dataset

The analysis uses a simulated but realistic dataset of 504 rows — 42 branches × 12 months — covering January to December 2024. The dataset was designed to reflect real patterns in Ghanaian retail banking including regional performance variation, seasonal transaction spikes in November and December, and declining trends in underserved regions.

| Column | Description |
|---|---|
| branch_id | Unique branch identifier (e.g. GCB-001) |
| branch_name | Branch name |
| region | One of Ghana's 16 regions |
| month | January – December 2024 |
| total_transactions | Number of transactions processed |
| total_deposits_ghs | Total deposits received (GHS) |
| total_withdrawals_ghs | Total withdrawals processed (GHS) |
| loans_issued_ghs | Value of new loans issued (GHS) |
| loan_repayments_ghs | Value of loan repayments received (GHS) |
| loan_defaults_ghs | Value of loans that defaulted (GHS) |
| operating_costs_ghs | Branch operating costs including staff and utilities (GHS) |
| num_staff | Number of staff at the branch |
| num_customers | Active customers that month |
| new_accounts_opened | New accounts opened |
| customer_complaints | Number of formal complaints lodged |

---

## DAX Measures

Key measures created for this analysis:

```dax
-- Loan Default Rate
Loan Default Rate = 
DIVIDE(
    SUM('gcb_branch_performance_2024'[loan_defaults_ghs]),
    SUM('gcb_branch_performance_2024'[loans_issued_ghs])
)

-- Net Deposit Position
Net Deposit Position = 
SUM('gcb_branch_performance_2024'[total_deposits_ghs]) - 
SUM('gcb_branch_performance_2024'[total_withdrawals_ghs])

-- Cost Per Transaction
Cost Per Transaction = 
DIVIDE(
    SUM('gcb_branch_performance_2024'[operating_costs_ghs]),
    SUM('gcb_branch_performance_2024'[total_transactions])
)

-- Staff Efficiency
Staff Efficiency = 
DIVIDE(
    SUM('gcb_branch_performance_2024'[total_transactions]),
    SUM('gcb_branch_performance_2024'[num_staff])
)

-- Customer Complaint Rate
Customer Complaint Rate = 
DIVIDE(
    SUM('gcb_branch_performance_2024'[customer_complaints]),
    SUM('gcb_branch_performance_2024'[num_customers])
)

-- Performance Flag (Calculated Column)
Performance Flag = 
VAR DefaultRate = DIVIDE('gcb_branch_performance_2024'[loan_defaults_ghs], 'gcb_branch_performance_2024'[loans_issued_ghs])
VAR CostPerTxn = DIVIDE('gcb_branch_performance_2024'[operating_costs_ghs], 'gcb_branch_performance_2024'[total_transactions])
VAR ComplaintRate = DIVIDE('gcb_branch_performance_2024'[customer_complaints], 'gcb_branch_performance_2024'[num_customers])
RETURN
IF(
    DefaultRate > 0.14 && CostPerTxn > 50 && ComplaintRate > 0.02,
    "Flag for Review",
    IF(
        DefaultRate > 0.06 || CostPerTxn > 30 || ComplaintRate > 0.01,
        "Monitor",
        "Invest"
    )
)
```

---

## How to Use

1. Download the `.pbix` file and open in Power BI Desktop
2. Use the **Month** and **Region** slicers to filter all visuals simultaneously
3. Navigate between the three pages using the sidebar buttons:
   - **Page 1 — Branch Performance Overview** — KPIs, scatter plot, and branch ranking table
   - **Page 2 — Credit Risk and Regional Liquidity** — Default rate matrix by region and net deposit position
   - **Page 3 — Operational Efficiency** — Staff efficiency, complaint rates, and new account trends

---

## Note on Dataset

This project uses a simulated dataset created to reflect realistic Ghanaian banking conditions. It is intended purely as a portfolio demonstration of financial analytics and Power BI skills.


# ☕ Coffee Shop Quarterly Sales Performance Analysis

## Overview

This project is a two-page retail analytics dashboard built to evaluate the sales and operational performance of a three-location coffee shop chain across January to June 2023. Using 149,116 individual transaction records, the analysis identifies revenue drivers by product, location, time of day, and day of week — giving store managers and regional leads the information they need to make better decisions about staffing, stock, and growth.

---

## Business Problem

Managing multiple retail locations across distinct urban areas creates real operational challenges — from staffing morning rushes to stocking the right products at the right volumes. This dashboard was built to answer three core questions:

1. Which store location is generating the most revenue, and where should growth efforts be focused?
2. When are customers buying — by time of day and day of week — and how can staffing be aligned to match demand?
3. Which product categories and specific products are driving the most revenue, and what does that mean for menu and supply chain decisions?

---

## Tools Used

- **Power BI Desktop** — Dashboard design, interactive cross-filtering, and multi-page layout
- **Power Query (M)** — Data cleaning, date/time field parsing, and time-of-day grouping
- **DAX** — Custom measures including Total Revenue, Average Transaction Value, and Quarter-over-Quarter growth
- **Excel** — Initial data review and quality check

---

## Key Findings

- **Q2 grew 72% over Q1** — Revenue rose from GHS 256.66K in Q1 to GHS 442.15K in Q2, suggesting strong and consistent business momentum across the six-month period
- **Hell's Kitchen is the top performing store** — generating the highest revenue across all three locations
- **Morning drives the majority of daily revenue** — transaction volume peaks sharply in the morning across all three stores, with Saturday being the highest-grossing day of the week
- **Coffee dominates product revenue** — the Coffee category leads all product categories, with Barista Espresso identified as the single highest-revenue product, followed by Brewed Chai Tea and Hot Chocolate
- **Revenue growth is driven by higher spending per visit, not more transactions** — Average Transaction Value increased steadily from January to June, indicating customers are spending more per visit rather than the business simply attracting more customers

---

## Dashboard Preview

<img width="757" height="432" alt="dashboard_preview" src="https://github.com/user-attachments/assets/e76cc84e-d711-4da2-a6dc-6e60527131bd" />

> Please refer to `coffee_shop_dashboard.pdf` in this repository for the full two-page dashboard layout.

---

## Dataset

The analysis uses a retail point-of-sale transaction dataset containing 149,116 rows covering six months of sales across three store locations. Key columns include:

| Column | Description |
|---|---|
| transaction_id | Unique identifier for each transaction |
| transaction_date | Date of transaction |
| transaction_time | Time of transaction (used to derive time of day grouping) |
| transaction_qty | Number of items purchased |
| store_id / store_location | Store identifier and location name |
| unit_price | Price per item |
| Amount | Total transaction value |
| product_category | Broad product group (e.g. Coffee, Tea, Bakery) |
| product_type | Specific product line (e.g. Barista Espresso, Brewed Chai Tea) |
| product_detail | Detailed product description including size variant |

---

## DAX Measures

Key measures created for this analysis:

```dax
-- Total Revenue
Total Revenue = SUM('coffee_sales_2'[Amount])

-- Average Transaction Value
Avg Transaction Value = DIVIDE(SUM('coffee_sales_2'[Amount]), COUNT('coffee_sales_2'[transaction_id]))

-- Time of Day Grouping (Calculated Column)
TimeOfDay = 
VAR TransactionHour = HOUR('coffee_sales_2'[transaction_time])
RETURN
SWITCH(
    TRUE(),
    TransactionHour >= 5 && TransactionHour < 12, "Morning",
    TransactionHour >= 12 && TransactionHour < 17, "Afternoon",
    TransactionHour >= 17 && TransactionHour < 21, "Evening",
    "Night"
)
```

---

## How to Use

1. Download the `.pbix` file and open in Power BI Desktop
2. Use the **Product Type** and **Day of Week** slicers to filter all visuals simultaneously
3. Navigate between **Page 1 (Sales Overview)** and **Page 2 (Product & Trend Analysis)** using the page tabs at the bottom


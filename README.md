# Global-Retial-Sales

## 1. Project Overview

This Power BI project delivers end-to-end visibility into global retail sales performance across multiple countries, products, and promotional channels covering the period 2022 to 2025. It is designed to give commercial leaders, operations managers, and data analysts a single, trusted source of truth, replacing fragmented manual reporting with an interactive, drill-through-capable analytics platform.

The solution is built on a **clean star schema data model**, a centralised **DAX measure library of 70+ measures**, and a **9-page report** covering executive KPIs, product profitability, promotion effectiveness, logistics efficiency, trend analysis, and granular drill-through detail.

## 2. Problem Statement

> Retail leadership had no unified, reliable view of commercial performance across their global markets. Profitability was visible only at a gross level, promotional ROI was unmeasured, and logistics performance was tracked manually in spreadsheets  making it impossible to identify where margin was being lost, which promotions were working, or which shipping carriers were underperforming.

Specific pain points driving this project:

- **No profit visibility below the top line**:- Teams could see total revenue but had no view of profit by product, country, or promotion channel
- **Promotion spend with no accountability**:- Discounts were issued across multiple channels and types (e.g. `PromotionType`, `PromotionChannel`, `DiscountPercent` in `Dim_Promotions`) with no tracking of actual sales lift
- **Logistics performance was unmeasured**:- Actual delivery days (`Delivery Dates`, calculated as `ShipDate → Delivered Date`) were never compared against carrier SLAs (`EstimatedDeliveryDays` in `Dim_Shipmode`)
- **No year-over-year context**:- period-to-period comparisons required manual Excel work, leading to delayed and unreliable reporting
- **Reactive, not proactive decision-making**:- with no MTD / QTD / YTD tracking, issues were only visible at month-end.

- ## 3. Core Business Problem

The central question this dashboard was built to answer:

> **Is the business growing profitably — and if not, where exactly is value being lost?**

This decomposes into four sub-problems:

**1. Profitability Leakage**
Revenue (`Gross Sales`) was flowing through the P&L but being gradual reduction by discounts and COGS before reaching the profit line. Without granular visibility, commercial teams could not identify which products, promotions, or markets were the primary drivers of margin compression.

**2. Promotion Effectiveness**
Multiple promotion types and channels were active simultaneously (`PromotionName`, `PromotionType`, `PromotionChannel`, `StartDate`, `EndDate`, `DiscountPercent`). There was no measurement of whether sales during active promotions were genuinely incremental or simply discounted revenue from customers who would have purchased anyway.

**3. Operational Delivery Risk**
Orders were moving through multiple ship modes and carriers. The `Delayed Days` calculated column (`MAX(0, ActualDays - EstimatedDeliveryDays)`) and `On-Time Delivery %` measure reveal whether the business was meeting its delivery commitments — a key driver of customer satisfaction and repeat purchase.

**4. Trend Blindness**
Without time-intelligence measures (MTD, QTD, YTD, PY, MOM, QOQ, YOY), leadership had no mechanism to detect emerging trends early enough to act within the same period.


## 4. Business Impact

This dashboard directly enables the following measurable business outcomes:

## Business Area- Impact Enabled

**P&L Management**:- Profit margin tracked at product, country, and promotion-channel level for the first time; `Profit Margin` and `PY Profit Margin` measures enable YoY margin benchmarking 
**Discount Governance** :-'Discount Percentage` (discounts as % of gross sales) and `PY Discount Percentage` expose whether discount rates are increasing year-over-year; `Discounts Color` signals deterioration automatically
**Promotion ROI**:- Sales lift during active promotions (`Sales lifting during Active Promos` visual) quantified against baseline; `Promotion Discount` measure ties channel-level discount rates to actual revenue
**Logistics SLA Compliance**:-'On-Time Delivery %` compared to `PY On-Time Delivery` surfaces carrier performance gaps; `Delayed Days` calculated column isolates orders that breached SLA 
**In-Period Tracking**:- `MTD Sales`, `QTD Sales`, `YTD Sales` with `MOM%`, `QOQ%`, `YOY%` allow leadership to identify in-period shortfalls before close
**Executive Self-Service**:-Field parameter (`KPIS` table) drives dynamic KPI switching on the Executive Overview, removing the need for analyst involvement in routine leadership queries 
**Waterfall P&L View**:-`Waterfall Value` measure (driven by `Waterfall Categories` table: Gross Sales → Discounts → Net Sales → COGS → Profit) provides a visual P&L bridge that explains profit movement in a single chart
**Geographic Prioritisation**:- Country-level sales and profit analysis (`Dim_Territory`, `shapeMap` visual) identifies which markets to grow, defend, or review

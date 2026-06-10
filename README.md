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

**1.  P&L Management**:- Profit margin tracked at product, country, and promotion-channel level for the first time; `Profit Margin` and `PY Profit Margin` measures enable YoY margin benchmarking

**2.  Discount Governance** :-'Discount Percentage` (discounts as % of gross sales) and `PY Discount Percentage` expose whether discount rates are increasing year-over-year; `Discounts Color` signals deterioration automatically

**3.  Promotion ROI**:- Sales lift during active promotions (`Sales lifting during Active Promos` visual) quantified against baseline; `Promotion Discount` measure ties channel-level discount rates to actual revenue

**4.  Logistics SLA Compliance**:-'On-Time Delivery %` compared to `PY On-Time Delivery` surfaces carrier performance gaps; `Delayed Days` calculated column isolates orders that breached SLA 

**5.  In-Period Tracking**:- `MTD Sales`, `QTD Sales`, `YTD Sales` with `MOM%`, `QOQ%`, `YOY%` allow leadership to identify in-period shortfalls before close

**6.  Executive Self-Service**:-Field parameter (`KPIS` table) drives dynamic KPI switching on the Executive Overview, removing the need for analyst involvement in routine leadership queries 

## 5. Dashboard Impact & Outcomes

The following outcomes are directly enabled by this dashboard:

- ✅ **Profit margin visible at every level** :- product, country, promotion channel, and time period
- ✅ **P&L bridge available on demand**:- the Profit Bridge waterfall shows the exact contribution of discounts and COGS to the profit line
- ✅ **Promotion effectiveness quantified**:- sales lift during active campaigns measured and visualised per promotion name and type
- ✅ **Logistics SLA compliance tracked**:- on-time delivery % benchmarked against prior year, by ship mode and carrier
- ✅ **Year-over-year comparison across all KPIs**:- every metric shows PY actual and directional indicator (▲/▼) with colour coding
- ✅ **In-period alerting**:- MTD/QTD/YTD against prior period enables proactive course correction before period close
- ✅ **Executive self-service**:- field parameters and collapsible slicer panel allow leadership to answer their own questions
- ✅ **Full drill-through capability**:- from executive summary through to order-level detail via Product Detailed and Country Detailed pages
- ✅ **Operational efficiency benchmarking**:- ship mode and carrier performance compared side by side


**Waterfall P&L View**:-`Waterfall Value` measure (driven by `Waterfall Categories` table: Gross Sales → Discounts → Net Sales → COGS → Profit) provides a visual P&L bridge that explains profit movement in a single chart

**Geographic Prioritisation**:- Country-level sales and profit analysis (`Dim_Territory`, `shapeMap` visual) identifies which markets to grow, defend, or review

## 6. Target Audience & Stakeholders

### Executive Leadership:- C-Suite & Commercial Directors
**Pages served:** Executive Overview, KPIs

Headline KPIs (Total Sales, Total Gross Sales, Total Profit, Total COGS, Total Discounts) with PY comparators and trend direction indicators. Field parameter slicer enables dynamic switching between metrics without analyst support. Designed for weekly or monthly business reviews.

### Commercial & Sales Management
**Pages served:** Product Deep-Dive, Trend & Growth Analytics, Country Detailed

Product-level profitability ranking, Profit Bridge waterfall analysis, country-wise sales and profit combo charts, and quarterly discount impact trending. Supports product portfolio decisions, market prioritisation, and promotional planning.

### Marketing & Promotions Teams
**Pages served:** Delivery & Promos, Executive Overview (Promotion Channel donut)

Discount percentage by promotion type, sales lift during active promotions, and promotion channel share of revenue. Enables data-driven decisions on which promotion types and channels to scale or retire.

### Supply Chain & Operations
**Pages served:** Delivery & Promos, Operational Efficiency

On-time delivery % by ship mode, average delivery days vs. SLA (`EstimatedDeliveryDays`), delayed days by carrier, and ship mode operational efficiency comparison. Supports carrier negotiation, route optimisation, and SLA review.

### BI & Data Analysts
**Pages served:** All pages + semantic model

Clean, documented star schema with centralised `CalMeasures` table, consistent naming conventions, and reusable time-intelligence patterns. The TMDL format enables version control and collaborative development.

## 7. Solution Architecture

## 7. Solution Architecture

```
Source Files (CSV)
         │
         ▼
Power Query (M) — ETL Layer
  ├── Fact_Sales.csv        → 18 columns, type enforcement, null replacement
  ├── Dim_Products.csv      → 2 columns, product catalogue
  ├── Dim_Promotions.csv    → 7 columns, promotion attributes + date range
  ├── DimShipMode.csv       → 4 columns, carrier + SLA days
  └── DimTerritory.csv      → 2 columns (after removing unused cols), country lookup
         │
         ▼
Star Schema Data Model
  ├── Fact_Sales            (central fact — transactions, financials, FK keys)
  ├── DimDate               (calculated calendar 2022–2025, time intelligence anchor)
  ├── Dim_Products          (product dimension)
  ├── Dim_Territory         (geographic dimension, Country data category)
  ├── Dim_Promotions        (promotion dimension with StartDate/EndDate)
  ├── Dim_Shipmode          (ship mode + EstimatedDeliveryDays SLA)
  ├── CalMeasures           (disconnected table — all 70+ DAX measures)
  ├── KPIS                  (field parameter — dynamic KPI switching)
  └── Waterfall Categories  (DATATABLE — ordered P&L bridge categories)
         │
         ▼
Calculated Columns (in Fact_Sales)
  ├── Delivery Dates = DATEDIFF(ShipDate, Delivered Date, DAY)
  └── Delayed Days   = MAX(0, Delivery Dates − EstimatedDeliveryDays)
         │
         ▼
DAX Measure Layer (CalMeasures)
  ├── Core KPIs         (Sales, Profit, COGS, Discounts, Gross Sales, Units Sold, Orders)
  ├── PY Comparators    (SAMEPERIODLASTYEAR for every core KPI)
  ├── Growth %          (DIVIDE-based YoY growth for every metric)
  ├── Time Intelligence (TOTALYTD, TOTALQTD, TOTALMTD, PREVIOUSMONTH, PREVIOUSQUARTER)
  ├── Operational       (On-Time Delivery %, Avg Delivery Days — USERELATIONSHIP pattern)
  ├── FORMAT measures   (string-formatted growth % with ▲/▼ directional indicator)
  ├── Color measures    (SWITCH TRUE() → Green/Red/Gray conditional formatting)
  └── Waterfall Value   (SWITCH on Waterfall Categories for P&L bridge)
         │
         ▼
Report Layer — 9 Pages
  Executive Overview → Product Deep-Dive → Delivery & Promos
  → Trend & Growth Analytics → Overview → KPIs
  → Product Detailed → Country Detailed → Operational Efficiency
```
### Relationships

| From Table | From Column | To Table | To Column | Active |
|---|---|---|---|---|
| Fact_Sales | OrderDate | DimDate | Date | ✅ Active |
| Fact_Sales | Delivered Date | DimDate | Date | ❌ Inactive (USERELATIONSHIP) |
| Fact_Sales | ShipDate | DimDate | Date | ❌ Inactive |
| Fact_Sales | ProductID | Dim_Products | ProductID | ✅ Active |
| Fact_Sales | TerritoryID | Dim_Territory | TerritoryID | ✅ Active |
| Fact_Sales | PromotionID | Dim_Promotions | PromotionID | ✅ Active |
| Fact_Sales | ShipModeID | Dim_Shipmode | ShipModeID | ✅ Active |

> **Note on inactive relationships:** `Avg Delivery Days` and `On-Time Delivery %` both use `USERELATIONSHIP(DimDate[Date], Fact_Sales[Delivered Date])` to activate the delivery date path at measure evaluation time, a correct and intentional role-playing date dimension pattern.

## 9. DAX Measures Reference

All measures reside in the `CalMeasures` table, organised into display folders.

### Sales

| Measure | DAX Pattern | Notes |
|---|---|---|
| `Total Sales` | `SUM(Fact_Sales[  Sales ])` | Net revenue after discounts |
| `PY Sales` | `CALCULATE([Total Sales], SAMEPERIODLASTYEAR(...))` | COALESCE to 0 on no-data periods |
| `PY Sales Growth%` | `DIVIDE([Total Sales]-[PY Sales],[PY Sales])` | |
| `PY FORMAT` | `FORMAT(...) & IF(... < 0, "▼", IF(... > 0, "▲", "▬"))` | String KPI label with direction |
| `PL Color` | `SWITCH(TRUE(), ... > 0, "#008000", ... < 0, "#FF0000", "#808080")` | Green/Red/Gray |
| `YTD Sales` | `TOTALYTD([Total Sales], DimDate[Date])` | |
| `QTD Sales` | `TOTALQTD([Total Sales], DimDate[Date])` | |
| `MTD Sales` | `TOTALMTD([Total Sales], DimDate[Date])` | |
| `PM Sales` | `CALCULATE([Total Sales], PREVIOUSMONTH(...))` | |
| `PQ Sales` | `CALCULATE([Total Sales], PREVIOUSQUARTER(...))` | |
| `YOY%` | `DIVIDE([Total Sales]-[PY Sales],[PY Sales],0)` | |
| `MOM%` | `DIVIDE([Total Sales]-[PM Sales],[PM Sales],0)` | |
| `QOQ%` | `DIVIDE([Total Sales]-[PQ Sales],[PQ Sales],0)` | |
| `Running Totals` | `CALCULATE([Total Sales], FILTER(ALLSELECTED(...), Date<=MAX(Date)))` | Cumulative to selected date |
| `Avg Sales Price` | `AVERAGE(Fact_Sales[  Sales ])` | |

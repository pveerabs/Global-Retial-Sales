# Global-Retial-Sales
# Power BI Link : https://app.powerbi.com/reportEmbed?reportId=8d295fb6-5e72-4cae-9339-8967af124f33&autoAuth=true&ctid=f1f14c92-fde3-489f-8eeb-514d2f167be6

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


### Profit

| Measure | DAX Pattern | Notes |
|---|---|---|
| `Total Profit` | `SUM(Fact_Sales[  Profit  ])` | |
| `PY Profit` | `CALCULATE([Total Profit], SAMEPERIODLASTYEAR(...))` | |
| `PY Profit Growth%` | `DIVIDE([Total Profit]-[PY Profit],[PY Profit])` | |
| `Profit Margin` | `DIVIDE([Total Profit],[Total Sales],0)` | |
| `PY Profit Margin` | `CALCULATE([Profit Margin], SAMEPERIODLASTYEAR(...))` | |
| `PY Profit Margin Growth` | `DIVIDE([Profit Margin]-[PY Profit Margin],[PY Profit Margin])` | |

### Gross Sales, COGS, Discounts

Each metric follows the same pattern: `Total [Metric]` → `PY [Metric]` → `PY [Metric] Growth%` → `[Metric] FORMAT` → `[Metric] Color`

> **Important colour convention:** `Discounts Color` is intentionally *inverted* — a decrease in discounts (negative growth%) colours green, an increase colours red. This correctly treats discount reduction as a positive business outcome.

### Operational Measures

| Measure | Logic | Notes |
|---|---|---|
| `On-Time Delivery %` | `COUNTROWS(FILTER(Fact_Sales, Delivery Dates <= RELATED(Dim_Shipmode[EstimatedDeliveryDays])))` / `COUNTROWS(Fact_Sales)` | Both wrapped in `USERELATIONSHIP(DimDate[Date], Fact_Sales[Delivered Date])` |
| `Avg Delivery Days` | `CALCULATE(AVERAGE(Fact_Sales[Delivery Dates]), USERELATIONSHIP(...))` | Uses inactive Delivered Date relationship |
| `PY On-Time Delivery` | `CALCULATE([On-Time Delivery %], SAMEPERIODLASTYEAR(...))` | |
| `PY Avg Delivery Days` | `CALCULATE([Avg Delivery Days], SAMEPERIODLASTYEAR(...))` | |
| `Total Orders` | `DISTINCTCOUNT(Fact_Sales[OrderID])` | |

### Waterfall P&L Bridge

```dax
Waterfall Value =
SWITCH(
    SELECTEDVALUE('Waterfall Categories'[Category]),
    "Gross Sales",  [Total Gross Sales],
    "Discounts",   -[Total Discounts],
    "Net Sales",    [Total Sales],
    "COGS",        -[Total COGS],
    "Profit",       [Total Profit]
)
```

This measure drives the Profit Bridge waterfall chart — a visual P&L decomposition showing the exact contribution of each component from Gross Sales down to Profit.
<img width="1153" height="722" alt="image" src="https://github.com/user-attachments/assets/67558413-f75b-4ea1-be44-ed5105a98f4d" />

## 10. Report Pages & Visuals

### Page 1 - Executive Overview
Single-page leadership summary. KPI cards for Sales, Profit, COGS, Discounts, Gross Sales with PY comparators. Monthly Sales Trend (line chart), Product KPI Analysis (clustered column), Top 5 Products by Profit Margin (table), Sales by Promotion Channel (donut). Field parameter slicer for dynamic metric switching. Slicers: Year, Country, Product. Navigation bookmarks to all main pages.

<img width="1321" height="865" alt="image" src="https://github.com/user-attachments/assets/129e38cd-c7bc-4738-8035-3503e667c0e4" />

### Page 2 - Product Deep-Dive
Product-level revenue and profitability. Gross Sales by Product (column chart), Profit Bridge Analysis (waterfall using `Waterfall Value` measure), product bar charts, donut breakdown. Slicers: Year, Country, Promotion Channel, Ship Mode.

<img width="1222" height="828" alt="image" src="https://github.com/user-attachments/assets/fc331ca9-de5a-4a74-b119-53700ee49054" />


### Page 3 - Delivery & Promos
Operational and promotional performance. Operational Efficiency (clustered bar), Ship Mode Operational Efficiency (column chart), Discount % by Promotion Type (column), Sales Lifting During Active Promos (bar chart). Slicers: Promotion Name, Year, Ship Mode.

<img width="1332" height="840" alt="image" src="https://github.com/user-attachments/assets/2a68f514-e81c-4667-9000-f5cd30c8e0fa" />


### Page 4 - Trend & Growth Analytics
Multi-year trend and seasonality analysis. Annual Business Performance (combo — Sales + Profit), Country-wise Sales & Profit Analysis (combo), Discount Impact on Quarterly Profit (combo), Profit by Year (line). Slicers: Year, Product, Quarter.

<img width="1341" height="835" alt="image" src="https://github.com/user-attachments/assets/305f832a-e7ce-4e10-9cff-dead473f5c84" />


### Page 5 - Overview
Full interactive single-page view with collapsible slicer panel (bookmark-controlled). Geographic shape map, all core visuals, full slicer set including Shipping Carrier. Designed for ad-hoc exploration.

<img width="1227" height="832" alt="image" src="https://github.com/user-attachments/assets/286a905d-1f91-4c18-b878-5a7433785287" />


### Page 6 - KPIs
Granular KPI scorecard with 15 KPI cards covering all core and operational metrics. Every metric shows current value, PY comparator, growth %, and colour-coded directional indicator. Slicers: Year, Country, Quarter. Three domain grouping sections (Sales / Operational / Efficiency).

<img width="1330" height="842" alt="image" src="https://github.com/user-attachments/assets/69f836cb-09df-4ca2-9e96-5cc25171a9cb" />


### Page 7 - Product Detailed
Matrix drill-through: products as rows, full measure set as columns (Sales, Gross Sales, Profit, COGS, Discounts, Units Sold, Profit Margin). Supports portfolio-level analysis.

<img width="827" height="343" alt="image" src="https://github.com/user-attachments/assets/f870541e-0b51-453e-8fe0-a14c0c4b8e8e" />


### Page 8 - Country Detailed
Four pivot matrices covering sales performance, order volumes, profit analysis, and promotion activity by country — enabling geographic deep-dives directly from summary pages.

<img width="866" height="392" alt="image" src="https://github.com/user-attachments/assets/5680855f-96a0-4cf8-bb02-eebfc37539ba" />


### Page 9 - Operational Efficiency
Transaction-level delivery table and shipmode/carrier pivot with efficiency metrics. Entry point for logistics investigations.

<img width="1097" height="236" alt="image" src="https://github.com/user-attachments/assets/612d2e26-f098-4e76-9409-c93af6f3742c" />

---

## 11. Steps to Improve Business Performance
The analytical framework built into this dashboard points to six concrete action areas:

**1. Reduce Discount Leakage**
The `Discount Percentage` and `PY Discount Percentage` measures, combined with the Discount Impact on Quarterly Profit visual, directly surface periods and promotion types where discounting is compressing margin without driving proportional volume. Action: set category-level discount caps; retire promotion types with high `DiscountPercent` and low observable sales lift.

**2. Rationalise the Product Portfolio**
The Top 5 Products by Profit Margin table and Profit Bridge waterfall identify products that generate revenue but consume disproportionate cost or discount. Action: classify products into a Grow / Maintain / Review / Exit matrix using `Profit Margin` vs. `Total Sales` as the two axes.

**3. Optimise Carrier & Ship Mode Selection**
The `On-Time Delivery %`, `Avg Delivery Days`, and `Delayed Days` measures reveal which carriers and ship modes are consistently meeting their `EstimatedDeliveryDays` SLA. Action: route priority orders through high-performing modes; trigger SLA review or carrier switch for any mode where `PY Avg Delivery Growth %` is trending upward.

**4. Target Promotion Investment by Channel**
`Sales by Promotion Channel` and `Sales Lifting During Active Promos` show which channels drive genuine incremental revenue vs. which simply discount existing demand. Action: reallocate promotion budget toward channels with the highest lift-to-discount ratio; use `StartDate` and `EndDate` from `Dim_Promotions` to compare in-promotion vs. out-of-promotion periods.

**5. Focus Growth Effort on High-Margin Markets**
The Country-wise Sales & Profit combo chart combined with the `Country Detailed` drill-through page identifies markets where sales volume is strong but profit margin is below average. Action: initiate a pricing or cost-structure review in any market where `Profit Margin` is more than 5 percentage points below the portfolio average.

**6. Shift from Reactive to Proactive Tracking**
The `MTD Sales`, `QTD Sales`, and `YTD Sales` measures with their `MOM%`, `QOQ%`, and `YOY%` growth variants enable week-by-week tracking within the current period. Action: implement a standing weekly review cadence using the KPIs page as the entry point — teams should not wait for month-end close to identify shortfalls.

## 12. Recommendations & Suggestions

### What This Model Does Well

**Centralised measure table (`CalMeasures`)** - all 70+ measures in a single disconnected table is a production best-practice pattern that makes the model portable, testable, and maintainable. Every measure is reusable across all report pages without duplication.

**Consistent FORMAT + Color measure pattern** - pairing every KPI with a `FORMAT` (string with ▲/▼) and `Color` (SWITCH-based hex) measure cleanly separates data logic from presentation logic. This makes the model easy to extend — adding a new KPI requires adding three measures (value, FORMAT, Color) rather than hard-coding formatting in the visual layer.

**USERELATIONSHIP for multi-date-role fact table** - using inactive relationships for `Delivered Date` and `ShipDate` with `USERELATIONSHIP()` in the delivery measures is the correct pattern for a role-playing date dimension. This avoids model duplication while enabling accurate delivery analytics.

**Waterfall Categories as a static DATATABLE** - using `DATATABLE()` to define the P&L bridge categories (Gross Sales → Discounts → Net Sales → COGS → Profit) is a clean, explicit approach that makes the waterfall chart order predictable and maintainable.

**Inverted colour logic for Discounts** - `Discounts Color` correctly treats discount reduction as green (positive). This is a detail that is often missed in less mature models and shows deliberate analytical thinking.

## 13. Technical Stack

| Component | Tool |
|---|---|
| Report & Visualisation | Power BI Desktop |
| Semantic Model Format | TMDL (Tabular Model Definition Language) — PBIR format |
| Data Modelling | Star Schema — 1 Fact table, 5 Dimension tables |
| Measure Language | DAX — Time Intelligence, USERELATIONSHIP, SWITCH, DIVIDE, COALESCE patterns |
| Data Transformation | Power Query (M) — folder connector, CSV import, type enforcement |
| Calendar Table | DAX `CALENDAR()` + `ADDCOLUMNS()` — 2022 to 2025 |
| Custom Visuals | Bing Maps (geographic shape map), PayPal KPI Donut Chart |
| Navigation | Bookmark actions, button-based page navigation, collapsible slicer panel |
| Dynamic Metrics | Field Parameters (`KPIS` table with `NAMEOF()` references) |
| P&L Bridge | `Waterfall Categories` DATATABLE + `Waterfall Value` SWITCH measure |
| Version Control | Git / GitHub (PBIR format enables line-level diff on model changes) |


## 14. Data Dictionary

### Fact_Sales

| Column | Type | Description |
|---|---|---|
| `OrderID` | String | Unique order identifier — used in `DISTINCTCOUNT` for `Total Orders` |
| `OrderDate` | Date | Order placement date — **active** relationship to `DimDate` |
| `ShipDate` | Date | Date order was shipped — inactive relationship to `DimDate` |
| `Delivered Date` | Date | Actual delivery date — inactive relationship to `DimDate`, activated via `USERELATIONSHIP` in delivery measures |
| `Country` | String | Destination country (denormalised — also in `Dim_Territory`) |
| `Products` | String | Product name (denormalised — FK via `ProductID`) |
| `Units Sold` | Number | Quantity of units per order line |
| `Manufacturing Price` | Integer | Unit manufacturing cost |
| `Sale Price` | Integer | Unit sale price before discounts |
| `Gross Sales` | Number | `Units Sold × Sale Price` — revenue before discounts |
| `Discounts` | Number | Total discount value applied to order line |
| `Sales` | Number | Net revenue (`Gross Sales − Discounts`) |
| `COGS` | Number | Cost of goods sold for the order line |
| `Profit` | Number | `Sales − COGS` |
| `TerritoryID` | Integer | FK to `Dim_Territory` |
| `PromotionID` | String | FK to `Dim_Promotions` |
| `ShipModeID` | Integer | FK to `Dim_Shipmode` |
| `ProductID` | String | FK to `Dim_Products` |
| `[Delivery Dates]` | Calc | `DATEDIFF(ShipDate, Delivered Date, DAY)` — actual days from ship to delivery |
| `[Delayed Days]` | Calc | `MAX(0, Delivery Dates − EstimatedDeliveryDays)` — days exceeding SLA (0 if on time) |

### DimDate

| Column | Description |
|---|---|
| `Date` | Primary key — daily grain, 2022-01-01 to 2025-12-31 |
| `Year` | Calendar year |
| `MonthNo` | Month number (1–12) — sort column for `MonthName` |
| `MonthName` | Abbreviated month name (Jan–Dec) |
| `Quarter` | Quarter label (Q1–Q4) |
| `YearMonth` | YYYY-MM format for sorting |
| `YearQuarter` | YYYY-Qn format for sorting |

### Dim_Promotions

| Column | Description |
|---|---|
| `PromotionID` | Primary key |
| `PromotionName` | Descriptive promotion name |
| `PromotionType` | Category of promotion (e.g. seasonal, clearance) |
| `DiscountPercent` | Headline discount rate offered (integer %) |
| `StartDate` | Promotion start date |
| `EndDate` | Promotion end date |
| `PromotionChannel` | Channel through which promotion was distributed |

### Dim_Shipmode

| Column | Description |
|---|---|
| `ShipModeID` | Primary key |
| `ShipMode` | Shipping mode name (e.g. Standard, Express) |
| `EstimatedDeliveryDays` | SLA — expected maximum delivery days for this mode |
| `ShippingCarrier` | Carrier name |




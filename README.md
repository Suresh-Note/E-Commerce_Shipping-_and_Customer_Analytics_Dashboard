# E-Commerce Shipping & Customer Analytics Dashboard

> An interactive Power BI dashboard delivering end-to-end visibility into shipping operations and customer shopping behaviour — turning raw transactional data into actionable business intelligence.


---

## Dashboard Preview


<img width="1202" height="679" alt="Shipping   Customer Analytics" src="https://github.com/user-attachments/assets/54961a15-adda-4d2f-be08-1367e23f7f42" />



---

## Overview

A unified Power BI solution covering two critical business domains:

- **Shipping Analytics** — delivery performance, carrier efficiency, shipping costs, fulfilment timelines
- **Customer Analytics** — purchase patterns, segments, preferred categories, seasonal trends

Built to help operations, marketing, and leadership teams make data-driven decisions faster.

---

## Key Insights Derived

> Replace the `[X]` placeholders with actual numbers from your dashboard.

1. **Carrier performance gap** — `[Carrier A]` leads with `[X]%` on-time delivery while `[Carrier B]` lags at `[Y]%`, representing a `[Z]%` performance gap that directly impacts customer satisfaction.

2. **Revenue concentration** — The top 3 product categories (`[Cat1]`, `[Cat2]`, `[Cat3]`) drive `[X]%` of total revenue, indicating high dependency on a narrow product mix.

3. **Regional delivery bottleneck** — `[Region name]` accounts for `[X]%` of delayed shipments despite being only `[Y]%` of order volume, signalling logistics issues in that zone.

4. **Seasonal demand spike** — Orders surge `[X]%` between `[Month]` and `[Month]`, with shipping costs rising `[Y]%` in the same window — a margin compression opportunity.

5. **Shipping mode economics** — Express shipping costs `[X]x` more than Standard but improves delivery time by only `[Y]` days on average, suggesting pricing review.

6. **Customer segment value** — The top `[X]%` of customers by spend generate `[Y]%` of revenue, a classic Pareto pattern worth targeting for retention campaigns.

> **Business Impact:** Addressing the top 3 delay drivers could recover an estimated `[₹X]` in avoidable operational cost per quarter.

---

## Key Features

| Feature | Description |
| --- | --- |
| Shipping Performance | On-time vs. delayed delivery breakdown by carrier and region |
| Cost Analysis | Average shipping cost per order, category, and destination |
| Order Fulfilment | Order-to-delivery cycle time trends |
| Customer Segmentation | Buyers grouped by frequency, spend, and preferred category |
| Shopping Trends | Monthly and seasonal demand patterns across product lines |
| Interactive Filters | Slice by date range, region, carrier, and product category |
| KPI Cards | At-a-glance metrics for total orders, revenue, delivery rate |

---

## Data Dictionary

| Column | Type | Description |
| --- | --- | --- |
| `Order_ID` | String | Unique identifier per order |
| `Order_Date` | Date | Date the order was placed |
| `Delivery_Date` | Date | Date the order was delivered |
| `Customer_ID` | String | Unique identifier per customer |
| `Product_Category` | String | Top-level product category |
| `Sub_Category` | String | Granular product sub-category |
| `Purchase_Amount` | Decimal | Order value in INR |
| `Shipping_Carrier` | String | Logistics partner (e.g., Blue Dart, Delhivery) |
| `Shipping_Mode` | String | Standard / Express / Same-Day |
| `Shipping_Cost` | Decimal | Cost incurred to ship the order |
| `Region` | String | Customer region/state |
| `Delivery_Status` | String | On-time / Delayed |

---

## Data Transformation (Power Query)

Key cleaning steps performed in Power Query:

1. **Removed duplicates** on `Order_ID`
2. **Standardised date formats** across `Order_Date` and `Delivery_Date`
3. **Created calculated column** `Delivery_Days = Delivery_Date - Order_Date`
4. **Derived** `Delivery_Status` flag (On-time if ≤ 5 days, else Delayed)
5. **Trimmed and cleaned** categorical fields (Region, Carrier, Category)
6. **Handled nulls** in `Shipping_Cost` by imputing category-level medians

---

## DAX Measures

# DAX Measures Documentation

This document lists the key DAX measures used in the E-Commerce Shipping & Customer Analytics dashboard, grouped by business domain.

---

## 1. Core KPI Measures

### Total Orders
```DAX
Total Orders = DISTINCTCOUNT('shipping_data'[Order_ID])
```
**Purpose:** Counts unique orders across the current filter context.

---

### Total Revenue
```DAX
Total Revenue = SUM('shipping_data'[Purchase_Amount])
```
**Purpose:** Sum of all purchase amounts — primary revenue KPI.

---

### Total Shipping Cost
```DAX
Total Shipping Cost = SUM('shipping_data'[Shipping_Cost])
```
**Purpose:** Total logistics spend.

---

### Average Order Value (AOV)
```DAX
AOV = DIVIDE([Total Revenue], [Total Orders], 0)
```
**Purpose:** Average value per order — key retail KPI.

---

## 2. Shipping Performance Measures

### On-Time Delivery Rate
```DAX
On-Time Delivery % = 
DIVIDE(
    CALCULATE([Total Orders], 'shipping_data'[Delivery_Status] = "On-time"),
    [Total Orders],
    0
)
```
**Purpose:** Percentage of orders delivered on time — core operational KPI.

---

### Delayed Orders Count
```DAX
Delayed Orders = 
CALCULATE([Total Orders], 'shipping_data'[Delivery_Status] = "Delayed")
```
**Purpose:** Count of delayed orders for drill-down analysis.

---

### Average Delivery Days
```DAX
Avg Delivery Days = 
AVERAGEX(
    'shipping_data',
    DATEDIFF('shipping_data'[Order_Date], 'shipping_data'[Delivery_Date], DAY)
)
```
**Purpose:** Mean fulfilment time across orders.

---

### Avg Shipping Cost per Order
```DAX
Avg Shipping Cost = DIVIDE([Total Shipping Cost], [Total Orders], 0)
```
**Purpose:** Unit economics of logistics spend.

---

## 3. Time Intelligence Measures

### Revenue YoY
```DAX
Revenue YoY = 
CALCULATE(
    [Total Revenue],
    SAMEPERIODLASTYEAR('Calendar'[Date])
)
```
**Purpose:** Same-period prior-year revenue for YoY comparison.

---

### Revenue YoY %
```DAX
Revenue YoY % = 
DIVIDE(
    [Total Revenue] - [Revenue YoY],
    [Revenue YoY],
    0
)
```
**Purpose:** Year-over-year growth percentage.

---

### Revenue MTD
```DAX
Revenue MTD = 
CALCULATE([Total Revenue], DATESMTD('Calendar'[Date]))
```
**Purpose:** Month-to-date revenue.

---

## 4. Customer Analytics Measures

### Total Customers
```DAX
Total Customers = DISTINCTCOUNT('shipping_data'[Customer_ID])
```

---

### Repeat Customer Rate
```DAX
Repeat Customer % = 
VAR RepeatCustomers = 
    CALCULATE(
        [Total Customers],
        FILTER(
            VALUES('shipping_data'[Customer_ID]),
            CALCULATE([Total Orders]) > 1
        )
    )
RETURN DIVIDE(RepeatCustomers, [Total Customers], 0)
```
**Purpose:** Measures customer loyalty — share of customers with more than one order.

---

### Customer Lifetime Value (CLV)
```DAX
CLV = DIVIDE([Total Revenue], [Total Customers], 0)
```
**Purpose:** Average revenue per customer.

---

## 5. Calculated Columns

### Delivery Days (Column)
```DAX
Delivery Days = 
DATEDIFF('shipping_data'[Order_Date], 'shipping_data'[Delivery_Date], DAY)
```

---

### Delivery Status Flag (Column)
```DAX
Delivery Status = 
IF('shipping_data'[Delivery Days] <= 5, "On-time", "Delayed")
```

---

### Order Month-Year (Column)
```DAX
Order Month-Year = FORMAT('shipping_data'[Order_Date], "MMM YYYY")
```

---

## Notes

- All measures assume a dedicated `Calendar` table is connected to `shipping_data[Order_Date]`.
- `DIVIDE()` is used over `/` to safely handle zero denominators.
- Time intelligence measures require a marked date table.
---

## Files in This Repository

| File | Description |
| --- | --- |
| `Shopping_Trends.pbix` | Power BI Desktop report |
| `shipping_data.xlsx` | Source dataset |
| `DAX_MEASURES.md` | Documentation of key DAX measures |
| `assets/` | Dashboard screenshots by page |
| `LICENSE` | MIT License |

---

## Tools & Technologies

| Tool | Purpose |
| --- | --- |
| **Power BI Desktop** | Dashboard design, data modelling, DAX measures |
| **Microsoft Excel** | Raw data storage and pre-processing |
| **DAX** | Custom KPIs, calculated columns, time-intelligence |
| **Power Query (M)** | Data cleaning, transformation, shaping |

---

## How to Use

1. **Clone** this repository.
2. Open **`Shopping_Trends.pbix`** in [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
3. Update the data source path to point to **`shipping_data.xlsx`** on your local machine.
4. Click **Refresh** to load the data.
5. Use slicers and filters to explore insights interactively.

---

## Author

**Suresh Kanchamreddy** — Aspiring Data Analyst

[![GitHub](https://img.shields.io/badge/GitHub-Suresh--Note-181717?logo=github)](https://github.com/Suresh-Note)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?logo=linkedin)](https://linkedin.com/in/suresh-kanchamreddy)

---

## License

Distributed under the MIT License. See [`LICENSE`](./LICENSE) for more information.

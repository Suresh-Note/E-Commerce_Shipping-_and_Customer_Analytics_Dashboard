# E-Commerce Shipping & Customer Analytics Dashboard

> An interactive Power BI dashboard that delivers end-to-end visibility into shipping operations and customer shopping behaviour — turning raw transactional data into actionable business intelligence.

---

## Dashboard Preview

![E-Commerce Shipping & Customer Analytics Dashboard](Shipping%20%26%20Customer%20Analytics.png)

---

## Overview

This dashboard is built on a real-world e-commerce dataset and provides a unified view of two critical business domains:

- **Shipping Analytics** — track delivery performance, carrier efficiency, shipping costs, and order fulfilment timelines.
- **Customer Analytics** — understand purchase patterns, customer segments, preferred product categories, and seasonal shopping trends.

Together these insights help operations, marketing, and leadership teams make data-driven decisions faster.

---

## Key Features

| Feature | Description |
|---|---|
| Shipping Performance | On-time vs. delayed delivery breakdown by carrier and region |
| Cost Analysis | Average shipping cost per order, category, and destination |
| Order Fulfilment | Order-to-delivery cycle time trends |
| Customer Segmentation | Buyers grouped by frequency, spend, and preferred category |
| Shopping Trends | Monthly and seasonal demand patterns across product lines |
| Interactive Filters | Slice by date range, region, carrier, and product category |
| KPI Cards | At-a-glance metrics for total orders, revenue, delivery rate, and more |

---

## Files in This Repository

| File | Description |
|---|---|
| `Shopping Trends.pbix` | Power BI Desktop report file — open this to explore the full dashboard |
| `shipping data.xlsx` | Source dataset containing order, shipping, and customer records |
| `Shipping & Customer Analytics.png` | Static preview of the dashboard |

---

## Data Source

The analysis is powered by **`shipping data.xlsx`**, which contains the following key fields:

- Order ID, Order Date, Delivery Date
- Product Category, Sub-category, Purchase Amount
- Shipping Carrier, Shipping Mode, Shipping Cost
- Customer ID, Location (State / Region)
- Delivery Status (On-time / Delayed)

---

## Tools & Technologies

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Dashboard design, data modelling, DAX measures |
| **Microsoft Excel** | Raw data storage and pre-processing |
| **DAX** | Custom KPIs, calculated columns, and time-intelligence measures |
| **Power Query (M)** | Data cleaning, transformation, and shaping |

---

## How to Use

1. **Clone or download** this repository.
2. Open **`Shopping Trends.pbix`** in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free download).
3. If prompted, update the data source path to point to **`shipping data.xlsx`** on your local machine.
4. Click **Refresh** to load the latest data.
5. Use the slicers and filters on each page to explore the insights interactively.

---

## Insights You Can Derive

- Which shipping carrier has the highest on-time delivery rate?
- What product categories drive the most revenue?
- Which regions experience the most shipping delays?
- What are the peak shopping months and how does that affect fulfilment?
- How does shipping mode (Standard / Express / Same-Day) impact cost and delivery time?
- Who are the highest-value customer segments?

---

## Project Structure

```
E-Commerce Shipping & Customer Analytics Dashboard/
│
├── Shopping Trends.pbix          # Power BI report
├── shipping data.xlsx            # Source data
├── Shipping & Customer Analytics.png  # Dashboard screenshot
└── README.md                     # Project documentation
```

---

## Author

**Suresh** — Data Analyst  
[![GitHub](https://img.shields.io/badge/GitHub-Suresh--Note-181717?logo=github)](https://github.com/Suresh-Note)

---

## License

This project is open for learning and portfolio purposes. Feel free to fork, explore, and build on it.

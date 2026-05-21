# 📋 Project Summary

## Business Context

This project simulates a retail chain analytics scenario where a **data analyst** is tasked with building an executive-facing sales dashboard. The company operates **4 stores** across two US regions and needs visibility into revenue drivers, employee performance, and margin health.

The stakeholder questions driving this dashboard were:

- Where are we making (and losing) money?
- Are discounts eating into our margins or driving volume?
- Which employees and stores need attention?
- What categories should we invest more in?

---

## Approach

### 1. Data Understanding & Profiling
- Explored all 4 tables: `Sales`, `Location`, `PriceList`, `Employees`
- Identified key relationships (Sales is the central fact table)
- Noted data quirks: `Date Hired` stored as Excel serial numbers; `Shirt` has only 1 SKU (Item ID 55)

### 2. Data Modeling in Power BI
- Built a **star schema** with Sales at the center
- Created 3 relationships: Location, Employees, PriceList
- Used `Many-to-One` cardinality for all dimension links
- Avoided bidirectional filtering to prevent ambiguity

### 3. DAX Measure Development
- Calculated **post-discount revenue** using `SUMX` for row-level logic
- Built **profit margin** by joining to PriceList via `RELATED()`
- Created **rankings** with `RANKX` for category and employee views
- Designed measures to work correctly within **slicer context** (region, store, category)

### 4. Dashboard Design
- Built with a clean, executive-friendly layout
- Used **KPI cards** for top-line numbers (Revenue, Margin, Units Sold)
- **Bar charts** for category and employee comparisons
- **Matrix/table** for discount analysis
- Applied consistent color theme and minimal clutter

---

## Key Findings

### 💰 Revenue
- Revenue varies significantly by category — **Shoes** generate the highest revenue per transaction despite fewer sales
- **General Merchandise** has the widest variety of items but middling margins

### 📉 Discounts
- Discounts ranged from **10% to 20%** with no structured tiering
- No clear evidence that higher discounts resulted in higher quantity sold — suggesting blanket discounting rather than strategic pricing
- Discount Revenue Loss is a notable metric for the business to track

### 🏪 Regional Performance
- **West (San Jose, CA)** stores are Large-format and likely higher-volume
- **North (New Haven, CT)** stores are Average-sized — may serve a different customer profile

### 👥 Employee Insights
- Senior Managers (Mike, Sam, Kathy, Albert) appear in **both sales and procurement** roles — this dual-role structure is worth flagging for governance reviews
- Sales Persons account for the bulk of transaction count

---

## Limitations & Future Work

| Limitation | Suggested Improvement |
|---|---|
| No date column in Sales | Add a Date dimension to enable time-series analysis (YoY, MoM) |
| Small dataset (~200 rows) | Dashboard patterns will scale with larger real-world data |
| Shirt has 1 SKU only | Investigate whether this is a data gap or product reality |
| No customer data | Adding customer IDs would enable basket analysis and LTV |
| Location only has 2 stores | Expand location dimension as more stores onboard |

---

## Skills Applied

| Skill | Usage |
|---|---|
| Power Query | Loaded and shaped 4 Excel tables |
| Data Modeling | Star schema design, relationship setup |
| DAX | 15+ custom measures including SUMX, RELATED, RANKX, DIVIDE |
| Power BI Visuals | Cards, bar charts, matrix, slicers, drillthrough |
| Business Analysis | Translated business questions into dashboard requirements |

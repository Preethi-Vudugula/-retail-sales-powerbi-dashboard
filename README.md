# 🛍️ Retail Sales Performance Dashboard — Power BI

> An end-to-end Business Intelligence project analyzing multi-store retail sales across products, regions, and employees — built to surface actionable insights for sales managers and executives.

---

## 📌 Project Overview

This Power BI dashboard was designed to answer critical business questions for a retail chain operating across **West (San Jose, CA)** and **North (New Haven, CT)** regions. The analysis covers **4 stores**, **20 employees**, and **5 product categories** — tracking revenue, profitability, discount behavior, and employee performance.

| Dimension        | Detail                                              |
|------------------|-----------------------------------------------------|
| **Tool**         | Microsoft Power BI Desktop                          |
| **Data Source**  | Multi-table Excel workbook (4 related tables)       |
| **Records**      | ~200 sales transactions                             |
| **Categories**   | Shoes, Shirts, Sunglasses, Umbrellas, General Merch |
| **Stores**       | 4 stores across 2 regions (West & North)            |
| **Employees**    | 18 staff — Senior Managers, Managers, Salespeople   |

---

## 🎯 Business Questions Answered

1. Which **product categories** generate the most revenue and profit?
2. How do **discount rates** impact overall revenue?
3. Which **stores and regions** are top performers?
4. Which **employees** drive the most sales volume?
5. What is the **profit margin** per category after purchase cost?
6. How does **sales volume vs. price** vary across items?

---

## 📊 Dashboard Features

| Feature | Description |
|---|---|
| **Revenue by Category** | Bar/column chart comparing gross sales across 5 categories |
| **Regional Performance** | West vs. North comparison by revenue and volume |
| **Employee Leaderboard** | Sales by employee with position-level filtering |
| **Discount Impact Analysis** | Scatter/matrix showing discount % vs. revenue loss |
| **Store-Level KPIs** | Cards showing total sales, avg discount, units sold per store |
| **Profit Margin View** | Calculated margin using purchase price vs. sale price |

---

## 🗂️ Data Model

The report is built on a **star schema** with 4 tables:

```
Sales (Fact Table)
├── Sales ID, Store ID, Employee ID, Item ID, Location ID
├── Category, Quantity, Sale Price, Discount %
│
├──► Location (Dimension)
│       Location ID → Region, State, City, Store Type, Size
│
├──► Employees (Dimension)
│       Employee ID → Name, Position, Date Hired
│
└──► PriceList (Dimension)
        Item ID + Category → Purchase Price
```

**Relationships:**
- `Sales[Location ID]` → `Location[Location ID]` (Many-to-One)
- `Sales[Employee ID]` → `Employees[Employee ID]` (Many-to-One)
- `Sales[Item ID]` → `PriceList[Item ID]` (Many-to-One)

---

## 📐 Key DAX Measures

```dax
-- Total Revenue (after discount)
Total Revenue = 
SUMX(Sales, Sales[Quantity] * Sales[Sale Price] * (1 - Sales[Discount %]))

-- Gross Profit
Gross Profit = 
SUMX(
    Sales,
    (Sales[Sale Price] * (1 - Sales[Discount %]) - RELATED(PriceList[Purchase Price]))
    * Sales[Quantity]
)

-- Profit Margin %
Profit Margin % = 
DIVIDE([Gross Profit], [Total Revenue], 0)

-- Average Discount Rate
Avg Discount % = AVERAGE(Sales[Discount %])

-- Units Sold
Total Units Sold = SUM(Sales[Quantity])
```

> Full DAX code available in [`/dax-measures/`](./dax-measures/)

---

## 📁 Repository Structure

```
retail-powerbi-dashboard/
│
├── 📊 final_bi_preethi.pbix         # Power BI report file
├── 📋 FINAL_Power_BI.xlsx           # Source data (4 sheets)
│
├── 📁 dax-measures/
│   └── all_measures.dax             # All custom DAX measures
│
├── 📁 docs/
│   ├── data-dictionary.md           # Column-level field definitions
│   └── project-summary.md           # Business context & conclusions
│
├── 📁 screenshots/
│   └── [add dashboard screenshots here]
│
└── README.md
```

---

## 🔍 Key Insights

- **Umbrellas** had the highest transaction count but lower revenue per unit — suggesting a high-volume, low-margin category
- **Shoes** carried the highest average sale price, contributing disproportionately to revenue
- **Senior Managers** (Mike, Sam, Kathy, Albert) appear in both sales and procurement roles — a dual-role structure worth analyzing for conflict-of-interest risk
- The **West region (San Jose)** stores tend to be Large-format — likely correlating with higher sales volume
- **Discount rates range from 10–20%** with no clear tiered strategy — an opportunity for pricing optimization

---

## 🛠️ Tools & Skills Demonstrated

`Power BI Desktop` · `DAX` · `Power Query (ETL)` · `Star Schema Modeling` · `Data Relationships` · `KPI Design` · `Excel Data Preparation`

---

## 🚀 How to Open

1. Download [`final_bi_preethi.pbix`](./final_bi_preethi.pbix)
2. Open with **Power BI Desktop** (free — [download here](https://powerbi.microsoft.com/desktop/))
3. If prompted for data source, point to `FINAL_Power_BI.xlsx` in the same folder
4. Explore the report pages and interact with slicers

---

## 👩‍💻 Author

**Preethi**  
Aspiring Data Analyst | Power BI · SQL · Excel  
📧 [your email] · 🔗 [LinkedIn URL] · 🌐 [Portfolio URL]

---

*⭐ If you found this project helpful, give it a star!*

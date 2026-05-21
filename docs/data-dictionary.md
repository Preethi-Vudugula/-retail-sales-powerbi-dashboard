# 📖 Data Dictionary

> This document defines all fields across the 4 tables in `FINAL_Power_BI.xlsx`.

---

## Table 1: Sales (Fact Table)

Primary table containing all transaction-level sales records.

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Sales ID` | Text | Unique transaction identifier | `1A399555` |
| `Store ID` | Integer | ID of the store where sale occurred (1–4) | `1` |
| `Employee ID` | Integer | ID of the employee who made the sale | `5` |
| `Category` | Text | Product category | `Shoes`, `Shirt`, `Sunglasses`, `Umbrella`, `General Merchandise` |
| `Item ID` | Integer | Unique product/SKU identifier | `36` |
| `Quantity` | Integer | Number of units sold in this transaction | `3` |
| `Sale Price` | Currency | Listed unit price before discount (USD) | `49.00` |
| `Discount %` | Decimal | Discount applied as a decimal (e.g., 0.10 = 10%) | `0.10` |
| `Location ID` | Integer | Links to Location table (1 = West, 2 = North) | `1` |
| `Region` | Text | Region label (redundant with Location, useful for quick filters) | `West` |

---

## Table 2: Location (Dimension)

Describes the physical store locations.

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Location ID` | Integer | Primary key — links to Sales[Location ID] | `1` |
| `Region` | Text | Geographic region | `West`, `North` |
| `State` | Text | US state abbreviation | `CA`, `CT` |
| `City` | Text | City name | `San Jose`, `New Haven` |
| `Type` | Text | Store format type | `Store` |
| `Size` | Text | Store size classification | `Large`, `Average` |

**Known Locations:**
| Location ID | City | State | Region | Size |
|---|---|---|---|---|
| 1 | San Jose | CA | West | Large |
| 2 | New Haven | CT | North | Average |

---

## Table 3: PriceList (Dimension)

Contains the purchase (cost) price for each item, used to calculate profit margin.

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Category` | Text | Product category — matches Sales[Category] | `Shoes` |
| `Item ID` | Integer | Primary key — links to Sales[Item ID] | `2` |
| `Purchase Price` | Currency | Wholesale/cost price per unit (USD) | `8.82` |
| `Employee ID` | Integer | ID of employee associated with procurement | `14` |

> **Note:** `Employee ID` in PriceList refers to the buyer/procurement employee, not the salesperson.

---

## Table 4: Employees (Dimension)

Employee roster with role and tenure information.

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Employee First Name` | Text | First name of employee | `Mike` |
| `Employee ID` | Integer | Primary key — links to Sales[Employee ID] | `5` |
| `Employee ID (Old)` | Integer | Legacy ID from previous system | `4` |
| `Date Hired` | Date (serial) | Date of hire stored as Excel serial number | `39248` |
| `Position` | Text | Job title/role | `Senior Manager`, `Manager`, `Sales Person` |

**Position Hierarchy:**
| Position | Count | Employees |
|---|---|---|
| Senior Manager | 4 | Mike, Sam, Kathy, Albert |
| Manager | 2 | Queen, Jason |
| Sales Person | 12 | Miranda, Jan, Sofia, Arthur, Daniel, Ann, Kevin, Fernando, Luis, Toby, Ernst, Alvarez |

---

## 🔗 Relationships Summary

| From Table | From Column | To Table | To Column | Cardinality |
|---|---|---|---|---|
| Sales | Location ID | Location | Location ID | Many-to-One |
| Sales | Employee ID | Employees | Employee ID | Many-to-One |
| Sales | Item ID | PriceList | Item ID | Many-to-One |

---

## 📦 Product Categories

| Category | Item IDs | Notes |
|---|---|---|
| General Merchandise | 30–39 | Broadest category by SKU count |
| Sunglasses | 20–29 | Mid-range price points |
| Umbrella | 10–19 | High transaction volume |
| Shirt | 55 | Single SKU — all shirts same item |
| Shoes | 1–9 | Highest average price |

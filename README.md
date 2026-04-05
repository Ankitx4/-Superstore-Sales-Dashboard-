# 📊 Superstore Sales Dashboard — Power BI Project

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Pages](https://img.shields.io/badge/Dashboard%20Pages-4-blue?style=for-the-badge)
![Dataset](https://img.shields.io/badge/Dataset-Superstore-orange?style=for-the-badge)

---

## 🎯 Project Overview

An end-to-end **Business Intelligence Dashboard** built in Microsoft Power BI using the classic Superstore dataset. This project covers the full BI workflow — from raw data modeling to an interactive 4-page executive dashboard — designed to help business leaders make faster, data-driven decisions.

> **"Turn 9,994 rows of raw sales data into clear, actionable executive insights."**

---

## 📁 Dataset

| Property | Detail |
|---|---|
| **Source** | Superstore Sales Dataset |
| **Rows** | 9,994 transactions |
| **Columns** | 21 fields |
| **Date Range** | 2014 – 2018 |
| **Region** | United States |
| **Categories** | Furniture, Technology, Office Supplies |

---

## 🏗️ Data Model — Star Schema

The raw data was transformed from a flat table into a proper **Star Schema** with 1 fact table and 4 dimension tables using Power Query (M language).

```
                    DimDate
                  (1,826 rows)
                 Order ↕ Ship
                      │
DimCustomer ──── Fact_Superstore ──── DimProduct
 (793 rows)       (9,994 rows)        (1,862 rows)
                      │
                  DimRegion
                 (631 rows)
```

### Tables Built

| Table | Rows | Key Columns |
|---|---|---|
| `Fact_Superstore` | 9,994 | Sales, Profit, Quantity, Discount + FK keys |
| `DimDate` | 1,826 | Date, Year, Quarter, Month, Month Name, Day, Day Name |
| `DimProduct` | 1,862 | Product ID, Product Name, Category, Sub-Category |
| `DimCustomer` | 793 | Customer ID, Customer Name, Segment |
| `DimRegion` | 631 | Postal Code, City, State, Region, Country |

### Relationships

| From | To | Column | Type |
|---|---|---|---|
| DimDate | Fact_Superstore | Date → Order_Date | Active (1:M) |
| DimDate | Fact_Superstore | Date → Ship_Date | Inactive (1:M) |
| DimProduct | Fact_Superstore | Product_ID | Active (1:M) |
| DimCustomer | Fact_Superstore | Customer_ID | Active (1:M) |
| DimRegion | Fact_Superstore | Postal_Code | Active (1:M) |

---

## 🧮 DAX Measures

All measures are stored in a dedicated `_Measures` table following best practices.

```dax
Total Sales = SUM(Fact_Superstore[Sales])

Total Profit = SUM(Fact_Superstore[Profit])

Total Orders = DISTINCTCOUNT(Fact_Superstore[Order_ID])

Total Quantity = SUM(Fact_Superstore[Quantity])

Profit Margin % = DIVIDE(SUM(Fact_Superstore[Profit]), SUM(Fact_Superstore[Sales]), 0)

Total Customers = DISTINCTCOUNT(Fact_Superstore[Customer_ID])

Avg Order Value = DIVIDE([Total Sales], [Total Orders], 0)

Avg Discount % = AVERAGE(Fact_Superstore[Discount])

Profit Status = IF([Total Profit] > 0, "✅ Profitable", "🚨 Losing Money")
```

---

## 📊 Dashboard Pages

### Page 1 — 📈 Sales Overview
> *"How is the business performing overall?"*

**Visuals:**
- 5 KPI Cards — Total Sales, Total Profit, Total Orders, Total Quantity, Profit Margin %
- Sales & Profit Trend Line by Month
- Sales by Category (Donut Chart)
- Top 5 Sub-Categories by Sales (Bar Chart)
- Sales vs Profit by Category (Clustered Bar)
- Year & Region Slicers

**Key Findings:**
- Total Revenue: **$2.30M**
- Total Profit: **$286.4K**
- Profit Margin: **12.47%**
- Best Month: **November** (seasonal peak)

---

### Page 2 — 🗺️ Regional Analysis
> *"Where are we winning and where are we losing?"*

**Visuals:**
- Sales by State (Map with bubble size)
- Sales by Region (Bar Chart)
- Top 10 States by Sales (Bar Chart)
- Top Cities by Sales (Bar Chart)
- Discount by Region (Bar Chart)
- Sales vs Profit by State (Scatter Plot)
- State Sales Treemap

**Key Findings:**
- **West region** leads in both Sales and Profit
- **California** is the #1 state at $0.29M
- **New York City** is the #1 city
- **Central region** gives the highest discounts ($558)

---

### Page 3 — 📦 Product Analysis
> *"Which products make us money and which ones don't?"*

**Visuals:**
- Top 5 Products by Sales (Bar Chart)
- Top 10 Most Profitable Products (Bar Chart)
- Profit Margin % by Category (Pie Chart)
- Discount vs Profit by Sub-Category (Scatter Plot)
- Bottom Performing Products (Bar Chart)

**Key Findings:**
- **Canon imageCLASS** is the #1 product by sales at $62K
- **Technology** drives 47.12% of profit margin
- **Furniture** earns only 6.74% of profit margin
- High discounts directly correlate with negative profit

---

### Page 4 — 👥 Customer Insights
> *"Who are our customers and how do they behave?"*

**Visuals:**
- Top 10 Customers by Sales (Bar Chart)
- Sales & Profit by Segment (Donut Chart)
- Profit by Segment (Bar Chart)
- Sales Trend by Segment Over Time (Line Chart)

**Key Findings:**
- **Sean Miller** is the #1 customer at $25K
- **Consumer segment** dominates at 44.95% of total sales
- **Consumer** is also most profitable at $134K
- **November** is peak month across all 3 segments

---

## 🔗 Dashboard Navigation Features

| Feature | Description |
|---|---|
| **Page Navigation Buttons** | Buttons on every page to jump between all 4 pages |
| **Synced Slicers** | Year & Region slicers sync across all pages automatically |
| **Drill Through** | Right-click any category/region to drill into detail page |
| **Custom Tooltips** | Hover over any data point for instant mini-dashboard popup |

---

## 💡 Key Business Insights

### 🚨 Problems Found
1. **Furniture is losing money** — $207K in sales but **negative profit in several states**. Heavy discounting is the cause.
2. **Texas & Pennsylvania** show high sales but dangerously low profit margins.
3. **Central region** gives the most discounts but is not the most profitable — discount strategy needs review.

### ✅ Opportunities Found
1. **Technology products** have the highest margin — increase investment and marketing here.
2. **November sales spike** across all segments — prepare inventory and campaigns ahead of time.
3. **Consumer segment** is the largest and most profitable — loyalty programs could maximize lifetime value.
4. **California & New York** are star markets — expand product range in these states.

---

## 🛠️ Tools & Skills Used

| Tool/Skill | Usage |
|---|---|
| **Power BI Desktop** | Dashboard development |
| **Power Query (M)** | Data cleaning & transformation |
| **DAX** | Calculated measures & KPIs |
| **Star Schema Design** | Data modeling |
| **Data Visualization** | 15+ visual types used |
| **UX Design** | Navigation, tooltips, drill-through |

---

## 📚 What I Learned

- Designing a **Star Schema** from a flat file dataset
- Writing **M code** in Power Query to generate a full date table from scratch
- Creating **DAX measures** using DIVIDE, DISTINCTCOUNT, CALCULATE
- Building **role-playing dimensions** (DimDate used for both Order Date and Ship Date)
- Designing **4-page interactive dashboards** with professional navigation
- Using **drill-through, tooltips, and synced slicers** for enterprise-level UX

---

## 🚀 How to Use

1. Download the `.pbix` file
2. Open in **Power BI Desktop** (free download at powerbi.microsoft.com)
3. Use the **Year and Region slicers** to filter all pages simultaneously
4. **Right-click** any category or region to drill through to detail pages
5. **Hover** over data points to see tooltip mini-dashboards

---

## 📬 Connect With Me

If you found this project helpful, feel free to connect!



- 💼 LinkedIn: *[https://www.linkedin.com/in/ankit-pandit-0329451a3/https://www.linkedin.com/in/ankit-pandit-0329451a3/]*


---

*Built as part of a structured Power BI learning journey from beginner to advanced.*

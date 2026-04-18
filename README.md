## Global Superstore Sales Analytics – Power BI Dashboard

**Student Name:** Queen Esther Kibegi  
**Admission Number:** 668897  
**Course:** DSA 3050A – Business Intelligence & Data Visualization  
**Class:** DSA3050A 
**Examination:** End-Semester Practical Examination  
**Date:** 18/04/2026


## Project Overview

This project presents a comprehensive Power BI analytical solution for the **Global Superstore** dataset. The dashboard enables stakeholders to monitor sales performance, profitability, product category trends, regional differences, and customer purchasing behavior through an interactive three-page interface.


## Problem Statement

The management of a global retail chain lacks a centralized, interactive tool to:
- Track key performance indicators (KPIs) across regions and product categories
- Identify seasonal sales patterns and anomalies
- Compare current performance against previous year benchmarks
- Recognize top-performing and underperforming products
- Make data-driven decisions to optimize inventory, pricing, and marketing strategies

This Power BI solution addresses these needs by transforming raw transactional data into actionable business intelligence.


## Dataset Description

**Source:** Global Superstore Dataset (Kaggle)  
**Link:** https://www.kaggle.com/datasets/aksha17/superstore-sales

**Key Characteristics:**

| Feature | Value |
|---------|-------|
| Format | Excel (.xlsx) with multiple sheets |
| Main table rows | 51,290 transactions |
| Time period | 2011 – 2014 (4 years) |
| Columns | 24 (including sales, profit, quantity, discount, customer details, product categories, geographic data) |

**Tables Created in Star Schema:**
- **Orders (Fact Table):** Transactional data (Sales, Profit, Quantity, Discount, Order Date)
- **Products (Dimension):** Unique product attributes (Category, Sub-Category, Product Name)
- **Customers (Dimension):** Unique customer attributes (Customer Name, Segment)
- **Date (Dimension):** Continuous date table for time intelligence


## Tools Used

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Data transformation, modeling, DAX, dashboard design |
| Power Query Editor | Data cleaning, splitting columns, conditional columns, merging tables |
| DAX (Data Analysis Expressions) | Calculated columns and measures (Total Sales, YTD, PY Sales, etc.) |
| GitHub | Version control and project documentation |


## Steps Followed

### Part A: Data Acquisition & Understanding
- Downloaded Global Superstore dataset from Kaggle
- Loaded Excel file into Power BI (Orders, People, Returns sheets)
- Analyzed table structure, data types, and business relevance



### Part B: Power Query Transformations (13+ steps)
- Removed duplicate rows and null Order IDs
- Converted Order Date from Text to Date (UK locale)
- Extracted Year, Month Name, Quarter, Day of Week from Order Date
- Created Profit Margin column (Profit / Sales)
- Replaced null Postal Code values with "Unknown"
- Trimmed text columns (Customer Name, City, State, Country)
- Removed unnecessary columns (Row ID)
- Created conditional column: Profitability Segment (High/Low Profit/Loss)
- Split Customer Name into First Name and Last Name
- Merged Products dimension into Orders table on Product ID
- Created separate Date table using CALENDAR DAX function

  
<img width="495" height="555" alt="image" src="https://github.com/user-attachments/assets/871b369d-5447-43b0-9f74-b5c9337057c6" />


### Part C: Data Modeling (Star Schema)
- Identified Orders as Fact Table; Products, Customers, Date as Dimension Tables
- Created relationships: Products → Orders (Product ID), Customers → Orders (Customer ID), Date_Table → Orders (Order Date)
- Set cardinality: One-to-many (dimension to fact)
- Marked Date_Table as official date table for time intelligence
- Hid unnecessary foreign key columns for cleaner model

  <img width="1091" height="660" alt="image" src="https://github.com/user-attachments/assets/75b8a980-5870-4b51-a48c-cca3ea6972f9" />


### Part D: DAX Measures & Calculated Columns

**Calculated Columns:**

- `Discount Category` = SWITCH based on Discount field
- `Order Value Tier` = SWITCH based on Sales amount

**DAX Measures (8+ measures):**
- `Total Sales = SUM('Orders'[Sales])`
- `Total Profit = SUM('Orders'[Profit])`
- `Profit Margin % = DIVIDE([Total Profit], [Total Sales])`
- `Total Quantity = SUM('Orders'[Quantity])`
- `Distinct Customers = DISTINCTCOUNT('Orders'[Customer ID])`
- `Avg Order Value = DIVIDE([Total Sales], [Distinct Customers])`
- `YTD Sales = TOTALYTD([Total Sales], 'Date_Table'[Date])`
- `PY Sales = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date_Table'[Date]))`

### Part E: Dashboard Design (3 Interactive Pages)

**Page 1 – Executive Summary**
- KPI cards (Total Sales, Total Profit, Profit Margin, Distinct Customers)
- Line chart: Sales & Profit trends over time
- Column chart: Total Sales by Product Category
- Slicers: Year, Region

  <img width="1091" height="703" alt="image" src="https://github.com/user-attachments/assets/4a6a2584-7465-4565-8550-8dd60d5a8c09" />


**Page 2 – Detailed Analysis**
- Stacked bar chart with drill-down hierarchy (Category → Sub-Category)
- Matrix: Sales & Profit by Region and Year
- Decomposition tree: Sales breakdown by Category, Region, Segment
- Slicers: Year, Category

  <img width="1121" height="662" alt="image" src="https://github.com/user-attachments/assets/844cad36-49f0-48cf-9109-4c0985e7a280" />


**Page 3 – Insights & Performance Monitoring**
- Line chart: Year-over-Year Sales comparison
- Table visuals: Top 5 and Bottom 5 products by Sales
- Clustered column chart: Monthly Sales vs Previous Year
- Slicers: Year, Category for cross-filtering

<img width="1174" height="762" alt="image" src="https://github.com/user-attachments/assets/10fd57c5-2da7-43b0-97ec-fb7aadfd3235" />

### Part F: Analytical Insights & Recommendations

**Five Insights:**
1. Technology category drives highest revenue and profit
2. Sales peak in November with sharp decline in December
3. Central region has lowest profit margin despite moderate sales
4. Top 5 products contribute 25% of total sales
5. Discounts above 20% do not proportionally increase sales

**Three Recommendations:**
1. Increase inventory and marketing for Technology products, especially pre-November
2. Review discount and pricing strategy for Central region
3. Reduce or eliminate discounts above 20% for low-margin products


## Dashboard Features

| Feature | Description |
|---------|-------------|
| **KPI Cards** | Real-time key metrics at the top of Executive Summary page |
| **Trend Analysis** | Line charts showing sales and profit over time |
| **Category Comparison** | Column charts comparing sales across product categories |
| **Drill-Down** | Hierarchy from Category to Sub-Category on Page 2 |
| **Matrix Breakdown** | Sales and profit by region across multiple years |
| **Decomposition Tree** | Advanced interactive breakdown of sales drivers |
| **YoY Comparison** | Current year sales vs previous year sales |
| **Top/Bottom N** | Top 5 and Bottom 5 products by sales |
| **Slicers** | Year and region filters on every page |
| **Cross-Filtering** | Click any data point to filter related visuals |



## Key DAX Measures

| Measure Name | Formula | Business Purpose |
|--------------|---------|------------------|
| Total Sales | `SUM('Orders'[Sales])` | Core revenue metric |
| Total Profit | `SUM('Orders'[Profit])` | Core profitability metric |
| Profit Margin % | `DIVIDE([Total Profit], [Total Sales])` | Efficiency measure |
| Distinct Customers | `DISTINCTCOUNT('Orders'[Customer ID])` | Customer reach |
| Avg Order Value | `DIVIDE([Total Sales], [Distinct Customers])` | Customer spending behavior |
| YTD Sales | `TOTALYTD([Total Sales], 'Date_Table'[Date])` | Year-to-date performance |
| PY Sales | `CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date_Table'[Date]))` | Baseline for growth |


## Key Insights

1. **Technology drives growth:** Technology category contributes ~40% of total sales and ~45% of total profit.
2. **Seasonal peak:** November shows highest sales each year, followed by a December decline.
3. **Regional disparity:** Central region has profit margin 8-12% lower than East and West regions.
4. **Product concentration:** Top 5 products account for 25% of all revenue.
5. **Discount inefficiency:** Discounts >20% yield only 15% more sales but reduce profit margin by over 30%.



## Challenges Encountered & Solutions

| Challenge | Solution |
|-----------|----------|
| Order Date loaded as text with UK format (dd/mm/yyyy) causing errors | Used locale conversion (`English (United Kingdom)`) in Power Query |
| Missing Postal Code values | Replaced nulls with "Unknown" for geographic consistency |
| Single flat table initially – no star schema | Created separate dimension tables (Products, Customers, Date) by referencing and removing duplicates |
| DAX syntax errors when creating calculated columns | Created each column separately using **New column** (not all at once) |
| Dark theme made text invisible on KPI cards | Switched to light gray canvas (`#F2F4F6`) with white card backgrounds and dark text |





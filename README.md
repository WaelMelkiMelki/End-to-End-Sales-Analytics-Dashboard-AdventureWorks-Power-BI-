# End-to-End Sales Analytics Dashboard (AdventureWorks) 📊

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-00758F?style=for-the-badge&logo=google-analytics&logoColor=white)

## 📖 Project Overview

This project is a comprehensive Business Intelligence solution designed to analyze sales performance for **AdventureWorks**, a fictional global manufacturing company. 

The goal was to transform raw data stored in **SQL Server** into an interactive **Power BI** dashboard that enables stakeholders to track KPIs such as **Total Sales, Profit Margins, and Year-over-Year (YoY) Growth**.

The solution follows the full BI lifecycle: **ETL -> Data Modeling -> DAX Calculations -> Visualization**.

---

## 📸 Dashboard Preview

![Dashboard Screenshot]([images/dashboard-screenshot.png](https://github.com/WaelMelkiMelki/End-to-End-Sales-Analytics-Dashboard-AdventureWorks-Power-BI-/blob/main/screens1.png))

---

## 🛠️ Tech Stack & Tools

*   **Data Source:** SQL Server 2025 (AdventureWorksDW2020 database) & CSV files.
*   **ETL & Data Cleaning:** Power Query (M Language).
*   **Data Modeling:** Power BI Desktop (Star Schema).
*   **Calculations:** DAX (Data Analysis Expressions).
*   **Visualization:** Power BI Desktop.

---

## 🏗️ Architecture & Workflow

### 1. Data Extraction & Transformation (ETL)
*   Connected Power BI to a local **SQL Server** instance.
*   Imported dimension and fact tables (`DimProduct`, `DimEmployee`, `FactResellerSales`, etc.).
*   Integrated supplementary data from **CSV files** (`ResellerSalesTargets`, `ColorFormats`).
*   **Power Query Steps:**
    *   Data type validation and column renaming for clarity.
    *   **Merging queries** to enrich the `DimEmployee` table.
    *   **Expanding columns** to retrieve Product Categories and Subcategories.
    *   Handling null values and data quality issues (e.g., correcting "Ware House" typos).

### 2. Data Modeling (Star Schema)
Designed a robust **Star Schema** optimized for performance and analysis:
*   **Fact Tables:** `FactResellerSales`, `FactResellerSalesTargets`.
*   **Dimension Tables:** `DimProduct`, `DimReseller`, `DimEmployee`, `DimSalesTerritory`.
*   **Relationships:** Established **One-to-Many (1:*)** relationships between Dimensions and Facts.
*   **Hierarchies:** Created `Product Hierarchy` (Category > Subcategory > Product) and `Geography Hierarchy` (Group > Country > Region) to enable drill-down capabilities.

### 3. Advanced DAX Calculations
Implemented complex measures to derive business intelligence:

*   **Core KPIs:**
    ```dax
    Total Sales = SUM(FactResellerSales[SalesAmount])
    Profit = [Total Sales] - [Total Cost]
    Profit Margin % = DIVIDE([Profit], [Total Sales])
    ```

*   **Time Intelligence (Time-Series Analysis):**
    ```dax
    // Year-to-Date Calculation
    Sales YTD = TOTALYTD([Total Sales], 'FactResellerSales'[OrderDate])

    // Previous Year Comparison
    Sales PY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('FactResellerSales'[OrderDate]))

    // Year-over-Year Growth
    Sales YoY Growth = DIVIDE([Total Sales] - [Sales PY], [Sales PY])
    ```

### 4. Visualization & Reporting
Built an interactive report featuring:
*   **KPI Cards:** Displaying high-level metrics (Profit, Margin).
*   **Line Charts:** Visualizing sales trends and growth over time.
*   **Map Visuals:** Geospatial analysis of sales performance by country.
*   **Dynamic Slicers:** Filtering by Year and Product Color.
*   **Drill-Down:** Enabling deep dives into product categories and subcategories.

---

## 🚀 How to Run

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/WaelMelkiMelki/End-to-End-Sales-Analytics-Dashboard-AdventureWorks-Power-BI-.git
    ```
2.  **Open the Project:**
    *   Open the `.pbix` file using **Power BI Desktop**.
3.  **Data Source Note:**
    *   The data is imported into the model, so the report will work without a database connection.
    *   To refresh data, you would need the local SQL Server instance with `AdventureWorksDW2020` installed.

---

## 👤 Author

**Wael Melki**  
*Machine Learning & Information Theory Engineer*

*   [LinkedIn](https://www.linkedin.com/in/wael-melki-097b56202/)
*   [GitHub](https://github.com/WaelMelkiMelki)

---
*This project is part of the PL-300 Microsoft Power BI Data Analyst certification path.*

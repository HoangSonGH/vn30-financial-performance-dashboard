# FINANCIAL PERFORMANCE VISUALIZATION SYSTEM FOR VN30 COMPANIES (2020 - 2024)

## 1. Project Overview
This project was developed to **Digitize, Store, and Automatically Visualize** the Financial Statement data of 20 companies within the VN30 index over a 5-year period (2020 - 2024). The system addresses the challenge of processing raw, scattered financial data by consolidating it into a centralized database (MySQL) and transforming it into dynamic analytical metrics (Power BI DAX) to support rapid investment decision-making.

* **Research Target:** 3 major industry sectors within the VN30 basket, including: **Banking (Bank), Manufacturing/Retail (Corporate), and Securities (Securities)**.
* **Core Objectives:** Market Trend Tracking, Peer Comparison, and In-depth evaluation of individual stocks (Company Profile).

---

## 2. Tech Stack
* **Database Management System:** MySQL Server (Local Instance).
* **Data Visualization & Analytics:** Power BI Desktop (Power Query, DAX, Data Modeling).
* **UI/UX Theme:** User experience optimized based on a template sourced from Metricalist.

---

## 3. Data Modeling
The project strictly implements a **Star Schema** to optimize calculation performance and dashboard loading speeds in Power BI.

### Dimension Tables:
* `dim_companies`: Stores company identification details (Ticker, Company Name, Sector, Exchange, Logo URL).
* `dim_calendar`: Manages the time dimension, standardized by Quarter and Year (TimeKey, Year, Quarter, YearQuarter).
* `dim_items`: Standardizes the chart of accounts across the 3 sectors (Balance Sheet, Income Statement, and Cash Flow).

### Fact Tables:
* `fact_financials`: Stores all extracted raw financial figures (Current Quarter value and Previous Quarter value).
* `financial_ratios`: Stores advanced financial metrics calculated automatically via **Stored Procedures** directly at the Database layer to reduce workload on the visualization layer.

---

## 4. Key Analytics Metrics
The system utilizes advanced DAX formulas combined with MySQL logic to perform dynamic time-series calculations:
* **Profitability Metrics:** Gross Margin, Net Margin, Return on Assets (ROA), Return on Equity (ROE).
* **Growth Metrics (QoQ):** Revenue Growth Rate, Net Profit After Tax (NPAT) Growth QoQ, and Total Asset Growth QoQ.
* **Capital Structure:** Debt-to-Equity Ratio shifting dynamically by quarter.

---

## 5. Power BI Dashboard Structure (Demo)

The report is seamlessly structured into **3 main functional modules** (corresponding to the navigation tabs):

### Tab 1: Market Overview
* Comprehensive overview of the market scale: Total Revenue and Net Profit of the VN30 basket.
* **Financial Performance Trend** chart: A combo chart combining Revenue bars with the Market ROE trend line over time.
* **Net Profit Contribution by Sector** donut chart: Analyzes the profit contribution share among the Bank, Corporate, and Securities blocks.

### Tab 2: Peer Comparison
* Allows users to flexibly select any 2 tickers (e.g., `CTG` vs `FPT`) for side-by-side comparison.
* Visually compares trend lines for **ROE Trend**, **Net Profit Growth (QoQ)**, **Net Margin**, and leverage structure (**Capital Structure**) across the years.

### Tab 3: Company Profile
* Dives deep into the internal financial structure of a selected enterprise (e.g., `FPT`).
* Integrates an automatic KPI Status tracking indicator (e.g., *Status: Healthy Revenue*).
* **Detailed Financial Matrix**: Dynamically deconstructs cash flows and asset structures into a standardized financial reporting format.

---

## 6. Instructions for Reviewers

> **IMPORTANT NOTE:** For the Reviewer's utmost convenience, all data from the local MySQL server has been configured to **Import Mode** and compressed directly within the report file. **You only need to download this repository and double-click to open `PowerBI_demo.pbip` (or `PowerBI_demo.pbix`) to fully interact, apply filters, and view all active dashboards instantly** without installing or reconfiguring any database server connections.

If you wish to re-run the entire pipeline from scratch using the Database:
1. **Step 1:** Initialize the Database by opening MySQL Workbench, creating a schema named `vn30_data`, and importing the source file `database.sql` (located in the `database/` folder of this repository).
2. **Step 2:** Open the Power BI file, navigate to `Transform Data` -> `Data source settings` -> Edit the local connection path (Local Server) to match your own MySQL configuration, and click `Refresh` to update the data.
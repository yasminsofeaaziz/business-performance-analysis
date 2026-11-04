# Project: Enterprise Business Performance Dashboard 2026

An end-to-end Microsoft Excel analytical dashboard designed to consolidate multi-departmental operational data (sales, finance, payroll, attendance, and procurement) into a unified data model for executive decision-making.

## Business Overview & Problem Statement

> Problem Statement

Organizations often face data silos where operational, financial, and HR metrics live in separate monthly files across disparate departments. This decentralization makes cross-departmental analysis difficult, increases data manipulation overhead, and delays actionable insights regarding operational costs, overtime expenditures, and margin fluctuations.

> Objective

To build an automated, scalable Excel analytics pipeline and interactive dashboard that consolidates monthly departmental reports into a single Star Schema data model. This dashboard provides executive leadership with real-time visibility into high-level KPIs (Revenue, Gross Profit, Expenses, Payroll, Overtime) and detailed departmental breakdowns.

## Dataset Architecture

The project processes monthly transactional exports across five core operational domains alongside corporate master references:

`03_Sales_Monthly`: Monthly revenue transactions (`Sales_2026_01_Jan.xlsx`, `Sales_2026_02_Feb.xlsx`, `Sales_2026_03_Mar.xlsx`, etc.).

`04_Finance_Expenses_Monthly`: Monthly expense records across operational units.

`05_HR_Payroll_Monthly`: Monthly base payroll expenditures per department.

`06_HR_Attendance_Monthly`: Employee hours worked, overtime logs, and attendance trackings.

`07_Procurement_Monthly`: Purchase Orders (PO) spending and vendor activity logs.

`08_NEW UPDATE APRIL`: April dynamic data refreshes.

`Budget_and_Sales_Targets.xlsx`: Target benchmarks for financial expense and revenue evaluations.

`Corporate_Master_Data.xlsx`: Dimensional master reference tables for lookup structures (e.g., Department, Employee, Account Masters).

## Tools & Methodology

- **Microsoft Power Query (ETL Engine):** Dynamic folder-based ingestion, data cleaning, schema standardization, and automated data transformations.

- **Power Pivot (Data Modeling & DAX Engine):** Multi-table relationship building, dimensional modeling (Fact and Dimension tables), and custom analytical calculations using Data Analysis Expressions (DAX).

- **Pivot Tables & Pivot Charts:** Aggregation layers dynamically linked via interactive Slicers and Timelines.

- **Excel Dashboard UI:** Custom-designed, clean executive layout with synchronized visual elements and KPI scorecards.

## Process

**1. Power Query (Ingestion & ETL)**
- Dynamic Folder Ingestion: Ingested raw Excel files from monthly departmental subfolders into Power Query.
- Data Profiling: Enabled Column Profile, Column Value Distribution, and Column Quality in the Data View to evaluate missing values, cardinality, and data anomalies.
- Data Cleaning & Massaging: Standardized text fields using `TRIM` and `UPPERCASE` transformations; replaced `NULL` values with `"No Record"` across transactional keys to safeguard join operations.
- Schema Structuring: Categorized tables into dedicated Fact Tables (transactional data) and Dimension Tables (master lookup metadata).
- Data Model Loading: Set load destinations to "Only Create Connection" and enabled "Add this data to the Data Model" to ensure lean workbook sizing.

**2. Power Pivot (Data Modeling & DAX)**
- Star Schema Construction: Formed relationships linking Dimension tables (`Corporate_Master_Data`) to transactional Fact tables using key attributes (e.g., `Department ID`, `Date ID`).
- Cardinality Analysis: Enforced strict `1-to-Many (1:*)` relationships and controlled cross-filter direction.
- DAX Calculations: Written custom DAX measures for aggregated metrics, variance, and margins:
  - Total Revenue & Gross Profit
  - Gross Margin % = DIVIDE([Gross Profit], [Total Revenue], 0)
  - Total Expenses & Expense Budget Variance
  - Total Hours Worked, Total OT Hours Worked, and Total OT Amount Paid
  - Total Purchase Orders Spend

**3. Pivot Tables & Visualization Layer**
- Aggregation Summaries: Created dedicated Pivot Tables for cost allocations across Departments.
- Interactive Controls: Connected global cross-filtering Slicers (Department) and Timelines (Month/Date) across all Pivot Table caches.
- Visual Alignment: Configured synchronized visual components including combo charts for Budget vs. Actual comparisons, doughnut charts for margin breakdowns, and horizontal bar charts for payroll distribution.

## Dashboard Features

Key Metrics Summary (YTD 2026)
- Business Revenue: RM 1.89M
- Gross Profit: RM 694.9K
- Business Expenses: RM 534.7K
- Total Payroll Cost: RM 1.53M
- Total Overtime Worked: 1,006.5 Hours
- Total Overtime Amount Paid: RM 60.1K
<img width="1856" height="710" alt="Screenshot 2026-11-02 213617" src="https://github.com/user-attachments/assets/db907fac-5aa0-473b-a1a2-8632434e525c" />


## Key Insights

**1. Revenue Trajectory & Gross Margin Decline:**
  - Monthly revenue demonstrates a steady downward trend from January (~RM 500K) through April (~RM 435K).
  - Gross Margin percentage weakened significantly over the period, dropping from a peak of 37.52% in January down to 24.00% in April.

**2. Overtime Hours Concentration:**
  - Overtime hours (1,006.5 Hrs total) are heavily concentrated in four departments: Sales (260.9 hrs), IT (264 hrs), Procurement (247.2 hrs), and Operations (234.4 hrs).
  - Administration, Finance, Marketing, and HR logged 0 OT hours, signaling potential workforce capacity imbalances or reporting gaps.

**3. Departmental Expense vs. Budget Variance:**
  - IT and Operations exhibit higher operational expenses compared to other business units, but actual expenses remain within budget thresholds across departments.

## Recommendations

- **Investigate Cost of Goods Sold (COGS) & Pricing Strategy:** Conduct a root-cause analysis on the contraction in Gross Margin % from January (37.52%) to April (24.00%). Review supplier pricing, raw material inflation, or product mix shifts.

- **Optimize Workforce & Overtime Allocation:** Evaluate workload distributions in IT, Sales, Procurement, and Operations to determine whether excessive OT hours indicate staffing shortages or inefficient processes. Redistributing tasks or strategic hiring could reduce the RM 60.1K OT burden.

- **Revenue Drive:** Implement targeted sales enablement or marketing strategies to reverse the month-over-month decline in gross revenue observed in Q1 and early Q2.

## Project Limitations

- **Static Data Sources:** Raw data relies on local Excel file directory structures rather than automated database connections (e.g., SQL Server or API integrations).

- **Historical Timeline scope:** Analysis currently covers Q1 and early Q2 (Jan–Apr 2026); continuous quarterly updates are required for full annual trend forecasting.

- **Manual Overtime Zero-Values:** Zero OT records across certain departments (e.g., HR, Admin) could stem from uncaptured timecard entries rather than zero overtime activity.

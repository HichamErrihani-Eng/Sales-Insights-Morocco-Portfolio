# 📊 Sales Insights: Revenue Analysis & Decision Dashboard

## 📖 Project Context
This project simulates a Data Analyst mission for **Atlas Distribution**, a hardware and peripherals distributor operating across several branches in Morocco. The company was facing declining sales and struggled with strategic decision-making.

The Sales Director lacked a clear vision of actual regional performance. Data was scattered across complex Excel files, making it difficult for regional managers to interpret raw numbers, leading to frustration and delays in decision-making.

**Objective:** To provide an automated solution that uncovers sales insights, visualizes trends, and supports data-driven decision-making.

## 🎯 Methodology & Project Planning (AIMS Grid)
I used the **AIMS Grid** (a project management framework) to structure the project:
*   **Purpose:** Unlock hidden sales insights to support decision-making and automate manual data gathering.
*   **Stakeholders:** Sales Director, Marketing Team, Customer Service, Data & Analytics Team, IT.
*   **End Result:** An automated, interactive dashboard providing quick and up-to-date sales insights.
*   **Success Criteria:** Uncover sales order insights, enable better decision-making, prove 10% cost savings, and save 20% of business time by stopping manual data gathering.

## 🛠️ Tech Stack & Data Pipeline

### 1. Data Discovery & Analysis (MySQL)
*   Imported the raw database (`db_dump.sql`) into MySQL Workbench.
*   Analyzed tables to identify and filter out garbage/aberrant values.
*   Executed complex SQL queries (JOINs, aggregations) to extract key KPIs (Revenue, Profit Margin, Sales Quantity).

### 2. Data Cleaning and ETL (Extract, Transform, Load)
*   **Connection:** Established a bridge between MySQL database and Power BI Desktop.
*   **Loading:** Loaded all tables into Power BI Desktop for seamless integration.
*   **Transformation (Power Query):** Cleaned and reshaped the dataset by resolving inconsistencies, handling missing values, and normalizing currencies to MAD (Moroccan Dirham) to align with analytical objectives.

### 3. Data Modeling & Visualization (Power BI & DAX)
*   Designed an optimized data model.
*   Utilized **DAX** (Data Analysis Expressions) to create dynamic measures: Total Revenue, Profit Margin %, and Year-over-Year (YoY) growth.
*   Designed an interactive, ergonomic dashboard for decision-makers.

## 💡 Key Insights & Results

*   **Overall Revenue:** Generated a total revenue of **985M MAD** over 4 years, with a profit margin of 2.5%. In 2020, revenue was 142M MAD with a profit of 2.1M MAD.
*   **Regional Performance:**
    *   **Casablanca-Settat** is the largest market by revenue (520M MAD, 52.8% contribution) but has a low profit margin (2.3%).
    *   **Rabat-Salé-Kénitra** generates the highest profit margin (10.48%).
    *   **Marrakech-Safi** has the lowest profit margin (-20.8%), negatively contributing to overall profit.
*   **Top Customers:** The biggest client (Electricalsara Stores) generated 413M MAD in revenue over 4 years.
*   **Top Products:** "Prod318" is the highest-selling product, generating 69M MAD.
*   **Trends:** Revenue dropped drastically in June 2020 compared to the previous year, with the lowest profit margin recorded in April 2020.

## 📁 Repository Contents
*   `Dashboard-Snapshots/` : Screenshots of the final dashboard.
*   `Sales_Insights_Using_SQL.sql` : SQL scripts for cleaning and analysis queries.
*   `Sales_Insights_fullProject.pbix` : Power BI source file.
*   `db_dump.sql` : Raw database dump (adapted for portfolio purposes).

## 🔗 References & Resources
*   [Codebasics - Original Project Inspiration](https://codebasics.io/panel/webinars/purchases)
*   [SQLBI - Learn DAX](https://www.sqlbi.com/learn/introducing-dax-video-course/0/)
*   [MySQL Documentation](https://dev.mysql.com/doc/)

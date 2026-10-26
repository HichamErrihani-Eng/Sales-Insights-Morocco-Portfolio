# 📊 Sales Insights Morocco — Revenue & Profitability Decision Dashboard

![MySQL](https://img.shields.io/badge/MySQL-Database-4479A1?logo=mysql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Time%20Intelligence-0078D4)
![Power Query](https://img.shields.io/badge/Power%20Query-M%20%2F%20ETL-217346)
![Status](https://img.shields.io/badge/Status-Completed-success)

> **End-to-end BI project** — from a relational MySQL database to an interactive Power BI dashboard that tells a Sales Director **where revenue is made, where margin is lost, and what to do about it**.

![Dashboard overview](Dashboard-Snapshots/Key%20Insights.png)

---

## ⚡ Executive Summary

| | |
|---|---|
| **Business problem** | Declining sales, no reliable view of regional performance, reporting done manually in Excel |
| **Solution** | Automated Power BI dashboard connected to a MySQL database (star schema, DAX measures, 3 analytical pages) |
| **Scope** | ~148,000 transactions · 14 cities · 9 regions · 38 customers · 338 products · Oct 2021 – Jun 2024 · amounts in MAD |
| **Key finding** | Casablanca generates **53% of revenue at only 2.55% margin**, one customer weighs **42% of sales**, and two markets are **loss-making** |
| **Outcome** | 4 data-driven recommendations on pricing, key-account risk and margin monitoring |

---

## 📖 Business Context

**Atlas Distribution** is a (fictional) distributor of computer hardware and peripherals, selling through **brick-and-mortar stores** and **e-commerce partners** across Morocco.

Sales were declining and the Sales Director had **no clear view of actual regional performance**. Data was scattered across complex Excel files, regional managers struggled to interpret raw numbers, and decisions were delayed.

**Objective:** replace manual reporting with an automated, interactive solution that surfaces sales and profitability insights and supports data-driven decisions.

---

## 🎯 Project Framing — AIMS Grid

| Dimension | Definition |
|---|---|
| **Purpose** | Unlock hidden sales insights and stop manual data gathering |
| **Stakeholders** | Sales Director · Marketing · Customer Service · Data & Analytics · IT |
| **End Result** | An automated, interactive dashboard with up-to-date sales and margin insights |
| **Success Criteria (targets)** | Faster decisions on loss-making markets · reduced time spent on manual reporting · margin monitored against a target |

---

## 🛠️ Architecture & Data Pipeline

```
┌──────────────┐     ┌───────────────┐     ┌──────────────────┐     ┌──────────────┐     ┌────────────────────┐
│ MySQL (sales)│ ──► │ SQL profiling │ ──► │ Power Query (M)  │ ──► │ Star schema  │ ──► │ DAX + Power BI     │
│ 5 tables     │     │ & data quality│     │ ETL, typing      │     │ 1 fact, 4 dim│     │ 3-page dashboard   │
└──────────────┘     └───────────────┘     └──────────────────┘     └──────────────┘     └────────────────────┘
```

### 1. Data Discovery & Quality (MySQL)
- Restored the `sales` database in **MySQL Workbench**: `transactions` (fact), `customers`, `products`, `markets` (city + region), `date`.
- Profiled tables with SQL (**JOINs, aggregations, GROUP BY**) to validate revenue, margin and volume KPIs.
- **Data-quality issue found and fixed:** 59 product codes referenced in sales were missing from the product table (≈ 47% of revenue appeared as *"(Blank)"* in visuals). They were added as `Unclassified` so every sale is traceable.

### 2. ETL (Power Query / M)
- Direct connection **MySQL → Power BI** (`localhost`, schema `sales`).
- Fact table built in **M**: explicit column selection, renaming, strong typing (dates, decimals, integers).
- Rows without a valid region filtered out.

### 3. Data Model & DAX
- **Star schema**: `Sales transactions` fact table → `customers`, `products`, `markets`, `date` dimensions (one-to-many relationships).
- Dedicated measures table with key DAX measures:

| Measure | Purpose |
|---|---|
| `Revenue`, `Sales Qty`, `Total Profit Margin` | Core KPIs |
| `Profit Margin %` | Profitability per city / customer / product |
| `Revenue Contribution %`, `Profit Margin Contribution %` | Share of each market in revenue vs profit |
| `Revenue LY` | Year-over-year comparison with `CALCULATE` + `SAMEPERIODLASTYEAR` |

- **What-if parameter `Profit Target`** + conditional formatting to flag markets below the target margin.

### 4. Dashboard (3 pages)

| Key Insights | Profit Analysis | Performance Insights |
|---|---|---|
| ![](Dashboard-Snapshots/Key%20Insights.png) | ![](Dashboard-Snapshots/Profit%20Analysis.png) | ![](Dashboard-Snapshots/Performance%20Insights.png) |
| Revenue, volume, trend, top customers & products | Revenue vs profit contribution, margin by market vs target | Revenue vs last year, margin trend, customer profitability |

Year / month slicers, cross-filtering between visuals, currency formatted in MAD.

---

## 💡 Key Insights (Oct 2021 – Jun 2024)

- 💰 **98.5M MAD** total revenue with an overall profit margin of only **~2.6%**.
- 🏙️ **Casablanca** dominates: **52M MAD (≈ 53% of revenue)** but with a thin **2.55% margin** → volume without profitability.
- 📉 **Loss-making markets:** **Laâyoune (−20.8%)** and **Oujda (−0.5%)** erode overall profit.
- ✅ **Marrakech** is the most profitable large market (**3.9% margin** on 5.9M MAD).
- ⚠️ **Key-account risk:** one customer, **Atlas Electro Distribution**, generates **41.3M MAD (≈ 42% of revenue)**.
- 🏬 **Channel mix:** brick-and-mortar **74.5M MAD** vs e-commerce **24.0M MAD**.
- 📦 **Top product:** Prod318 (6.9M MAD).
- 📆 **Trend:** revenue peaked in **2022 (41.4M MAD)** and fell in **2023 (33.6M MAD)**; the lowest monthly margin was **April 2024 (0.5%)**.

---

## ✅ Recommendations

1. **Laâyoune & Oujda** — review pricing, discounts and logistics costs before investing further in volume.
2. **Casablanca** — protect margin: renegotiate supplier terms and push higher-margin products.
3. **Key-account dependency** — diversify revenue by developing mid-size accounts and e-commerce partners.
4. **Monitoring** — use the *Profit Target* parameter as a monthly alert for markets falling below target margin.

---

## 🧠 Skills Demonstrated

| Area | Skills |
|---|---|
| **SQL** | Data profiling, JOINs, aggregations, data-quality checks, referential integrity |
| **Data Engineering** | MySQL → Power BI pipeline, ETL in Power Query (M), reproducible setup |
| **Data Modeling** | Star schema, fact/dimension design, relationships, measures table |
| **DAX** | KPIs, contribution %, time intelligence (`SAMEPERIODLASTYEAR`), what-if parameter |
| **Data Visualization** | Dashboard UX for executives, conditional formatting, slicers, cross-filtering |
| **Business Analysis** | AIMS Grid, stakeholder framing, insight → recommendation storytelling |

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `db_dump_morocco.sql` | MySQL dump of the `sales` database |
| `Sales_Insights_Using_SQL.sql` | SQL exploration and analysis queries |
| `Sales_Insights_fullProject.pbix` | Power BI report connected to MySQL |
| `Dashboard-Snapshots/` | Dashboard screenshots |

## ▶️ How to Reproduce

1. Install **MySQL Server** (8.4+), **MySQL Workbench** and **MySQL Connector/NET** (required by Power BI).
2. In Workbench, open and run `db_dump_morocco.sql`.
3. Open `Sales_Insights_fullProject.pbix` in **Power BI Desktop**.
4. *Transform data → Data source settings → `localhost;sales` → Edit permissions*: enter your MySQL credentials (keep **Encrypt connections** checked), then **Refresh**.

---

## ℹ️ About the Data

Atlas Distribution is a fictional company and the dataset is **synthetic**, built for portfolio purposes. Dataset structure and project framing are inspired by the [Codebasics Sales Insights case study](https://codebasics.io/).

## 🔗 Resources

- [SQLBI — Introducing DAX](https://www.sqlbi.com/learn/introducing-dax-video-course/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Power BI Documentation](https://learn.microsoft.com/power-bi/)

---

## 👤 About Me

**Hicham Errihani** — *Senior Data Analyst / BI Expert*

~20 years of experience turning operational data into decisions, in **industrial manufacturing environments** (production KPI reporting and manufacturing analytics with SQL Server, T-SQL, Excel/VBA and Power BI) and in **institutional data & AI** work. Master's degree in **Computer Engineering & Big Data** (ENSA Berrechid).

🎯 Open to **Data / BI Architect** and **Data Engineer** opportunities.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Hicham%20Errihani-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/hicham-errihani-815755266)
[![Email](https://img.shields.io/badge/Email-errihanihicham1%40gmail.com-D14836?logo=gmail&logoColor=white)](mailto:errihanihicham1@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-HichamErrihani--Eng-181717?logo=github&logoColor=white)](https://github.com/HichamErrihani-Eng)

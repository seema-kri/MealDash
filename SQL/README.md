
# 🗄️ MealDash — SQL Analytics Queries

This directory contains the production T-SQL scripts executed against the Microsoft Fabric SQL Analytics Endpoint to answer all 10 business-critical delivery operations questions[cite: 2, 4].

---

## 📂 Folder Contents

| File Name | Format | Description |
|---|---|---|
| **`MyQueries.zip`** | ZIP Archive | Packaged `.sql` scripts containing the complete query suite for questions Q1 through Q10[cite: 2, 4]. |

---

## 🔍 Analytical Questions Solved in SQL

| # | Business Question | SQL Techniques Applied[cite: 2, 4] | Key Metric / Result[cite: 4] |
|---|---|---|---|
| **Q1** | Overall baseline delivery speed | `AVG()`, `MIN()`, `MAX()` aggregations[cite: 4] | **26 min avg** (10 to 54 min range)[cite: 4] |
| **Q2** | Slowest city by volume & latency | `GROUP BY`, sample size counts (`COUNT(*)`)[cite: 4] | **Metropolitan** slowest by volume (27 min, 34K+ orders)[cite: 4] |
| **Q3** | Traffic congestion impact | Conditional groupings, ordering[cite: 4] | **Jam adds +10 mins** vs. Low traffic[cite: 4] |
| **Q4** | Weather condition variance | Category aggregations[cite: 4] | **Fog & Cloudy** are slowest (28 min)[cite: 4] |
| **Q5** | Geospatial distance effect | Multi-tier `CASE WHEN` bucketing[cite: 4] | Steepest latency penalty occurs at **5 km boundary**[cite: 4] |
| **Q6** | Fleet & vehicle type comparison | Dimensional aggregations[cite: 4] | Minor variance (~3 min difference across types)[cite: 4] |
| **Q7** | Delivery agent rating impact | Rating tier binning (`CASE WHEN`)[cite: 4] | **4.5+ rated agents deliver 10–13 mins faster**[cite: 4] |
| **Q8** | Multiple orders / trip bundling | Multi-delivery groupings[cite: 4] | Non-linear acceleration (**22m → 47m** for stacked drops)[cite: 4] |
| **Q9** | Festive period delay impact | Boolean flag aggregations[cite: 4] | **Festival days are 75–80% slower** (45 min vs. 25 min)[cite: 4] |
| **Q10** | Longitudinal SLA drift | Window functions: `AVG() OVER (ROWS 6 PRECEDING)`[cite: 4] | **Flat 7-day rolling trend** (25–26 mins); delays are structural[cite: 4] |

---

## 🛠️ Execution Environment

* **Target Engine:** Microsoft Fabric SQL Analytics Endpoint / T-SQL (compatible with standard PostgreSQL / SQL Server engines)[cite: 2].
* **Detailed Technical Documentation:** For line-by-line query walkthroughs, methodology reasoning, and sample-size confidence ratings, refer to [`Docs/SQL_Report.pdf`](../Docs/SQL_Report.pdf)[cite: 2, 4].

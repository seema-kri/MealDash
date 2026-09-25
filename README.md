# 🍔 MealDash — Delivery Operations Analytics

**Diagnosing why delivery times vary across a 45,000+ order quick-commerce dataset using Excel, SQL, Microsoft Fabric, and Power BI — turning the findings into three specific, actionable recommendations.**

---

## Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Dataset Description](#dataset-description)
- [Tools & Technologies](#tools--technologies)
- [Project Structure](#project-structure)
- [Data Cleaning & Preparation](#data-cleaning--preparation)
- [EDA & Key Insights](#eda--key-insights)
- [Dashboard](#dashboard)
- [How to Run This Project](#how-to-run-this-project)
- [Final Recommendations & Future Work](#final-recommendations--future-work)
- [Author & Contact](#author--contact)

---

## Overview

MealDash is a quick-commerce delivery operations analysis built on a real, ~45,000-order dataset. It follows a full analytics pipeline — Excel for cleaning, SQL for answering 10 defined business questions, Microsoft Fabric for a governed data pipeline, and Power BI for a 3-page live dashboard — and ends in three specific, ops-actionable recommendations rather than open-ended observations.

## Problem Statement

Delivery times at MealDash vary widely: some orders arrive in 10 minutes, others take almost an hour, with no quick, repeatable way to know why. Diagnosing a single slow week meant manually digging through raw data for a day or two. This project builds a repeatable pipeline that answers "why was it slow, and what can we do about it?" in minutes instead of days.

## Dataset Description

| Detail | Value |
|---|---|
| Records | ~45,000 delivery orders |
| Fields | Delivery timestamps, GPS coordinates, weather, traffic density, agent ratings, vehicle type, festival-day flag |
| Source | [Zomato Delivery Operations Analytics Dataset — Kaggle](https://www.kaggle.com/datasets/saurabhbadole/zomato-delivery-operations-analytics-dataset) |
| Type | Real-world, no synthetic data |

Raw and cleaned versions are in [`Data/`](Data/).

## Tools & Technologies

| Tool | Role |
|---|---|
| **Excel (Power Query)** | First cleaning pass — nulls, formats, categorical standardization, Haversine-based `Distance_km` column |
| **SQL** (Fabric SQL Analytics Endpoint) | Answered all 10 business questions — CTEs, CASE-based bucketing, window functions (`PERCENTILE_CONT`, rolling averages) |
| **Microsoft Fabric** (Lakehouse + Dataflow Gen2) | Governed, repeatable pipeline pulling cleaned data from GitHub into a Lakehouse |
| **Power BI** | 3-page live dashboard with DAX measures, built on the same semantic model as the SQL layer |
| **Git / GitHub** | Version control and project hosting |

## Project Structure

```
MealDash/
├── Dashboard/
│   ├── Mealdash_Dashboard.pbix
│   ├── Mealdash_Dashboard.pbit
│   └── Mealdash_Dashboard.pdf
├── Data/
│   ├── Clean/MealDash_Clean.csv
│   └── Raw/Raw_Data.csv
├── Docs/
│   ├── MealDash_BRD.pdf
│   ├── MealDash_DAX_Measures.pdf
│   ├── MealDash_Presentation.pdf/.pptx
│   └── SQL_Report.pdf
├── Excel_Analysis/
│   ├── MealDash_Excel_Analysis.xlsx
│   └── Charts.png, Pivot.png
├── SQL/
│   └── Q1_...sql – Q10_...sql
├── Screenshots/
│   └── Overview.png, DeepDive.png, TrendOverTime.png, Fabric.png
├── LICENSE
└── README.md
```

## Data Cleaning & Preparation

- Handled nulls and inconsistent formats in Excel Power Query
- Standardized categorical fields (city type, weather, traffic density)
- Calculated straight-line delivery distance (`Distance_km`) from GPS coordinates using the Haversine formula
- Version-controlled the cleaned dataset on GitHub as a refreshable source, then loaded it into a Fabric Lakehouse via Dataflow Gen2 rather than relying on a one-time manual upload

## EDA & Key Insights

10 business questions were answered in SQL, each reported alongside its sample size so no finding is trusted blindly. Full reasoning: [SQL Findings Report](Docs/SQL_Report.pdf).

| # | Question | Finding |
|---|---|---|
| 1 | Overall delivery time | 26 min average, 10–54 min range |
| 2 | Slowest city | Metropolitan slowest by volume (27 min, 34,000+ orders) |
| 3 | Traffic impact | Jam adds ~10 min vs. Low traffic |
| 4 | Weather impact | Fog and Cloudy slowest (28 min), not storms as expected |
| 5 | Distance impact | Biggest time cost is crossing the 5 km mark, then plateaus |
| 6 | Vehicle type impact | Minor effect (~3 min) |
| 7 | Agent rating impact | **4.5+ rated agents are 10–13 min faster** |
| 8 | Bundled orders impact | **2–3 bundled orders more than doubles delivery time** |
| 9 | Festival impact | **Festival days are 75–80% slower** than normal days |
| 10 | Trend over time | Flat, no long-term drift; patterns are structural |

## Dashboard

A 3-page Power BI dashboard, built on the same semantic model as the SQL layer, with DAX measures documented in [`Docs/MealDash_DAX_Measures.pdf`](Docs/MealDash_DAX_Measures.pdf):

- **Page 1 — Executive Overview:** total orders, avg delivery time, festival impact %, slow-delivery rate
- **Page 2 — Delivery Drivers Deep Dive:** distance, rating, vehicle condition, bundling — all slicer-driven
- **Page 3 — Trend Over Time:** daily averages smoothed with a 7-day rolling average

![Executive Overview](Screenshots/Overview.png)

🔗 **[Open the Live Interactive Dashboard](https://app.fabric.microsoft.com/links/SJ5wVO19En?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare&bookmarkGuid=c964f109-a243-4282-9765-edfe9330625c)**
*(Microsoft sign-in required — static export also available: [Mealdash_Dashboard.pdf](Dashboard/Mealdash_Dashboard.pdf))*

## How to Run This Project

1. **Clone the repository**
   ```bash
   git clone https://github.com/seema-kri/MealDash.git
   ```
2. **Explore the data** in [`Data/`](Data/) (raw and cleaned CSVs)
3. **Run the SQL queries** in [`SQL/`](SQL/) — one file per business question, built for Fabric's SQL Analytics Endpoint, works on standard T-SQL/PostgreSQL with minor syntax adjustments
4. **Open the dashboard** via the [live link](https://app.fabric.microsoft.com/links/SJ5wVO19En?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare&bookmarkGuid=c964f109-a243-4282-9765-edfe9330625c) or `Dashboard/Mealdash_Dashboard.pbix` in Power BI Desktop
5. **Read the full reasoning** in [`Docs/`](Docs/) — BRD, SQL Findings Report, DAX Measures reference

## Final Recommendations & Future Work

**Recommendations**
1. **Pre-plan festival-day staffing** — festival deliveries take 75–80% longer, the single largest effect found; low volume (896 orders) makes this a high-ROI, low-effort fix
2. **Cap bundled deliveries at 1 extra order** — 2–3 bundled orders more than doubles delivery time (22→47 min), and the cost accelerates non-linearly
3. **Use agent ratings for order routing** — 4.5+ rated agents deliver 10+ minutes faster than every lower bucket, a strong routing signal

**Future Work**
- Validate the festival-day effect against a full year of festival dates
- Replace straight-line (Haversine) distance with actual road-route distance
- Investigate the direction of causation between agent rating and delivery speed
- Add a live data connection for ongoing monitoring, not one-time diagnosis

## Author & Contact

**Seema Kumari** — Data Analyst
📧 [seemakri136@gmail.com](mailto:seemakri136@gmail.com)
🔗 [LinkedIn](https://linkedin.com/in/seema-kumari-375763308)
📊 [Live Dashboard](https://app.fabric.microsoft.com/links/SJ5wVO19En?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare&bookmarkGuid=c964f109-a243-4282-9765-edfe9330625c)

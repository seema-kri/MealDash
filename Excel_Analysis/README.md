# 📗 MealDash — Excel & Power Query Analysis

This directory contains the initial exploratory data analysis (EDA), data transformations, Pivot Table summaries, and baseline charts for the **MealDash Delivery Operations** dataset.

---

## 📂 Folder Contents

| File / Asset | Format | Description |
|---|---|---|
| **`MealDash_Excel_Analysis.xlsx`** | Workbook | Main Excel workbook with Power Query data cleaning steps, calculated columns, Pivot Tables, and summary sheets.[cite: 2, 3] |
| **`Pivot.png`** | Image | Summary view of Pivot Tables aggregating delivery time by City, Traffic, Vehicle Condition, and Weather. |
| **`Charts.png`** | Image | Visual charts generated from Pivot Tables illustrating operational time variations across core dimensions. |

---

## 🛠️ Key Transformations in Power Query

1. **Null & Data Cleansing:** Removed corrupted records, standardized text strings, and formatted timestamps.[cite: 2, 3]
2. **Geospatial Distance Calculation:** Applied the **Haversine formula** to convert merchant and customer GPS coordinates into straight-line delivery distances (`Distance_km`).[cite: 2, 3]
3. **Operational Bucketing:** Segmented ratings, distances, and traffic into standardized categories for consistent pivot slicing.[cite: 2, 3]

---

## 📊 Summary of Pivot Findings

<div align="center">

| Pivot Analysis Dimension | Key Baseline Finding |
|---|---|
| **City Type** | Semi-Urban is slowest at **49.73 min**, followed by Metropolitan at **27.31 min** and Urban at **22.98 min**. |
| **Traffic Density** | Congestion causes steep delays (**31.18 min** in Jam vs. **21.27 min** in Low traffic). |
| **Weather Conditions** | Overcast conditions (**Cloudy: 28.92 min**, **Fog: 28.91 min**) are slower than Sunny weather (**21.86 min**). |
| **Vehicle Condition** | Poor fleet condition (`Index 0`) causes noticeable delays (**30.07 min**) compared to maintained fleets (**~24.4 min**). |
| **Overall Operational Volume** | **41,547 Normal Deliveries** vs. **4,037 Slow Deliveries** (Grand Average: **26.29 min**, Median: **26.00 min**). |

</div>

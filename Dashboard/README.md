
# 📊 MealDash — Interactive Power BI Dashboard

A cloud-hosted, 3-page interactive delivery operations analytics report built on Microsoft Fabric and Power BI.

[![Open Live Report](https://img.shields.io/badge/Power_BI-Open_Live_Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://app.fabric.microsoft.com/links/SJ5wVO19En?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare&bookmarkGuid=c964f109-a243-4282-9765-edfe9330625c)

---

## ⚡ Executive KPI Summary

| Metric | Value | Business Context |
|---|---|---|
| **Total Orders Analyzed** | **45,584** | Full historical operational volume |
| **Baseline Avg Delivery Time** | **26.29 mins** | Standard benchmark across normal conditions |
| **Festival Avg Delivery Time** | **45.50 mins** | Average turnaround on festive dates |
| **Festival Impact Penalty** | **+75%** | Marginal time delay spikes during festivals |
| **Slow Deliveries Ratio** | **8.86%** | Orders breaching target SLAs |

---

## 📑 Report Structure & Key Breakdown

### 1️⃣ Page 1: Executive Overview (`Overview.png`)
* **Primary Scope:** High-level operational baseline, macro environmental drivers, and overall SLA adherence.
* **Core Visualizations & Findings:**
  * **Festival Impact:** Normal days average **26 mins** (36%) vs. Festival days at **46 mins** (64%).
  * **City Category:** Semi-Urban is slowest (**50 min** avg) vs. Metropolitan (**27 min**) and Urban (**23 min**).
  * **Traffic Congestion:** Jam conditions drive times up to **31 mins**, compared to **21 mins** in Low traffic.
  * **Weather Factors:** Fog and Cloudy conditions create the highest weather lag (**29 mins**).
  * **Vehicle Performance:** Minor differences across vehicle types (Motorcycles at **28 mins**, Scooters/Bikes at **25–26 mins**).

---

### 2️⃣ Page 2: Operational Deep Dive (`DeepDive.png`)
* **Primary Scope:** Root-cause analysis isolating controllable drivers (staffing, vehicle health, trip density, distance).
* **Core Visualizations & Findings:**
  * **Distance Bucketing:** Delivery times jump from **22 mins** ($0\text{–}5\text{ km}$) to **30 mins** ($10\text{+} \text{ km}$), with marginal latency leveling off past 10 km.
  * **Agent Rating Influence:** Drivers rated **4.5+** deliver in **24 mins**, outperforming lower-rated tiers ($<4.5$) who average **35–37 mins** (~11–13 min gap).
  * **Order Stacking / Bundling:** Adding multiple drops creates severe non-linear penalties:
    * *No Extra Drop:* **23 mins**
    * *1 Extra Drop:* **27 mins**
    * *2 Extra Drops:* **40 mins**
    * *3 Extra Drops:* **48 mins**
  * **Vehicle Health:** Poor condition vehicles average **30 mins**, compared to **24–26 mins** for Fair, Good, or Excellent fleets.

---

### 3️⃣ Page 3: Trend Over Time (`TrendOverTime.png`)
* **Primary Scope:** Longitudinal SLA analysis using a 7-day rolling average to detect operational drift.
* **Core Finding:**
  * While day-to-day averages oscillate naturally between **23 and 30 mins**, the 7-day smoothed rolling baseline remains flat around **25–26 mins**.
  * Confirms that bottlenecks are **structural and operational**, rather than caused by progressive system degradation over time.

---

## 🛠️ Interactive Slicers & Features

* **Dynamic Filtering:** Filter entire reports by `City`, `Traffic Density`, `Festival Flag`, `Distance Tier`, `Rating Tier`, and `Vehicle Condition`.
* **One-Click Reset:** Dedicated **Clear all slicers** button to restore baseline portfolio visibility.
* **Governed Backend:** Connected directly to a Microsoft Fabric Lakehouse semantic model.

---

## 🔗 Live Access

👉 **[Launch Interactive Dashboard in Browser](https://app.fabric.microsoft.com/links/SJ5wVO19En?ctid=e93d71d6-b5c0-4b78-a861-d9964ecdfcd6&pbi_source=linkShare&bookmarkGuid=c964f109-a243-4282-9765-edfe9330625c)**

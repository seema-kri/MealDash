
# 📦 MealDash — Data Directory

Data storage for the MealDash quick-commerce analytics pipeline.

---

## 📂 Structure

* **`Raw/Raw_Data.csv`**: Original uncleaned Kaggle dataset (45,000+ records).
* **`Clean/MealDash_Clean.csv`**: Transformed analytical dataset connected to Microsoft Fabric via Dataflow Gen2.

---

## 🛠️ Data Prep Summary

* **Nulls & Formatting**: Imputed missing values and standardized categorical fields.
* **Geospatial Feature**: Calculated `Distance_km` from GPS coordinates using the Haversine formula.
* **Ingestion**: Cleaned CSV is ingested into Microsoft Fabric Lakehouse for SQL analytics and Power BI modeling.

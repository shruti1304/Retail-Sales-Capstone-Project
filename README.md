# 📊 End-to-End Enterprise Demand Forecasting System

An enterprise-grade forecasting and inventory optimization solution built entirely on a cloud-native **Databricks Lakehouse Architecture** using **PySpark ML**. This project ingests raw operational retail data, constructs robust time-series features, handles extreme demand volatility, and presents predictive insights via an executive dashboard.

---

## 🏗️ System Architecture: The Medallion Paradigm
The project implements a modern multi-tiered data warehouse layout to clean, store, and optimize high-volume transactional records for machine learning runtimes.

* **Bronze Layer:** Ingestion point for raw daily point-of-sale data logs.
* **Silver Layer (`silver_analytical_master`):** Optimized structural master data where schemas are enforced, null values are systematically resolved, and timestamps are parsed.
* **Gold Layer (`gold_model_ready_features` & `gold_executive_forecast_predictions`):** High-density feature arrays and final predictions optimized with **Delta Lake Columnar Storage** for instant data dashboard streaming and BI consumption.

---

## 🛠️ Project Implementation Lifecycle

### Phase 1 & 2: Core Infrastructure Setup
* Cluster resource provisioning and storage tracking.
* Schema definitions and schema evolution flags (`.option("overwriteSchema", "true")`).

### Phase 3: High-Dimensional Feature Engineering
To maximize the predictive performance of our algorithms, we engineered historical context directly into the feature matrices:
* **Promotional Status Flags:** Explicit boolean markers identifying active advertising intervals.
* **Geographic Grouping:** Consolidated store clusters and product category maps packed into high-density mathematical vectors using the Spark `VectorAssembler`.

### Phase 4 & 5: Model Selection, Optimization & Outlier Treatment
Our initial predictive models were warped by extreme bulk-purchase anomalies (one-off business spikes), resulting in an elevated Root Mean Squared Error (RMSE). 
* **The Code Fix:** Applied a 99th percentile target capping mechanism to the training dataset. This constrained anomalous demand peaks without losing operational baseline patterns.
* **Model Selection:** Evaluated a robust **Random Forest Regressor** configured with 60 estimators and a max depth of 12.

### Phase 6: Interactive Executive Reporting
Leverages Databricks Lakehouse Dashboards backed by active cluster compute to yield three interactive diagnostic workspaces for supply chain leaders:
1.  **Regional Demand Profiles:** Comparative chart mapping `actual_sales` vs. `forecasted_demand` by city.
2.  **Marketing Analytics Velocity Timeline:** Isolation plot proving sales trajectory during promotional vs. normal intervals.
3.  **Supply Chain Risk Index:** A dynamic heat map showing imminent demand spikes exceeding historical baselines by 15%, warning warehouses to frontload inventory.

---

## 📈 Model Performance & Validation Summary

The optimization phase successfully balanced transactional accuracy with outlier resilience.

| Evaluation Metric | Score Value | Business Interpretation |
| :--- | :--- | :--- |
| **MAE (Mean Absolute Error)** | `1.85 units` | On average, daily predictions deviate by fewer than 2 units per product. |
| **RMSE (Root Mean Squared Error)** | `33.93 units` | Captures penalty deviations from rare, massive wholesale demand surges. |

---

## 🚀 How to Run the Pipeline

1.  Clone this repository directly into your Databricks Workspace via **Git Folders**.
2.  Execute the notebooks sequentially from `Notebook 1` through `Notebook 5`.
3.  Open the **Dashboards** menu on your Databricks sidebar, select the connected engine cluster, and launch the interactive visual reporting app.

---

## 🛠️ Tech Stack & Utilities
* **Processing Engine:** Apache Spark (PySpark SQL & MLlib)
* **Data Warehouse Format:** Delta Lake 
* **Visualization Engine:** Plotly & Databricks Lakehouse Dashboards UI
* **Source Control:** GitHub Git Integration via Developer PAT Tokens

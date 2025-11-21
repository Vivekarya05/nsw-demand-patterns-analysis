

<img width="1920" height="1080" alt="AM" src="https://github.com/user-attachments/assets/94a4bc00-1e0f-4743-aa0f-5b95793db474" />






# 🔌 NSW Electricity Demand Forecasting (2024)

A fully engineered forecasting workflow built using AEMO NEM operational data, Python, MongoDB, and applied time-series & machine-learning techniques.

This project demonstrates an end-to-end pipeline similar to the analytical processes used by teams in AEMO Operations Planning, Origin Energy Analytics, and NSW Energy System Forecasting.

---

## 📂 System Architecture & Key Components

### 📥 Data Layer
* Source: AEMO DISPATCHREGIONSUM , ' NEMOSIS ' python Library (5-minute interval operational demand)
* Storage: **MongoDB** (scalable, query-efficient document store)
* Retrieval: Python-based ETL → Cleaned + structured daily demand dataset

### 🧹 Data Engineering
* Timestamp alignment & index normalisation
* NSW1 region extraction
* Duplicate/missing value validation
* 5-min → **daily aggregation**
* Calendar feature tagging (weekday, month, season)

### 📊 Exploratory Analysis
* Daily load shape
* Weekly behavioural patterns
* Seasonal variation
* Hour × month heatmaps
* Rolling trend curves (7-day, 30-day)

### 🔧 Feature Engineering
* Lag variables (**lag_1, lag_7**)
* Rolling statistics (**RM7, RM30**)
* Seasonality & calendar drivers
* Normalised & model-ready dataset stored in MongoDB

### 🤖 Forecasting Models
| Model | RMSE | Notes |
| :--- | :--- | :--- |
| Naive Baseline | $\approx 703$ MW | |
| SARIMA | $\approx 937$ MW | |
| XGBoost (initial) | $\approx 704$ MW | |
| **XGBoost (tuned)** | $\approx \mathbf{615}$ MW | **Best performance** |

### 📅 Final Output
* A **30-day NSW demand forecast** for January 2025, generated using tuned XGBoost.

---

## 🧭 Project Workflow Overview

The project follows a standard, robust **Extract-Load-Transform (ELT)** and **Machine Learning Operations (MLOps)** pipeline, ensuring data quality, feature stability, and reproducible model outputs. 

* ### Step 1: Data Ingestion & Storage
    * Operational 5-minute data is extracted from the AEMO NEM data source using the **NEMOSIS** API wrapper.
    * Raw data is loaded into **MongoDB** for persistent and flexible storage.

* ### Step 2: ETL & Feature Creation
    * Data is queried from MongoDB, filtered for the **NSW1** region, and validated for completeness.
    * The 5-minute data is aggregated to a **Daily Demand** time series.
    * **Feature Engineering** is applied, including creating lag variables (1-day, 7-day), rolling means, and calendar features (month, season).
    * The final, model-ready dataset is saved back into MongoDB.

* ### Step 3: Model Training & Selection

    * The dataset is split into training and validation sets.
    * Baseline (**Naive**), Time Series (**SARIMA**), and Ensemble (**XGBoost**) models are trained and evaluated using **RMSE**.
    * **XGBoost** is selected and hyper-parameters are tuned to minimise the forecast error (achieving **RMSE $\approx 615$ MW**).

* ### Step 4: Final Forecasting & Output
    * The tuned **XGBoost** model is used to generate a **30-day forward forecast** for January 2025.
    * The final forecast output (times, predicted demand values) is stored and visualised for operational stakeholders.
    * 
 <img width="1104" height="708" alt="_- visual selection (11)" src="https://github.com/user-attachments/assets/dddd2ef4-5eca-4650-a59c-1ebcd6808d10" />

##  🤖 Machine Learning Forecasting Pipeline
<img width="1104" height="708" alt="_- visual selection (12)" src="https://github.com/user-attachments/assets/297adcbb-2f33-4c33-878b-29f7796b4955" />

  

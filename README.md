# 🚀 End-to-End Lakeflow Spark Declarative Pipeline (Bronze–Silver–Gold)

## 📌 Project Description

This project demonstrates a **production-grade, SQL-based Lakeflow Spark Declarative Pipeline** built on Databricks using the **Bronze → Silver → Gold** architecture.

The pipeline ingests raw files incrementally, enforces data quality, applies Change Data Capture (CDC), preserves historical data, and serves analytics-ready datasets through Gold materialized views that power dashboards.

The solution avoids full data reprocessing, reduces compute cost, and closely mirrors how modern data engineering pipelines are built in real-world enterprises.
<img width="772" height="289" alt="NEW4" src="https://github.com/user-attachments/assets/74d9ad11-1084-4b3f-a287-fc5dca5cea98" />

<img width="784" height="367" alt="5" src="https://github.com/user-attachments/assets/b15541ee-708a-4439-a824-ecb40b683845" />
<img width="943" height="364" alt="NEW2" src="https://github.com/user-attachments/assets/49d65aa3-989a-4c9c-b43f-770a3f15d2f8" />
<img width="792" height="364" alt="NEW5" src="https://github.com/user-attachments/assets/f170c3ce-2439-4bde-9e92-3ee80b786fdf" />

---

## 🎯 Problem Statement

Traditional batch ETL pipelines:
- Reprocess full datasets on every run
- Increase compute cost
- Delay insights
- Require manual orchestration and recovery

This project redesigns such workflows using **Lakeflow Spark Declarative Pipelines**, enabling:
- Incremental processing
- Automatic dependency management
- Built-in monitoring and recovery
- Scalable analytics

---

## 🏗️ Architecture

Raw Files (Cloud Storage / Volumes)
---->
Bronze Streaming Table
---->
Silver Current (SCD Type 1 + Expectations)
---->
Gold Materialized Views (Analytics)

Bronze
---->
Silver History (Append-only SCD Type 2)



---

## 🛠️ Tech Stack

- Databricks Lakeflow Spark Declarative Pipelines (DLT / SDP)
- Spark SQL
- Delta Lake
- Unity Catalog
- Auto Loader (`read_files`)
- Databricks Jobs
- Databricks SQL Dashboards

---

## 📂 Repository Structure

JUST DOWNLOAD DBC FILE AND IMPORT IN DATABRICKS ACCOUNT THE STRUCTRE IS IN PROPER MANNER 


---

## 🔹 Pipeline Layers

### 🟤 Bronze Layer – Raw Ingestion
- Streaming table using Auto Loader
- Incremental ingestion from cloud storage (Volumes)
- Append-only raw data
- Metadata captured (ingest time, source file)

**Purpose:** Preserve raw data and enable scalable ingestion.

---

### ⚪ Silver Layer – Current Data (SCD Type 1)
- Streaming table with CDC using `APPLY CHANGES INTO`
- Maintains latest record per business key
- Enforces data quality using expectations
- Invalid records dropped using `ON VIOLATION DROP ROW`

**Purpose:** Provide clean, analytics-ready current data.

---

### ⚪ Silver History – Audit Layer (SCD Type 2)
- Append-only streaming table
- Stores all versions of records
- Same business key can appear multiple times

**Note:**  
Validity windows (`valid_from`, `valid_to`) are derived at query time and are not stored in the pipeline.

---

### 🟡 Gold Layer – Analytics
- Materialized views built on Silver Current
- Incrementally refreshed
- Used for dashboards and reporting

Examples:
- Total users
- Average age
- Age distribution

---

## ✅ Key Features

- Incremental ingestion (no full reprocessing)
- Change Data Capture (SCD Type 1)
- Historical data preservation (SCD Type 2)
- Data quality enforcement using expectations
- Automatic dependency management
- Built-in monitoring via event logs
- Failure recovery with exactly-once processing
- Performance optimization using Z-ORDER
- Job-based orchestration
- Dashboard powered by Gold layer

---

## 📊 Monitoring & Observability

Pipeline execution is monitored using the Databricks **Event Log**, which provides:
- Pipeline start and end time
- Records processed
- Expectation violations
- Errors and warnings

Example:

SELECT *
FROM system.event_log
WHERE pipeline_id = '<pipeline_id>'
ORDER BY event_time DESC; 

---

### ⏱️ Orchestration
The pipeline is executed via a Databricks Job
Supports manual and scheduled execution
Ensures Gold tables and dashboards are always up to date

📈 Dashboard
Built on Gold materialized views
Displays KPIs and aggregated analytics
Automatically refreshed through the pipeline job

▶️ How to Run
Upload raw CSV/JSON files to the configured Volume path
Run the Lakeflow Spark Declarative Pipeline
Trigger the Databricks Job
Query Gold tables or view the dashboard

🎤 What This Project Demonstrates
An end-to-end, production-style Lakeflow Spark Declarative Pipeline using SQL with:
Incremental ingestion
CDC (SCD Type 1)
Historical tracking (SCD Type 2)
Data quality enforcement
Monitoring, recovery, and analytics-ready outputs

👤 Author

Nikesh Purohit
Aspiring Data Engineer | Databricks | SQL | Lakeflow | Delta Lake

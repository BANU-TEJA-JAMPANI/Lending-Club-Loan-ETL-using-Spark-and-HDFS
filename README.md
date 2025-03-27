# Lending Club Loan ETL using Spark and HDFS

This project implements an end-to-end ETL (Extract, Transform, Load) pipeline using **Apache Spark** and **HDFS** for processing Lending Club's loan data. It simulates a real-world data engineering workflow for a consumer finance company, handling raw data cleaning, transformation, and preparation for downstream analytics.

---

## 🔍 Project Overview

Financial institutions and P2P lending platforms often deal with massive volumes of customer and loan data. This project focuses on building a scalable data processing pipeline to clean, enrich, and store Lending Club loan data using PySpark and HDFS.

---

## 🧱 Technologies Used

- **Apache Spark** (PySpark)
- **HDFS (Hadoop Distributed File System)**
- **Python 3**
- **Jupyter Notebook / Zeppelin / CLI**

---

## 📂 Data Sources

The dataset consists of:
- **Customer data** (borrowers' personal and financial details)
- **Loan application data**
- **Loan repayment history**
- **Loan defaulter information**

---

## ⚙️ ETL Workflow

### 🔹 1. Ingestion
- Load raw CSV files from HDFS into Spark DataFrames.

### 🔹 2. Cleaning & Transformation
- Rename columns for clarity
- Handle null values and data type conversions
- Add ingestion timestamp
- Standardize state codes
- Remove duplicates
- Generate unique hash keys using `sha2()`

### 🔹 3. Risk Scoring (Basic Logic)
- Calculate risk indicators using default history and repayment metrics.

### 🔹 4. Save to HDFS
- Write cleaned data back to HDFS in a structured format (e.g., `/user/yourname/cleaned/`).

---

## 📝 Example Transformations

```python
from pyspark.sql.functions import sha2, concat_ws, current_timestamp

df_cleaned = df_raw \
    .withColumnRenamed("annual_inc", "annual_income") \
    .withColumn("ingest_date", current_timestamp()) \
    .withColumn("member_hash", sha2(concat_ws("||", *["emp_title", "emp_length", "home_ownership", "annual_income", "zip_code", "addr_state", "grade", "sub_grade", "verification_status"]), 256))

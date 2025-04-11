# 💰 Lending Club Loan Spark Project

In this project, we load a large Lending Club dataset from HDFS into Apache Spark, perform extensive data cleaning and processing, and calculate a custom **loan score** based on repayment history, financial health, and credit behavior. The final cleaned and scored data is then written back to HDFS for use by downstream analytics and reporting teams.

---

## 📌 Business Objectives

- Load the raw Lending Club dataset from HDFS
- Divide it into 5 logically separated datasets
- Clean and process each part using PySpark
- Create permanent external tables for SQL access
- Calculate a loan score to evaluate borrower risk
- Write all cleaned and scored data back to HDFS

---

## 🧱 Dataset Breakdown (5 Parts)

1. **`customers_data`** – Borrower profile info (income, employment, credit limit)
2. **`loans_data`** – Loan info (amount, term, interest rate, loan status)
3. **`loan_repayments_data`** – Historical repayments, principal, interest, late fees
4. **`loan_defaulters_delinq`** – Delinquency-based defaulters (delinq_2yrs, delinq_amnt, mths_since_last_delinq)
5. **`loan_defaulters_detail`** – Credit risk flags (public records, bankruptcies, credit inquiries)

---

## 🧮 Loan Score Calculation

The loan score is based on 3 critical categories:

| Category             | Weight | Columns Used                                                                 |
|----------------------|--------|------------------------------------------------------------------------------|
| Repayment History    | 20%    | total_payment_received, last_payment                                        |
| Defaulter History    | 45%    | delinq_2yrs, pub_rec, pub_rec_bankruptcies, inq_last_6mths                  |
| Financial Health     | 35%    | home_ownership, loan_status, funded_amnt, grade_points                      |

> 📌 The final loan score is written to HDFS under:  
`/user/<itv016573>/LendingClubData/processed/loan_score/`

---

## 🏗️ Permanent Tables & Views

To support downstream analytics and reporting teams:
- Cleaned datasets are written as **external Hive/Spark tables**
- Tables are SQL-accessible and used in reporting dashboards
- Temporary views and managed tables are created as needed

---

## 🗂️ Project Structure
LendingClubSparkProject/
├── CONF/                          # Spark and project configuration files
├── SETUP/                         # Data loading and permanent table creation
│   ├── intro.py                   # Split raw Excel into 5 datasets
│   └── permanent_table.py         # Create permanent Hive/Spark SQL tables
├── DATA_CLEANING/                 # Clean each dataset part
│   ├── clean_customers_data.py
│   ├── clean_loans_data.py
│   ├── clean_loan_repayments_data.py
│   ├── clean_loan_defaulters_data.py
│   └── clean_bad_loan_defaulters_data.py
├── SCORING/
│   └── loan_score_calculator.py   # Loan score computation logic
├── DOCS/                          # Documentation files
│   ├── data_dictionary.xlsx       # Column-wise descriptions
│   └── scoring_logic.md           # Loan scoring logic explanation
├── data/                          # Raw Excel dataset
│   └── LendingClubData.xlsx
├── main.py                        # Entry point to run the full pipeline
├── requirements.txt               # Python & PySpark dependencies
├── README.md                      # Project overview
└── .gitignore                     # Ignored files/folders



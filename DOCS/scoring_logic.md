# 📊 Loan Scoring Logic

This document explains how the Loan Score is calculated based on three major risk assessment categories:


## 1. Loan Payment History (20%)

Evaluates how the customer has repaid previous loans.

Metrics:
- total_payment_received
- last_payment_amount

Higher and timely payments contribute positively to the score.

---

## 2. Financial Health (35%)

Assesses the customer’s financial position and risk profile.

Metrics:
- home_ownership
- loan_status
- funded_amnt
- grade_points

Customers with owned/mortgaged property, approved loans, and better grades receive higher scores.

---

## 3. Loan Defaulters History (45%)

The most heavily weighted component. It checks if the customer has a history of:

- Delinquency
- Public records
- Bankruptcies
- Credit enquiries

### Key columns:
- delinq_2yrs
- pub_rec
- pub_rec_bankruptcies
- inq_last_6mths

---

## Data Preparation

Processed DataFrames created from `loan_defaulters.csv`:

1. Cast columns to integer:
   - delinq_2yrs
   - pub_rec
   - pub_rec_bankruptcies
   - inq_last_6mths

2. Replace nulls with 0 using:
```python
.fillna(0, subset=[...])

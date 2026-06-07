# Power BI DAX Formulas - Banking Analytics Project

This document compiles the Data Analysis Expressions (DAX) measures required to build the Executive Dashboard using the Gold Layer metrics.

---

## 📈 Key Performance Indicators (KPI Cards)

### 1. Total Deposits
Calculates the aggregate financial deposits held across all customer accounts.
```dax
Total Deposits = SUM(gold_customer_360[total_balance])
```
* **Formatting:** Currency (`$`), auto/1 decimal place.

### 2. Active Accounts
Counts only the accounts currently flagged as active.
```dax
Active Accounts = SUM(gold_customer_360[active_accounts])
```
* **Formatting:** Whole number (`#,##0`).

### 3. Delinquency Rate
Calculates the percentage of defaulted loans relative to the total number of loans issued.
```dax
Delinquency Rate = 
DIVIDE(
    SUM(gold_customer_360[defaulted_loans]),
    SUM(gold_customer_360[total_loans]),
    0
)
```
* **Formatting:** Percentage (`%`).

### 4. Fraud Mitigation Rate
Measures the percentage of fraud cases successfully investigated and confirmed (or blocked/mitigated).
```dax
Fraud Mitigation Rate = 
DIVIDE(
    SUM(gold_fraud_analysis[confirmed_frauds]),
    SUM(gold_fraud_analysis[fraud_count]),
    0
)
```
* **Formatting:** Percentage (`%`).

---

## 📊 Transaction & Performance Chart Measures

### 5. Daily Transaction Success Rate
Used in your Daily Trends line chart to plot transaction success over time.
```dax
Transaction Success Rate = 
DIVIDE(
    SUM(gold_daily_transaction_trends[successful_count]),
    SUM(gold_daily_transaction_trends[transaction_count]),
    0
)
```
* **Formatting:** Percentage (`%`).

### 6. Net Flow (Credits vs. Debits)
Aggregates the flow of money in branches (Credits minus Debits).
```dax
Net Flow = SUM(gold_branch_performance[net_flow])
```
* **Formatting:** Currency (`$`).

---

## 🍩 Loan Portfolio Segment Measures (Donut Chart)

### 7. Home Loan Share (%)
Extracts the proportion of total loan volume allocated to Home Loans.
```dax
Home Loan Share = 
VAR TotalLoans = SUM(gold_loan_portfolio[total_loan_amount])
VAR HomeLoans = CALCULATE(
    SUM(gold_loan_portfolio[total_loan_amount]),
    gold_loan_portfolio[loan_type] = "Home Loan"
)
RETURN 
DIVIDE(HomeLoans, TotalLoans, 0)
```
* **Formatting:** Percentage (`%`).

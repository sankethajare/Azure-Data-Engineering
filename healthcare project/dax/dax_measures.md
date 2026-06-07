# Power BI DAX Formulas - Healthcare Analytics Project

This document compiles the Data Analysis Expressions (DAX) measures required to build the simple, beginner-friendly Healthcare Dashboard.

---

## 📈 Key Performance Indicators (KPI Cards)

### 1. Total Patients
Counts the unique patients processed in the hospital.
```dax
Total Patients = DISTINCTCOUNT(patients_silver[patient_id])
```
* **Formatting:** Whole number (`#,##0`).

### 2. Total Encounters
Counts the total number of patient visits (encounters).
```dax
Total Encounters = COUNT(encounters_silver[encounter_id])
```
* **Formatting:** Whole number (`#,##0`).

### 3. Recovery Rate
Measures the percentage of encounters resulting in successful recovery.
```dax
Recovery Rate = 
DIVIDE(
    SUM(department_performance[recovered_count]),
    SUM(department_performance[total_encounters]),
    0
)
```
* **Formatting:** Percentage (`%`).

### 4. Total Billings
Calculates the aggregate billing amounts.
```dax
Total Billings = SUM(billing_silver[total_amount])
```
* **Formatting:** Currency (`$`), auto/1 decimal place.

---

## 📊 Filtered Visual Measures

### 5. Inpatient Visits (Donut Chart Detail)
Counts patient visits categorized as Inpatient.
```dax
Inpatient Visits = 
CALCULATE(
    COUNT(encounters_silver[encounter_id]),
    encounters_silver[encounter_type] = "Inpatient"
)
```

### 6. Outpatient Visits (Donut Chart Detail)
Counts patient visits categorized as Outpatient.
```dax
Outpatient Visits = 
CALCULATE(
    COUNT(encounters_silver[encounter_id]),
    encounters_silver[encounter_type] = "Outpatient"
)
```

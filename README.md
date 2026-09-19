# MYSQL: E-commerce Customer Churn Analysis
This repository contains a comprehensive MySQL-based data pipeline and exploratory data analysis project focused on customer churn in the e-commerce sector. The project covers end-to-end data processing—from raw dataset ingestion and data cleaning (imputation, outlier handling) to schema transformation, relationship modeling, and business insights generation.

---

## 📌 Project Overview

Customer retention is critical for e-commerce platforms. This project transforms a raw dataset of 5,630 customer records into a clean, structured MySQL database (`ecomm`). Using advanced SQL queries, data inconsistencies are normalized, missing values are imputed using statistical methods (mean and mode), derived columns are generated, and actionable business insights are extracted.

---

## 🛠️ Key Data Operations & Pipeline Workflow

### 1. Database & Table Setup
* Initialized the `ecomm` database.
* Created the core table `customer_churn` containing customer demographics, tenure, order history, satisfaction scores, and transaction details.

### 2. Data Cleaning & Normalization
* **Mean Imputation:** Calculated and rounded the mean values to fill missing entries in numerical features:
  * `WarehouseToHome`
  * `HourSpendOnApp`
  * `OrderAmountHikeFromlastYear`
  * `DaySinceLastOrder`
* **Mode Imputation:** Used statistical mode (most frequent occurrence) to replace missing values in:
  * `Tenure`
  * `CouponUsed`
  * `OrderCount`
* **Outlier Removal:** Identified and dropped invalid records where `WarehouseToHome > 100`.
* **Inconsistency Handling:** Standardized categorical values for consistency across queries:
  * Unified login devices (`'Phone'` ➔ `'Mobile Phone'`).
  * Unified product categories (`'Mobile'` ➔ `'Mobile Phone'`).
  * Standardized payment modes (`'COD'` ➔ `'Cash on Delivery'`, `'CC'` ➔ `'Credit Card'`).

### 3. Data Transformation & Schema Evolution
* **Column Renaming:** Fixed typographical errors in schema attributes (`PreferedOrderCat` ➔ `PreferredOrderCat`, `HourSpendOnApp` ➔ `HoursSpentOnApp`).
* **Feature Engineering:**
  * Created `ComplaintReceived` (`'Yes'`/`'No'`) mapped from original `Complain` flag.
  * Created `ChurnStatus` (`'Churned'`/`'Active'`) mapped from original `Churn` flag.
* **Schema Optimization:** Dropped redundant binary columns (`Complain`, `Churn`).

### 4. Database Expansion & Relational Modeling
* Created a secondary table, `customer_returns`, tracking return dates and refund amounts.
* Established relational integrity using `CustomerID` as a **Foreign Key** referencing `customer_churn(CustomerID)`.

---

## 📊 Business Insights & Exploratory Queries

The repository includes SQL queries designed to answer critical business questions:
* **Churn Breakdown:** Retreived overall churn vs. active counts, as well as churn percentage relative to complaints received.
* **Customer Demographics:** Segmented churn metrics across city tiers, distance buckets (`Very Close`, `Close`, `Moderate`, `Far`), and product preferences.
* **Promotions & Engagement:** Analyzed coupon usage by gender, maximum app hours spent per category, and satisfaction scores among complaining customers.
* **Returns Analysis:** Executed `INNER JOIN` operations between customer churn and return records to isolate high-risk, churned customers who submitted formal complaints.

---


## 📁 Repository Structure
---

## 💻 How to Run the Project

1. **Prerequisites:**
   * MySQL Server (v8.0+ recommended)
   * MySQL Workbench or any preferred SQL client

2. **Execution Steps:**
   * Clone the repository:
   * Open `customer_churn_analysis.sql` in MySQL Workbench.
   * Run the script sequentially or block-by-block to build the schema, populate data, run cleaning updates, and execute analytical queries.

---

## 📝 Technologies Used
* **Database Management System:** MySQL
* **Tools:** MySQL Workbench
* **Language:** SQL (DDL, DML, Aggregation, Subqueries, Joins, Windowing & Case Expressions)

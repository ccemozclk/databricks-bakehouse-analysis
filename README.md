# Bakehouse Sales & Customer Analysis with PySpark on Databricks

This repository contains the code and analysis for a data engineering project focused on the "Bakehouse" dataset. The project was developed entirely within the Databricks platform, leveraging PySpark and Spark SQL to perform end-to-end data ingestion, cleaning, transformation, and analysis.

This project serves as a practical application of skills learned from DataCamp's PySpark and Databricks curriculum.

## 🚀 Technologies Used

* **Core Engine:** Apache Spark (via PySpark)
* **Platform:** Databricks
* **Primary APIs:** PySpark DataFrame API & Spark SQL
* **Language:** Python
* **Version Control:** Git & GitHub

## 📊 Dataset

The project utilizes the `bakehouse` schema, which includes the following tables:
* `sales_transactions`: Fact table containing all individual sales records.
* `sales_customers`: Dimension table with customer information.
* `sales_franchises`: Dimension table with franchise/store details.
* `sales_suppliers`: Dimension table for product suppliers.
* `media_customer_reviews`: Customer feedback and ratings.
* `media_gold_reviews_chunked`: A second table of (premium) customer reviews.

## 🛠️ Project Workflow

The analysis followed a structured data engineering lifecycle:

### 1. Data Ingestion & Exploration
* Loaded all six tables from the `bakehouse` schema into PySpark DataFrames.
* Conducted initial data exploration by checking schemas (`.printSchema()`) and row counts (`.count()`).
* Inspected sample data using `.show()`  to understand data types and potential quality issues.

### 2. Data Cleaning & Preparation
* Handled missing values in critical columns using `.na.drop()` (e.g., for transaction IDs) and `.na.fill()` (e.g., for categorical data).
* Performed type casting on key columns, such as converting sales figures from `string` to `double` and date strings to `timestamp` format using `.withColumn()`  and `.cast()`.

### 3. Data Enrichment (Joins & Unions)
* Created a single, enriched "master analysis table" by joining the main `sales_transactions` fact table with the `sales_customers` and `sales_franchises` dimension tables.
* Applied **broadcast join optimization** (`broadcast()`)  on the smaller dimension tables to improve query performance.
* Combined the two distinct customer review tables (`media_customer_reviews` and `media_gold_reviews_chunked`) into a single DataFrame using `.union()`.

### 4. Analysis (DataFrame API vs. Spark SQL)
Performed analysis using both of PySpark's primary APIs:

* **DataFrame API:** Used programmatic methods like `.groupBy()`, `.agg()` , and `.filter()`  to calculate key metrics.
* **Spark SQL:** Registered the DataFrames as temporary views (`.createOrReplaceTempView()`) and used `spark.sql()`  to run complex, multi-step aggregations and queries.

### 5. Optimization 
* **Caching:** Persisted the master analysis table in memory using `.cache()` to speed up iterative queries during the analysis phase.
* **Query Planning:** Used `.explain()`  to inspect the physical query plan and confirm that optimizations (like broadcast joins) were being correctly applied.


## 🚀 How to Run
1.  Clone this repository to your local machine.
2.  Import the `.ipynb` notebook file into your Databricks workspace.
3.  Ensure you have access to the `bakehouse` schema (or modify the data source paths in the notebook).
4.  Attach a running Spark cluster to the notebook.
5.  Run the cells sequentially to reproduce the analysis.

## 👤 Author
* **Cem OZCELİK/ccemozclk**
* [(https://www.linkedin.com/in/cemozcel%C4%B1k/)]

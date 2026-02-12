# Incremental Data Loading Pipeline (Python + SQLite)

A production-style incremental ETL pipeline built using Python, Pandas, and SQLite to efficiently load only new data into a data warehouse.

This project demonstrates how real-world data engineering systems avoid reprocessing historical data by detecting and loading only newly generated records based on timestamps.


## 📌 Project Overview

Modern data systems continuously generate new data. Reloading the full dataset repeatedly is inefficient and costly. Incremental data loading solves this by processing only the records that have not yet been loaded.

This project implements a complete incremental data pipeline using a real-world e-commerce dataset. The pipeline reads order data, identifies newly added records using a timestamp column, and loads only those records into a warehouse table.

The implementation follows production-style practices including:

* Structured data warehouse design
* Schema alignment
* Logging and monitoring
* Data validation
* Incremental change detection
* Safe re-execution without duplication


## 🎯 Business Use Case

E-commerce platforms generate new orders continuously. Analytics teams require updated sales data for reporting, dashboards, and operational monitoring.

Instead of reloading all historical orders daily, this pipeline:

* Detects newly created orders
* Loads only new records
* Maintains an up-to-date warehouse
* Reduces processing time and storage usage

This is similar to how real production ETL pipelines support daily reporting systems.


## 📊 Dataset

**Brazilian E-Commerce Public Dataset (Olist)**

The dataset contains real online marketplace order data including purchase timestamps, delivery dates, and order status.

Primary dataset used:

* `olist_orders_dataset.csv`

Key column used for incremental logic:

* `order_purchase_timestamp`

This timestamp is used to identify new records that should be inserted into the warehouse.


## 🏗 Architecture

```
CSV Dataset (Raw Data)
        ↓
Python ETL Pipeline (Jupyter Notebook)
        ↓
Incremental Timestamp Filtering
        ↓
SQLite Data Warehouse (fact_orders)
        ↓
Analytics / Reporting
```


## ⚙️ Technologies Used

* Python
* Pandas
* SQLite
* Jupyter Notebook
* Python Logging


## 🔄 How Incremental Loading Works

1. The pipeline checks the latest timestamp already stored in the warehouse.
2. Source data is scanned for records newer than that timestamp.
3. Only those records are selected.
4. New records are inserted into the warehouse table.
5. The pipeline logs execution details.

If the pipeline runs again without new data, nothing is inserted.

This ensures efficient and repeatable execution.


## 📂 Project Structure

```
incremental_loading_project/
│
├── data/
│   └── olist_orders_dataset.csv
│
├── warehouse/
│   └── warehouse.db
│
├── incremental_pipeline.ipynb
│
└── README.md
```


## 🧱 Data Warehouse Schema

Table: `fact_orders`

| Column                  | Description                           |
| ----------------------- | ------------------------------------- |
| order_id                | Unique order identifier (Primary Key) |
| customer_id             | Customer reference                    |
| order_status            | Order status                          |
| purchase_timestamp      | Order purchase time                   |
| approved_at             | Order approval time                   |
| delivered_customer_date | Delivery completion time              |


## ▶️ How to Run the Project

### 1. Install dependencies

```bash
pip install pandas
```

SQLite is included with Python.


### 2. Download dataset

Download the Olist dataset and place the file:

```
data/olist_orders_dataset.csv
```


### 3. Run notebook

Open and execute:

```
incremental_pipeline.ipynb
```

Run cells in order.


### 4. First Execution

* Creates warehouse table
* Loads all historical data


### 5. Subsequent Executions

* Loads only new records
* Prevents duplicate insertion


## 🧪 Pipeline Validation

The pipeline verifies:

* Timestamp conversion
* Schema alignment
* Duplicate detection
* Successful insertion count

Logging tracks each execution step.


## 🚀 Performance Optimization Techniques

* Incremental loading instead of full reload
* Selective column extraction
* Primary key enforcement
* Timestamp-based filtering

These techniques reduce processing time and storage overhead.


## 📈 Monitoring

Python logging is used to monitor:

* Database connection
* Number of records inserted
* Pipeline completion

The pipeline can be safely re-run without data duplication.


## 🔮 Future Improvements

* Automate pipeline using Apache Airflow
* Cloud storage integration (AWS S3)
* Partitioned warehouse tables
* Migration to PostgreSQL or Snowflake
* Streaming ingestion using Kafka
* Change Data Capture (CDC)


## 🎓 Learning Outcomes

This project demonstrates:

* Incremental ETL design
* Data warehouse schema management
* Timestamp-based change detection
* Data pipeline monitoring
* Production-style pipeline structure



## ⭐ If you found this project useful

Give it a star ⭐ and feel free to fork or extend the pipeline.

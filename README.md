# Airbnb End-to-End Data Engineering Pipeline

A modern end-to-end data engineering project built using AWS, Snowflake, and dbt following Medallion Architecture principles (Bronze → Silver → Gold).

---

# 📌 Project Overview

This project demonstrates a complete cloud-based analytics engineering workflow using Airbnb datasets such as:

* Bookings
* Hosts
* Listings

The pipeline ingests raw CSV data, processes and transforms it using dbt, and creates analytics-ready datasets optimized for reporting and business intelligence.

---

# 🚀 Tech Stack

| Technology | Purpose                         |
| ---------- | ------------------------------- |
| Python     | Environment & execution         |
| AWS S3     | Cloud storage                   |
| Snowflake  | Cloud data warehouse            |
| dbt        | Data transformation             |
| SQL        | Data modeling & transformations |
| Git/GitHub | Version control                 |

---

# 🏗️ Architecture

```text
Raw CSV Files
      ↓
AWS S3
      ↓
Snowflake Staging
      ↓
Bronze Layer (Raw)
      ↓
Silver Layer (Cleaned)
      ↓
Gold Layer (Analytics Ready)
```

---

# 📂 Project Structure

```bash
AWS_DBT_Snowflake/
│
├── SourceData/
│   ├── bookings.csv
│   ├── hosts.csv
│   └── listings.csv
│
├── DDL/
│   ├── ddl.sql
│   └── resources.sql
│
├── aws_dbt_snowflake_project/
│   ├── models/
│   │   ├── bronze/
│   │   ├── silver/
│   │   └── gold/
│   │
│   ├── macros/
│   ├── snapshots/
│   ├── tests/
│   ├── analyses/
│   └── seeds/
│
├── pyproject.toml
├── main.py
└── README.md
```

---

# 🥉 Bronze Layer

Stores raw ingested data with minimal transformations.

Models:

* bronze_bookings
* bronze_hosts
* bronze_listings

---

# 🥈 Silver Layer

Cleans and standardizes data.

Tasks:

* Remove duplicates
* Handle null values
* Standardize formats
* Data validation

Models:

* silver_bookings
* silver_hosts
* silver_listings

---

# 🥇 Gold Layer

Business-ready analytical datasets.

Includes:

* Fact tables
* One Big Table (OBT)
* Aggregated metrics

---

# 🔥 Key Features

## Incremental Loading

Processes only new or updated records for better performance.

```sql
WHERE created_at > (
    SELECT MAX(created_at)
    FROM {{ this }}
)
```

---

## Slowly Changing Dimensions (SCD Type 2)

Tracks historical changes in data using dbt snapshots.

Example:

* Host profile changes
* Listing updates
* Booking modifications

---

## Custom dbt Macros

Reusable SQL logic for:

* Categorization
* Data cleaning
* Utility operations

---

## Data Quality Testing

Includes:

* Not null tests
* Unique tests
* Referential integrity checks
* Source validation

---

# ⚙️ Setup Instructions

## 1. Clone Repository

```bash
git clone <repository-url>
cd AWS_DBT_Snowflake
```

---

## 2. Create Virtual Environment

### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

### Linux / Mac

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

or

```bash
pip install -e .
```

---

# ❄️ Snowflake Configuration

Create:

```bash
~/.dbt/profiles.yml
```

Example:

```yaml
aws_dbt_snowflake_project:
  outputs:
    dev:
      type: snowflake
      account: <account-id>
      user: <username>
      password: <password>
      role: ACCOUNTADMIN
      database: AIRBNB
      warehouse: COMPUTE_WH
      schema: dbt_schema
      threads: 4

  target: dev
```

---

# ▶️ Running dbt

## Test Connection

```bash
dbt debug
```

---

## Run Models

```bash
dbt run
```

---

## Run Specific Layers

```bash
dbt run --select bronze.*
dbt run --select silver.*
dbt run --select gold.*
```

---

## Run Tests

```bash
dbt test
```

---

## Run Snapshots

```bash
dbt snapshot
```

---

## Generate Documentation

```bash
dbt docs generate
dbt docs serve
```

---

# 📊 Concepts Used

* Medallion Architecture
* ELT Pipelines
* Incremental Models
* SCD Type 2
* Data Warehousing
* Analytics Engineering
* Data Lineage
* Dimensional Modeling

---

# 🎯 Future Enhancements

* CI/CD pipeline integration
* Dashboard integration
* Monitoring & alerting
* Data quality dashboards
* Advanced business KPIs
* BI tool integration

---

# 👩‍💻 Author

Sachi Gadkari
B.Tech IT Student
Cloud & Full Stack Enthusiast

---

# 📚 Learning Goals

This project was built to explore:

* Modern data engineering workflows
* Cloud-native analytics systems
* dbt transformations
* Snowflake data warehousing
* Production-grade data pipelines

---

# 📝 License

This project is created for educational and portfolio purposes.

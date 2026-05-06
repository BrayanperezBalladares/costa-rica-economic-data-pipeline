# Costa Rica Economic Data Pipeline

## Overview

Costa Rica Economic Data Pipeline is an end-to-end data engineering project designed to ingest, validate, transform and serve public economic indicators from Costa Rica.

The project focuses on building a production-style pipeline using modern data engineering practices such as layered data architecture, data quality checks, orchestration, distributed processing and business intelligence reporting.

The first version of the project focuses on exchange rate indicators from Costa Rica, with the goal of expanding later into additional economic and social indicators.

---

## Business Problem

Companies that import products, manage pricing, analyze financial risk or operate in international markets need reliable and updated economic data.

In Costa Rica, exchange rate movements can directly affect:

- Product pricing
- Import costs
- Profit margins
- Financial planning
- Inventory decisions
- Business reporting

This project simulates a real-world data pipeline that allows a business team to monitor economic indicators daily and make data-driven decisions.

---

## Project Goals

The main goals of this project are:

- Extract public economic indicators from official Costa Rican data sources.
- Store raw data in a structured bronze layer.
- Clean and standardize the data into a silver layer.
- Build analytics-ready datasets in a gold layer.
- Apply data quality checks to detect missing values, duplicates and abnormal values.
- Orchestrate the pipeline using Airflow.
- Transform data using PySpark and Databricks.
- Serve the final data to a business intelligence dashboard.
- Document the complete pipeline for portfolio and professional purposes.

---

## Tech Stack

| Area | Technology |
|---|---|
| Programming Language | Python |
| Orchestration | Apache Airflow / Astronomer |
| Distributed Processing | Databricks + PySpark |
| Storage Format | Delta Lake |
| Data Quality | Great Expectations / Custom Checks |
| Visualization | Power BI / Metabase |
| Version Control | Git + GitHub |
| Environment Management | dotenv |
| Testing | Pytest |

---

## Data Sources

The initial version of this project will use public economic indicators from Costa Rica.

Planned sources:

- Banco Central de Costa Rica, BCCR
- Instituto Nacional de Estadística y Censos, INEC

Initial indicators:

- Exchange rate buy value
- Exchange rate sell value

Future indicators may include:

- Inflation
- Interest rates
- Employment indicators
- Consumer price index
- Economic activity indicators

---

## Architecture

The project follows a medallion architecture:

```text
Data Sources
    |
    v
Python Extractors
    |
    v
Bronze Layer
Raw data exactly as received from the source
    |
    v
Silver Layer
Cleaned, normalized and validated data
    |
    v
Gold Layer
Business-ready analytical datasets
    |
    v
Dashboard
Power BI / Metabase
```

---

## Data Layers

### Bronze Layer

The bronze layer stores raw data as received from the original source.

Example:

```text
data/bronze/bccr/exchange_rate/year=2026/month=05/day=06/
```

The goal of this layer is to preserve the original response for traceability and reprocessing.

### Silver Layer

The silver layer contains cleaned and standardized records.

Expected fields:

```text
date
indicator_code
indicator_name
currency
value
unit
source
extracted_at
loaded_at
```

### Gold Layer

The gold layer contains business-ready datasets for dashboards and analysis.

Expected fields:

```text
date
buy_rate
sell_rate
spread
average_rate
daily_change_buy
daily_change_sell
seven_day_moving_average_buy
seven_day_moving_average_sell
month
year
loaded_at
```

---

## Pipeline Flow

The expected pipeline flow is:

```text
1. Extract data from public APIs
2. Validate raw API response
3. Save raw data into the bronze layer
4. Transform bronze data into silver data
5. Run data quality checks
6. Build gold analytical tables
7. Publish dashboard-ready datasets
8. Log pipeline execution results
```

---

## Data Quality Checks

The project will include data quality checks such as:

- API response is not empty.
- Date field is not null.
- Indicator value is numeric.
- Exchange rate value is greater than zero.
- There are no duplicated records by date and indicator.
- Sell exchange rate is greater than or equal to buy exchange rate.
- Daily variation is within a reasonable business range.
- All expected indicators are available for the execution date.

---

## Repository Structure

```text
costa-rica-economic-data-pipeline/
│
├── dags/
│   └── Airflow DAGs
│
├── src/
│   ├── extractors/
│   │   └── API extraction logic
│   │
│   ├── loaders/
│   │   └── Data loading logic
│   │
│   ├── transformers/
│   │   └── Data transformation logic
│   │
│   ├── quality/
│   │   └── Data quality checks
│   │
│   └── utils/
│       └── Shared utilities
│
├── notebooks/
│   └── Exploratory notebooks
│
├── databricks/
│   └── Databricks PySpark jobs
│
├── data/
│   ├── bronze/
│   ├── silver/
│   └── gold/
│
├── tests/
│   └── Unit tests
│
├── docs/
│   └── Technical documentation
│
└── dashboard/
    └── Dashboard screenshots and notes
```

---

## Current Status

Project status:

```text
In progress — Week 1: repository setup and extraction layer design.
```

Current phase:

```text
Day 1 — Initial repository structure and README documentation.
```

---

## Roadmap

### Week 1

- Create GitHub repository.
- Define project structure.
- Write initial README.
- Research BCCR API.
- Build local Python extractor.
- Save raw data into bronze layer.
- Create first transformation script.

### Week 2

- Add data quality checks.
- Add Airflow DAG.
- Integrate Databricks.
- Build silver and gold layers.
- Create initial dashboard.
- Improve documentation.
- Publish project progress on LinkedIn.

---

## Future Improvements

Planned improvements:

- Add more BCCR indicators.
- Add INEC datasets.
- Add automated alerts for abnormal exchange rate changes.
- Add Great Expectations validations.
- Add CI checks with GitHub Actions.
- Add dashboard screenshots.
- Add AI-assisted data documentation.
- Deploy the pipeline using a cloud-based scheduler.

---

## Author

Created by Brayan as a professional data engineering portfolio project focused on real public data from Costa Rica.
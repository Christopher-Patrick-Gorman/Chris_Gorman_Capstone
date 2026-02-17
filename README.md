# TripleSeat Event Data Pipeline

## Overview
This project delivers a production-style ETL pipeline that converts complex TripleSeat event and lead data into a reliable analytics layer, enabling operational reporting and application integration.

The pipeline supports reporting on:  
• Event performance trends  
• Booking activity  
• Lead tracking and operational insights  

### Project Status
This repository represents the ingestion and transformation layer.

The current production architecture uses a MySQL operational store  
with a Flask API and React frontend maintained in a private repository.

---

## Key Features

• Automated API ingestion with pagination handling  
• Normalization of nested JSON into a relational schema  
• Incremental processing with idempotent upserts  
• Dual-target architecture (Snowflake warehouse + MySQL operational store)  
• Production scheduling via cron on a Linux VM  
• Separation of ingestion pipeline and application layer  

---

## Business Problem
Raw TripleSeat API responses contained nested JSON structures and inconsistent formats, making it difficult to create reliable analytics or support downstream applications.  

The goal of this project was to create a repeatable data pipeline that normalizes event data and makes it accessible for reporting and operational use.

---

## Solution
I designed a Python-based ETL pipeline that:

1. Authenticates with the TripleSeat API  
2. Extracts paginated event and lead data  
3. Normalizes nested JSON fields (rooms, locations)  
4. Loads structured data into Snowflake for analytics  
5. Enabled future incremental loading and application support through a MySQL implementation  

---

## Architecture Evolution

The project originally loaded transformed data into **Snowflake** as a warehouse for analytics.  
This version focused on batch ingestion and schema normalization.

As the project expanded, I introduced an application-oriented architecture to support incremental updates and interactive use of the data. This included:

• **MySQL** as the operational analytics database  
• **Flask backend** exposing REST endpoints  
• **React frontend** for data exploration  

The MySQL version supports incremental processing and upserts based on transaction GUIDs and last-modified timestamps.

The application layer is maintained in a separate private repository, while this repository focuses on the data ingestion and transformation pipeline.

---

## Architectural Decisions

• **Snowflake** was chosen initially for analytical flexibility and rapid schema iteration  
• **MySQL** was introduced to support low-latency application queries and incremental processing  
• **Cron scheduling** provided lightweight orchestration appropriate to pipeline complexity  
• **Separate repositories** were used to decouple ingestion logic from application code and improve maintainability  

---

## Deployment Context

The pipeline was deployed on a Linux-based Linode virtual machine.

API ingestion tasks were scheduled using cron, allowing the pipeline  
to run automatically on a recurring basis.

The Snowflake implementation used batch loads, while a later MySQL-based  
architecture introduced incremental processing with upsert logic based  
on transaction GUIDs and last-modified timestamps.

---

## Deployment & Orchestration

The pipeline is deployed on a **Linode virtual machine**, where scheduled jobs run via **cron** to automate data ingestion.

Operational characteristics:

• Scripts execute on a recurring schedule  
• Snowflake loads are batch-based  
• MySQL implementation supports incremental loads and upserts  
• Upsert logic uses transaction GUID and last-modified date  

---

## Tech Stack

Python • Pandas • REST APIs • OAuth  
Snowflake • MySQL  
Flask • React  
Cron • Linux • Linode VM  

---

## Architecture
![Architecture](docs/architecture.png)

---

## Data Flow

**Initial warehouse flow:**  
TripleSeat API → Python ETL → Snowflake → Analytics  

**Current operational flow:**  
TripleSeat API → Python ETL (cron on Linode) → MySQL → Flask API → React App  

---

## Example Output

| Metric | Description |
|--------|------------|
| Total Events | Count of all events |
| Room Utilization | Capacity vs attendance |
| Lead Tracking | Operational visibility into bookings |

---

## How to Run

### Configuration / Secrets

This project requires API and database credentials that are not included in the repository.

Credentials are stored locally in JSON files (ignored by git) and loaded at runtime.  
Example files (not committed):

- `TripleSeat_API/API_Key.json`
- `TripleSeat_API/API_Secret.json`
- `TripleSeat_API/SnowFlakeUser.json`
- `TripleSeat_API/SnowFlakePass.json`
- `TripleSeat_API/SnowFlakeAccount.json`

> Note: These files are excluded via `.gitignore` to prevent committing secrets.

### Steps

1. Configure environment variables  
2. Execute ETL scripts  
3. Data loads into Snowflake or MySQL depending on configuration  

---

## Key Learnings

• Designing idempotent ETL processes for API-based data sources  
• Modeling semi-structured JSON into analytics-friendly schemas  
• Tradeoffs between warehouse-first vs operational-store architectures  
• Implementing incremental ingestion using change tracking fields  
• Operationalizing pipelines with scheduling and environment isolation  

---

## Future Improvements

• Automated data quality checks  
• Pipeline monitoring and alerting  
• Containerized deployment  
• Enhanced API layer performance  


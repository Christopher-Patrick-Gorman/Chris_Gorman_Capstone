# TripleSeat Event Data Pipeline

## Overview
This project builds an automated data pipeline that extracts event and lead data from the TripleSeat API, transforms nested structures, and loads the data for analytics and application use.

The pipeline supports reporting on:
• Event performance trends  
• Booking activity  
• Lead tracking and operational insights  

### Project Status
This repository represents the ingestion and transformation layer.

The current production architecture uses a MySQL operational store
with a Flask API and React frontend maintained in a private repository.

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

## Configuration / Secrets

This project requires API and database credentials that are not included in the repository.

Credentials are stored locally in JSON files (ignored by git) and loaded at runtime.  
Example files (not committed):

- `TripleSeat_API/API_Key.json`
- `TripleSeat_API/API_Secret.json`
- `TripleSeat_API/SnowFlakeUser.json`
- `TripleSeat_API/SnowFlakePass.json`
- `TripleSeat_API/SnowFlakeAccount.json`

> Note: These files are excluded via `.gitignore` to prevent committing secrets.

1. Configure environment variables  
2. Execute ETL scripts  
3. Data loads into Snowflake or MySQL depending on configuration  

---

## Key Learnings

• Handling nested JSON structures  
• Pagination strategies for API ingestion  
• Warehouse schema design  
• Designing incremental data pipelines  
• Building application layers on top of analytical datasets  

---

## Future Improvements

• Automated data quality checks  
• Pipeline monitoring and alerting  
• Containerized deployment  
• Enhanced API layer performance  


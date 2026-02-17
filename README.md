# TripleSeat Event Data Pipeline

## Overview
This project builds an automated data pipeline that extracts event and lead data from the TripleSeat API, transforms nested structures, and loads the data into Snowflake for analytics and dashboarding.

The pipeline supports reporting on:
• Event performance trends  
• Booking activity  
• Lead conversion metrics  

## Business Problem
The organization needed a centralized dataset to track event performance and customer behavior. Raw API responses contained nested structures and inconsistent formats that made reporting difficult.

## Solution
I designed a Python-based ETL pipeline that:

1. Authenticates with the TripleSeat API
2. Extracts paginated event and lead data
3. Normalizes nested JSON fields (rooms, locations)
4. Loads structured data into Snowflake
5. Feeds downstream dashboards

## Architecture Evolution

The project originally loaded transformed data into Snowflake as a warehouse for analytics.

As the scope expanded, I introduced an application layer to enable direct interaction with the dataset. This included:

• MySQL as the operational analytics database  
• Flask backend exposing REST endpoints  
• React frontend for data exploration  

The application layer is maintained in a separate private repository, while this repository focuses on the data ingestion and transformation pipeline.

## Tech Stack
Python • Pandas • REST APIs • OAuth • Snowflake • Cron Scheduling

## Architecture
![Architecture](docs/architecture.png)

## Data Flow
API → Python ETL → Snowflake → BI Dashboard

## Example Output
| Metric | Description |
|--------|------------|
| Total Events | Count of all events |
| Room Utilization | Capacity vs attendance |
| Lead Conversion | Leads → bookings |

## How to Run
1. Add environment variables
2. Run pipeline script
3. Data loads into Snowflake

## Key Learnings
• Handling nested JSON structures  
• Pagination strategies  
• Warehouse schema design  

## Future Improvements
• Incremental loads  
• Error logging  
• Data quality checks  

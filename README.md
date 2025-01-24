# -ETL-project-
ETL Data Pipeline Implementation Using AWS Glue, S3, and Athena.
# ETL Data Pipeline Implementation Using AWS Glue

![image](https://github.com/user-attachments/assets/31113570-c33a-4d62-a8ab-3497c8659c8a)

## Project Overview
This project demonstrates the implementation of an ETL pipeline for processing airline, airport, and flight data using AWS Glue, S3, and Athena. It automates data ingestion, transformation, and querying to generate insights for operational analysis.

## Tools & Technologies
- **AWS Glue**: Used for data transformation and job orchestration.
- **Amazon S3**: Served as the raw and curated data storage.
- **Athena**: Enabled querying and visualization of the curated data.
- **SQL**: For data transformations and aggregation in Athena.
- **IAM**: To manage secure access to AWS resources.

## Features
1. **Data Sources**:
   - Airline, airport, and flight data stored in S3.
   - Raw data ingested into AWS Glue for further processing.

2. **ETL Workflow**:
   - Crawlers: Automatically discover raw data schemas and create Glue tables.
   - ETL Jobs: Join and transform datasets with SQL queries.
   - Output: Store curated data in S3 for reporting.
![image](https://github.com/user-attachments/assets/7a66d90b-d29c-44c2-84a0-0c64b593af89)
![image](https://github.com/user-attachments/assets/c454d57b-5363-4ff3-bd03-59b1fededa19)
![image](https://github.com/user-attachments/assets/9ae422d2-519b-4293-8979-af634dc34b87)

3. **Athena Analysis**:
   - Created tables for curated data.
   - Generated insights using SQL queries, such as flight counts by airline and airport.

## Steps to Reproduce
### 1. Setup
- Create AWS Glue Database: `studentID_assignment5_db`.
- Set up S3 buckets:
  - `studentID-assignment5-raw-bucket`
  - `studentID-assignment5-curated-bucket`

### 2. Data Ingestion
- Upload `.csv` files into respective folders (`airlines`, `airports`, `flights`) in the raw bucket.

### 3. Crawlers
- Configure and run Glue Crawlers for each dataset.
- Verify the creation of raw tables in the Glue database.


![image](https://github.com/user-attachments/assets/2fec11d2-0a40-486c-9bc8-ed012f8a56e0)

![image](https://github.com/user-attachments/assets/987557bd-bb4a-40de-bfc9-4ff5d9aefae8)

### 4. ETL Job
- Use Glue Studio to:
  - Add source nodes for raw data.
  - Join tables using SQL:
    ```sql
    SELECT 
        al.airline, 
        ap.airport, 
        fl.month, 
        COUNT(*) AS flt_cnt
    FROM fl
    JOIN ap ON (fl.origin_airport = ap.iata_code)
    JOIN al ON (fl.airline = al.iata_code)
    WHERE day_of_week IN (1, 2, 3, 4, 5)
    GROUP BY al.airline, ap.airport, fl.month;
    ```
  - Output results to the curated bucket.

### 5. Athena Queries
- Load the curated data into Athena.
- Run SQL queries to generate insights (see `SQL/Athena_Queries.sql`).

![image](https://github.com/user-attachments/assets/f9a49c70-1cad-43d0-80e0-17b010591d0b)

![image](https://github.com/user-attachments/assets/66339a67-f827-453c-a083-adc0a6b49d25)

![image](https://github.com/user-attachments/assets/57e1f369-8c5f-4df4-b1d6-6f5dd6182511)

## Deliverables
- **ETL Pipeline**: End-to-end automation from raw data ingestion to curated data output.
- **Insights**: Flight counts by airlines and airports, trends, and analytics.
- **Screenshots**: Include key configurations and execution results.

## Results
- Successfully processed and curated datasets for querying.
- Improved efficiency in analyzing airline operations using AWS services.

## Repository Contents
- `SQL/`: Contains SQL scripts used in Athena.
- `Scripts/`: Glue job scripts or configurations.
- `Resources/`: Sample data files used for testing.
- `Screenshots/`: Visuals showcasing the ETL process and results.



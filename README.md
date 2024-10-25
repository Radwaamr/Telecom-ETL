# Telecom-ETL-SSIS

## Overview

This project is an **ETL (Extract, Transform, Load)** solution designed for a telecom company, created using **SQL Server Integration Services (SSIS)**. The project processes telecom event data stored in `.csv` files, transforming it based on business rules, and loading it into a target database.

## Project Structure

- **Data Sources**: Input files are `.csv` files containing telecom event data. These files are processed in batches, and each batch contains key telecom data like IMSI, IMEI, CELL, LAC, EVENT_TYPE, and EVENT_TS (timestamp).
  
- **ETL Process**:
  - **Extraction**: Reads `.csv` files stored in a specified folder. Files are processed in batches every 5 minutes.
  - **Transformation**: Implements several data cleaning and transformation steps, including:
    - Null value checks for IMSI, CELL, LAC.
    - Parsing the IMEI into two separate fields.
    - Validating timestamp format.
    - Rejecting invalid records and logging them into a separate table.
  - **Loading**: Loads the transformed data into a target database table (`dim_audit`), ensuring data quality through validation checks.

## Key Features

1. **Data Transformation**:
    - IMSI values are checked for null values, and rejected if null.
    - IMEI is split into two columns (`TAC` and `SNR`) for further analysis.
    - Ensures all timestamps are in the `YYYY-MM-DD HH:MM:SS` format.
  
2. **Data Validation**:
    - Invalid records are rejected and stored in a separate file for further inspection.
    - Regular quality checks ensure the correct number of records is processed and loaded.

3. **Error Handling**:
    - Failed or rejected records are logged in a separate table.
    - All operations are recorded in an audit table for tracking.

## File Structure

- `.dtsx`: SSIS package files containing the ETL logic.
- `.dtproj`: SSIS project file.
- `.sln`: Visual Studio solution file for the project.

## How to Run the Project

1. Ensure **SQL Server Integration Services (SSIS)** is installed and configured.
2. Clone the repository and open the solution in **SQL Server Data Tools (SSDT)** or **Visual Studio** with SSIS integration.
3. Adjust the connection strings and folder paths in the package to match your environment.
4. Execute the package to start processing the telecom data.

## Data Fields

| Column       | Description                                |
|--------------|--------------------------------------------|
| ID           | Unique identifier for each transaction     |
| IMSI         | Subscriber identifier                      |
| IMEI         | Device identifier                          |
| CELL         | Cell tower ID                              |
| LAC          | Location Area Code                         |
| EVENT_TYPE   | Type of telecom event                      |
| EVENT_TS     | Event timestamp                            |




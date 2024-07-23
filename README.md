# Logistics-Data-Management
## Overview
This project demonstrates a data pipeline that uses GCP Storage, Apache Airflow, Hive, and Dataproc to handle and process data files. The pipeline is triggered when a new file is detected in GCP Storage. It then creates and manages Hive tables, inserts data from the external table into a partitioned table, moves the processed file to an archive directory, and re-triggers the pipeline for continuous processing.

## Architecture
- **GCP Storage**: Stores raw data files and archived files.
- **Apache Airflow**: Orchestrates the workflow and manages task execution.
- **Hive**: Manages the external and partitioned tables, executes data operations.
- **Datapro**c: Provides the environment for running Hive queries and managing big data operations.
- **Sensors and Operators**:
  - **GCSObjectsWithPrefixExistenceSenso**r: Detects the arrival of new files in GCP Storage.
  - **Hive Operators**:
    - Create an external table from the GCP Storage path.
    - Create a partitioned table if it does not already exist.
    - Insert records from the external table into the partitioned table.
    - BashOperator: Moves the file from the raw directory to the archive directory in GCP Storage.
    - TriggerDagRunOperator: Re-triggers the DAG to ensure continuous processing.

## License

This project is licensed under the [MIT License](LICENSE).

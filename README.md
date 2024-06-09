# Databricks Overview

## Cluster Types

### All-purpose Clusters
- Designed for collaborative use, such as ad hoc analysis, data exploration, and development.
- Multiple users can share these clusters.
- Cost-effective for tasks that benefit from resource sharing.
- May not guarantee immediate availability due to resource sharing.

### Job Clusters
- Specifically for running automated jobs.
- Terminate once the job is completed, reducing resource usage and cost.
- Dedicated to a specific task and optimized for performance.
- More suitable for workflows with strict Service Level Agreements (SLAs).

| Aspect          | All-purpose Clusters                                         | Job Clusters                                               |
|-----------------|--------------------------------------------------------------|------------------------------------------------------------|
| SLA Requirements| Versatile but less predictable for strict SLAs               | Dedicated and optimized for performance                    |
| Resource Usage  | Cost-effective for exploration and development tasks         | Efficient for time-sensitive tasks, releasing resources promptly |
| Trade-offs      | Flexibility but potential delay due to resource sharing      | Prioritizes specific jobs but higher resource costs        |

![Cluster Types](https://github.com/Psingh12354/databricks/assets/55645997/cd21c411-5fdc-4399-8c6b-b111b2120964)

## Databricks Lakehouse
- Combines the advantages of Data Lakes and Data Warehouses.
- Stores data in Parquet format and transaction logs in JSON format.

## Utilities
- `dbutils`: Module for interacting with Databricks.
  - `dbutils.help()`: Lists available modules.
  - `dbutils.fs.help()`: Provides file system utilities, e.g., `dbutils.fs.ls('path')`.

## Database Commands
- `describe database db_name;`: Retrieves the location of a database.
- `spark.Table`: Registers a table through SparkSession.
- `DESCRIBE DATABASE` or `DESCRIBE SCHEMA`: Returns metadata of a database.

![Edit History](https://github.com/Psingh12354/databricks/assets/55645997/952d2198-8a0f-4fbf-8148-c022ae6114cf)

## Delta Lake
- Builds upon standard data formats.
- VACUUM command: Deletes unused data files older than a specified retention period.
- Supports ACID transactions and scalable metadata handling.
- Delta tables store data in Parquet format with transaction logs in JSON format.

## Databricks Repos
- Supports Git operations like pull, fetch, and manage branches.
- Useful for managing development work and versioning.

## Data Exploration
- `dbfs:/user/hive/warehouse/db_hr.db`: Default location for databases.
- PIVOT: Transforms rows into columns for better readability.
- `CREATE TABLE USING`: Creates external tables from external data sources (e.g., CSV).
- `CREATE SCHEMA`: Alias for `CREATE DATABASE`.

## Spark Structured Streaming
- `trigger(availableNow=True)`: Runs the stream in batch mode and stops after processing available data.
- Auto Loader: Tracks discovered files using checkpointing for exactly-once ingestion guarantees.
- Default processing interval: `trigger(processingTime="500ms")`.

## Delta Live Tables (DLT)
- Enables creating streaming live tables using the `STREAM()` function.
- Use `COMMENT "Contains PII"` to indicate that a new table includes personally identifiable information (PII).

## Data Ingestion
- COPY INTO: Suitable for ingesting thousands of files.
- Auto Loader: Preferred for ingesting millions of files or more and handles schema evolution.

## Databricks Jobs
- Orchestrates data processing tasks in a Directed Acyclic Graph (DAG).
- Allows repairing failed multi-task jobs by rerunning only the unsuccessful tasks and their dependents.
- `MERGE` command: Writes data into Delta tables while avoiding duplicate records.

## User-Defined Functions (UDF)
```sql
CREATE FUNCTION blue() RETURNS STRING COMMENT 'Blue color code' LANGUAGE SQL RETURN '0000FF';
```

## Querying Data
- `spark.readStream`: Reads streaming data.
- `SELECT * FROM file_format.'path.type'`: Queries a table using file format and path.
- `CREATE TABLE table_name DEEP CLONE source_table`: Creates a deep clone of a table.
- `CREATE TABLE table_name SHALLOW CLONE source_table`: Creates a shallow clone of a table.

## Databricks SQL
- `Data Explorer`: Manages data object permissions.
- View types:
  - Standard view: `CREATE VIEW view_name AS query`
  - Temporary view: `CREATE TEMP VIEW view_name AS query`
  - Global temporary view: `CREATE GLOBAL TEMP VIEW view_name AS query`

## Medallion Architecture
- **Gold tables**: Refined data suitable for business reporting (e.g., BI dashboards).
- **Silver tables**: Cleansed and conformed data.
- **Bronze tables**: Raw data with minimal transformation.
- **Raw data**: Unprocessed data directly ingested from source systems.

![Medallion Architecture](https://github.com/Psingh12354/databricks/assets/55645997/168f3c24-4555-4c99-98c9-498c5c0aec20)

## Sample Query
- The query below is in the Bronze layer, reading data from cloud storage into an uncleaned orders table.

```python
(spark.readStream
        .format("cloudFiles")
        .option("cloudFiles.format", "json")
        .load(ordersLocation)
     .writeStream
        .option("checkpointLocation", checkpointPath)
        .table("uncleanedOrders")
)
```

## Connecting to GitHub
- Follow the steps outlined in [Databricks documentation](https://docs.databricks.com/en/repos/get-access-tokens-from-git-provider.html).

## Parquet File Format
- Parquet is a columnar storage file format, preferred for its efficiency in data storage and retrieval.
- [Learn more about Parquet](https://towardsdatascience.com/demystifying-the-parquet-file-format-13adb0206705).

## Time Travel
- `DESCRIBE HISTORY employees`: Retrieves history and version details of a table.
- Query nested data (e.g., JSON): `SELECT customer_id, profile:name FROM customer`.

![Time Travel](https://github.com/Psingh12354/databricks/assets/55645997/556df0d5-16f0-4c99-8451-a0ac7f8929a3)

![Garbage Collection](https://github.com/Psingh12354/databricks/assets/55645997/380852bc-a8a8-42d4-8634-a7e86e88216f)

## Querying Table Details
- `DESCRIBE DETAILS tablename`: Retrieves all details about the given table.

## Triggers in Spark Structured Streaming
- `.trigger(once=True)`: Processes one batch of data.
- `.trigger(availableNow=True)`: Processes data immediately.
- `.trigger(processingTime='60 minutes')`: Sets a 1-hour processing interval.

## Managing Data Quality with DLT
- Expectations apply data quality checks on each record passing through a query.

![DLT Data Quality](https://github.com/Psingh12354/databricks/assets/55645997/52d5c201-34d7-460a-b591-f2bd5b82ebd6)

## Reading Data from DLT
```python
spark.readStream.table("table_name")
```

## Auto Loader
- Incrementally processes new data files as they arrive in cloud storage.
- Provides a Structured Streaming source called cloudFiles.

## Creating Tables in Databricks
```sql
-- Creates a Delta table
CREATE TABLE student (id INT, name STRING, age INT);

-- Use data from another table
CREATE TABLE student_copy AS SELECT * FROM student;

-- Creates a CSV table from an external directory
CREATE TABLE student USING CSV LOCATION '/mnt/csv_files';

-- Specify table comment and properties
CREATE TABLE student (id INT, name STRING, age INT)
    COMMENT 'this is a comment'
    TBLPROPERTIES ('foo'='bar');

-- Create partitioned table
CREATE TABLE student (id INT, name STRING, age INT)
    PARTITIONED BY (age);

-- Create a table with a generated column
CREATE TABLE rectangles(a INT, b INT, area INT GENERATED ALWAYS AS (a * b));
```

## UDF Example
```sql
CREATE FUNCTION convert_f_to_c(unit STRING, temp DOUBLE)
RETURNS DOUBLE
RETURN CASE
  WHEN unit = "F" THEN (temp - 32) * (5/9)
  ELSE temp
END;

SELECT convert_f_to_c(unit, temp) AS c_temp
FROM tv_temp;
```

## Set Operators
- Demonstrating set operators using `number1` and `number2` tables.

```sql
CREATE TEMPORARY VIEW number1(c) AS VALUES (3), (1), (2), (2), (3), (4);
CREATE TEMPORARY VIEW number2(c) AS VALUES (5), (1), (1), (2);

SELECT c FROM number1 EXCEPT SELECT c FROM number2;
SELECT c FROM number1 MINUS SELECT c FROM number2;
SELECT c FROM number1 EXCEPT ALL SELECT c FROM number2;
SELECT c FROM number1 MINUS ALL SELECT c FROM number2;
SELECT c FROM number1 INTERSECT SELECT c FROM number2;
SELECT c FROM number1 UNION SELECT c FROM number2;
```

## Filter vs Transform
```sql
SELECT filter(array(1, 2, 3, 4), i -> i % 2 == 0);  -- Result
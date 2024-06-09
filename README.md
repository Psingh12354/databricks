## Databricks Overview

### Cluster Types

1. **All-purpose Clusters:**
   - Used for ad hoc analysis, data exploration, and development.
   - Designed for collaborative use, allowing multiple users to share the cluster.
   - Cost-effective for tasks that benefit from resource sharing.
   - May not provide the same level of predictability in meeting strict Service Level Agreements (SLAs).

2. **Job Clusters:**
   - Dedicated to running automated jobs and terminate once the job is completed.
   - Optimized for performance and meeting strict SLAs.
   - More efficient for focused, time-sensitive tasks, as they release resources promptly after completion.
   - Higher resource costs compared to all-purpose clusters.

### Databricks Lakehouse

- Combines the advantages of data lakes and data warehouses.
- Stores data in Parquet format and transaction logs in JSON format.
- Supports schema enforcement and time travel.

### Utilities

- `dbutils`: Provides a set of utilities to interact with Databricks.
  - `dbutils.help()`: Lists available modules.
  - `dbutils.fs.help()`: Lists file system utilities, e.g., `dbutils.fs.ls('path')`.

### Database Commands

- `describe database db_name;`: Retrieves the location of a database.
- `spark.Table`: Registers a table through SparkSession.
- `DESCRIBE DATABASE` or `DESCRIBE SCHEMA`: Returns metadata of a database, including name, comment, and location on the filesystem.

### Delta Lake

- Builds upon standard data formats.
- VACUUM command: Deletes unused data files older than a specified retention period.
- Supports ACID transactions and scalable metadata handling.
- Delta tables store data in Parquet format with transaction logs in JSON format.

### Databricks Repos

- Supports Git operations like pull, fetch, and manage branches.
- Useful for managing development work and versioning.

### Data Exploration

- `dbfs:/user/hive/warehouse/db_hr.db`: Default location for databases.
- PIVOT: Transforms rows into columns for better readability.
- `CREATE TABLE USING`: Creates external tables from external data sources (e.g., CSV).
- `CREATE SCHEMA`: Alias for `CREATE DATABASE`.

### Spark Structured Streaming

- `trigger(availableNow=True)`: Runs the stream in batch mode and stops after processing available data.
- Auto Loader: Tracks discovered files using checkpointing for exactly-once ingestion guarantees.
- Default processing interval: `trigger(processingTime="500ms")`.

### Delta Live Tables (DLT)

- Enables creating streaming live tables using the `STREAM()` function.
- Use `COMMENT "Contains PII"` to indicate that a new table includes personally identifiable information (PII).

### Data Ingestion

- COPY INTO: Suitable for ingesting thousands of files.
- Auto Loader: Preferred for ingesting millions of files or more and handles schema evolution.

### Databricks Jobs

- Orchestrates data processing tasks in a Directed Acyclic Graph (DAG).
- Allows repairing failed multi-task jobs by rerunning only the unsuccessful tasks and their dependents.
- `MERGE` command: Writes data into Delta tables while avoiding duplicate records.

### User-Defined Functions (UDF)

- Create UDFs using SQL syntax.
  ```sql
  CREATE FUNCTION blue() RETURNS STRING COMMENT 'Blue color code' LANGUAGE SQL RETURN '0000FF';
  ```

### Querying Data

- `spark.readStream`: Reads streaming data.
- `SELECT * FROM file_format.'path.type'`: Queries a table using file format and path.
- `CREATE TABLE table_name DEEP CLONE source_table`: Creates a deep clone of a table.
- `CREATE TABLE table_name SHALLOW CLONE source_table`: Creates a shallow clone of a table.

### Databricks SQL

- `Data Explorer`: Manages data object permissions.
- View types:
  - Standard view: `CREATE VIEW view_name AS query`
  - Temporary view: `CREATE TEMP VIEW view_name AS query`
  - Global temporary view: `CREATE GLOBAL TEMP VIEW view_name AS query`

### Medallion Architecture

- **Gold tables**: Refined data suitable for business reporting (e.g., BI dashboards).
- **Silver tables**: Cleansed and conformed data.
- **Bronze tables**: Raw data with minimal transformation.
- **Raw data**: Unprocessed data directly ingested from source systems.

### Connecting to GitHub

- Follow the steps outlined in [Databricks documentation](https://docs.databricks.com/en/repos/get-access-tokens-from-git-provider.html).

### Parquet File Format

- Parquet is a columnar storage file format.
- Preferred for its efficiency in data storage and retrieval.

### Time Travel

- `DESCRIBE HISTORY employees`: Retrieves history and version details of a table.
- Query nested data (e.g., JSON): `SELECT customer_id, profile:name FROM customer`.

### Triggering Execution

- `.trigger(once=True)`: Processes one batch of data.
- `.trigger(availableNow=True)`: Processes data immediately.
- `.trigger(processingTime='60 minutes')`: Sets a 1-hour processing interval.

### Managing Data Quality with DLT

- Expectations apply data quality checks on each record passing through a query.

### Auto Loader

- Automatically processes new files in cloud storage with options for schema inference and evolution.

### Creating Tables

- SQL commands to create various types of tables and specify comments and properties.

### Set Operators

- Demonstrates the use of set operators like `EXCEPT`, `MINUS`, `INTERSECT`, and `UNION` on tables.

### Transformations and Filters

- `filter` and `transform` functions for manipulating arrays.
  ```sql
  SELECT filter(array(1, 2, 3, 4), i -> i % 2 == 0);
  SELECT transform(array(1, 2, 3, 4), i -> i * 2);
  ```

### Alert Destinations

- Supported destinations: Email, Slack, Webhook, MS Teams, PagerDuty.

This summary covers key aspects of Databricks, including cluster types, Delta Lake, Databricks Repos, Structured Streaming, and various commands and utilities for managing and processing data.
# databricks

Based on Apache Spark

### Cluster

- All-purpose clusters, such as ad hoc analysis, data exploration, and development, are designed for collaborative use. Multiple users can share them.
On the other hand, job clusters are specifically for running automated jobs. They terminate once the job is completed, reducing resource usage and cost.
SLA Requirements:

- A job cluster might be more suitable if your workflow requires meeting a strict Service Level Agreement (SLA). Job clusters are dedicated to a specific task and can be optimized for performance.
All-purpose clusters, while versatile, may not provide the same level of predictability in meeting SLAs.
Resource Usage and Cost:

- All-purpose clusters are more cost-effective for tasks like exploration and development, where resource sharing is beneficial.
Job clusters are more efficient for focused, time-sensitive tasks, as they release resources promptly after completion.
Trade-offs:

- All-purpose clusters allow flexibility but may not guarantee immediate availability due to resource sharing.
Job clusters prioritize your specific job but come with higher resource costs.

<img width="531" alt="image" src="https://github.com/Psingh12354/databricks/assets/55645997/cd21c411-5fdc-4399-8c6b-b111b2120964">

- Lakehouse contain positive aspect of Data Lake & Data Warehouse.
- ```dbutils.help()``` this module help in getting list of module to interact with databricks.
- ```dbutils.fs.help()``` this module provide utilitties which interact with file system. ___eg :___ dbutils.fs.ls('path')
- To revise or move back to last change or any previous changes you can click on below **last edit....**
<img width="649" alt="image" src="https://github.com/Psingh12354/databricks/assets/55645997/952d2198-8a0f-4fbf-8148-c022ae6114cf">

- To get the location of database use this command```descibe database db_name;```
- ```spark.Table``` to registered table through SparkSession.
- The VACUUM command deletes the unused data files older than a specified data retention period.
- Delta Lake builds upon standard data formats. Delta lake table gets stored on the storage in one or more data files in Parquet format, along with transaction logs in JSON format.
- Databricks Repos supports git Pull operation. It is used to fetch and download content from a remote repository and immediately update the local repo to match that content.
- According to the Databricks Lakehouse architecture, the storage account hosting the customer data is provisioned in the data plane in the Databricks customer's cloud account.
- One advantage of Databricks Repos over the built-in Databricks Notebooks versioning is that Databricks Repos supports creating and managing branches for development work.
- The DESCRIBE DATABASE or DESCRIBE SCHEMA returns the metadata of an existing database (schema). The metadata information includes the database’s name, comment, and location on the filesystem. If the optional EXTENDED option is specified, database properties are also returned.
- ```dbfs:/user/hive/warehouse/db_hr.db``` in this we created a db_hr database under default location
- PIVOT transforms the rows of a table by rotating unique values of a specified column list into separate columns. In other words, It converts a table from a long format to a wide format.
- ```CREATE TABLE USING``` allows to specify an external data source type like CSV format, and with any additional options. This creates an external table pointing to files stored in an external location.
- ```CREATE SCHEMA``` is an alias for ```CREATE DATABASE``` statement. While usage of SCHEMA and DATABASE is interchangeable, SCHEMA is preferred.
- CREATE TABLE AS SELECT statements, or CTAS statements create and populate Delta tables using the output of a SELECT query. CTAS statements automatically infer schema information from query results and do not support manual schema declaration.
- In Spark Structured Streaming, we use ```trigger(availableNow=True)``` to run the stream in batch mode where it processes all available data in multiple micro-batches. The trigger will stop on its own once it finishes processing the available data.
- Auto Loader keeps track of discovered files using checkpointing in the checkpoint location. Checkpointing allows Auto loader to provide exactly-once ingestion guarantees.
- By default, if you don’t provide any trigger interval, the data will be processed every half second. This is equivalent to ```trigger(processingTime=”500ms")```
- In DLT pipelines, You can stream data from other tables in the same pipeline by using the ```STREAM()``` function. In this case, you must define a streaming live table using CREATE STREAMING LIVE TABLE syntax.
Remember: to query another live table, prepend always the LIVE. keyword to the table name.
```
CREATE STREAMING LIVE TABLE table_name
AS
    SELECT *
    FROM STREAM(LIVE.another_table)
```
- To successfully complete the task and indicate that the new table includes personally identifiable information (PII), the correct line of code to fill in the blank is: ```COMMENT “Contains PII”```
### When to use copy into or Auto Loader
- If you’re going to ingest files in the order of thousands, you can use COPY INTO. If you are expecting files in the order of millions or more over time, use Auto Loader.
- If your data schema is going to evolve frequently, Auto Loader provides better primitives around schema inference and evolution.
  
- Databricks Jobs allow to orchestrate data processing tasks. This means the ability to run and manage multiple tasks as a directed acyclic graph (DAG) in a job.
- You can repair failed multi-task jobs by running only the subset of unsuccessful tasks and any dependent tasks. Because successful tasks are not re-run, this feature reduces the time and resources required to recover from unsuccessful job runs.
- To write data into a Delta table while avoiding the writing of duplicate records, you can use the ```MERGE``` command
- To define UDF in sql use below like query ```CREATE FUNCTION blue() RETURNS STRING COMMENT 'Blue color code' LANGUAGE SQL RETURN '0000FF';```
- The COPY INTO statement is generally used to copy data from files or a location into a table. If the data engineer runs this statement daily to copy the previous day’s sales into the "transactions" table and the number of records hasn't changed after today's execution, it's possible that the data from today's file might not have differed from the data already present in the table.
- spark.readStream is a method in Apache Spark used for reading streaming data. It returns a DataStreamReader that can be used to read data streams as a streaming DataFrame. This is particularly useful for incremental data processing (streaming) - when you read input data, Spark determines what new data were added since the last read operation and processes only them
- To schedule a job to run once per day you need to use Quartz Cron. Cron syntax specifies a time in the format <seconds> <minutes> <hours> <day-of-month> <month> <day-of-week>. Numbers are used for the values and special characters can be used for multiple values.
- A data engineer needs to create a table in Databricks using data from their organization’s existing SQLite database ```org.apache.spark.sql.jdbc```
- Default location of storage ```dbfs:/user/hive/warehouse```
- To create a new table all_transactions that contains all records from march_transactions and april_transactions without duplicate records, you should use the UNION operator, as shown in option B. This operator combines the result sets of the two tables while automatically removing duplicate records.
- The reason why the data files still exist while the metadata files were deleted is because the table was external. When a table is external in Spark SQL (or in other database systems), it means that the table metadata (such as schema information and table structure) is managed externally, and Spark SQL assumes that the data is managed and maintained outside of the system. Therefore, when you execute a DROP TABLE statement for an external table, it removes only the table metadata from the catalog, leaving the data files intact. On the other hand, for managed tables (option E), Spark SQL manages both the metadata and the data files. When you drop a managed table, it deletes both the metadata and the associated data files, resulting in a complete removal of the table.
- A table in a database allows you to store structured data persistently. It provides a physical representation of data, and other users can query, modify, and analyze it. Unlike temporary views, tables are durable and can be accessed across sessions and users. By creating a table, the data engineer ensures that the data is stored and can be efficiently utilized by others.
- ```spark.table()``` function returns the specified Spark SQL table as a PySpark DataFrame
- MERGE INTO allows to merge a set of updates, insertions, and deletions based on a source table into a target Delta table. With MERGE INTO, you can avoid inserting the duplicate records when writing into Delta tables.
- To query a table u can use ```Select * from file_format.`path.type` ```. In this we can pass whole path or just give the folder location and run all the files together, or just give ```path/*.type```
- To make a copy of delta table we have two options : Deep Clone & Shadow Clone.
- Deep Clone copies full data + metadata from source to target. ```Create table table_name deep clone source_table```
- Shallow Clone create copy of table by just coping Delta connection logs. ```Create table table_name shallow clone source_table```
- ```Data Explorer``` in Databricks SQL allows you to manage data object permissions. This includes granting privileges on tables and databases to users or groups of users.
- View is the virtual table which doesn't have any existence. In databricks it's classiedmfied in 3 types.
- ```Create view view_name as query``` it's a common view.
- Temporary view work base on sparksession when it calls it started and when session closed view closed. ```Create temp view view_name as query```
- Global temporary view is based on cluster. ```Create global temp view view_name as query```
- In summary, Gold tables contain valuable whose output goes to dashboard like BI, refined data that is suitable for business reporting, while Silver tables provide a cleansed and conformed view of key business entities, bronze add schema to tables, and raw data is unprocessed data.[For More details](https://www.databricks.com/glossary/medallion-architecture)
<img width="692" alt="image" src="https://github.com/Psingh12354/databricks/assets/55645997/168f3c24-4555-4c99-98c9-498c5c0aec20">
- Below query is in bronze layer becuase if u see it's reading data from some cloud and target table name is uncleaned order with this you can guess it's a silver layer.
```
(spark.readStream
        .format("cloudFiles")
        .option("cloudFiles.format", "json")
        .load(ordersLocation)
     .writeStream
        .option("checkpointLocation", checkpointPath)
        .table("uncleanedOrders")
)```

- Steps required to connect through github [steps](https://docs.databricks.com/en/repos/get-access-tokens-from-git-provider.html)
- To know why we use Parquet & what is Column orient, Row oriented and Hybrid Architecture [Link](https://towardsdatascience.com/demystifying-the-parquet-file-format-13adb0206705)
- ```DESCRIBE DETAILS tablename``` to get all the details about the given table.
### Time Travel
- ```DESCRIBE HISTORY employees``` to get history of given table including version details.
- If supposed one column have nested data like json, we can use databricks inbuilt approach to traverse it ```select customer_id,profile:name from customer``` Here profile is Column inside we have json key as name.

<img width="387" alt="image" src="https://github.com/Psingh12354/databricks/assets/55645997/556df0d5-16f0-4c99-8451-a0ac7f8929a3">
<img width="365" alt="image" src="https://github.com/Psingh12354/databricks/assets/55645997/a0b59c7b-0af7-41e8-9c36-2f237dd6739a">
<img width="224" alt="image" src="https://github.com/Psingh12354/databricks/assets/55645997/b9d469a0-c156-4c2c-8630-f65e442fa4ee">
- Garbage collection
<img width="410" alt="image" src="https://github.com/Psingh12354/databricks/assets/55645997/380852bc-a8a8-42d4-8634-a7e86e88216f">



  
- QUARINTINE tABLE
- Optimize(Incredibly small data)
- Data in Delta table stored in Parquet table
- Pivot use to convert table from long format to wide format
- View can be accessed by different session but temp view can't.
- ```filter(expr, func)```Here filter tooks 2 param one is array as expression and 2nd is func example code ```SELECT filter(array(1, 2, 3), x -> x % 2 == 1);```
- ```dbfs:/user?hive/warehouse```  where database stored.

- JSON data is text based format
### Trigger
- ```.trigger(once=True)``` is supposed to process only one patch of data.
- ```.trigger(availableNow=True)``` setting is used for incremental batch processing in Structured Streaming it help in processing data immediately.
- To run any query in micro-batch use trigger.
- To have an up and running job with a 1-hour processing interval; ```.trigger(processingTime='60 minutes')```
  
| Aspect                | Triggered Execution      | Continuous Execution    | Development         | Production          |
|-----------------------|--------------------------|-------------------------|---------------------|---------------------|
| Execution Trigger     | Event-driven             | Continuous data arrival | N/A                 | N/A                 |
| Processing Characteristics | Batch or near-real-time | Real-time processing    | Iterative development & testing | Stable, optimized execution |
| Environment           | N/A                      | N/A                     | Interactive notebooks or development environments | Dedicated clusters optimized for performance |
| Resource Allocation   | N/A                      | N/A                     | Limited resources for experimentation and testing | Dedicated resources for stable and scalable execution |

This table outlines the differences between triggered execution, continuous execution, development, and production stages in Databricks across various aspects such as execution trigger, processing characteristics, environment, and resource allocation.

### Manage data quality with DLT
Expectations are optional clauses you add to Delta Live Tables dataset declarations that apply data quality checks on each record passing through a query.
<img width="691" alt="image" src="https://github.com/Psingh12354/databricks/assets/55645997/52d5c201-34d7-460a-b591-f2bd5b82ebd6">

### To read data from DLT
- ```spark.readStream.table("table_name")```

### Auto loader
Auto Loader incrementally and efficiently processes new data files as they arrive in cloud storage without any additional setup.
- Auto Loader provides a Structured Streaming source called cloudFiles. Given an input directory path on the cloud file storage, the cloudFiles source automatically processes new files as they arrive, with the option of also processing existing files in that directory. Auto Loader has support for both Python and SQL in Delta Live Tables.
- To pass a comment we have follow below structure

```
CREATE TABLE payments
COMMENT "This table contains sensitive information"
AS SELECT * FROM bank_transactions
```

### Create table in DB
```
-- Creates a Delta table
> CREATE TABLE student (id INT, name STRING, age INT);

-- Use data from another table
> CREATE TABLE student_copy AS SELECT * FROM student;

-- Creates a CSV table from an external directory
> CREATE TABLE student USING CSV LOCATION '/mnt/csv_files';

-- Specify table comment and properties
> CREATE TABLE student (id INT, name STRING, age INT)
    COMMENT 'this is a comment'
    TBLPROPERTIES ('foo'='bar');

-- Specify table comment and properties with different clauses order
> CREATE TABLE student (id INT, name STRING, age INT)
    TBLPROPERTIES ('foo'='bar')
    COMMENT 'this is a comment';

-- Create partitioned table
> CREATE TABLE student (id INT, name STRING, age INT)
    PARTITIONED BY (age);

-- Create a table with a generated column
> CREATE TABLE rectangles(a INT, b INT,
                          area INT GENERATED ALWAYS AS (a * b));
```

### UDF
```
CREATE FUNCTION convert_f_to_c(unit STRING, temp DOUBLE)
RETURNS DOUBLE
RETURN CASE
  WHEN unit = "F" THEN (temp - 32) * (5/9)
  ELSE temp
END;

SELECT convert_f_to_c(unit, temp) AS c_temp
FROM tv_temp;
```

### Action b/w 2 tables
- Use number1 and number2 tables to demonstrate set operators in this page.

```
> CREATE TEMPORARY VIEW number1(c) AS VALUES (3), (1), (2), (2), (3), (4);

> CREATE TEMPORARY VIEW number2(c) AS VALUES (5), (1), (1), (2);

> SELECT c FROM number1 EXCEPT SELECT c FROM number2;
  3
  4

> SELECT c FROM number1 MINUS SELECT c FROM number2;
  3
  4

> SELECT c FROM number1 EXCEPT ALL (SELECT c FROM number2);
  3
  3
  4

> SELECT c FROM number1 MINUS ALL (SELECT c FROM number2);
  3
  3
  4

> (SELECT c FROM number1) INTERSECT (SELECT c FROM number2);
  1
  2

> (SELECT c FROM number1) INTERSECT DISTINCT (SELECT c FROM number2);
  1
  2

> (SELECT c FROM number1) INTERSECT ALL (SELECT c FROM number2);
  1
  2
  2

> (SELECT c FROM number1) UNION (SELECT c FROM number2);
  1
  3
  5
  4
  2

> (SELECT c FROM number1) UNION DISTINCT (SELECT c FROM number2);
  1
  3
  5
  4
  2

> SELECT c FROM number1 UNION ALL (SELECT c FROM number2);
  3
  1
  2
  2
  3
  4
  5
  1
  1
  2

```

### Filter vs Transform
```
SELECT filter(array(1, 2, 3, 4), i -> i % 2 == 0);
>>> 2,4
SELECT transform(array(1, 2, 3, 4), i -> i % 2 == 0);
>>> False,True,False,True
SELECT transform(array(1, 2, 3, 4), i -> i*2);
>>> 2,4,6,8
```
### Alert destination supported by Databricks
- Email
- Slack
- Webhook
- MS Teams
- PagerDuty

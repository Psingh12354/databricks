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
- To successfully complete the task and indicate that the new table includes personally identifiable information (PII), the correct line of code to fill in the blank is: ```COMMENT “Contains PII”```
- To write data into a Delta table while avoiding the writing of duplicate records, you can use the ```MERGE``` command
- To define UDF in sql use below like query ```CREATE FUNCTION blue() RETURNS STRING COMMENT 'Blue color code' LANGUAGE SQL RETURN '0000FF';```
- The COPY INTO statement is generally used to copy data from files or a location into a table. If the data engineer runs this statement daily to copy the previous day’s sales into the "transactions" table and the number of records hasn't changed after today's execution, it's possible that the data from today's file might not have differed from the data already present in the table.
- A data engineer needs to create a table in Databricks using data from their organization’s existing SQLite database ```org.apache.spark.sql.jdbc```
- To create a new table all_transactions that contains all records from march_transactions and april_transactions without duplicate records, you should use the UNION operator, as shown in option B. This operator combines the result sets of the two tables while automatically removing duplicate records.
- The reason why the data files still exist while the metadata files were deleted is because the table was external. When a table is external in Spark SQL (or in other database systems), it means that the table metadata (such as schema information and table structure) is managed externally, and Spark SQL assumes that the data is managed and maintained outside of the system. Therefore, when you execute a DROP TABLE statement for an external table, it removes only the table metadata from the catalog, leaving the data files intact. On the other hand, for managed tables (option E), Spark SQL manages both the metadata and the data files. When you drop a managed table, it deletes both the metadata and the associated data files, resulting in a complete removal of the table.
- A table in a database allows you to store structured data persistently. It provides a physical representation of data, and other users can query, modify, and analyze it. Unlike temporary views, tables are durable and can be accessed across sessions and users. By creating a table, the data engineer ensures that the data is stored and can be efficiently utilized by others
- In summary, Gold tables contain valuable, refined data that is suitable for business reporting, while Silver tables provide a cleansed and conformed view of key business entities, bronze add schema to tables, and raw data is unprocessed data.
- Steps required to connect through github [steps](https://docs.databricks.com/en/repos/get-access-tokens-from-git-provider.html)
- To know why we use Parquet & what is Column orient, Row oriented and Hybrid Architecture [Link](https://towardsdatascience.com/demystifying-the-parquet-file-format-13adb0206705)
- ```DESCRIBE DETAILS tablename``` to get all the details about the given table.
### Time Travel
- ```DESCRIBE HISTORY employees``` to get history of given table including version details.

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
- To have an up and running job with a 1-hour processing interval; ```.trigger(processingTime='60 minutes')```

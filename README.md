# Delta Live and Delta Lake

This branch browses through Delta Lake and Delta Live.
---------------------------------------------------------------------
<h1>Delta Lake</h1>
Delta Lake, developed by Databricks, enhances data lakes performance and it can be used together to create a more efficient and reliable data lake environment. Since the data in data lakes (Data Lake Storage, AWS S3, or Hadoop HDFS) can be structred, semi-structured or unstructured, lack of data consistency and a robust data schema is a common problem. 

<h2>Delta Lake Advantages</h2>
<h3>Data Consistency and ACID Transactions</h3>
Delta Lake brings ACID (Atomicity, Consistency, Isolation, Durability) transactions to data lakes. This means it ensures data consistency and reliability even in the presence of failures. Traditional Data Lakes often lack these guarantees, which can lead to data quality issues in certain use cases.

<h3>Schema Enforcement</h3>
Delta Lake allows you to enforce a schema on your data. This schema enforcement feature ensures that new data adheres to the specified schema, making it easier to manage and query structured data within a Data Lake.

<h3>Time Travel and Versioning</h3>
Delta Lake provides time travel capabilities, allowing you to query data at different points in time and recover from mistakes or data corruption. This is valuable for auditing, debugging, and maintaining data quality.

<hr>
<h1>Delta Live</h1>
Delta Live is a higher-level data orchestration and ETL (Extract, Transform, Load) platform built on top of Delta Lake. It provides a more comprehensive solution for managing data pipelines, jobs, and workflows.
Delta Live focuses on real-time streaming data processing. It's designed to handle data as it's generated or ingested in real-time, making it suitable for use cases where low-latency data processing is critical. By using Delta Live, we can simply avoid the complexities of complicated python scripts including ETL related tasks. In fact, Delta Live provides high level python functions as well as ability to fully control the ETL by SQL (i.e. without Python dependencies). 

It is noteworthy, Delta Live is closely integrated with Databricks. Delta Live Tables is not a standalone product thereby, to use that Databricks account and cluster is required.

```python
dbutils.fs.ls('path/to/the/file')
```
<hr>

[Link](https://learn.microsoft.com/en-us/azure/architecture/browse/) to Microsoft proposed Azured based architectures

<hr>

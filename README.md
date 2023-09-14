# AzureDatabricks_Analyzer

To deploy databricks our based application firstly we need to explain databricks attributes. Basically, there are two types of clusters in databricks:

All purpose: We create them using UI for our own goal
Job Clusters: created automatically by jobs (not us) to perform a task

To compare them, job clusters automatically are deleted after job completion. Also, they are so useful for automated jobs (like ETL) and cheaper price compared to all purposes.
<hr>

## Databricks Cluster Configuration
### Node
Multi Node: One node would be the driver node (master) and others would be workers controlled by the driver. Suggested for computationally intensive tasks. 
Single Node: The single node option suits well for moderate to low level of computation-intensive tasks and the node acts both as driver and the worker. Also, due to having one node, they are not horizontally scalable and suitable for complicated ETL processes.

 ### Access Mode
 Single User: There is only one user who can have access
 Shared: Multiple users and workloads share the same cluster resources including CPU, Memory, etc.
 No Isolation Shared: Multiple users and workloads share the same cluster resources the same as shared option. However, admin can define max and min level of usage for each user in using a specific resource. As a result, the performance of other users may not be affected by significant level of usage of a user.

### Databricks Runtime
Databricks runtime: It includes the libraries and dependencies for Python, R, Scala, Java, Ubuntu, Delta lake, etc., suitable for ETL, data processing and simple machine learning-related tasks.

Databricks runtime ML: This options adds AI libraries like PyTorch, Keras, TF, etc., on top of the previous plan where makes it a good option for deploying AI models.

Photon Runtime: It has photon engine appended to databricks runtime, making it a beneficial choice by running SQL commands faster and more efficient in terms of costs.

Databricks Runtime Light: This option suits simple automated tasks not requiring advanced features. 

### Auto Termination
We can set the data time of auto termination of cluster to avoid unnecessary costs.

### Auto Scaling
We can set the min and max number of worker nodes based on the workload (job intensity). Not recommended for streaming workloads.

### Cluster VM Type/Size
Based on the task, we can set the cluster to be like Memory optimized, Compute Optimzed, GPU accelerated and so on. For instance, GPU accelerated is recommended for Deep Learning based tasks.

<hr>

<h3>Steps to run a notebook (.ipynb file) on Databricks:</h3>
<h5>1. Create a Cluster in compute tab</h5>
<h5>2. Navigate through the desired directory in workspace tab</h5>
<h5>3. Create a notebook file in the directory</h5>
<h5>4. Make sure the notebook is connected to the correct cluster</h5>
<h5>5. You can set schedule for the notebook to be run, similar to Airflow (optional)</h5>

<hr>

For Storage, Azure Data Lake is used (similar to Amazon S3). To make storage access for notebook, you may authenticate either in notebook or in cluster configuration as below:

In the notebook:
```python

spark.conf.set(
     "fs.azure.account.key.<WRITE-STORAGE-NAME>.dfs.core.windows.net",
     "WRITE-YOUR-ACCESS-KEY"
 )

```

In cluster configuration while creating the cluster (advanced options>spark config) add these two lines:

```
fs.azure.account.key.<WRITE-STORAGE-NAME>.dfs.core.windows.net
WRITE-YOUR-ACCESS-KEY
```
In case of avoiding Azure Data Lake, files can be uploaded directly on Databricks File System (security concern: all project collaborators have access to workspace and those files) and it can be accessed by:

```python
dbutils.fs.ls('path/to/the/file')
```

<hr> 
<h4>Since Databricks uses Spark, let's briefly dive into Spark architecture:</h4>
In spark, there exists one driver node (driver machine) and multiple worker nodes. Driver runs its driver program that includes communicating with cluster manager to allocate resources, and recognizing the number of jobs to enhance parallel processing goal (driver does not involve in data processing). In fact, the driver program divides the data processing into jobs > stages > tasks. 

In Spark, each worker node has one Java Virtual Machine (JVM) executor (Spark is written and run in Java). Executors read and write the data processing tasks. Also, each worker node has X cores (in databricks X>4) that are known as slots of the executors. Slots will receives tasks (divided from stages) then they return the result.

To scale the clusters, there are two methods namely, horizontal and vertical scaling. Vertical scaling is to increase the number of cores of each node and also horizontal scaling is to increase the number of nodes (worker nodes). Horizontal scaling can handle computationally intensive tasks due to limit on number of manageable cores by each node.
<hr>

[Link](https://learn.microsoft.com/en-us/azure/architecture/browse/) to Microsoft proposed Azured based architectures

<hr>

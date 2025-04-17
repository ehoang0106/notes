4 Questions to ask:
- What kind of database works?
- How much data do you have?
- Is serverless a requirement?
- How do we optimize the costs?

## Redshift and EMR

- Redshift is relational database and it's not replacement for RDS
- Redshift supports single-AZ and multi-AZ. Can create multi cluster in different AZs. Multi-AZ supports 2 AZs at one time. Converting single to multi-AZ requires an existing snapshot
- EMR is made up of EC2. This means can employ EC2 instance for cost-saving
- EMR for Apache Hadoop and Apache Spark. This service offers serveral built-in open--source tools to process vast amount of big data. Has ability to leverage HDFS, EMRFS, and local storage

## Kinesis, Athena, and Glue

- Kinesis is the only service with real-time response. 
- SQS and kinesis can both be queues. SQS is simpler, and Kinesis is faster and can store data up to a year
- Serverless SQL means Athena
- Glue is serverless ETL service. Can create schema for data when paired with Athena
- Can use QuickSight to query Athena to build dashboard and visualizations
- Know Data Stream and Data Firehose. Data Firehose is near real time while Data Stream is real time

## QuickSight and OpenSearch or ElasticSearch

- Creating a dashboard? QuickSight is go-to tool for visualizing data
- OpenSearch is primarily used for analyzing log files and various documents, especially with ETL process
- OpenSearch services and Elasticsearch service(predecessor) are extremely similar. They both follow the same concepts

## Data Pipeline

- It's a ETL service
- Implement automated workflows for movement and transformation of data
- Integrates with storage service and compute service
- Data-driven and task-dependent ETL workloads are perfect use case

## Amazon MSK

- A managed service for building and running Apache Kafka streaming application
- The service handles control plane operations (creation, updating, deletion)
- You manage data plane operations
- Push broker logs to CloudWatch, S3, Kinesis Data Firehose
- API call are logged to CloudTrail

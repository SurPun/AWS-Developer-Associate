# Section 31 AWS Other Services

## 447. AWS SES

AWS SES — Simple Email Service

- Send emails to people using:
    - SMTP interface
    - Or AWS SDK

- Ability to receive email. Integrates with:
    - S3
    - SNS
    - Lambda

- Integrated with IAM for allowing to send emails

## 448. Amazon OpenSearch Service - Overview

Amazon OpenSearch Service

- Amazon OpenSearch is successor to Amazon ElasticSearch
- In DynamoDB, queries only exist by primary key or indexes...
- With OpenSearch, you can search any field, even partially matches
- It's common to use OpenSearch as a complement to another database
- Two modes: managed cluster or serverless cluster
- Does not natively support SQL (can be enabled via a plugin)
- Ingestion from Kinesis Data Firehose, AWS loT, and CloudWatch Logs
- Security through Cognito & IAM, KMS encryption, TLS
- Comes with OpenSearch Dashboards (visualization)

## 449. Amazon Athema - Overview

- Serverless query service to analyze data stored in Amazon S3
- Uses standard SQL language to query the files (built on Presto)
- Supports CSV, JSON, ORC, Avro, and Parquet
- Pricing: $5.00 per TB of data scanned
- Commonly used with Amazon Quicksight for reporting/dashboards
- Use cases: Business intelligence / analytics / reporting, analyze & query VPC Flow Logs, ELB Logs, CloudTrail trails, etc...
- ExamTip: analyze data in S3 using serverless SQL, use Athena

Amazon Athena — Performance Improvement

- Use columnar data for cost-savings (less scan)
    - Apache Parquet or ORC is recommended
    - Huge performance improvement
    - Use Glue to convert your data to Parquet or ORC

- Compress data for smaller retrievals (bzip2, gzip, |z4, snappy, zlip, zstd...)
- Partition datasets in S3 for easy querying on virtual columns
    - s3://yourBucket/path To Table
        -/<PARTITION_COLUMN_NAME>=<VALUE>
            -/<PARTITION_COLUMN_NAME>=<VALUE>
                -/<PARTITION_COLUMN_NAME>=<VALUE>
                    -/etc...
    - Example: s3://athena-examples/flight/parquet/year= | 99 |     month= | /day=1/
- Use larger files (> 128 MB) to minimize overhead

Amazon Athena - Federated Query

- Allows you to run SQL queries across data stored in relational, non-relational, object, and custom data sources (AWS or on-premises)
- Uses Data Source Connectors that run on AWS Lambda to run Federated Queries (e.g., CloudWatch Logs, DynamoDB, RDS, ...)
- Store the results back in Amazon s3

## 451. Amazon MSK - Overview

Amazon Managed Streaming for Apache Kafka (Amazon MSK)

- Alternative to Amazon Kinesis
- Fully managed Apache Kafka on AWS
    - Allow you to create, update, delete clusters
    - MSK creates & manages Kafka brokers nodes & Zookeeper nodes for you
    - Deploy the MSK cluster in yourVPC, multi-AZ (up to 3 for HA)
    - Automatic recovery from common Apache Kafka failures
    - Data is stored on EBS volumes for as long as you want
- MSK Serverless
    - Run Apache Kafka on MSK without managing the capacity

Kinesis Data Streams vs Amazon MSK

| Kinesis Data Streams | Amazon MSK |
| --- | --- |
| 1 MB message size limit | 1 MB default, configure for higher (ex: 10MB) |
| Data Streams with Shards | Kafka Topics with Partitions |
| Shard Splitting & Merging | Can only add partitions to a topic |
| TLS In-flight encryption | PLAINTEST or TLS In-flight Encryption |
| KMS at-rest encryption | KMS at-rest encryption |

## 452. Amaon Certificate Manager

AWS Certificate Manager (ACM)

- Let's you easily provision, manage, and deploy SSL/TLS Certitcates
- Used to provide in-flight encryption for websites (HTTPS)
- Supports both public and private TLS certificates
- Free of charge for public TLS certificates
- Automatic TLS certificate renewal
- Integrations with (load TLS certificates on)
    - Elastic Load Balancers
    - CloudFront Distributions
    - APls on API Gateway
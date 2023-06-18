# Section 8: AWS Fundamentals: RDS + Aurora + ElastiCache

## 76. Amazon RDS Overview

Amazon RDS Overview

- RDS stands for Relational Database Service
- It's a managed DB service for DB use SQL as a query language.
- It allows you to create databases in the cloud that are managed by AWS
  - Postgres
  - MySQL
  - MariaDB
  - Oracle
  - Microsoft SQL Server
  - Aurora (AWS Proprietary database)

Advantage over using RDS versus deploying DB on EC2

- RDS is a managed service:

  - Automated provisioning, OS patching
  - Continuous backups and restore to specific timestamp (Point in Time Restore)!
  - Monitoring dashboards
  - Read replicas for improved read performance
  - Multi AZ setup for DR (Disaster Recovery)
  - Maintenance windows for upgrades
  - Scaling capability (vertical and horizontal)
  - Storage backed by EBS (gp2 or io1)

- BUT you can't SSH into your instances

RDS — Storage Auto Scaling

- Helps you increase storage on your RDS DB instance dynamically

- When RDS detects you are running out of free database storage, it scales automatically

- Avoid manually scaling your database storage

- You have to set Maximum Storage Threshold (maximum limit for DB storage)

- Automatically modify storage if:

  - Free storage is less than 10% of allocated storage
  - Low-storage lasts at least 5 minutes
  - 6 hours have passed since last modification
  - Useful for applications with unpredictable workloads

- Supports all RDS database ae (MariaDB, MySQL, PostgreSQL, SQL Server, Oracle)

## 77. RDS Read Replicas vs Multi AZ

RDS Read Replicas for read scalability

- Up to 15 Read Replicas
- Within AZ, Cross AZ or Cross Region
- Replication is ASYNC, so reads are eventually consistent
- Replicas can be promoted to their own DB
- Applications must update the connection string to leverage read replicas

## 79. Amazon Aurora

Amazon Aurora

- Aurora is a proprietary technology from AWS (not open sourced)
- Postgres and MySQL are both supported as Aurora DB (that means your drivers will work as if Aurora was a Postgres or MySQL database)
- Aurora is “AWS cloud optimized” and claims 5x performance improvement
  over MySQL on RDS, over 3x the performance of Postgres on RDS
- Aurora storage automatically grows in increments of |OGB, up to 128 TB.
- Aurora can have up to |5 replicas and the replication process is faster than MySQL (sub 10 ms replica lag)
- Failover in Aurora is instantaneous. It’s HA native.
- Aurora costs more than RDS (20% more) — but is more efficient

Features of Aurora

- Automatic fail-over
- Backup and Recovery
- Isolation and security
- Industry compliance
- Push-button scaling
- Automated Patching with Zero Downtime
- Advanced Monitoring
- Routine Maintenance
- Backtrack: restore data at any point of time without using backups

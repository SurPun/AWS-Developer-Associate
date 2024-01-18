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
- Aurora is “AWS cloud optimized” and claims 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
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

## 81. RDS & Aurora Security

RDS & Aurora Security

- At-rest encryption:
- Database master & replicas encryption using AWS KMS — must be defined as launch time
- If the master is not encrypted, the read replicas cannot be encrypted
- To encrypt an un-encrypted database, go through a DB snapshot & restore as encrypted
- In-flight encryption: TLS-ready by default, use the AWSTLS root certificates client-side
- IAM Authentication: IAM roles to connect to your database (instead of username/pw)
- Security Groups: Control Network access to your RDS / Aurora DB
- No SSH available except on RDS Custom
- Audit Logs can be enabled and sent to CloudWatch Logs for longer retention

## 82. RDS Proxy

Amazon RDS Proxy

- Fully managed database proxy for RDS
- Allows apps to pool and share DB connections established with the database
- Improving database efficiency By reducing the stress on database resources (e.g., CPU, RAM) and minimize open connections (and timeouts)
- Serverless, autoscaling, highly available (multi-AZ)
- Reduced RDS & Aurora failover time by up 66%
- Supports RDS (MySQL, PostgreSQL, MariaDB, MS Sol Server) al fore (MysOL PostgreSQL)
- No code changes required for most apps
- Enforce IAM Authentication for DB, and securely store credentials in AWS Secrets Manager
- RDS Proxy is never publicly accessible (must be accessed from VPC)

## 83. RDS Overview

Amazon ElastiCache Overview

- The same way RDS is to get managed Relational Databases...
- ElastiCache is to get managed Redis or Memcached
- Caches are in-memory databases with really high performance, low latency
- Helps reduce load off of databases for read intensive workloads
- Helps make your application stateless
- AWS takes care of OS maintenance / patching, optimizations setup, configuration, monitoring, failure recovery and backups
- Using ElastiCache involves heavy application code changes

## 85. ElastiCache Strategies

- Lazy Loading/Cache-Aside/Lazy Population Python Pseudocode

```py
# Python

def get_user(user_id):

  # Check the cache
  record = cache.get(user_id)

  if record is None:
    # Run a DB query
    record = db.query("select * from users where id = ?", user_id)

    # Populate the cache
    cache.set(user_id, record)

    return record
  else:
    return record

# App code
user = get_user(17)
```

- Write-Through Python Pseudocode

```py
# Python
def save_user(user_id, values):

  # Save to DB
  record = db. query (“update users ... where id = ?", user_id, values)

  # Push into cache
  cache.set(user_id, record)

  return record

# App code
user = save_user(17, {"name": "Nate Dogg"})
```

- Lazy Loading / Cache aside is easy to implement and works for many situations as a foundation, especially on the read side
- Write-through is usually combined with Lazy Loading as targeted for the queries or workloads that benefit from this optimization
- Setting aTTL is usually not a bad idea, except when you're using Write-through. Set it to a sensible value for your application
- Only cache the data that makes sense (user profiles, blogs, etc...)

## 86. Amazon MemoryDB for Redis - Overview

Amazon MemoryDB for Redis

- Redis-compatible, durable, in-memory database service
- Ultra-fast performance with over |60 millions requests/second
- Durable in-memory data storage with Multi-AZ transactional log
- Scale seamlessly from 10s GBs to 100s TBs of storage
- Use cases: web and mobile apps, online gaming, media streaming, ...

Microservices Applications:

    Web, mobile, retail, gaming, media and entertainment, banking, finance, and more ..

Amazon MemoryDB for Redis:

    Redis-compatible, durable, in-memory database

In-Memory Speed:

    Stores data in-memory across up to hundreds of nodes for ultra-fast performance

Multi-AZ Transactional Log:

    Stores data across multiple Availability Zones to provide durability and fast recovery

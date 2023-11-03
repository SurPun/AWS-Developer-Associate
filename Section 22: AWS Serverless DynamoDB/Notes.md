# Section 22: AWS Serverless DynamoDB

## 317. DynamoDB Overview

Traditional Architecture

- Traditional applications leverage RDBMS databases
- These databases have the SQL query language
- Strong requirements about how the data should be modeled
- Ability to do query joins, aggregations, complex computations
- Vertical scaling (getting a more powerful CPU / RAM / IO)
- Horizontal scaling (increasing reading capability by adding EC2 / RDS Read Replicas)

NoSQL databases

- NoSQL databases are non-relational databases and are distributed
- NoSQL databases include MongoDB, DynamoDB., ...
- NoSQL databases do not support query joins (or just limited support)
- All the data that is needed for a query is present in one row
- NoSQL databases don’t perform aggregations such as ‘SUM”,"“AVG", ...
- NoSQL databases scale horizontally

- There's no “right or wrong” for NoSQL vs SQL, they just require to model the data differently and think about user queries differently

Amazon DynamoDB

- Fully managed, highly available with replication across multiple AZs
- NoSQL database - not a relational database
- Scales to massive workloads, distributed database
- Millions of requests per seconds, trillions of row, 100s of TB of storage
- Fast and consistent in performance (low latency on retrieval)
- Integrated with IAM for security, authorization and administration
- Enables event driven programming with DynamoDB Streams
- Low cost and auto-scaling capabilities
- Standard & Infrequent Access (IA) Table Class

DynamoDB - Basics

- DynamoDB is made of Tables
- Each table has a Primary Key (must be decided at creation time)
- Each table can have an infinite number of items (= rows)
- Each item has attributes (can be added over time — can be null)
- Maximum size of an item is 400KB

- Data types supported are:
 - Scalar Types — String, Number, Binary, Boolean, Null
 - Document Types — List, Map
 - Set Types — String Set, Number Set, Binary Set

DynamoDB — Primary Keys

- Option 1: Partition Key (HASH)
 - Partition key must be unique for each item
 - Partition key must be “diverse” so that the data is distributed
 - Example: “User_ID” for a users table

DynamoDB — Primary Keys

- Option 2: Partition Key + Sort Key (HASH + RANGE)
 - The combination must be unique for each item
 - Data is grouped by partition key
 - Example: users-games table, “User_ID” for Partition Key and “Game_ID” for Sort Key

DynamoDB -— Partition Keys (Exercise)

- We're building a movie database
- What is the best Partition Key to maximize data distribution?
 - movie_id
 - producer_name
 - leader_actor_name
 - movie_language

- “movie_id” has the highest cardinality so it’s a good candidate
- “movie_language”’ doesn’t take many values and may be skewed towards English so it’s not a great choice for the Partition Key

## 319. DynamoDB WCU & RCU - Throughput

DynamoDB — Read/Write Capacity Modes

- Control how you manage your table's capacity (read/write throughput)

- Provisioned Mode (default)
 - You specify the number of reads/writes per second
 - You need to plan capacity beforehand
 - Pay for provisioned read & write capacity units

- On-Demand Mode
 - Read/writes automatically scale up/down with your workloads
 - No capacity planning needed
 - Pay for what you use, more expensive ($$$)

- You can switch between different modes once every 24 hours

R/W Capacity Modes — Provisioned

- Table must have provisioned read and write capacity units
- Read Capacity Units (RCU) — throughput for reads
- Write Capacity Units (WCU) — throughput for writes
- Option to setup auto-scaling of throughput to meet demand
- Throughput can be exceeded temporarily using “Burst Capacity”
- If Burst Capacity has been consumed, you'll get a “ProvisionedThroughputExceededException”
- It's then advised to do an exponential backoff retry

DynamoDB — Write Capacity Units (WCU)

- One Write Capacity Unit (WCU) represents one write per second for an item up to 1 KB in size
- If the items are larger than 1 KB, more WCUs are consumed

Strongly Consistent Read vs. Eventually Consistent Read

- Eventually Consistent Read (default)
 - If we read just after a write, it’s possible we'll get some stale data because of replication

- Strongly Consistent Read
 - If we read just after a write, we will get the correct data
 - Set “ConsistentRead” parameter to True in API calls (GetItem, BatchGetItem, Query, Scan)
 - Consumes twice the RCU

DynamoDB — Read Capacity Units (RCU)

- One Read Capacity Unit (RCU) represents one Strongly Consistent Read per second, or two Eventually Consistent Reads per second, for an item up to 4 KB in size
- If the items are larger than 4 KB, more RCUs are consumed

DynamoDB -— Partitions Internal

- Data is stored in partitions
- Partition Keys go through a hashing algorithm to know to which partition they go to
- WCUs and RCUs are spread evenly across partitions

DynamoDB -— Throttling

- If we exceed provisioned RCUs or WCUs, we get “ProvisionedThroughputExceededException”
- Reasons:
 - Hot Keys — one partition key is being read too many times (e.g., popular item)
 - Hot Partitions
 - Very large items, remember RCU and WCU depends on size of items
- Solutions:
 - Exponential backoff when exception is encountered (already in SDK)
 - Distribute partition keys as much as possible
 - If RCU issue, we can use DynamoDB Accelerator (DAX)

R/W Capacity Modes — On-Demand

- Read/writes automatically scale up/down with your workloads
- No capacity planning needed (WCU / RCU)
- Unlimited WCU & RCU, no throttle, more expensive
- You're charged for reads/writes that you use in terms of RRU and WRU
- Read Request Units (RRU) — throughput for reads (same as RCU)
- Write Request Units (WRU) — throughput for writes (same as WCU)
- 2.5x more expensive than provisioned capacity (use with care)
- Use cases: unknown workloads, unpredictable application traffic, ...

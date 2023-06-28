# Quiz 5: RDS, Aurora, & ElastiCache

1. Amazon RDS supports the following databases, EXCEPT:

- MongoDB

RDS supports MySQL, PostgreSQL, MariaDB, Oracle, MS SQL Server, and Amazon Aurora.

2. You're planning for a new solution that requires a MySQL database that must be available even in case of a disaster in one of the Availability Zones. What should you use?

- Enable Multi-AZ

Multi-AZ helps when you plan a disaster recovery for an entire AZ going down. If you plan against an entire AWS Region going down, you should use backups and replication across AWS Regions.

3. We have an RDS database that struggles to keep up with the demand of requests from our website. Our million users mostly read news, and we don't post news very often. Which solution is NOT adapted to this problem?

- RDS Multi-AZ

Be very careful with the way you read questions at the exam. Here, the question is asking which solution is NOT adapted to this problem. ElastiCache and RDS Read Replicas do indeed help with scaling reads.

4. You have set up read replicas on your RDS database, but users are complaining that upon updating their social media posts, they do not see their updated posts right away. What is a possible cause for this?

- Read Replicas have Asynchronous Replication, therefore it's likely your users will only read Eventual Consistency

5. Which RDS (NOT Aurora) feature when used does not require you to change the SQL connection string?

- Multi-AZ

Multi-AZ keeps the same connection string regardless of which database is up.

6. Your application running on a fleet of EC2 instances managed by an Auto Scaling Group behind an Application Load Balancer. Users have to constantly log back in and you don't want to enable Sticky Sessions on your ALB as you fear it will overload some EC2 instances. What should you do?

- Store session data in ElastiCache

Storing Session Data in ElastiCache is a common pattern to ensuring different EC2 instances can retrieve your user's state if needed.

7. An analytics application is currently performing its queries against your main production RDS database. These queries run at any time of the day and slow down the RDS database which impacts your users' experience. What should you do to improve the users' experience?

- Setup a Read Replica

Read Replicas will help as your analytics application can now perform queries against it, and these queries won't impact the main production RDS database.

8. You are running an ElastiCache Redis cluster which you want to ensure it is high available. What should you do?

- Enable Multi-AZ

9. Your company has a production Node.js application that is using RDS MySQL 5.6 as its database. A new application programmed in Java will perform some heavy analytics workload to create a dashboard on a regular hourly basis. What is the most cost-effective solution you can implement to minimize disruption for the main application?

- Create a Read Replica in a different AZ and run the analytics workload on the replica database

10. You would like to create a disaster recovery strategy for your RDS PostgreSQL database so that in case of a regional outage the database can be quickly made available for both read and write workloads in another AWS Region. The DR database must be highly available. What do you recommend?

- Create a Read Replica in a different region and enable Multi-AZ on the Read Replica

A Read Replica in a different AWS Region than the source database can be used as a standby database and promoted to become the new production database in case of a regional disruption. So, we'll have a highly available (because of Multi-AZ) RDS DB Instance in the destination AWS Region with both read and write available.

11. You have migrated the MySQL database from on-premises to RDS. You have a lot of applications and developers interacting with your database. Each developer has an IAM user in the company's AWS account. What is a suitable approach to give access to developers to the MySQL RDS DB instance instead of creating a DB user for each one?

- Enable IAM Database Authentication

12. Which of the following statement is true regarding replication in both RDS Read Replicas and Multi-AZ?

- Read Replica uses Asynchronous Replication and Multi-AZ uses Synchronous Replication

13. How do you encrypt an unencrypted RDS DB instance?

- Create a snapshot of the unencrypted RDS DB instance, copy the snapshot and tick "Enable encryption", then restore the RDS DB instance from the encrypted snapshot

14. For your RDS database, you can have up to ............ Read Replicas.

- 15

15. Which RDS database technology does NOT support IAM Database Authentication?

- Oracle

16. You have an un-encrypted RDS DB instance and you want to create Read Replicas. Can you configure the RDS Read Replicas to be encrypted?

- No

You can not create encrypted Read Replicas from an unencrypted RDS DB instance.

17. How many Aurora Read Replicas can you have in a single Aurora DB Cluster?

- 15

18. Amazon Aurora supports both .......................... databases.

- MySQL and PostgresSQL

19. What is the maximum number of Read Replicas you can add in an ElastiCache Redis Cluster with Cluster-Mode Disabled?

- 5

20. You have an ElastiCache Redis Cluster that serves a popular application. You have noticed that there are a large number of requests that go to the database because a large number of items are removed from the cache before they expire. What is this called and how to solve it?

- Cache Evictions, Scale up or out your ElastiCache Redis Cluster

21. You have a MySQL RDS database instance on which you want to enforce SSL connections. What should you do?

- Execute a REQUIRE SSL SQLstatement to all your DB users

22. You have an ElastiCache cluster with small cache size, so you want to ensure that only the data that's requested will be loaded into the cluster. Which caching strategy should you use?

- Lazy Loading

Lazy Loading would load data into the cache only when necessary (actively requested data from the database).

23. You're hosting a dynamic website fronted by an ElastiCache Cluster. You have been instructed to keep latency to a minimum for all read requests for every user. Also, writes can take longer to happen. Which caching strategy do you recommend?

- Write Through

This has longer writes, but the reads are quick and the data is always updated in the cache.

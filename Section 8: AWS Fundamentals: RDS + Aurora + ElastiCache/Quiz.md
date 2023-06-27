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

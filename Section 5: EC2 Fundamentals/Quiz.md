# Quiz 2 EC2 Fundamentals Quiz

1. Which EC2 Purchasing Option can provide you the biggest discount, but it is not suitable for critical jobs or databases?

- Spot Instances

Spot Instances are good for short workloads and this is the cheapest EC2 Purchasing Option. But, they are less reliable because you can lose your EC2 instance.

2. What should you use to control traffic in and out of EC2 instances?

- Security Groups

Security Groups operate at the EC2 instance level and can control traffic.

3. How long can you reserve an EC2 Reserved Instance?

- 1 or 3 years

EC2 Reserved Instances can be reserved for 1 or 3 years only.

4. You would like to deploy a High-Performance Computing (HPC) application on EC2 instances. Which EC2 instance type should you choose?

- Compute Optimized

Compute Optimized EC2 instances are great for compute-intensive workloads requiring high-performance processors (e.g., batch processing, media transcoding, high-performance computing, scientific modeling & machine learning, and dedicated gaming servers).

5. Which EC2 Purchasing Option should you use for an application you plan to run on a server continuously for 1 year?

- Reserved Instances

Reserved Instances are good for long workloads. You can reserve EC2 instances for 1 or 3 years.

6. You are preparing to launch an application that will be hosted on a set of EC2 instances. This application needs some software installation and some OS packages need to be updated during the first launch. What is the best way to achieve this when you launch the EC2 instances?

- Write a bash script that installs the required software and updates to your OS, then use this script in EC2 User Data when you launch your EC2 instances

EC2 User Data is used to bootstrap your EC2 instances using a bash script. This script can contain commands such as installing software/packages, download files from the Internet, or anything you want.

7. Which EC2 Instance Type should you choose for a critical application that uses an in-memory database?

- Memory Optimized

Memory Optimized EC2 instances are great for workloads requiring large data sets in memory.

8. You have an e-commerce application with an OLTP database hosted on-premises. This application has popularity which results in its database has thousands of requests per second. You want to migrate the database to an EC2 instance. Which EC2 Instance Type should you choose to handle this high-frequency OLTP database?

- Storage Optimized

Storage Optimized EC2 instances are great for workloads requiring high, sequential read/write access to large data sets on local storage.

9. Security Groups can be attached to only one EC2 instance.

- False

Security Groups can be attached to multiple EC2 instances within the same AWS Region/VPC.

10. You're planning to migrate on-premises applications to AWS. Your company has strict compliance requirements that require your applications to run on dedicated servers. You also need to use your own server-bound software license to reduce costs. Which EC2 Purchasing Option is suitable for you?

- Dedicated Hosts

Dedicated Hosts are good for companies with strong compliance needs or for software that have complicated licensing models. This is the most expensive EC2 Purchasing Option available.

11. You would like to deploy a database technology on an EC2 instance and the vendor license bills you based on the physical cores and underlying network socket visibility. Which EC2 Purchasing Option allows you to get visibility into them?

- Dedicated Hosts

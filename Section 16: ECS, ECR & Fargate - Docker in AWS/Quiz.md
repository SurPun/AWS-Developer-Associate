# Quiz 13: Containers on AWS Quiz

1. You have multiple Docker-based applications hosted on-premises that you want to migrate to AWS. You don't want to provision or manage any infrastructure, you just want to run your containers on AWS. Which AWS service should you choose?

- Elastic Container Service (ECS) with Fargate Launch Type

AWS Fargate allows you to run your containers on AWS without managing any servers.

2. Two of the launch types of ECS are: 

- Amazon EC2 Launch Type and Fargate Lunch Type

3. You have an application hosted on an ECS Cluster (EC2 Launch Type) where you want your ECS tasks to upload files to an S3 bucket. Which IAM Role for your ECS Tasks should you modify?

- ECS Task Role

ECS Task Role is the IAM Role used by the ECS task itself. Use when your container wants to call other AWS services like S3, SQS, etc.

4. You're planning to migrate a WordPress website running on Docker containers from on-premises to AWS. You have decided to run the application in an ECS Cluster, but you want your Docker containers to access the same WordPress website content such as website files, images, videos, etc. What do you recommend to achieve this?

- Mount an EFS volume

EFS volume can be shared between different EC2 instances and different ECS Tasks. It can be used as a persistent multi-AZ shared storage for your containers.

5. EFS volume can be shared between different EC2 instances and different ECS Tasks. It can be used as a persistent multi-AZ shared storage for your containers.

- Create an IAM task role for the new application


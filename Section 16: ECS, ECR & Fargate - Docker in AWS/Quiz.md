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

6. You are migrating your on-premises Docker-based applications to Amazon ECS. You were using Docker Hub Container Image Library as your container image repository. Which is an alternative AWS service which is fully integrated with Amazon ECS?

- Elastic Container Registry (ECR)

Amazon ECR is a fully managed container registry that makes it easy to store, manage, share, and deploy your container images. It won't help in running your Docker-based applications.

7. You have a Classic ECS cluster that you want to enable IAM roles for your ECS tasks so that they can make API requests to AWS services. Which ECS configuration option should you enable in /etc/ecs/ecs.config?

- ECS_ENABLE_TASK_IAM_ROLE

Although this wasn't discussed during the hands-on, you need to know about that important setting in the "ecs.config" file.

8. You have a CodePipeline pipeline, which contains a build stage that uses AWS CodeBuild. This build stage builds your Docker images and pushes them to Amazon Elastic Container Registry (ECR). The build stage fails with an authorization issue. What is the issue?

- Double-check your IAM role and permissions for the AWS CodeBuild service

Any permissions issues against ECR are most likely due to IAM permissions. Your CodeBuild service must have the required permissions to push Docker images to ECR repositories.

9. You are looking to run multiple copies of the same application on the same EC2 instance and expose it with a load balancer. The application is available as a Docker image. You should use ............................

- Application Load Balanacer + ECS

Thanks to the Dynamic Port Mapping feature.

10. You have a containerized application stored as Docker images in an ECR repository, that you want to run on an ECS cluster. You're trying to launch two copies of the same Docker container on the same EC2 container instance. The first container successfully starts, but the second container doesn't. You have checked that there's enough CPU and RAM on the EC2 container instance. What is the problem here?

- The host port defined in the task definition

To enable random host port, set host port = 0 (or empty), which allows multiple containers of the same type to launch on the same EC2 container instance.


11. A newly launched EC2 container instance can't be registered with your ECS cluster. What is NOT a reason for this issue?

- The security group on the EC2 instance does not allow inbound traffic

Security Groups do not matter when an EC2 instance registers with the ECS service. By default, Security Groups allow all outbound traffic.

12. You want to pull Docker images from a private ECR repository. Which AWS CLI command can you use?

```
$(aws ecr get-login --no-include-email)
docker pull $ECR_IMAGE_URL
```

13. You have an ECS cluster where you want to run 4 ECS services. Each ECS service needs to interact with various AWS services. Which of the following is the best practice while giving permissions to these ECS services?

- Create 4 ECS Task roles and attach them to the relevant ECS Task definition

14. Which ECS Task Placement strategy is the MOST cost-efficient?

- binpack

15. Which ECS ECS Task Placement constraint allows you to place each ECS Task on a different EC2 container instance?

- distinctInstance
# Section 16: ECS, ECR & Fargate - Docker in AWS

## 166. Docker Introduction

What is Docker?

- Docker is a software development platform to deploy apps
- Apps are packaged in containers that can be run on any OS
- Apps run the same, regardless of where they're run
 - Any machine
 - No compatibility issues
 - Predictable behavior
 - Less work
 - Easier to maintain and deploy
 - Works with any language, any OS, any technology
- Use cases: microservices architecture, lift-and-shift apps from on-premises to the AWS cloud, ...

## 167. Amazon ECS

Amazon ECS - EC2 Launch Type

- ECS = Elastic Container Service
- Launch Docker containers on AWS = Launch ECS Tasks on ECS Clusters
-  EC2 Launch Type: you must provision & maintain the infrastructure (the EC2 instances)
- Each EC2 Instance must run the ECS Agent to register in the ECS Cluster
- AWS takes care of starting / stopping containers

Amazon ECS — Fargate Launch Type

- Launch Docker containers on AWS
- You do not provision the infrastructure (no EC2 instances to manage)
- It's all Serverless!
- You just create task definitions
- AWS just runs ECS Tasks for you based on the CPU / RAM you need
- To scale, just increase the number of tasks. Simple - no more EC2 instances

Amazon ECS — IAM Roles for ECS

- EC2 Instance Profile (EC2 Launch Type only):
 - Used by the ECS agent
 - Makes API calls to ECS service
 - Send container logs to CloudWatch Logs
 - Pull Docker image from ECR
 - Reference sensitive data in Secrets Manager or SSM Parameter Store

- ECS Task Role:
 - Allows each task to have a specific role
 - Use different roles for the different ECS Services you run
 - Task Role is defined in the task definition

 Amazon ECS — Load Balancer Integrations

- Application Load Balancer supported and works for most use cases
- Network Load Balancer recommended only for high throughput / high performance use cases, or to pair it with AWS Private Link
- Classic Load Balancer supported but not recommended (no advanced features — no Fargate)

Amazon ECS — Data Volumes (EFS)

- Mount EFS file systems onto ECS tasks
- Works for both EC2 and Fargate launch types
- Tasks running in any AZ will share the same data in the EFS file system
- Fargate + EFS = Serverless

- Use cases: persistent multi-AZ shared storage for your containers

- Note:
 - Amazon S3 cannot be mounted as a file system

## 171. Amazon ECS - Auto Scaling

ECS Service Auto Scaling

- Automatically increase/decrease the desired number of ECS tasks

- Amazon ECS Auto Scaling uses AWS Application Auto Scaling
 - ECS Service Average CPU Utilization
 - ECS Service Average Memory Utilization - Scale on RAM
 - ALB Request Count Per Target — metric coming from the ALB

- Target Tracking — scale based on target value for a specific CloudWatch metric
- Step Scaling — scale based on a specified CloudWatch Alarm
- Scheduled Scaling — scale based on a specified date/time (predictable changes)

- ECS Service Auto Scaling (task level) # EC2 Auto Scaling (EC2 instance level)
- Fargate Auto Scaling is much easier to setup (because Serverless)

EC2 Launch Type — Auto Scaling EC2 Instances

- Accommodate ECS Service Scaling by adding underlying EC2 Instances

- Auto Scaling Group Scaling
 - Scale your ASG based on CPU Utilization
 - Add EC2 instances over time

- ECS Cluster Capacity Provider
 - Used to automatically provision and scale the infrastructure for your ECS Tasks
 - Capacity Provider paired with an Auto Scaling Group
 - Add EC2 Instances when you're missing capacity (CPU, RAM...)

## 172. Amazon ECS - Rolling Updates

ECS Rolling Updates

- When updating from v1 to v2, we can control how many tasks can be started and stopped, and in which order

## 174. Amazon ECS Task Definitions - Deep Dive

Amazon ECS — Task Definitions

- Task definitions are metadata in JSON form to tell ECS how to run a Docker container

- It contains crucial information, such as:
 - Image Name
 - Port Binding for Container and Host
 - Memory and CPU required
 - Environment variables
 - Networking information
 - IAM Role
 - Logging configuration (ex CloudWatch)

- Can define up to 10 containers in a Task Definition

Amazon ECS — Load Balancing (EC2 Launch Type)

- We get a Dynamic Host Port Mapping if you define only the container port in the task definition
- The ALB finds the right port on your EC2 Instances
- You must allow on the EC2 instance’s Security Group any port from the ALB's Security Group

Amazon ECS — Load Balancing (Fargate)

- Each task has a unique private IP
- Only define the container port (host port is not applicable)

- Example
 - ECS ENI Security Group
  - Allow port 80 from the ALB
 - ALB Security Group
  - Allow port 80/443 from web

Amazon ECS — Environment Variables

- Environment Variable
 - Hardcoded — e.g, URLs
 - SSM Parameter Store — sensitive variables (e.g,, API keys, shared configs)
 - Secrets Manager — sensitive variables (e.g., DB passwords)
- Environment Files (bulk) — Amazon $3

Amazon ECS — Data Volumes (Bind Mounts)

- Share data between multiple containers in the same Task Definition
- Works for both EC2 and Fargate tasks
- EC2 Tasks — using EC2 instance storage
 - Data are tied to the lifecycle of the EC2 instance
- Fargate Tasks — using ephemeral storage
 - Data are tied to the container(s) using them
 - 20 GiB — 200 GiB (default 20 GiB)

- Use cases:
 - Share ephemeral data between multiple containers
 - “Sidecar” container pattern, where the “'sidecar” container used to send metrics/logs to other destinations (separation of conerns)
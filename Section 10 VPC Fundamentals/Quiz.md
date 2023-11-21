# Quiz 7: VPC Quiz

1. Security Groups operate at the ................. level while NACLs operate at the ................. level.

- EC2 Instance, Subnet

2. You have attached an Internet Gateway to your VPC, but your EC2 instances still don't have access to the internet. What is NOT a possible issue?

- The Security Group does not allow traffic in

Security groups are stateful and if traffic can go out, then it can go back in.

3. You would like to provide Internet access to your EC2 instances in private subnets with IPv4 while making sure this solution requires the least amount of administration and scales seamlessly. What should you use?

- NAT Gateway

4. When using VPC Endpoints, what are the only two AWS services that have a Gateway Endpoint available?

- Amazon S3 & DynamoDB 

These two services have a VPC Gateway Endpoint (remember it), all the other ones have an Interface endpoint (powered by Private Link - means a private IP).

5. You have 3 VPCs A, B, and C. You want to establish a VPC Peering connection between all the 3 VPCs. What should you do?

- Establish 3 VPC Peering connections (A-B, A-C, B-C)

6. How can you capture information about IP traffic inside your VPCs?

- Enable VPC Flow Logs

VPC Flow Logs is a VPC feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC.

7. You need to set up a dedicated connection between your on-premises corporate datacenter and AWS Cloud. This connection must be private, consistent, and traffic must not travel through the Internet. Which AWS service should you use?

- AWS Direct Connect

8. A web application hosted on a fleet of EC2 instances managed by an Auto Scaling Group. You are exposing this application through an Application Load Balancer. Both the EC2 instances and the ALB are deployed on a VPC with the following CIDR 192.168.0.0/18. How do you configure the EC2 instances' security group to ensure only the ALB can access them on port 80?

- Add an Inbound Rule with port 80 and ALB's Security Group as the source

This is the most secure way of ensuring only the ALB can access the EC2 instances. Referencing by security groups in rules is an extremely powerful rule and many questions at the exam rely on it. Make sure you fully master the concepts behind it!
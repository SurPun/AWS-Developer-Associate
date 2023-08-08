# Section 12: AWS CLI, SDK, IAM Roles & Policies

## 126. AWS EC2 Instance Metadata

EC2 Instance Metadata (IMDS)

- AWS EC? Instance Metadata (IMDS) is powerful but one of the least known
features to developers
- It allows AWS EC2 instances to "learn about themselves” without using an
IAM Role for that purpose.
-The URL is http://169.254, 169.254/latest/meta-data
-You can retrieve the IAM Role name from the metadata, but you CANNOT
retrieve the IAM Policy.
-Metadata = Info about the EC2 instance
-Userdata = launch script of the EC2 instance

## 129. AWS CLI with MFA

MFA with CLI

- To use MFA with the CLI, you must create a temporary session
- To do so, you must run the STS GetSessionToken API call
- aws sts get-session-token --serial-number arn-of-the-mfa-device --token- code code-from-token --duration-seconds 3600

## 130. AWS SDK Overview

AWS SDK Overview

- We have to use the AWS SDK when coding against AWS Services such
as DynamoDB
- Fun fact... the AWS CLI uses the Python SDK (boto3)
- The exam expects you to know when you should use an SDK
- We'll practice the AWS SDK when we get to the Lambda functions
- Good to know: if you don't specify or configure a default region, then
us-east-1 will be chosen by default
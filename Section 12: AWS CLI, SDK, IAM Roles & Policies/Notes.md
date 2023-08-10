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

## 131. Exponential Backoff & Service Limit Increase

AWS Limits (Quotas)

- API Rate Limits
 - Describelnstances API for EC2 has a limit of 100 calls per seconds
 - GetObject on S3 has a limit of 5500 GET per second per prefix
 - For Intermittent Errors: implement Exponential Backoff
 - For Consistent Errors: request an API throttling limit increase

- Service Quotas (Service Limits)
 - Running On-Demand Standard Instances: | 152 vCPU
 - You can request a service limit increase by opening a ticket
 - You can request a service quota increase by using the Service Quotas API

Exponential Backoff (any AWS service)

- If you get ThrottlingException intermittently, use exponential backoff
- Retry mechanism already included in AWS SDK API calls
- Must implement yourself if using the AWS API as-is or in specific cases
 - Must only implement the retries on 5xx server errors and throttling
 - Do not implement on the 4x client errors

 ## 132. AWS Credentials Provider & Chain

 
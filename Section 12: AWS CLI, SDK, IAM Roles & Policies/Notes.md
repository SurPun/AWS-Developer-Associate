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

## MFA with CLI

MFA with CLI

- To use MFA with the CLI, you must create a temporary session
- To do so, you must run the STS GetSessionToken API call
- aws sts get-session-token --serial-number arn-of-the-mfa-device --token- code code-from-token --duration-seconds 3600
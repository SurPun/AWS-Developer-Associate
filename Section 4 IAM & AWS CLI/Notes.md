# Section 4: IAM & AWS CLI

## 11 IAM (Users, Groups, Policies)

IAM Users should have least privilege which is a principle of granting only the permissions required to complete a task.

## 13 IAM Policies (Manged by AWS or Custom created by users.)

- IAM Policies Structure

  Consists of :

      - Version: policy language version, always include ‘201 2-10-7"
      - Id:an identifier for the policy (optional)
      - Statement: one or more individual statements (required)
        Statements consists of
        - Sid: an identifier for the statement (optional)
        - Effect: whether the statement allows or denies access(Allow, Deny)

## 15 MFA Device

- Authenticator app
- Security Key
- Hardware TOTP Token

## 17 AWS Access Keys, CLI and SDK

What's AWS Access Keys :

- To access AWS, you have three options:

  - AWS Management Console (protected by password + MFA)
  - AWS Command Line Interface (CLI): protected by access keys
  - AWS Software Developer Kit (SDK) - for code: protected by access keys

  - Access Key ID = username

  - Secret Access Key = password

  What's AWS CLI :

  - A tool that enables you to interact with AWS services using commands in your command-line shell

  - Direct access to the public APIs of AWS services

  - You can develop scripts to manage your resources

  - It's open-source https://github.com/aws/aws-cli

  - Alternative to using AWS Management Console

  What's the AWS SDK? :

  - AWS Software Development Kit (AWS SDK)

  - Language-specific APls (set of libraries)

  - Enables you to access and manage AWS services programmatically

  - Embedded within your application

  - Supports
    - SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node .js, C++)
  - Mobile SDKs (Android, iOS, ...)

  - loT Device SDKs (Embedded C, Arduino, ...)

  - Example: AWS CLI is built on AWS SDK for Python

## 22 AWS CloudShell

- Alternative to using AWS CLI
- CloudShell is not available in all region
- CloudShell has its own environment so you get your own repository and you can also download and upload files to and from the environment.

## 23 IAM Roles for AWS Services

- Some AWS service will need to perform actions on your behalf.
- To do so, we will assign permissions to AWS services with IAM Roles.
- Common Roles:
  - EC2 Instance Roles
  - Lambda Function Roles
  - Roles for CloudFormation

## 26 IAM Security Tools Hands On

- IAM Credentials Report (account-level)

  - A report that lists all your account's users and the status of their various credentials

- IAM Access Advisor (user-level)

  - Access advisor shows the service permissions granted to a user and when those services were last accessed.

  - You can use this information to revise your policies.

## 27 IAM Best Practices

IAM Guidelines & Best Practices

- Don't use the root account except for AWS account setup

- One physical user = One AWS user

- Assign users to groups and assign permissions to groups

- Create a strong password policy

- Use and enforce the use of Multi Factor Authentication (MFA)

- Create and use Roles for giving permissions to AWS services

- Use Access Keys for Programmatic Access (CLI / SDK)

- Audit permissions of your account using IAM Credentials Report & IAM
  Access Advisor

- Never share IAM users & Access Keys

## 28 Shared Responsibility Model for IAM

AWS

- Infrastructure (global network security)

- Configuration and vulnerability analysis

- Compliance validation

USER

- Users, Groups, Roles, Policies management and monitoring

- Enable MFA on all accounts Rotate all your keys often

- Use IAM tools to apply appropriate permissions

- Analyze access patterns & review permissions

## 29 IAM Summary

- Users: mapped to a physical user, has a password for AWS Console
- Groups: contains users only
- Policies: JSON document that outlines permissions for users or groups
- Roles: for EC2 instances or AWS services
- Security: MFA + Password Policy
- AWS CLI: manage your AWS services using the command-line
- AWS SDK: manage your AWS services using a programming language
- Access Keys: access AWS using the CL! or SDK
- Audit: IAM Credential Reports & IAM Access Advisor

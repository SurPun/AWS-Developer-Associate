# Quiz 1: IAM & AWS CLI Quiz

1. What is a proper definition of an IAM Role?

   - An IAM entity that defines a set of permissions for making requests to AWS services, and will be used by an AWS service.

Some AWS services need to perform actions on your behalf. To do so, you assign permissions to AWS services with IAM Roles.

2. Which of the following is an IAM Security Tool?

   - IAM Credentials Report

IAM Credentials report lists all your AWS Account's IAM Users and the status of their various credentials.

3. Which answer is INCORRECT regarding IAM Users?

   - IAM Users access AWS services using root account credentials

IAM Users access AWS services using their own credentials (username & password or Access Keys).

4. Which of the following is an IAM best practice?

   - Don't use the root user account

Use the root account only to create your first IAM User and a few account/service management tasks. For everyday tasks, use an IAM User.

5. What are IAM Policies?

   - JSON documents that define a set of permissions for making requests to AWS services, and can be used by IAM Users, User Groups, and IAM Roles.

6. Which principle should you apply regarding IAM Permissions?

   - Grant least Privilege

7. What should you do to increase your root account security?

   - Enable Multi-Factor Authentication (MFA)

When you enable MFA, this adds another layer of security. Even if your password is stolen, lost, or hacked your account is not compromised.

8. IAM User Groups can contain IAM Users and other User Groups.

   - False

IAM User Groups can contain only IAM Users.

9. An IAM policy consists of one or more statements. A statement in an IAM Policy consists of the following, EXCEPT:

   - Version

A statement in an IAM Policy consists of Sid, Effect, Principal, Action, Resource, and Condition. Version is part of the IAM Policy itself, not the statement.

10. According to the AWS Shared Responsibility Model, which of the following is AWS responsibility?

    - AWS Infrastructure

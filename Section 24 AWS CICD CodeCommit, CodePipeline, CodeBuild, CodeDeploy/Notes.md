# Section 24: AWS CICD: CodeCommit, CodePipeline, CodeBuild, CodeDeploy

## 363. Introduction to CICD in AWS

CICD — Introduction

- We have learned how to:
 - Create AWS resources, manually (fundamentals)
 - Interact with AWS programmatically (AWS CLI)
 - Deploy code to AWS using Elastic Beanstalk

- All these manual steps make it very likely for us to do mistakes!

- We would like our code “in a repository” and have it deployed onto AWS
 - Automatically
 - The right way
 - Making sure it's tested before being deployed
 - With possibility to go into different stages (dey, test, staging, prod)
 - With manual approval where needed

- To be a proper AWS developer... we need to learn AWS CICD

CICD — Introduction

- This section is all about automating the deployment we've done so far while adding increased safety

- We'll learn about:
 - AWS CodeCommit — storing our code
 - AWS CodePipeline — automating our pipeline from code to Elastic Beanstalk
 - AWS CodeBuild — building and testing our code
 - AWS CodeDeploy — deploying the code to EC2 instances (not Elastic Beanstalk)
 - AWS CodeStar — manage software development activities in one place
 - AWS CodeArtifact — store, publish, and share software packages
 - AWS CodeGuru — automated code reviews using Machine Learning

Continuous Integration (Cl)

- Developers push the code to a code repository often (e.g., GitHub, CodeCommit, Bitbucket...)
- A testing / build server checks the code as soon as It's pushed (CodeBuild, Jenkins Cl, ...)
- The developer gets feedback about the tests and checks that have passed / failed
- Find bugs early, then fix bugs
- Deliver faster as the code is tested
- Deploy often
- Happier developers, as they're unblocked

Continuous Delivery (CD)

- Ensures that the software can be released reliably whenever needed
- Ensures deployments happen often and are quick
- Shift away from “one release every 3 months” to "5 releases a day”
- That usually means automated deployment (e.g., CodeDeploy, Jenkins CD, Spinnaker, ...

## 364. CodeCommit Overview

AWS CodeCommit

- Version control is the ability to understand the various changes that happened to the code over time (and possibly roll back)
- All these are enabled by using a version control system such as Git
- A Git repository can be synchronized on your computer, but it usually is uploaded on a central online repository
- Benefits are:
 - Collaborate with other developers
 - Make sure the code is backed-up somewhere
 - Make sure it's fully viewable and auditable

AWS CodeCommit

- Git repositories can be expensive
- The industry includes GitHub, GitLab, Bitbucket, ...
- And AWS CodeCommit:
 - Private Git repositories
 - No size limit on repositories (scale seamlessly)
 - Fully managed, highly available
 - Code only in AWS Cloud account => increased security and compliance
 - Security (encrypted, access control, ...)
 - Integrated with Jenkins, AWS CodeBuild, and other Cl tools

CodeCommit — Security

- Interactions are done using Git (standard)
- Authentication
 - SSH Keys —- AWS Users can configure SSH keys in their IAM Console
 - HTTPS — with AWS CLI Credential helper or Git Credentials for IAM user

- Authorization
 - IAM policies to manage users/roles permissions to repositories
- Encryption
 - Repositories are automatically encrypted at rest using AWS KMS
 - Encrypted in transit (can only use HTTPS or SSH — both secure)
- Cross-account Access
 - Do NOT share your SSH keys or your AWS credentials
 - Use an IAM Role in your AWS account and use AWS STS (AssumeRole API)


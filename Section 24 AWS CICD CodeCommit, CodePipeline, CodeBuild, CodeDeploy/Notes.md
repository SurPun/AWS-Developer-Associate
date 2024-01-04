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

## 367. CodePipeline Overview

AWS CodePipeline

- Visual Workflow to orchestrate your CICD
- Source — CodeCommit, ECR, $3, Bitbucket, GitHub
- Build — CodeBuild, Jenkins, CloudBees, TeamCity
- Test — CodeBuild, AWS Device Farm, 3"? party tools, ...
- Deploy — CodeDeploy, Elastic Beanstalk, CloudFormation, ECS, S3, ...
- Invoke — Lambda, Step Functions
- Consists of stages:
 - Each stage can have sequential actions and/or parallel actions
 - Example: Build > Test Deploy => LoadTesting > ...
 - Manual approval can be defined at any stage

CodePipeline — Artifacts

- Each pipeline stage can create artifacts
- Artifacts stored in an S3 bucket and passed on to the next stage

CodePipeline — Troubleshooting

- For CodePipeline Pipeline/Action/Stage Execution State Changes
- Use CloudWatch Events (Amazon EventBridge). Example:
 - You can create events for failed pipelines
 - You can create events for cancelled stages

- If CodePipeline fails a stage, your pipeline stops, and you can get information in the console
- If pipeline can't perform an action, make sure the “IAM Service Role attached does have enough IAM permissions (IAM Policy)
- AWS CloudTrail can be used to audit AWS API calls

## 370. CodeBuild Overview

AWS CodeBuild

- Source — CodeCommit, 3, Bitbucket, GitHub
- Build instructions: Code file buildspec.yml or insert manually in Console
- Output logs can be stored in Amazon S3 & CloudWatch Logs
- Use CloudWatch Metrics to monitor build statistics
- Use EventBridge to detect failed builds and trigger notifications
- Use CloudWatch Alarms to notify if you need “thresholds” for failures

- Build Projects can be defined within CodePipeline or CodeBuild

CodeBuild — Supported Environments

- Java
- Ruby
- Python
- Go
- Node,js
- Android
- NET Core
- PHP
- Docker — extend any environment you like

CodeBuild — buildspec.yml

- buildspec.yml file must be at the root of your code
- env — define environment variables
 - variables — plaintext variables
 - parameter-store — variables stored in SSM Parameter Store
 - secrets-manager — variables stored in AWS Secrets Manager

- phases — specify commands to run:
 - install — install dependencies you may need for your build
 - pre_build — final commands to execute before build
 - Build — actual build commands
 - post_build — finishing touches (e.g,, zip output)

- artifacts — what to upload to S3 (encrypted with KMS)
- cache — files to cache (usually dependencies) to S3 for future build speedup

## 373. CodeDeploy Overview

AWS CodeDeploy

- Deployment service that automates application deployment
- Deploy new applications versions to EC2 Instances, On-premises servers, Lambda functions, ECS Services
- Automated Rollback capability in case of failed deployments, or trigger CloudWatch Alarm
- Gradual deployment control
- A file named appspec.yml defines how the deployment happens

CodeDeploy — EC2/On-premises Platform

- Can deploy to EC2 Instances & on-premises servers
- Perform in-place deployments or blue/green deployments
- Must run the CodeDeploy Agent on the target instances
- Define deployment speed
 - AllAtOnce: most downtime
 - HalfAtATime: reduced capacity by 50%
 - OneAtATime: slowest, lowest availability impact
 - Custom: define your %

CodeDeploy Agent

- The CodeDeploy Agent must be running on the EC2 instances as a pre- requisites
- It can be installed and updated automatically if you're using Systems Manager
- The EC2 Instances must have sufficient permissions to access Amazon S3 to get deployment bundles

CodeDeploy — Lambda Platform

- CodeDeploy can help you automate traffic shift for Lambda aliases
- Feature is integrated within the SAM framework
- Linear: grow traffic every N minutes until 100%
 - LambdaLinear 1OPercentEvery3Minutes
 - LambdaLinear 1OPercentEvery1OMinutes
- Canary: try X percent then 100%
 - LambdaCanary 1OPercent5Minutes
 - LambdaCanary 1OPercent30Minutes
- AllAtOnce: immediate

CodeDeploy — ECS Platform

- CodeDeploy can help you automate the deployment of a new ECS Task Definition
- Only Blue/Green Deployments
- Linear: grow traffic every N minutes until 100%
 - ECSLinear 1OPercentEvery3Minutes
 - ECSLinear 10PercentEvery1OMinutes
- Canary: try X percent then 100%
 - ECSCanary 1OPercent5Minutes
 - ECSCanary 1OPercent30Minutes
 - AllAtOnce: immediate


# Section 25 AWS Serverless Sam - Serverless Application Model

## 385. SAM Overview

AWS SAM

- SAM = Serverless Application Model
- Framework for developing and deploying serverless applications
- All the configuration is YAML code
- Generate complex CloudFormation from simple SAM YAML file
- Supports anything from CloudFormation: Outputs, Mappings, Parameters, Resources...
- Only two commands to deploy to AWS
- SAM can use CodeDeploy to deploy Lambda functions
- SAM can help you to run Lambda, API Gateway, DynamoDB locally

AWS SAM — Recipe

- Transform Header indicates it’s SAM template:
 - Transform: ‘AWS: :Serverless-2016-10-31'
- Write Code
 - AWS: :Serverless::Function
 - AWS: :Serverless: :Api
 - AWS: :Serverless::SimpleTable
- Package & Deploy:
 - aws cloudformation package / sam package
 - aws cloudformation deploy / sam deploy

SAM — CLI Debugging

- Locally build, test, and debug your serverless applications that are defined using AWS SAM templates
- Provides a lambda-like execution environment locally
- SAM CLI + AWS Toolkits => step-through and debug your code
- Supported IDEs: AWS Cloud9, Visual Studio Code, JetBrains, PyCharm, IntelliJ, ..
- AWS Toolkits: IDE plugins which allots you to build, test, debug, deploy, and cee Lambda functions built using AWS SAM

## 391. SAM Policy Templates

SAM Policy Templates

- List of templates to apply permissions to your lambda Functiions
- Full list available here: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-policy-templates.html#serverless-policy-template-table
- Important examples:
 - S3ReadPolicy: Gives read only permissions to objects in S3
 - SQSPollerPolicy: Allows to poll an SQS queue
 - DynamoDBCrudPolicy: CRUD = create read update delete

## 392. SAM with CodeDeploy

SAM and CodeDeploy

- SAM framework natively uses CodeDeploy to update Lambda functions
- Traffic Shifting feature
- Pre and Post traffic hooks features to validate deployment (before the traffic shift starts and after it ends)
- Easy & automated rollback using CloudWatch Alarms

SAM and CodeDeploy

- AutoPublishAlias
 - Detects when new code is being deployed
 - Creates and publishes an updated
 - Points of that function with the latest code
 - Points the alias to the updated version of the Lambda function

- DeploymentPreference
 - Canary, Linear, AllAtOnce
- Alarms
 - Alarms that can trigger a rollback
- Hooks
 - Pre and post traffic shifting Lambda functions to test your deployment
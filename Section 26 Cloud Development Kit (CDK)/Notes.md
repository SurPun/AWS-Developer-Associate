# Section 26 Cloud Development Kit (CDK)

## 395. AWS Cloud Development Kit (CDK)

- Define your cloud infrastructure using a familiar language:
 - JavaScript/TypeScript, Python, Java, and .NET

- Contains high level components called constructs

- The code is “compiled” into a CloudFormation template (JSON/YAML)

- You can therefore deploy infrastructure and application runtime code together
 - Great for Lambda functions
 - Great for Docker containers in ECS / EKS

CDK vs SAM

- SAM:
 - Serverless focused
 - Write your template declaratively in JSON orYAML
 - Great for quickly getting started with Lambda
 - Leverages CloudFormation

- CDK
 - All AWS services
 - Write infra in a programming language JavaScript/TypeScript, Python, Java, and NET
 - Leverages CloudFormation

CDK + SAM

- You can use SAM CLI to locally test your CDK apps
- You must first run cdk synth


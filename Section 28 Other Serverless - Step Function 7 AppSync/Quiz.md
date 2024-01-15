# Quiz 25: Other Serverless Quiz

1. You want to orchestrate a series of AWS Lambda functions into a workflow. Which AWS service should you use?

- AWS Step Functions

AWS Step Functions is a low-code visual workflow service used to orchestrate AWS services, automate business processes, and build Serverless applications. It manages failures, retries, parallelization, service integrations, ...

2. Your developers are creating a mobile application and would like to have a managed GraphQL backend. Which AWS service do you recommend?

- AWS AppSync

AWS AppSync is a fully managed service that makes it easy to develop GraphQL APIs by handling the heavy lifting of securely connecting to data sources like DynamoDB, Lambda, and more.

3. You want to orchestrate multiple Lambda functions and wait for the result of all of them before making a final decision. What do you recommend?

- Step Functions Parallel States and then one final Task State

4. You have a Step Functions workflow which consists of a series of Task States invoking a set of Lambda functions. While execution, one of the states has an error with the following error code States.Permissions. How do you solve this problem?

- You need to give the Step Functions workflow the required IAM permissions to execute the Lambda function invoked by this Task State

5. Which of the following AWS services does not support the WebSocket protocol?

- DynamoDB

6. You have a GraphQL based API hosted on-premises that you want to migrate to AWS. Which AWS service should you choose?

- AppSync
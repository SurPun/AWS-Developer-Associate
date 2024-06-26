# Quiz 18: Lambda Quiz

1. You have created a Lambda function that typically will take around 1 hour to process some data. The code works fine when you run it locally on your machine, but when you invoke the Lambda function it fails with a "timeout" error after 3 seconds. What should you do?

- Run your code somewhere else (e.g., EC2 instance)

Lambda's maximum execution time is 15 minutes. You can run your code somewhere else such as an EC2 instance or use Amazon ECS.

2. Which of the following is the best way to inject a dynamic DB_URL variable into your Lambda function's code?

- Use Lambda's Environment Variables

Lambda's Environment Variables allows you to adjust your function's behavior without updating code.

3. A Lambda function that's invoked asynchronously, fails to process from time to time after 3 retries. To troubleshoot the issue, you would like to collect and analyze these events later on. What is the best practice you can do?

- Add a Dead Letter Queue (DLQ) to send messages to SQS

This is good as SQS will hold the failed messages for some days so we have time to consume and analyze them.

4. You have enabled a Dead Letter Queue (DLQ) for your Lambda function and configured it to send failed messages to SNS. While testing, you don't see any events there even though you can tell from CloudWatch metrics that you have failures. What is most likely the reason for this?

- Your Lambda function's execution role is missing permissions

5. You have enabled X-Ray integration on your Lambda function but it doesn't work. What is a possible cause for this?

- Check IAM permissions in your lambda function's execution role

6. While updating a Lambda function, you get the following exception An error occurred: InvalidParameterValueException when calling the UpdateFunctionCode operation: Unzipped size must be smaller than 262144000 bytes. How should you solve this issue?

- The uncompressed deployment package .zip exceeds AWS Lambda Limits

7. A Lambda function makes requests to 3rd party API. To successfully make the requests, the 3rd party API requires you to send a token which is a long string of 8 KB. Where should you place this token?

- Place it in the deployment package .zip file

8. Every time you release a Lambda function version, it gets a new number and you have to manually update all the AWS resources linked to your function (e.g., event triggers). What should you do?

- Use Lambda Aliases, and update the Alias to point to the new version

9. You have updated a Lambda function and created a new version. Now, you want to test out the new version and ensure it can sustain production traffic. You are risk-averse and don't want to take down your whole application. What should you do?

- Use Lambda Aliases, and point to the new and old versions, then assign weights

10. You have a Lambda function used to retrieve data from an RDS DB instance. Each time the Lambda function is invoked, it establishes a new connection to your database. These connections make a load on your database and degrade its performance. So, you tell your developers to use long-lived database connections. They tell you that .......................................

- They will move the database connection object outside of the function handler

11. Your Lambda function written in Node.js wants to connect to an RDS PostgreSQL database in your VPC. The Lambda function must use the Node.js driver for PostgreSQL to connect to the database. How do you bundle your Lambda function to add the dependencies?

- Put the function and the dependencies in one folder and zip them together

12. How do you declare a Lambda function in a CloudFormation template?

- Upload all the code asa_ .zip file to an S3 bucket and refer to the object in AWS: : Lambda: : Function block

13. Which of the following allows you to deploy your Lambda function globally so that requests made to a CloudFront distribution are filtered at the AWS Edge Locations?

- Lambda@Edge

14. What is the recommended way to store temporary files used by your Lambda function that will be discarded when the function stops execution?

- Use the local directory /tmp

15. The maximum size for a Lambda function /tmp space is .........................

- 10240 MB

16. Which of the following AWS services allows you to schedule your Lambda function to be invoked every hour?

- Amazon EventBridge

https://docs.aws.amazon.com/lambda/latest/dg/services-cloudwatchevents.html

17. To use your Lambda function with an Application Load Balancer, the Lambda function must be registered with ...........................

- A Target Group

18. You have enabled and configured Event Notifications in your S3 bucket to invoke a Lambda function every time an object is uploaded to your S3 bucket. You have noticed that there's duplicate logging into CloudWatch Logs with the same request ID. What do you think is the reason for this?

- The Lambda function has failed and retries have happened

19. Which of the following AWS service does NOT require a Lambda Event Source Mapping?

- Simple Notification Service (SNS)

Because it's asynchronous.

20. Which of the following is the recommended way to send the result of an asynchronous Lambda function to an SQS queue?

- Use Lambda Destinations

21. AWS Lambda natively supports the following programming languages, EXCEPT .......................

- C++

22. You have a Lambda function written in Python which has a lot of dependencies. Each time you update and deploy your function, it takes 15 minutes to natively compile these dependencies and therefore deployments have been really slow. What do you suggest?

- Create a Lambda Layer and include all the dependencies in it

23. You want to give another AWS account access to invoke a Lambda function in your AWS account. Which of the following can NOT be used to do so?

- Lambda Execution Role

24. You have a CloudFormation template that declares a Lambda function. The Lambda function's code is stored in an S3 bucket with Versioning enabled. You use S3Bucket, S3Key, and S3ObjectVersion in the CloudFormation template to reference the code. You have updated the Lambda function's code then uploaded it to S3, but the function hasn't been updated. What should you do?

- Update S30bjectVersion to reference the updated code

25. Which of the following Lambda features can NOT be used to create a custom runtime if it isn't natively supported by AWS Lambda?

- Lambda Destinations

26. You are using CodeDeploy for automated deployments to your Lambda function. You updated your Lambda function's code and want to deploy the new version, test it with a small amount of traffic, then totally shift to the new version. Which CodeDeploy deployment type do you recommend?

- Canary
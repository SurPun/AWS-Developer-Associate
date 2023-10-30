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

6. 
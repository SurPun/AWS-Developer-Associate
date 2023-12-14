Quiz 17: Monitoring & Audit Quiz

1. You have a couple of EC2 instances in which you would like their Standard CloudWatch Metrics to be collected every 1 minute. What should you do?

- Enable Detailed Monitoring

This is a paid offering and is disabled by default. When enabled, the EC2 instance's metrics are available in 1-minute periods.

2. High-Resolution Custom Metrics can have a minimum resolution of ........................

- 1 second

3. You have an RDS DB instance that's configured to push its database logs to CloudWatch. You want to create a CloudWatch alarm if there's an Error found in the logs. How would you do that?

- Create a CloudWatch Logs Metric Filter that filter the logs for the keyword Error , then create a CloudWatch Alarm based on that Metric Filter

4. You have an application hosted on a fleet of EC2 instances managed by an Auto Scaling Group that you configured its minimum capacity to 2. Also, you have created a CloudWatch Alarm that is configured to scale in your ASG when CPU Utilization is below 60%. Currently, your application runs on 2 EC2 instances and has low traffic and the CloudWatch Alarm is in the ALARM state. What will happen?

- The CloudWatch Alarm will remain in ALARM state but never decrease the number of EC2 instances in the ASG

The number of EC2 instances in an ASG can not go below the minimum capacity, even if the CloudWatch alarm would in theory trigger an EC2 instance termination.

5. How would you monitor your EC2 instance memory usage in CloudWatch?

- Use Unified CloudWatch Agent to push memory usage as a custom metric to CloudWatch

6. A CloudWatch Alarm set on a High-Resolution Custom Metric can be triggered as often as ......................

- 10 seconds

If you set an alarm on a high-resolution metric, you can specify a high-resolution alarm with a period of 10 seconds or 30 seconds, or you can set a regular alarm with a period of any multiple of 60 seconds.

7. You have made a configuration change and would like to evaluate the impact of it on the performance of your application. Which AWS service should you use?

- Amazon CloudWatch

8. Someone has terminated an EC2 instance in your AWS account last week, which was hosting a critical database that contains sensitive data. Which AWS service helps you find who did that and when?

- AWS CloudTrail

AWS CloudTrail allows you to log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. It provides the event history of your AWS account activity, audit API calls made through the AWS Management Console, AWS SDKs, AWS CLI. So, the EC2 instance termination API call will appear here. You can use CloudTrail to detect unusual activity in your AWS accounts.

9. You have CloudTrail enabled for your AWS Account in all AWS Regions. What should you use to detect unusual activity in your AWS Account?

- CloudTrail Insights

10. One of your teammates terminated an EC2 instance 4 months ago which has critical data. You don't know who made this so you are going to review all API calls within this period using CloudTrail. You already have CloudTrail set up and configured to send logs to the S3 bucket. What should you do to find out who made this?

- Analyze CloudTrail logs in S3 bucket using Amazon Athena

You can use the CloudTrail Console to view the last 90 days of recorded API activity. For events older than 90 days, use Athena to analyze CloudTrail logs stored in the S3 bucket.

11. Someone changed the configuration of a resource and made it non-compliant. Which AWS service can you use to find out who made the change?

- AWS CloudTrail

12. You would like to test out a complex CloudWatch Alarm that responds to globally increased traffic on your application. You are in a test environment. How can you test out this alarm in a cost-effective manner and efficiently?

- Use the set-alarm-state CLI command

13. You want to continuously monitor RAM usage for an application hosted on an EC2 instance. By default, CloudWatch doesn't push RAM usage, so you will use a CloudWatch custom metric. Which API call allows you to push custom metric data to CloudWatch?

- PutMetricData

14. By default, all logs stored in CloudWatch Logs are automatically expiring after 7 days.

- False

By default, they never expire.

15. In CloudWatch Logs, Log Retention Policy defined at ........................... level.

- Log Groups
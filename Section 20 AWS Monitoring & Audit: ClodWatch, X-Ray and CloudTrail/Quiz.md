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
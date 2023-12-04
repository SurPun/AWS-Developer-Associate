# Section 20 AWS Monitoring & Audit: ClodWatch, X-Ray and CloudTrail

## 242. Monitoring Overview in AWS

Why Monitoring is Important

- We know how to deploy applications
 - Safely
 - Automatically
 - Using Infrastructure as Code
 - Leveraging the best AWS components!

- Our applications are deployed, and our users don't care how we did it...

- Our users only care that the application is working!
 - Application latency: will it increase over time?
 - Application outages: customer experience should not be degraded
 - Users contacting the IT department or complaining is not a good outcome
 - Troubleshooting and remediation

- Internal monitoring:
 - Can we prevent issues before they happen?
 - Performance and Cost
 - Trends (scaling patterns)
 - Learning and Improvement

Monitoring in AWS

- AWS CloudWatch:
 - Metrics: Collect and track key metrics
 - Logs: Collect, monitor analyze and store log files
 - Events: Send notifications when certain events happen in your AWS
 - Alarms: React in real-time to metrics / events

- AWS X-Ray:
 - Troubleshooting application performance and errors
 - Distributed tracing of microservices

- AWS Cloud Trail:
 - Internal monitoring of API calls being made
 - Audit changes to AWS Resources by your users

# 243. CloudWatch Custom Metrics

CloudWatch Custom Metrics

- Possibility to define and send your own custom metrics to CloudWatch
- Example: memory (RAM) usage, disk space, number of logged in users ...
- Use API call PutMetricData

- Ability to use dimensions (attributes) to segment metrics
 - Instance.id
 - Environment.name
 
- Metric resolution (StorageResolution API parameter — two possible value):
 - Standard: 1 minute (60 seconds)
 - High Resolution: 1/5/10/30 second(s) — Higher cost
- Important: Accepts metric data points two weeks in the past and two hours in the future (make sure to configure your EC2 instance time correctly)
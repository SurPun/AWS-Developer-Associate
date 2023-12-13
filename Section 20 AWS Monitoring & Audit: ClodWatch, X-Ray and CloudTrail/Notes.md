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

## 243. CloudWatch Custom Metrics

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

## 244. CloudWatch Logs

CloudWatch Logs

- Log groups: arbitrary name, usually representing an application
- Log stream: instances within application / log files / containers
- Can define log expiration policies (never expire, 1 day to 10 years...)
- CloudWatch Logs can send logs to:
 - Amazon S3 (exports)
 - Kinesis Data Streams
 - Kinesis Data Firehose
 - AWS Lambda
 - OpenSearch

- Logs are encrypted by default
- Can setup KMS-based encryption with your own keys

CloudWatch Logs - Sources

- SDK, CloudWatch Logs Agent, CloudWatch Unified Agent
- Elastic Beanstalk: collection of logs from application
- ECS: collection from containers
- AWS Lambda: collection from function logs
- VPC Flow Logs:VPC specific logs
- API Gateway
- Cloud Trail based on filter
- Route53: Log DNS queries

CloudWatch Logs Insights

- Search and analyze log data stored in CloudWatch Logs
- Example: find a specific IP inside a log, count occurrences of “ERROR" in your logs...
- Provides a purpose-built query language
 - Automatically discovers fields from AWS services and JSON log events
 - Fetch desired event fields, fitter based on conditions, calculate aggregate statistics, sort events, limit number of events...
 - Can save queries and add them to CloudWatch Dashboards

- Can query multiple Log Groups in different AWS accounts
- It's a query engine, not a real-time engine

CloudWatch Logs — S3 Export

- Log data can take up to 12 hours to become available for export
- The API call is CreateExportTask
- Not near-real time or real-time... use Logs Subscriptions instead

CloudWatch Logs Subscriptions

- Get a real-time log events from CloudWatch Logs for processing and analysis
- Send to Kinesis Data Streams, Kinesis Data Firehose, or Lambda
- Subscription Filter — filter which logs are events delivered to your destination

CloudWatch Logs Subscriptions

- Cross-Account Subscription — send log events to resources in a different AWS account (KDS, KDF)

## 246. CloudWatch Agent & CloudWatch Logs Agent

CloudWatch Logs for EC2

- By default, no logs from your EC2 machine will go to CloudWatch
- You need to run a CloudWatch agent on EC2 to push the log files you want
- Make sure IAM permissions are correct
- The CloudWatch log agent can be setup on-premises too

CloudWatch Logs Agent & Unified Agent

- For virtual servers (EC2 instances, on-premise servers...)
- CloudWatch Logs Agent
 - Old version of the agent
 - Can only send to CloudWatch Logs

- CloudWatch Unified Agent
 - Collect additional system-level metrics such as RAM processes, etc...
 - Collect logs to send to CloudWatch Logs
 - Centralized configuration using SSM Parameter Store

CloudWatch Unified Agent — Metrics

- Collected directly on your Linux server / EC2 instance
- CPU (active, guest, idle, system, user, steal)
- Disk metrics (free, used, total), Disk IO (writes, reads, bytes, iops)
- RAM (free, inactive, used, total, cached)
- Netstat (number of TCP and UDP connections, net packets, bytes)
- Processes (total, dead, bloqued, idle, running, sleep)
- Swap Space (free, used, used %)
- Reminder: out-of-the box metrics for EC2 — disk, CPU, network (high level)

## 247. CloudWatch Logs - Metric Filters

CloudWatch Logs Metric Filter

- CloudWatch Logs can use filter expressions
 - For example, find a specific IP inside of a log
 - Or count occurrences of ERROR’ in your logs
 - Metric filters can be used to trigger alarms

- Filters do not retroactively filter data. Filters only publish the metric data points for events that happen after the filter was created.

- Ability to specify up to 3 Dimensions for the Metric Filter (optional)

## 249. CloudWatch Alarms

CloudWatch Alarms

- Alarms are used to trigger notifications for any metric
- Various options (sampling, %, max, min, etc...)
- Alarm States:
 - OK
 - INSUFFICIENT_DATA
 - ALARM

- Period:
 - Length of time in seconds to evaluate the metric
 - High resolution custom metrics: 10 sec, 30 sec or multiples of 60 sec

CloudWatch Alarm Targets

- Stop, Terminate, Reboot, or Recover an EC2 Instance
- Trigger Auto Scaling Action
- Send notification to SNS (from which you can do pretty much anything)

- Amazon EC2 - EC2 Auto Scaling - Amazon SNS

CloudWatch Alarms — Composite Alarms

- CloudWatch Alarms are on a single metric
- Composite Alarms are monitoring the states of multiple other alarms
- AND and OR conditions
- Helpful to reduce “alarm noise” by creating complex composite alarms

EC2 Instance Recovery

- Status Check:
 - Instance status = check the EC2 VM
 - System status = check the underlying hardware

- Recovery: Same Private, Public, Elastic IP metadata, placement group

CloudWatch Alarm: good to know

- Alarms can be created based on CloudWatch Logs Metrics Filters

- To test alarms and notifications, set the alarm state to Alarm using CLI aws cloudwatch set-alarm-state --alarm-name "myalarm" --state-value ALARM --state-reason "testing purposes"

## 251. CloudWatch Synthetics

- Configurable script that monitor your APIs, URLs, Websites, ...
- Reproduce what your customers do programmatically to find issues before customers are impacted
- Checks the availability and latency of your endpoints and_can store load time data and screenshots of the U
- Integration with CloudWatch Alarms
- Scripts written in Node.js or Python
- Programmatic access to a headless Google Chrome browser
- Can run once or on a regular schedule

## 252. Amazon EventBridge

Amazon EventBridge (formerly CloudWatch Events)

- Schedule: Cron jobs (scheduled scripts)
    - Schedule Every hour => Trigger script on Lambda function

- Event Pattern: Event rules to react to a service doing something
    - IAM Root User Sign in Event => SNS Topic with Email Notification

- Trigger Lambda functions, send SQS/SNS messages...

Amazon EventBridge

- Event buses can be accessed by other AWS accounts using Resource-based Policies

- You can archive events (all/filter) sent to an event bus (indefinitely or set period)

- Ability to replay archived events

Amazon EventBridge — Schema Registry

- EventBridge can analyze the events in your bus and infer the schema

- The Schema Registry allows you to generate code for your application, that will know in advance how data is structured in the event bus

- Schema can be versioned

Amazon EventBridge — Resource-based Policy

- Manage permissions for a specific Event Bus
- Example: allow/deny events from another AWS account or AWS region
- Use case: aggregate e all events from your AWS Organization in a single AWSaccount or region

## 255. X-Ray Overview

AWS X-Ray

- Debugging in Production, the good old way:
 - Test locally
 - Add log statements everywhere
 - Re-deploy in production

- Log formats differ across applications using CloudWatch and analytics is hard.
- Debugging: monolith “easy”, distributed services “hard”
- No common views of your entire architecture!
- Enter... AVVS X-Ray!

AWS X-Ray advantages

- Troubleshooting performance (bottlenecks)
- Understand dependencies in a microservice architecture
- Pinpoint service issues
- Review request behavior
- Find errors and exceptions
- Are we meeting time SLA?
- Where I am throttled?
- Identify users that are impacted

X-Ray compatibility

- AWS Lambda
- Elastic Beanstalk
- ECS
- ELB
- API Gateway
- EC2 Instances or any application server (even on premise)

AWS X-Ray Leverages Tracing

- Tracing is an end to end way to following a “request”
- Each component dealing with the request adds its own “trace”
- Tracing is made of segments (+ sub segments)
- Annotations can be added to traces to provide extra-information
- Ability to trace:
    - Every request
    - Sample request (as a % for example or a rate per minute)
- X-Ray Security:
    - IAM for authorization
    - KMS for encryption at rest


AWS X-Ray How to enable it?

1. Your code (Java, Python, Go, Node,js, .NET) must import the AWS X-Ray SDK
- Very little code modification needed
- The application SDK will then capture:
    - Calls to AWS services
    - HTTP / HTTPS requests
    - Database Calls (MySQL, PostgreSQL, DynamoDB)
    - Queue calls (SQS)

2) Install the X-Ray daemon or enable X-Ray AWS Integration
-  X-Ray daemon works as a low level UDP packet interceptor (Linux / Windows / Mac...)
- AWS Lambda / other AWS services already run the X-Ray daemon for you
- Each application must have the IAM rights to write data to X-Ray

The X-Ray magic

- X-Ray service collects data from all the different services
- Service map is computed from all the segments and traces
- X-Ray is graphical, so even non technical people can help troubleshoot

AWS X-Ray Troubleshooting

- If X-Ray is not working on EC2
 - Ensure the EC2 IAM Role has the proper permissions
 - Ensure the EC2 instance is running the X-Ray Daemon

- To enable on AWS Lambda:
 - Ensure it has an IAM execution role with proper policy (AWSX-RayWriteOnlyAccess)
 - Ensure that X-Ray is imported in the code
 - Enable Lambda X-Ray Active Tracing

## 257. X-Ray: Instrumentation and Concepts

X-Ray Instrumentation in your code

- Instrumentation means the measure of product's performance, diagnose errors, and to write trace information.
- To instrument your application code, you use the X-Ray SDK
- Many SDK require only configuration changes
- You can modify your application code to customize and annotation the data that the SDK sends to X- Ray, using interceptors, filters, handlers, middleware...

X-Ray Concepts

- Segments: each application / service will send them
- Subsegments: if you need more details in your segment
- Trace: segments collected together to form an end-to-end trace
- Sampling: decrease the amount of requests sent to X-Ray, reduce cost
- Annotations: Key Value pairs used to index traces and use with filters
- Metadata: Key Value pairs, not indexed, not used for searching

- The X-Ray daemon / agent has a config to send traces cross account:
    - make sure the IAM permissions are correct — the agent will assume the role
    - This allows to have a central account for all your application tracing

X-Ray Sampling Rules

- With sampling rules, you control the amount of data that you record
- You can modify sampling rules without changing your code

- By default, the X-Ray SDK records the first request each second, and five percent of any additional requests.
- One request per second is the reservoir, which ensures that at least one trace is recorded each second as long the service is serving requests.
- Five percent is the rate at which additional requests beyond the reservoir size are sampled.

X-Ray Custom Sampling Rules

- You can create your own rules with the reservoir and rate

Example Higher minimum rate for POSTs

- Rule name - POST minimum
- Priority - 100
- Reservoir - 10
- Rate - 0.10
- Service name - *
- Service type - *
- Host - *
- HTTP method - POST
- URL path - *
- Resource ARN - *

Example Debugging rule to trace all requests for a problematic route

A high-priority rule applied temporarily for debugging.

- Rule name - DEBUG - history updates Priority - 1
- Reservoir - 1
- Rate - 1
- Service name - Scorekeep
- Service type - *
- Host - *
- HTTP method - PUT
- URL path - /history/*
- Resource ARN - *

## 259. X-Ray APIs

X-Ray Write APls (used by the X-Ray daemon)

```
"Effect": "Allow",

"Action": [
    “xray:PutTraceSegments",
    "xray:PutTelemetryRecords",
    "xray:GetSamplingRules",
    "xray:GetSamplingTargets",
    "xray:GetSamplingStatisticSummaries"
],

"Resource": [
    "*"
]
```

- PutTraceSegments: Uploads segment documents to AWS X-Ray
- PutTelemetryRecords: Used by the AWS X-Ray daemon to upload telemetry.
    - SegmentsReceivedCount,
    - SegmentsRejectedCounts,
    - BackendConnectionErrors...

- GetSamplingRules: Retrieve all sampling rules (to know what/when to send)
- GetSampling Targets & GetSamplingStatisticSummaries: advanced
- The X-Ray daemon needs to have an IAM policy authorizing the correct API calls to function correctly.

X-Ray Read APIs — continued

```
"Effect": "Allow",

"Action": [
    "xray:GetSamplingRules",
    “xray:GetSamplingTargets",
    "xray:GetSamplingStatisticSummaries",
    “xray:BatchGetTraces",
    “xray:GetServiceGraph",
    "xray:GetTraceGraph",
    “xray:GetTraceSummaries",
    "xray:GetGroups",
    "xray:GetGroup",
    “xray:GetTimeSeriesServiceStatistics"
],

"Resource": [
    "*"
]
```

- GetServiceGraph: main graph
- BatchGetTraces: Retrieves a list of traces specified by ID. Each trace is a collection of segment documents that originates from a single request.
- GetTraceSummaries: Retrieves IDs and annotations for traces available for a pace time frame using an optional filter To get the full traces, pass the trace IDs to BatchGet Traces.
- GetTraceGraph: Retrieves a service graph for one or more specific trace IDs.

## 260. X-Ray with Elastic Beanstalk

X-Ray with Elastic Beanstalk

- AWS Elastic Beanstalk platforms include the X-Ray daemon
- You can run the daemon by setting an option in the Elastic Beanstalk console or with a configuration file (in.ebextensions/xray-daemon.config)

    ```
    option_settings:
        aws:elasticbeanstalk: xray:
            XRayEnabled: true
    ```

- Make sure to give your instance profile the correct IAM permissions so that the X-Ray daemon can function correctly
- Then make sure your application code is instrumented with the X-Ray SDK
- Note: The X-Ray daemon is not provided for Multicontainer Docker

## 261. X-Ray & ECS

- ECS Cluster
    - X-Ray Container as a Daemon

- ECS Cluster
    - X-Ray Container as a "Side Car"

- Fargate Cluster
    - X-Ray Container as a "Side Car"

## 262. AWS Distro for Open Telemetry

AWS Distro for Open Telemetry

- Secure, procucuen recy AWS-supported distribution of the open-source project Opentelemetry project
- Provides a single set of APIs, libraries, agents, and collector services
- Collects distributed traces and metrics from your apps
- Collects metadata from your AWS resources and services
- Auto-instrumentation Agents to collect traces without changing your code
- Send traces and metrics to multiple AWS services and partner solutions
 - X-Ray, CloudWatch, Prometheus...
- Instrument your apps running on AWS (e.g., EC2, ECS, EKS, Fargate, Lambda) as well as on-premises
- Migrate from X-Ray to AWS Distro for Temeletry if you want to standardize with open-source APIs from Telemetry or send traces to multiple destinations simultaneously
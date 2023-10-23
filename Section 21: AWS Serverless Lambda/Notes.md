# Section 21: AWS Serverless Lambda

## 268. Serverless Introduction

What's serverless?

- Serverless is a new paradigm in which the developers don't have to manage servers anymore...
- They just deploy code
- They just deploy... functions !
- Initially... Serverless == FaaS (Function as a Service)
- Serverless was pioneered by AWS Lambda but now also includes anything that’s managed: “databases, messaging, storage, etc.”
- Serverless does not mean there are no servers... it means you just don’t manage / provision / see them

Serverless in AWS

- AWS Lambda
- DynamoDB
- AWS Cognito
- AWS API Gateway
- Amazon S3
- AWS SNS & SQS
- AWS Kinesis Data Firehose
- Aurora Serverless
- Step Functions
- Fargate

## 269. AWS Lambda Overview

Why AWS Lambda

- Virtual Servers in the Cloud
- Limited by RAM and CPU
- Continuously running
- Scaling means intervention to add / remove servers

- Virtual functions — no servers to manage!
- Limited by time - short executions
- Run on-demand
- Scaling is automated!

Benefits of AWS Lambda

- Easy Pricing:
 - Pay per request and compute time
 - Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time
- Integrated with the whole AWS suite of services
- Integrated with many programming languages
- Easy monitoring through AWS CloudWatch
- Easy to get more resources per functions (up to 1OGB of RAM!)
- Increasing RAM will also improve CPU and network!

AWS Lambda language support

- Node.,js (JavaScript)
- Python
- Java (Java 8 compatible)
- C# (.NET Core)
- Golang
- C# / Powershell
- Ruby
- Custom Runtime API (community supported, example Rust)

- Lambda Container Image
 - The container image must implement the Lambda Runtime API
 - ECS / Fargate is preferred for running arbitrary Docker images

AWS Lambda Integrations Main ones

- API Gateway
- Kinesis
- DynamoDB
- S3
- CloudFront
- CloudWatch Events EventBridge
- CloudWatch Logs
- SNS
- SQS
- Cognito

Examples:

- Serverless Thumbnail creation
- Serverless CRON Job

AWS Lambda Pricing: example

- You can find overall pricing information here: https://aws.amazon.com/lambda/pricing/
- Pay per calls:
 - First 1,000,000 requests are free
 - $0.20 per 1 million requests thereafter ($0.0000002 per request)

- Pay per duration: (in increment of 1 ms)
 - 400,000 GB-seconds of compute time per month if FREE
 - == 400,000 seconds if function is |GB RAM
 - == 3,200,000 seconds if function is 128 MB RAM
 - After that $1.00 for 600,000 GB-seconds

- It is usually very cheap to run AWS Lambda so it’s very popular

## 271. AWS Lambda Synchronous Invocations

Lambda — Synchronous Invocations

- Synchronous: CLI, SDK, API Gateway, Application Load Balancer
- Results is returned right away
- Error handling must happen client side (retries, exponential backoff, etc...)

Lambda - Synchronous Invocations - Services

- User Invoked:
 - Elastic Load Balancing (Application Load Balancer)
 - Amazon API Gateway
 - Amazon CloudFront (Lambda@Edge)
 - Amazon S3 Batch

- Service Invoked:
 - Amazon Cognito
 - AWS Step Functions

- Other Services:
 - Amazon Lex
 - Amazon Alexa
 - Amazon Kinesis Data Firehose

## 273. Lambda & Application Load Balancer

Lambda Integration with ALB

- To expose a Lambda function as an HTTP(S) endpoint...
- You can use the Application Load Balancer (or an API Gateway)
- The Lambda function must be registered in a target group

ALB Multi-Header Values

- ALB can support multi header values (ALB setting)
- When you enable multi-value headers, HTTP headers and query string parameters that are sent with multiple values are shown as arrays within the AWS Lambda event and response objects.

## 275. Lambda Asynchronous Invocations & DLQ

Lambda — Asynchronous Invocations

- S3, SNS, CloudWatch Events...
- The events are placed in an Event Queue
- Lambda attempts to retry on errors
 - 3 tries total
 - 1 minute wait after 1st, then 2 minutes wait 
- Make sure the processing is idempotent (in case of retries)
- If the function is beer will see duplicate logs entries in CloudWatch Logs
- Can define a DLQ (dead-letter queue) — SNS or SQS — for failed processing (need correct IAM permissions)
- Asynchronous invocations allow you to speed up the processing if you don’t need to wait for the result (ex: you need 1000 files processed)

Lambda - Asynchronous Invocations - Services

- Amazon Simple Storage Service (S3)
- Amazon Simple Notification Service (SNS)
- Amazon CloudWatch Events / EventBridge
- AWS CodeCommit (CodeCommit Trigger: new branch, new tag, new push)
- AWS CodePipeline (invoke a Lambda function during the pipeline, Lambda must callback)

--- other -----

- Amazon CloudWatch Logs (log processing)
- Amazon Simple Email Service
- AWS CloudFormation
- AWS Config
- AWS loT
- AWS loT Events

## 280. Lambda & S3 Event Notifications

S3 Events Notifications

- S3:ObjectCreated, S$3:ObjectRemoved, S3:ObjectRestore, S3:Replication...
- Object name filtering possible (*jpg)
- Use case: generate thumbnails of images uploaded to S3
- S3 event notifications typically deliver events in seconds but can sometimes take a minute or longer
- If two writes are made to a single non-versioned object at the same time, it is possible that only a single event notification will be sent
- If you want to ensure that an event notification is sent for every successful write, you can enable versioning on your bucket.

## 282. Lambda Event Source Mapping

Lambda - Event Source Mapping

- Kinesis Data Streams
- SQS & SQS FIFO queue
- DynamoDB Streams
- Common denominator: records need to be polled from the source
- Your Lambda function is invoked synchronously

Streams & Lambda (Kinesis & DynamoDB)

- An event source mapping creates an iterator for each shard, processes items in order
- Start with new items, from the beginning or from timestamp
- Processed items aren't removed from the stream (other consumers can read them)
- Low traffic: use batch window to accumulate records before processing
- You can process multiple batches in parallel
 - up to IO batches per shard
 - in-order processing is still guaranteed for each partition key.

Streams & Lambda — Error Handling

- By default, if your function returns an error, the entire batch is reprocessed until the function succeeds, or the items in the batch expire.
- To ensure in-order processing, processing for the affected shard is paused until the error is resolved
- You can configure the event source mapping to:
 - discard old events
 - restrict the number of retries
 - split the batch on error (to work around Lambda timeout issues)
- Discarded events can go to a Destination

Lambda - Event Source Mapping SQS & SQS FIFO

- Event Source Mapping will poll SQS (Long Polling)
- Specify batch size (1-10 messages)
- Recommended: Set the queue visibility timeout to 6x the timeout of your Lambda function
- To use a DLQ
 - set-up on the = SQS queue, not Lambda (DLQ for Lambda is only for async invocations)
- Or use a Lambda destination for failures

Queues & Lambda

- Lambda also supports in-order processing for FIFO (first-in, first-out) queues, scaling up to the number of active message groups.
- For standard queues, items aren't necessarily processed in order.
- Lambda scales up to process a standard queue as quickly as possible.
- When an error occurs, batches are returned to the queue as individual items and might be processed in a different grouping than the original batch.
- Occasionally, the event source mapping might receive the same item from the queue twice, even if no function error occurred.
- Lambda deletes items from the queue after they're processed successfully.
- You can configure the source queue to send items to a dead-letter queue if they can't be processed.

Lambda Event Mapper Scaling

- Kinesis Data Streams & DynamoDB Streams:
 - One Lambda invocation per stream shard
 - If you use parallelization, up to 10 batches processed per shard simultaneously

- SQS Standard:
 - Lambda adds 60 more instances per minute to scale up
 - Up to 1000 batches of messages processed simultaneously
- SQS FIFO:
 - Messages with the same GroupID will be processed in order
 - The Lambda function scales to the number of active message groups

## 284. Lambda Event & Context

Lambda — Event and Context Objects

- Event Object
 - JSON-formatted document contains data for the function to process
 - Contains information from the invoking service (e.g., EventBridge, custom, ...)
 - Lambda runtime converts the event to an object (e.g., dict type in Python)
 - Example: input arguments, invoking service arguments, ...

- Context Object
 - Provides methods and properties that provide information about the invocation, function, and runtime environment
 - Passed to your function by Lambda at runtime
 - Example: aws_request_id, function_name, memory_limit_in_mb, ...

## 285. Lambda Destinations

Lambda — Destinations

- Nov 2019: Can configure to send result to destination
- Asynchronous invocations - can define destinations for successful and failed event:
 - Amazon SQS
 - Amazon SNS
 - AWS Lambda
 - Amazon EventBridge bus

- Note: AWS recommends you use destinations instead of DLQ now (but both can be used at the same time)
- Event Source mapping: for discarded event batches
 - Amazon SQS
 - Amazon SNS
- Note: you can send events to a DLQ directly from SQS


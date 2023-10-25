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

## 287. Lambda Permissions - IAM Roles & Resources Policies

Lambda Execution Role (IAM Role)

- Grants the Lambda function permissions to AWS services / resources
- Sample managed policies for Lambda:
 - AWSLambdaBasicExecutionRole — Upload logs to CloudWatch.
 - AWSLambdaKinesisExecutionRole — Read from Kinesis
 - AWSLambdaDynamoDBExecutionRole — Read from DynamoDB Streams
 - AWSLambdaSQSQueueExecutionRole — Read from SQS
 - AWSLambdaVPCAccessExecutionRole — Deploy Lambda function in VPC
 - AWSXRayDaemonWriteAccess — Upload trace data to X-Ray.

- When you use an event source mapping to invoke your function, Lambda uses the execution role to read event data.
- Best practice: create one Lambda Execution Role per function

Lambda Resource Based Policies

- Use resource-based policies to give other accounts and AWS services permission to use your Lambda resources
- Similar to S3 bucket policies for $3 bucket
- An IAM principal can access Lambda:
 - if the IAM policy attached to the principal authorizes it (e.g. user access)
 - OR if the resource-based policy authorizes (e.g. service access)
- When an AWS service like Amazon S3 calls your Lambda function, the resource-based policy gives it access.

## 289. Lambda Environmental Variables

Lambda Environment Variables

- Environment variable = key / value pair in String” form
- Adjust the function behavior without updating code
- The environment variables are available to your code
- Lambda Service adds its own system environment variables as well
- Helpful to store secrets (encrypted by KMS)
- Secrets can be encrypted by the Lambda service key, or your own CMK

## 291. Lambda Monitoring & X-Ray Tracing

Lambda Logging & Monitoring

- CloudWatch Logs:
 - AWS Lambda execution logs are stored in AWS CloudWatch Logs
 - Make sure your AWS Lambda function has an execution role with an IAM policy that authorizes writes to CloudWatch Logs

- CloudWatch Metrics:
 - AWS Lambda metrics are displayed in AWS CloudWatch Metrics
 - Invocations, Durations, Concurrent Executions
 - Error count, Success Rates, Throttles
 - Async Delivery Failures
 - Iterator Age (Kinesis & DynamoDB Streams)

Lambda Tracing with X-Ray

- Enable in Lambda configuration (Active Tracing)
- Runs the X-Ray daemon for you
- Use AWS X-Ray SDK in Code
- Ensure Lambda Function has a correct IAM Execution Role
 - The managed policy is called AWSXRayDaemonWriteAccess
- Environment variables to communicate with X-Ray
 - .X_AMZN_TRACE_ID: contains the tracing header
 - AWS_XRAY_CONTEXT_MISSING: by default, LOG_ERROR
 - AWS_XRAY_DAEMON_ADDRESS: the X-Ray Daemon IP_ADDRESS:PORT

## 293. Lambda@Edge & CloudFront Functions

Customization At The Edge

- Many modern applications execute some form of the logic at the edge
- Edge Function:
 - A code that you write and attach to CloudFront distributions
 - Runs close to your users to minimize latency
- CloudFront provides two types: CloudFront Functions & Lambda@Edge
- You don't have to manage any servers, deployed globally

- Use case: customize the CDN content
- Pay only for what you use
- Fully serverless

CloudFront Functions & Lambda@Edge
Use Cases

- Website Security and Privacy
- Dynamic Web Application at the Edge
- Search Engine Optimization (SEO)
- Intelligently Route Across Origins and Data Centers
- Bot Mitigation at the Edge
- Real-time Image Transformation
- A/B Testing
- User Authentication and Authorization
- User Prioritization
- User Tracking and Analytics

CloudFront Functions

- Lightweight functions written in JavaScript
- For high-scale, latency-sensitive CDN customizations
- Sub-ms startup times, millions of requests/second
- Used to change Viewer requests and responses:
 - Viewer Request: after CloudFront receives a request from a viewer
 - Viewer Response: before CloudFront forwards the response to the viewer
- Native feature of CloudFront (manage code entirely within CloudFront)

Lambda@Edge

- Lambda functions written in NodeJS or Python
- Scales to 1000s of requests/second
- Used to change CloudFront requests and responses:
 - Viewer Request — after CloudFront receives a request from a viewer
 - Origin Request — before CloudFront forwards the request to the origin
 - Origin Response — after CloudFront receives the response from the origin
 - Viewer Response — before CloudFront forwards the response to the viewer
- Author your functions in one AWS Region (us-east-!), then CloudFront replicates to its locations

CloudFront Functions vs. Lambda@Edge - Use Cases

CloudFront Functions

- Cache key normalization
 - Transform request attributes (headers, cookies, Ewell strings, URL) to create an optimal Cache Key

- Header manipulation
 - Insert/modify/delete HTTP headers in the request or response

- URL rewrites or redirects

- Request authentication & authorization
 - Create and validate user-generated tokens (e.g., JWT) to allow/deny requests

Lambda@Edge

- Longer execution time (several ms)
- Adjustable CPU or memory
- Your code depends on a 3rd libraries (e.g., AWS SDK to access other AWS services)
- Network access to use external services for processing
- File system access or access to the body of HTTP requests

## 294. Lambda in VPC

Lambda by default

- By default, your Lambda function is launched outside your own VPC (in an AWS-owned VPC)
- Therefore it cannot access resources in your VPC (RDS, ElastiCache, internal ELB...)

Lambda in VPC

- You must define the VPC ID, the Subnets and the Security Groups
- Lambda will create an ENI (Elastic Network Interface) in your subnets
- AWSLambdaVPCAccessExecutionRole

Lambda in VPC — Internet Access

- A Lambda function in yourVPC does not have internet access
- Deploying a Lambda function in a public subnet does not give it Internet access or a public IP
- Deploying a Lambda function in a private subnet gives it internet access if you have a NAT Gateway / Instance
- You can use VPC endpoints to privately access AWS services without a NAT

Note: Lambda - CloudWatch Logs works even without endpoint or NAT Gateway

## 296. Lambda Function Performance

Lambda Function Configuration

- RAM:
 - From 128MB to 10GB in 1MB increments
 - The more RAM you add, the more vCPU credits you get
 - At 1,792 MB, a function has the equivalent of one full vCPU
 - After |,792 MB, you get more than one CPU, and need to use multi-threading in your code to benefit from it

- If your application is CPU-bound (computation heavy), increase RAM
- Timeout: default 3 seconds, maximum is 900 seconds (15 minutes)

Lambda Execution Context

- The execution context is a temporary runtime environment that initializes any external dependencies of your lambda code
- Great for database connections, HTTP clients, SDK clients...
- The execution context is maintained for some time in anticipation of another Lambda function invocation
- The next function invocation can “re-use” the context to execution time and save time in initializing connections objects
- The execution context includes the/tmp directory

Lambda Functions /tmp space

- If your Lambda function needs to download a big file to work...
- If your Lambda function needs disk space to perform operations...
- You can use the /tmp directory
- Max size is 1OGB
- The directory content remains when the execution context is frozen, providing transient cache that can be used for multiple invocations (helpful to checkpoint your work)
- For permanent persistence of object (non temporary), use s3
- To encrypt content on /tmp, you must generate KMS Data Keys

## 298. Lambda Layers

Lambda Layers

- Custom Runtimes
 - Ex C++ https://github.com/awslabs/aws-lambda-cpp
 - Ex: Rust https://github.com/awslabs/aws-lambda-rust-runtime

- Externalize Dependencies to re-use them

## 300. Lambda File Systems Mounting

Lambda — File Systems Mounting

- Lambda functions can access EFS file systems if they are running in aVPC
- Configure Lambda to mount EFS file systems to local directory during initialization
- Must leverage EFS Access Points
- Limitations: watch out for the EFS connection limits (one function instance = one connection) and connection burst limits

## 301. Lambda Concurrency

Lambda Concurrency and Throttling

- Concurrency limit: up to 1000 concurrent executions
- Can set a “reserved concurrency” at the function level (=limit)
- Each invocation over the concurrency limit will trigger a ‘Throttle’
- Throttle behavior:
 - If synchronous invocation => return ThrottleError - 429
 - If asynchronous invocation => retry automatically and then go to DLQ
- If you need a higher limit, open a support ticket

Concurrency and Asynchronous Invocations

- If the function doesn't have enough concurrency available to process all events, additional requests are throttled.
- For throttling errors (429) and system errors (500-series), Lambda returns the event to the queue and attempts to run the function again for up to 6 hours.
- The retry interval increases exponentially from | second after the first attempt to a maximum of 5 minutes.

Cold Starts & Provisioned Concurrency

- Cold Start:
 - New instance => code is loaded and code outside the handler run (init)
 - If the init is large (code, dependencies, SDK...) this process can take some time.
 - First request served by new instances has higher latency than the rest

- Provisioned Concurrency:
 - Concurrency is allocated before the function is invoked (in advance)
 - So the cold start never happens and all invocations have low latency
 - Application Auto Scaling can manage concurrency (schedule or target utilization)

- Note:
 - Note: cold starts in VPC have been dramatically reduced in Oct & Nov 2019
 - https://aws.ama

## 303. Lambda External Dependencies

Lambda Function Dependencies

- If your Lambda function depends on external libraries: for example AWS X-Ray SDK, Database Clients, etc...
- You need to install the packages alongside your code and zip it together
 - For Node,js, use npm & “node_modules” directory
 - For Python, use pip --target options
 - For Java, include the relevant Jar files
- Upload the zip straight to Lambda if less than 50MB, else to S3 first
- Native libraries work: they need to be compiled on Amazon Linux
- AWS SDK comes by default with every Lambda function

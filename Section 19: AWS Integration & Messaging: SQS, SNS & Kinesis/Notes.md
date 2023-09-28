# Section 19: AWS Integration & Messaging: SQS, SNS & Kinesis

## 213. Introduction to Messaging

AWS Integration & Messaging (SQS, SNS & Kinesis)

Section Introduction

- When we start deploying multiple applications, they will inevitably need to communicate with one another
- There are two patterns of application communication

1. Synchronous communications (application to application)
 - Buying Service <-> Shipping Service

2. Asynchronous / Event based (application to queue to application)
 - Buying Service -> Queue -> Shipping Service

Section Introduction

- Synchronous between applications can be problematic if there are sudden spikes of traffic
- What if you need to suddenly encode !000 videos but usually it’s 10?
- In that case, it's better to decouple your applications,
 - using SQS: queue model
 - using SNS: pub/sub model
 - using Kinesis: real-time streaming model
- These services can scale independently from our application!

## 214. Amazon SQS - Standard Queues

Amazon SQS — Standard Queue

- Oldest offering (over 10 years old)
- Fully managed service, used to decouple applications

- Attributes:
 - Unlimited throughput, unlimited number of messages in queue
 - Default retention of messages: 4 days, maximum of 14 days
 - Low latency (<10 ms on publish and receive)
 - Limitation of 256KB per message sent

- Can have duplicate messages (at least once delivery, occasionally)
- Can have out of order messages (best effort ordering)

SQS — Producing Messages

- Produced to SQS using the SDK (SendMessage API)
- The message is persisted in SQS until a consumer deletes it
- Message retention: default 4 days, up to 14 days

- Example: send an order to be processed
 - Order id
 - Customer id
 - Any attributes you want

- SOS standard: unlimited throughput

SQS — Consuming Messages

- Consumers (running on EC2 instances, servers, or AWS Lambda)...
- Poll SQS for messages (receive up to 10 messages at a time)
- Process the messages (example: insert the message into an RDS database)
- Delete the messages using the DeleteMessage API

SQS — Multiple EC2 Instances Consumers

- Consumers receive and process messages in parallel
- At least once delivery
- Best-effort message ordering
- Consumers delete messages after processing them
- We can scale consumers horizontally to improve throughput of processing

Amazon SQS - Security

- Encryption:
 - In-flight encryption using HTTPS API
 - At-rest encryption using KMS keys
 - Client-side encryption if the client wants to perform encryption decryption itself

- Access Controls: IAM policies to regulate access to the SQS API

- SQS Access Policies (similar to $3 bucket policies)
 - Useful for cross-account access to SQS queues
 - Useful for allowing other services (SNS, S3...) to write to an SQS queue

## 216. SQS Queue Access Policy

SQS Queue Access Policy

- Cross Account Access

- Publish S3 Event Notifications to SQS Queue

## 217. SQS - Message Visibility Timeout

SQS — Message Visibility Timeout

- After a message is polled by a consumer, it becomes invisible to other consumers
- By default, the “message visibility timeout’ is 30 seconds
- That means the message has 30 seconds to be processed
- After the message visibility timeout is over, the message is “Visible” in SQS

- If a message is not processed within the visibility timeout, it will be processed twice
- A consumer could call the ChangeMessageVisibility API to get more time
- If visibility timeout is high (hours), and consumer crashes, re-processing will take time
- If visibility timeout is too low (seconds), we may get duplicates

## Amazon SQS — Dead Letter Queue (DLQ)

- If a consumer fails to process a message within the Visibility Timeout... the message goes back to the queue!
- We can set a threshold of how many times a message can go back to the queue
- After the MaximumReceives threshold is exceeded, the message goes into a dead letter queue (DLQ)
- Useful for debugging!
- DLQ of a FIFO queue must also be a FIFO queue
- DLQ of a Standard queue must also be a Standard queue
- Make sure to process the messages in the DLQ before they expire:
 - Good to set a retention of |4 days in the DLQ

SQS DLO — Redrive to Source

- Feature to help consume messages in the DLQ to understand what is wrong with them
- When our code is fixed, we can redrive the messages from the DLQ back into the source queue (or any other queue) in batches without writing custom code
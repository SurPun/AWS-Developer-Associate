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

- Oldest offering (over |0 years old)
- Fully managed service, used to decouple applications

- Attributes:
 - Unlimited throughput, unlimited number of messages in queue
 - Default retention of messages: 4 days, maximum of |4 days
 - Low latency (<10 ms on publish and receive)
 - Limitation of 256KB per message sent

- Can have duplicate messages (at least once delivery, occasionally)
- Can have out of order messages (best effort ordering)


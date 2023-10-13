# Quiz 16: Messaging & Integration Quiz

1. You have an e-commerce website and you are preparing for Black Friday which is the biggest sale of the year. You expect that your traffic will increase by 100x. Your website already using an SQS Standard Queue. What should you do to prepare your SQS Queue?

- Do nothing, SQS scales automatically

2. How would you configure your SQS messages to be processed by consumers only after 5 minutes of being published to your SQS Queue?

- Increase the DelaySeconds parameter

SQS Delay Queues is a period of time during which Amazon SQS keeps new SQS messages invisible to consumers. In SQS Delay Queues, a message is hidden when it is first added to the queue. (default: 0 mins, max.: 15 mins)

3. You have an SQS Queue where each consumer polls 10 messages at a time and finishes processing them in 1 minute. After a while, you noticed that the same SQS messages are received by different consumers resulting in your messages being processed more than once. What should you do to resolve this issue?

- Increase the Visibility Timeout

SQS Visibility Timeout is a period of time during which Amazon SQS prevents other consumers from receiving and processing the message again. In Visibility Timeout, a message is hidden only after it is consumed from the queue. Increasing the Visibility Timeout gives more time to the consumer to process the message and prevent duplicate reading of the message. (default: 30 sec., min.: 0 sec., max.: 12 hours)

4. You have a fleet of EC2 instances (consumers) managed by an Auto Scaling Group that used to process messages in an SQS Standard Queue. Lately, you have found a lot of messages processed twice and after further investigation, you found that these messages can not be processed successfully. How would you troubleshoot (debug) why these messages fail?

- SQS Dead Letter Queue

SQS Dead Letter Queue is where other SQS queues (source queues) can send messages that can't be processed (consumed) successfully. It's useful for debugging as it allows you to isolate problematic messages so you can debug why their processing doesn't succeed.

5. Which SQS Queue type allows your messages to be processed exactly once and in order?

- SQS FIFO Queue

SQS FIFO (First-In-First-Out) Queues have all the capabilities of the SQS Standard Queue, plus the following two features. First, The order in which messages are sent and received are strictly preserved and a message is delivered once and remains available until a consumer process and deletes it. Second, duplicated messages are not introduced into the queue.

6. You have 3 different applications that you'd like to send them the same message. All 3 applications are using SQS. What is the best approach would you choose?

- Use SNS + SQS Fan Out Pattern

This is a common pattern where only one message is sent to the SNS topic and then "fan-out" to multiple SQS queues. This approach has the following features: it's fully decoupled, no data loss, and you have the ability to add more SQS queues (more applications) over time.

7. You have a Kinesis data stream with 6 shards provisioned. This data stream usually receiving 5 MB/s of data and sending out 8 MB/s. Occasionally, your traffic spikes up to 2x and you get a ProvisionedThroughputExceededException exception. What should you do to resolve the issue?

- Add more Shards

The capacity limits of a Kinesis data stream are defined by the number of shards within the data stream. The limits can be exceeded by either data throughput or the number of reading data calls. Each shard allows for 1 MB/s incoming data and 2 MB/s outgoing data. You should increase the number of shards within your data stream to provide enough capacity.

8. You have a website where you want to analyze clickstream data such as the sequence of clicks a user makes, the amount of time a user spends, and where the navigation begins, and how it ends. You decided to use Amazon Kinesis, so you have configured the website to send these clickstream data all the way to a Kinesis data stream. While you checking the data sent to your Kinesis data stream, you found that the users' data is not ordered and the data for one individual user is spread across many shards. How would you fix this problem?

- For each record sent to Kinesis add a partition key that represents the identity of the user

Kinesis Data Stream uses the partition key associated with each data record to determine which shard a given data record belongs to. When you use the identity of each user as the partition key, this ensures the data for each user is ordered hence sent to the same shard.

9. Which AWS service is most appropriate when you want to perform real-time analytics on streams of data?

- Amazon Kinesis Data Analytics

Use Kinesis Data Analytics with Kinesis Data Streams as the underlying source of data.

10. You are running an application that produces a large amount of real-time data that you want to load into S3 and Redshift. Also, these data need to be transformed before being delivered to their destination. What is the best architecture would you choose?

- Kinesis Data Streams + Kinesis Data Firehose

This is a perfect combo of technology for loading data near real-time data into S3 and Redshift. Kinesis Data Firehose supports custom data transformations using AWS Lambda.

11. Which of the following is NOT a supported subscriber for AWS SNS?

- Amazon Kinesis Data Streams

Note: Kinesis Data Firehose is now supported, but not Kinesis Data Streams.

12. Which AWS service helps you when you want to send email notifications to your users?

- Amazon SNS

13. You have an SNS topic with 1000s of subscribers and you want to send some messages to certain subscribers and not others. What SNS feature allows you to do so?

- SNS Message Filtering

SNS Message Filtering allows you to filter messages sent to SNS topic's subscriptions.

14. You have an e-commerce website and you are preparing for Black Friday which is the biggest sale of the year. You expect that your traffic will increase by 100x. Your website already using an SQS Standard queue. Due to the spike in traffic, consumers may fail multiple times while processing messages within the Visibility Timeout, due to some constrains to the application database. What else should you do to handle failed messages?

- Implement a Dead Letter Queue (DLQ) with a redrive policy

15. Your SQS costs are extremely high. Upon closer look, you notice that your consumers are polling your SQS queues too often and getting empty data as a result. What should you do?

- Enable Long Polling

16. SQS message size limit is 256 KB, but you want to send messages of 1 MB. You should ........................

- Use the SQS Extended Client Library

17. You can configure an SQS queue to keep messages for a maximum of .................. days.

- 14 Days

You can configure the Amazon SQS message retention period to a value from 1 minute to 14 days. The default is 4 days.


18. Which SQS FIFO message attribute allows multiple messages belong to the same group to be processed in order?

- MessageGroupId

19. Which SQS FIFO message attribute prevents messages with the same deduplication ID to be delivered during a 5-minutes period?

- messageDeduplicationId

20. A Kinesis Data Stream that you manage experiencing an increase in traffic due to a sale day. Your Kinesis Data Streams currently has 6 shards, and you have been asked to split shards to become 10 shards. You have been using a consuming application based on Kinesis Client Library (KCL) and are running on a set of EC2 instances. What's the maximum number of EC2 instances that can be deployed to process the messages in shards?

- 10

When using Kinesis Client Library, each shard is to be read-only by one KCL instance. So, if you have 10 shards, then the maximum KCL instances you can have is 10.

21. You are running an SQS FIFO queue with 10 message groups (defined by MessageGroupID). What's the maximum number of consumers can consume simultaneously?

- 10

ou can have as many consumers as "MessageGroupID" for your SQS FIFO queues.

22. You can configure a Kinesis Data Stream to keep records for a maximum of .................. days.

- 365 Days

23. You have a Kinesis Data Stream where you intermittently get a ProvisionedThroughputExceededException exception in your producers' applications. The following can be used to resolve the error, EXCEPT .......................

- Contact AWS Support to increase your Kinesis Data Stream's Capacity

24. What should you use to increase the read throughput for Kinesis Data Streams consumers up to 2 MB/s per consumer per shard?

- Enhanced Fan-out Consumer

25. You have a hot shard in a Kinesis Data Stream, thus causing many ProvisionedThroughputExceededException exceptions. What operation allows you to increase the number of shards?

- Shard Splitting

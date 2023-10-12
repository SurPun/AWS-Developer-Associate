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
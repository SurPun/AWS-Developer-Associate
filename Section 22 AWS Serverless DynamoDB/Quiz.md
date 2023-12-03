# Quiz 19: DynamoDB Quiz

1. Before you create a DynamoDB table, you need to provision the EC2 instance the DynamoDB table will be running on.

- False

DynamoDB is serverless with no servers to provision, patch, or manage and no software to install, maintain or operate. It automatically scales tables up and down to adjust for capacity and maintain performance. It provides both provisioned (specify RCU & WCU) and on-demand (pay for what you use) capacity modes.

2. You have provisioned a DynamoDB table with 10 RCUs and 10 WCUs. A month later you want to increase the RCU to handle more read traffic. What should you do?

- Increase RCU and keep WCU the same

RCU and WCU are decoupled, so you can increase/decrease each value separately.

3. You have an e-commerce website where you are using DynamoDB as your database. You are about to enter the Christmas sale and you have a few items which are very popular and you expect that they will be read often. Unfortunately, last year due to the huge traffic you had the ProvisionedThroughputExceededException exception. What would you do to prevent this error from happening again?

- Create a DAX Cluster

DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to 10x performance improvement. It caches the most frequently used data, thus offloading the heavy reads on hot keys of your DynamoDB table, hence preventing the "ProvisionedThroughputExceededException" exception.

4. You have developed a mobile application that uses DynamoDB as its datastore. You want to automate sending welcome emails to new users after they sign up. What is the most efficient way to achieve this?

- Enable DynamoDB Streams and configure it to invoke a Lambda function to send emails

DynamoDB Streams allows you to capture a time-ordered sequence of item-level modifications in a DynamoDB table. It's integrated with AWS Lambda so that you create triggers that automatically respond to events in real-time.

5. You are running an application in production that is leveraging DynamoDB as its datastore and is experiencing smooth sustained usage. There is a need to make the application run in development mode as well, where it will experience an unpredictable volume of requests. What is the most cost-effective solution that you recommend?

- Use Provisioned Capacity Mode with Auto Scaling enabled for production and use On- Demand Capacity Mode for development

6. The maximum size of an item in a DynamoDB table is ...................

- 400kb

7. DynamoDB tables scale ..........................

- Horizontally

8. When your DynamoDB table's Primary Key is a combination of Partition Key + Sort Key, then ...................... must be unique.

- Partition Key + Sort Key

9. You have taken the decision to use DynamoDB as the database for a blog posts website. While designing the blog posts table, which column should you use as the Partition Key for optimal distribution?

- blog_id

10. An application writes 12 items per second into a DynamoDB table, with each item 8 KB in size. What WCU should you choose?

- 96

12 * (8 KB / 1 KB) = 96 WCU.
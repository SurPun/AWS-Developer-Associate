# Quiz 10: Amazon S3 Advanced Quiz

1. How can you be notified when there's an object uploaded to your S3 bucket?

- S3 Event Notifications

2. You have an S3 bucket that has S3 Versioning enabled. This S3 bucket has a lot of objects, and you would like to remove old object versions to reduce costs. What's the best approach to automate the deletion of these old object versions?

- S3 Lifecycle Rules - Expiration Actions

3. How can you automate the transition of S3 objects between their different tiers?

- S3 Lifecycle Rules

4. While you're uploading large files to an S3 bucket using Multi-part Upload, there are a lot of unfinished parts stored in the S3 bucket due to network issues. You are not using these unfinished parts and they cost you money. What is the best approach to remove these unfinished parts?

- Use an S3 Lifecycle Policy to automate old/unfinished parts deletion

5. You are looking to build an index of your files in S3, using Amazon RDS PostgreSQL. To build this index, it is necessary to read the first 250 bytes of each object in S3, which contains some metadata about the content of the file itself. There are over 100,000 files in your S3 bucket, amounting to 50 TB of data. how can you build this index efficiently?

- Create an application that will traverse the S3 bucket, issue a Byte Range Fetch for the first 250 bytes, and store that information in RDS

6. You have a large dataset stored on-premises that you want to upload to the S3 bucket. The dataset is divided into 10 GB files. You have good bandwidth but your Internet connection isn't stable. What is the best way to upload this dataset to S3 and ensure that the process is fast and avoid any problems with the Internet connection?

- Use S3 Multi-part Upload & S3 Transfer Acceleration

7. You would like to retrieve a subset of your dataset stored in S3 with the CSV format. You would like to retrieve a month of data and only 3 columns out of 10, to minimize compute and network costs. What should you use?

- S3 Select

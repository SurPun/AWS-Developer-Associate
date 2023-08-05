# Quiz 8: Amazon S3 Quiz

1. You have a 25 GB file that you're trying to upload to S3 but you're getting errors. What is a possible solution for this?

- Use Multi-Part upload when uploading files larger than 5GB

Multi-Part Upload is recommended as soon as the file is over 100 MB.

2. You're getting errors while trying to create a new S3 bucket named dev. You're using a new AWS Account with no S3 buckets created before. What is a possible cause for this?

- S3 bucket names must be globally unique and dev is already taken

3. You have enabled versioning in your S3 bucket which already contains a lot of files. Which version will the existing files have?

- null

4. You have updated an S3 bucket policy to allow IAM users to read/write files in the S3 bucket, but one of the users complain that he can't perform a PutObject API call. What is a possible cause for this?

- The IAM user must have an explicit DENY in the attached IAM Policy

Explicit DENY in an IAM Policy will take precedence over an S3 bucket policy.

5. You want the content of an S3 bucket to be fully available in different AWS Regions. That will help your team perform data analysis at the lowest latency and cost possible. What S3 feature should you use?

- S3 Replication

S3 Replication allows you to replicate data from an S3 bucket to another in the same/different AWS Region.

6. You have 3 S3 buckets. One source bucket A, and two destination buckets B and C in different AWS Regions. You want to replicate objects from bucket A to both bucket B and C. How would you achieve this?

- Configure replication from bucket A to bucket B, then from bucket A to bucket C

7. Which of the following is NOT a Glacier Deep Archive retrieval mode?

- Expedited (1-5 minutes)

8. Which of the following is NOT a Glacier Flexible retrieval mode?

- Instant (10 seconds)
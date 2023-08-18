# Section 13: Advanced Amazon S3

## 134. S3 Lifecycle Rules (with S3 Analytics)

Amazon S3 - Moving between Storage Classes

- You can transition objects between storage classes

- For infrequently accessed object, move them to Standard IA

- For archive objects that you don't need fast access to, move them to Glacier or Glacier Deep Archive

- Moving objects can be automated using a Lifecycle Rules

Amazon S3 — Lifecycle Rules

- Transition Actions — configure objects to transition to another storage class
 - Move objects to Standard IA class 60 days after creation
 - Move to Glacier for archiving after 6 months

- Expiration actions — configure objects to expire (delete) after some time
 - Access log files can be set to delete after a 365 days
 - Can be used to delete old versions of files (if versioning is enabled)
 - Can be used to delete incomplete Multi-Part uploads

- Rules can be created for a certain prefix (example: s3://mybucket/mp3/*)
- Rules can be created for certain objects Tags (example: Department: Finance)

Amazon S3 — Lifecycle Rules (Scenario 1)

- Your application on EC2 creates images thumbnails after profile photos are uploaded to Amazon S3. These thumbnails can be easily recreated, and only need to be kept for 60 days. The source images should be able to be immediately retrieved for these 60 days, and afterwards, the user can wait up to 6 hours. How would you design this?

- S3 source images can be on Standard, with a lifecycle configuration to transition them to Glacier after 60 days

- S3 thumbnails can be on One-Zone IA, with a lifecycle configuration to expire them (delete them) after 60 days

Amazon S3 — Lifecycle Rules (Scenario 2)

- A rule in your company states that you should be able to recover your deleted S3 objects immediately for 30 days, although this may happen rarely. After this time, and for up to 365 days, deleted objects should be recoverable within 48 hours.

- Enable S3 Versioning in order to have object versions, so that ‘deleted objects” are in fact hidden by a‘‘delete marker” and can be recovered
- Transition the “noncurrent versions” of the object to Standard IA
- Transition afterwards the “‘noncurrent versions’ to Glacier Deep Archive

Amazon S3 Analytics — Storage Class Analysis

- Help you decide when to transition objects to the right storage class
- Recommendations for Standard and Standard IA
 - Does NOT work for One-Zone IA or Glacier
- Report is updated daily
- 24 to 48 hours to start seeing data analysis
- Good first step to put together Lifecycle Rules (or improve them)!

## 136. S3 Event Notifications

S3 Event Notifications

- S3:ObjectCreated, S3:ObjectRemoved, S3:ObjectRestore, S3:Replication...
- Object name filtering possible (*.jpg)
- Use case: generate thumbnails of images uploaded to $3
- Can create as many “‘S3 events” as desired
- S3 event notifications typically deliver events in seconds but can sometimes take a minute or longer

S3 Event Notifications with Amazon EventBridge

- Advanced filtering options with JSON rules (metadata, object size, name...)
- Multiple Destinations — ex Step Functions, Kinesis Streams / Firehose...
- EventBridge Capabilities — Archive, Replay Events, Reliable delivery
# Section 14: Amazon S3 Security

## 141. S3 Encryption

Amazon s3 — Object Encryption

- You can encrypt objects in S3 buckets using one of 4 methods
- Server-Side Encryption (SSE)
 - Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3) — Enabled by Default
  - Encrypts s3 objects using keys handled, managed, and owned by AWS
 - Server-Side Encryption with KMS Keys stored in AWS KMS (SSE-KMS)
  - Leverage AWS Key Management Service (AWS KMS) to manage encryption keys
 - Server-Side Encryption with Customer-Provided Keys (SSE-C)
  - When you want to manage your own encryption keys
- Client-Side Encryption
- It's important to understand which ones are for which situation for the exam

Amazon s3 Encryption — SSE-S3

- Encryption using keys handled, managed, and owned by AWS
- Object is encrypted server-side
- Encryption type is AES-256
- Must set header "x-amz-server-side-encryption”: "AES256"
- Enabled by default for new buckets & new objects

Amazon S3 Encryption — SSE-KMS

- Encryption using keys handled and managed by AWS KMS (Key Management Service)
- KMS advantages: user control + audit key usage using CloudTrail
- Object is encrypted server side
- Must set header "x-amz-server-side-encryption": "aws:kms"

SSE-KMS Limitation

- If you use SSE-KMS, you may be impacted by the KMS limits
- When you upload, it calls the GenerateDataKey KMS API
- When you download, it calls the Decrypt KMS API
- Count towards the KMS quota per second (5500, 10000, 30000 req/s based on region)
- You can request a quota increase using the Service Quotas Console

Amazon s3 Encryption — SSE-C

- Server-Side Encryption using keys fully managed by the customer outside of AWS
- Amazon S3 does NOT store the encryption key you provide
- HTTPS must be used
- Encryption key must provided in HTTP headers, for every HTTP request made

Amazon s3 Encryption — Client-Side Encryption

- Use client libraries such as Amazon s3 Client-Side Encryption Library
- Clients must encrypt data themselves before sending to Amazon s3
- Clients must decrypt data themselves when retrieving from Amazon s3
- Customer fully manages the keys and encryption cycle

Amazon s3 — Encryption in transit (SSL/TLS)

- Encryption in flight is also called SSL/TLS

- Amazon S3 exposes two endpoints:
 - HTTP Endpoint — non encrypted
 - HTTPS Endpoint — encryption in flight

- HTTPS is recommended
- HTTPS is mandatory for SSE-C
- Most clients would use the HTTPS endpoint by default

## 142. About DSSE-KMS

- DSSE-KMS is just "double encrypion based on KMS".

## 144. S3 Default Encryption

Amazon S3 — Default Encryption vs. Bucket Policies

- SSE-S3 encryption is automatically applied to new objects stored in S3 bucket

- Optionally, you can “force encryption” using a bucket policy and refuse any API call to PUT an $3 object without encryption headers (SSE-KMS or SSE-C)

- Note: Bucket Policies are evaluated before ‘Default Encryption”

## 145. S3 CORS

What is CORS?

- Cross-Origin Resource Sharing (CORS)
- Origin = scheme (protocol) + host (domain) + port
 - example: https://www.example.com (implied port is 443 for HTTPS, 80 for HTTP)
- Web Browser based mechanism to allow requests to other origins while visiting the main origin
- Same origin: http://example.com/app | & Sh le.com/app2
- Different origins: http://www.example.com & http://otherexample.com
- The requests won't be fulfilled unless the other origin allows for the requests, using CORS Headers (example: Access-Control-Allow-Origin)

Amazon s3 — CORS

- If a client makes a cross-origin request on our S3 bucket, we need to enable the correct CORS headers
- It's a popular exam question
- You can allow for a specific origin or for * (all origins)

## 147. S3 MFA Delete

Amazon S3 — MFA Delete

- MFA (Multi-Factor Authentication) — force users to generate a code on a
device (usually a mobile phone or hardware) before doing important operations on s3
- MFA will be required to:
 - Permanently delete an object version
 - Suspend Versioning on the bucket
- MFA won't be required to:
 - Enable Versioning
 - List deleted versions
- To use MFA Delete, Versioning must be enabled on the bucket
- Only the bucket owner (root account) can enable/disable MFA Delete

## 149. S3 Access Logs

S3 Access Logs

- For audit purpose, you may want to log all access to s3 buckets
- Any request made to s3, from any account, authorized or denied, will be logged into another s3 bucket
- That data can be analyzed using data analysis tools...
- The target logging bucket must be in the same AWS region
- The log format is at:
 - https://docs.aws.amazon.com/AmazonS3/latest/dev/LogFormat.html

S3 Access Logs: Warning

- Do not set your logging bucket to be the monitored bucket
- It will create a logging loop, and your bucket will grow exponentially

## 151. S3 Pre-signed URLs

Amazon S3 — Pre-Signed URLs

- Generate pre-signed URLs using the s3 Console, AWS CLI or SDK

- URL Expiration
 - s3 Console — | min up to 720 mins (12 hours)
 - AWS CLI — configure expiration with —expires-in parameter in seconds (default 3600 secs, max. 604800 secs ~ 168 hours)

- Users given a pre-signed URL inherit the permissions of the user
that generated the URL for GET / PUT

- Examples:
 - Allow only logged-in users to download a premium video from your s3 bucket
 - Allow an ever-changing list of users to download files by generating URLs dynamically
 - Allow temporarily a user to upload a file to a precise location in your s3 bucket

## 153. S3 Access Points

S3 - Access Points

- Access Points simplify security management for S3 Buckets
- Each Access Point has:
 - its own DNS name (Internet Origin or VPC Origin)
 - an access point policy (similar to bucket policy) — manage security at scale

S3 - Access Points - VPC Origin

- We can define the access point to be accessible only from within the VPC

- You must create aVPC Endpoint to access the Access Point (Gateway or Interface Endpoint)

- The VPC Endpoint Policy must allow access to the target bucket and Access Point

## 154. S3 Object Lambda

S3 Object Lambda

- Use AWS Lambda Functions to change the object before it is  retrieved by the caller application

- Only one S3 bucket is needed, on top of which we create S3 Access Point and S3 Object Lambda Access

- Use Cases:
 - Redacting personally identifiable information for analytics or non- production environments.
 - Converting across data formats, such as converting XML to JSON.
 - Resizing and watermarking images on the fly using caller-specific details, such as the user who requested the object.
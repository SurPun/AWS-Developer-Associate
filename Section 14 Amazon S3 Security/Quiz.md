# Quiz 11: Amazon S3 Security Quiz

1. Your client wants to make sure that file encryption is happening in S3, but he wants to fully manage the encryption keys and never store them in AWS. You recommend him to use .............................

- SSE-C

With SSE-C, the encryption happens in AWS and you have full control over the encryption keys.

2. A company you're working for wants their data stored in S3 to be encrypted. They don't mind the encryption keys stored and managed by AWS, but they want to maintain control over the rotation policy of the encryption keys. You recommend them to use ....................

- SSE-KMS

With SSE-KMS, the encryption happens in AWS, and the encryption keys are managed by AWS but you have full control over the rotation policy of the encryption key. Encryption keys stored in AWS.

3. Your company does not trust AWS for the encryption process and wants it to happen on the application. You recommend them to use ....................

- Client-Side Encryption

With Client-Side Encryption, you have to do the encryption yourself and you have full control over the encryption keys. You perform the encryption yourself and send the encrypted data to AWS. AWS does not know your encryption keys and cannot decrypt your data.

4. You have a website that loads files from an S3 bucket. When you try the URL of the files directly in your Chrome browser it works, but when you try to visit a website with a different domain that tries to load these files it doesn't. What's the problem?

- CORS is wrong

Cross-Origin Resource Sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. To learn more about CORS, go here: https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html

5. Which S3 encryption method mandates that you use HTTPS while uploading/download objects?

- SSE-C

6. You have enabled versioning and want to be extra careful when it comes to deleting files on an S3 bucket. What should you enable to prevent accidental permanent deletions?

- Enable MFA Delete

MFA Delete forces users to use MFA codes before deleting S3 objects. It's an extra level of security to prevent accidental deletions.

7. You would like all your files in an S3 bucket to be encrypted by default. What is the optimal way of achieving this?

- Do nothing, Amazon S3 automatically encrypt new objects using Server-Side Encryption with S3-Managed Keys (SSE-S3)

8. You suspect that some of your employees try to access files in an S3 bucket that they don't have access to. How can you verify this is indeed the case without them noticing?

- Enable S3 Access Logs and analyze them using Athena

S3 Access Logs log all the requests made to S3 buckets and Amazon Athena can then be used to run serverless analytics on top of the log files.

9. You are looking to provide temporary URLs to a growing list of federated users to allow them to perform a file upload on your S3 bucket to a specific location. What should you use?

- S3 Pre-Signed URL

S3 Pre-Signed URLs are temporary URLs that you generate to grant time-limited access to some actions in your S3 bucket.


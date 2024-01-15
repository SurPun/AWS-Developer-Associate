# Section 30: AWS Security & Encryption KMS, Encryption SDK, SSM Parameter Store, IAM & STS

## 425. Encryption 101

Why encryption? Encryption in flight (TLS / SSL)

- Data is encrypted before sending and decrypted after receiving
- TLS certificates help with encryption (HTTPS)
- Encryption in flight ensures no MITM (man in the middle attack) can happen

Why encryption? Server-side encryption at rest

- Data is encrypted after being received by the server
- Data is decrypted before being sent
- It is stored in an encrypted form thanks to a key (usually a data key)
- The encryption / decryption keys must be managed somewhere, and the server must have access to it

Why encryption?

Client-side encryption

- Data is encrypted by the client and never decrypted by the server
- Data will be decrypted by a receiving client
- The server should not be able to decrypt the data
- Could leverage Envelope Encryption

## 426. KMS Overview

AWS KMS (Key Management Service)

- Anytime you hear“‘encryption” for an AWS service, it’s most likely KMS
- AWS manages encryption keys for us
- Fully integrated with IAM for authorization
- Easy way to control access to your data
- Able to audit KMS Key usage using Cloud Trail
- Seamlessly integrated into most AWS services (EBS, $3, RDS, SSM...)
- Never ever store your secrets in plaintext, especially in your code!
 - KMS Key Encryption also available through API calls (SDK, CLI)
 - Encrypted secrets can be stored in the code / environment variables

KMS Keys Types

- KMS Keys is the new name of KMS Customer Master Key
- Symmetric (AES-256 keys)
 - Single encryption key that is used to Encrypt and Decrypt
 - AWS services that are integrated with KMS use Symmetric CMKs
 - You never get access to the KMS Key unencrypted (must call KMS API to use)

- Asymmetric (RSA & ECC key pairs)
 - Public (Encrypt) and Private Key (Decrypt) pair
 - Used for Encrypt/Decrypt, or Sign/Verify operations
 - The public key is downloadable, but you can’t access the Private Key unencrypted
 - Use case: encryption outside of AWS by users who can’t call the KMS API

AWS KMS (Key Management Service)

- Types of KMS Keys:
 - AWS Owned Keys (free): SSE-S3, SSE-SQS, SSE-DDB (default key)
 - AWS Managed Key: free (aws/service-name, example: aws/rds or aws/ebs)
 - Customer managed keys created in KMS: $1 / month
 - Customer managed keys imported (must be symmetric key): $1 / month
 - + pay for API call to KMS ($0.03 / 10000 calls) Encryption key management

Encryption key management

- Owned by Amazon DynamoDB
- AWS managed key Lea
 - Key alias: aws/dynamodb

- Stored in your account, and owned and managed by you

Automatic Key rotation:

- AWS-managed KMS Key: automatic every 1 year
- Customer-managed KMS Key: (must be enabled) automatic every 1 year
- Imported KMS Key: only manual rotation possible using alias

KMS Key Policies

- Control access to KMS keys, “similar” to S3 bucket policies
- Difference: you cannot control access without them

- Default KMS Key Policy:
 - Created if you don't provide a specific KMS Key Policy
 - Complete access to the key to the root user = entire AWS account

- Custom KMS Key Policy:
 - Define users, roles that can access the KMS key
 - Define who can administer the key
 - Useful for cross-account access of your KMS key

Copying Snapshots across accounts

1. Create a Snapshot, encrypted with your own KMS Key (Customer Managed Key)

2. Attach a KMS Key Policy to authorize cross-account access

3. Share the encrypted snapshot

4. (in target) Create a copy of the Snapshot, encrypt it with a CMK in your account

5. Create a volume from the snapshot

## 428. KMS Encryption Patterns and Envelope Encryption

Envelope Encryption

- KMS Encrypt API call has a limit of 4 KB
- If you want to encrypt >4 KB, we need to use Envelope Encryption
- The main API that will help us is the GenerateDataKey API

- For the exam: anything over 4 KB of data that needs to be encrypted must use the Envelope Encryption == GenerateDataKey API

Encryption SDK

- The AWS Encryption SDK implemented Envelope Encryption for us
- The Encryption SDK also exists as a CLI tool we can install
- Implementations for Java, Python, C, JavaScript

- Feature - Data Key Caching:
 - re-use data keys instead of creating new ones for each encryption
 - Helps with reducing the number of calls to KMS with a security trade-off
 - Use LocalCryptoMaterialsCache (max age, max bytes, max number of messages)

KNS Symmetric - API Summary

- Encrypt: encrypt up to 4 KB of data through KMS
- GenerateDataKey: generates a unique symmetric data key (DEK)
 - returns a plaintext copy of the data key
 - AND a copy that is encrypted under the CMK that you specify
- GenerateDataKeyWithoutPlaintext:
 - Generate a DEK to use at some point (not immediately)
 - DEK that is encrypted under the CMK that you specify (must use Decrypt later)
- Decrypt: decrypt up to 4 KB of data (including Data Encryption Keys)
- GenerateRandom: Returns a random byte string
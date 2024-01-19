# Quiz 27: AWS Security & Encryption Quiz

1. To enable In-flight Encryption (In-Transit Encryption), we need to have ........................

- an HTTPS endpoint with an SSL certificate

In-flight Encryption = HTTPS, and HTTPS can not be enabled without an SSL certificate.

2. Server-Side Encryption means that the data is sent encrypted to the server.

- False

Server-Side Encryption means the server will encrypt the data for us. We don't need to encrypt it beforehand.

3. In Server-Side Encryption, where do the encryption and decryption happen?

- Both Encryption and Decryption happen on the server

In Server-Side Encryption, we can't do encryption/decryption ourselves as we don't have access to the corresponding encryption key.

4. In Client-Side Encryption, the server must know our encryption scheme before we can upload the data.

- False

With Client-Side Encryption, the server doesn't need to know any information about the encryption scheme being used, as the server will not perform any encryption or decryption operations.

5. You need to create KMS Keys in AWS KMS before you are able to use the encryption features for EBS, S3, RDS ...

- False

You can use the AWS Managed Service keys in KMS, therefore we don't need to create our own KMS keys.

6. AWS KMS supports both symmetric and asymmetric KMS keys.

- True

KMS keys can be symmetric or asymmetric. Symmetric KMS key represents a 256-bit key used for encryption and decryption. An asymmetric KMS key represents an RSA key pair used for encryption and decryption or signing and verification, but not both. Or it represents an elliptic curve (ECC) key pair used for signing and verification.

7. You have an AMI that has an encrypted EBS snapshot using KMS CMK. You want to share this AMI with another AWS account. You have shared the AMI with the desired AWS account, but the other AWS account still can't use it. How would you solve this problem?

- You need to share the KMS CMK used to encrypt the AMI with the other AWS account

8. What should you use to control access to your KMS CMKs?

- KMS Key Policies

9. You have a Lambda function used to process some data in the database. You would like to give your Lambda function access to the database password. Which of the following options is the most secure?

- Have it as an encrypted environment variable and decrypt it at runtime

This is the most secure solution amongst these options.

10. You have a secret value that you use for encryption purposes, and you want to store and track the values of this secret over time. Which AWS service should you use?

- SSM Parameter Store

SSM Parameters Store can be used to store secrets and has built-in version tracking capability. Each time you edit the value of a parameter, SSM Parameter Store creates a new version of the parameter and retains the previous versions. You can view the details, including the values, of all versions in a parameter's history.


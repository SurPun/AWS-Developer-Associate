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


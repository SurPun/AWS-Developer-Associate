# AWS-Developer-Associate

AWS Developer Associate

- [Udemy Course](https://www.udemy.com/share/101WgC3@dc-QdI5aJejjXvDjjRVOBlaTxW_T3fqLGlEWEeKTs4B6_qUbKg7HLI3E4jVYNn_s)

Goals :

- [ ] Developer Associate Certification

NOTES :

- [AWS Regional Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/?p=ngi&loc=4)

Logs :

- [ ] Get Associate Developer Cert by October 2023
- [ ] Learn EKS Fargate
- [ ] Learn Docker Image

## 116. S3 Website Overview

Amazon S3 — Static Website Hosting

- S3 can host static websites and have them accessible on the Internet

- The website URL will be (depending on the region)
    - http://bucket-name.s3-website-aws-region.amazonaws.com

    OR

    - http://bucket-name.s3-website.aws-region.amazonaws.com

- If you get a 403 Forbidden error, make sure the bucket policy allows public reads!

## 119. S3 Versioning

Amazon S3 - Versioning

- You can version your files in Amazon $3
- It is enabled at the bucket level
- Same key overwrite will change the “version”: |, 2, 3...
- It is best practice to version your buckets
 - Protect against unintended deletes (ability to restore a version)
 - Easy roll back to previous version
- Notes:
 - Any file that is not versioned prior to enabling versioning will have version “null”
 - Suspending versioning does not delete the previous versions

## 121. S3 Replication

Amazon S3 — Replication (CRR & SRR)

- Must enable Versioning in source and destination buckets
- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)
- Buckets can be in different AWS accounts
- Copying is asynchronous
- Must give proper IAM permissions to S3

- Use cases:
 - CRR-— compliance, lower latency access, replication across accounts
 - SRR — log aggregation, live replication between production and test accounts
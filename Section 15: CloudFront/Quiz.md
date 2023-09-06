# Quiz 12: CloudFront Quiz

1. You have a paid content that is stored in the S3 bucket. You want to distribute that content globally, so you have set up a CloudFront Distribution and configured the S3 bucket to only exchange data with your CloudFront Distribution. Which CloudFront feature allows you to securely distribute this paid content?

- CloudFront Signed URL

CloudFront Signed URLs are commonly used to distribute paid content through dynamically generated signed URLs.

2. You have a CloudFront Distribution that serves your website hosted on a fleet of EC2 instances behind an Application Load Balancer. All your clients are from the United States, but you found that some malicious requests are coming from other countries. What should you do to only allow users from the US and block other countries?

- Use CloudFront Geo Restriction

3. You have a static website hosted on an S3 bucket. You have created a CloudFront Distribution that points to your S3 bucket to better serve your requests and improve performance. After a while, you noticed that users can still access your website directly from the S3 bucket. You want to enforce users to access the website only through CloudFront. How would you achieve that?

- Configure your CloudFront Distribution and create an Origin Access Control, then update your S3 Bucket Policy to only accept requests from your CloudFront Distribution.

4. A website is hosted on a set of EC2 instances fronted by an Application Load Balancer. You have created a CloudFront Distribution and set up its origin to point to your ALB. What should you use to provide access to hundreds of private files served by your CloudFront distribution?

- CloudFront Signed Cookies

Signed Cookies are useful when you want to access multiple files.

5. What does this S3 bucket policy do?

```
{

    "Version": "2012-10-17",

    "Id": "Mystery policy",

    "Statement": [{

        "Sid": "What could it be?",

        "Effect": "Allow",

        "Principal": {

           "Service": "cloudfront.amazonaws.com"

        },

        "Action": "s3:GetObject",

        "Resource": "arn:aws:s3:::examplebucket/*",
        "Condition": {
            "StringEquals": {
                "AWS:SourceArn": "arn:aws:cloudfront::123456789012:distribution/EDFDVBD6EXAMPLE"
            }
        }

    }]

}
```

- Only allows the S3 bucket content to be accessed from your CloudFront Distribution

6. You have a React Single Page Application hosted on an S3 Bucket and served through CloudFront Distribution. You have made an update to your React application and pushed it to S3, but the old version is still cached at CloudFront, and clients still see the old version. You want the new update to be propagated immediately. What would you do?

- Use CloudFront Invalidation

7. You are hosting highly dynamic content in an S3 bucket in the us-east-1 region. You want to make this data to be available with low latency in Singapore's ap-southeast-1 region. What do you recommend?

- S3 Cross-Region Replication

S3 Cross-Region Replication allows you to replicate the data from one S3 bucket in an AWS region to another S3 bucket in another AWS region.

8. Using a CloudFront Distribution, you can cache based on the following, EXCEPT

- HTTP Methods

9. When you're configuring a CloudFront distribution to use Signed URLs/Cookies, it is recommended to use ............................ signer instead of ................................ signer.

- Trusted Key Group, CloudFront key Pair
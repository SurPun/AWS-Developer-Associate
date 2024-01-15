# Quiz 26: Advanced IAM Quiz

1. A company hired you to get some tasks done in their AWS Account. What is the best way to get access to their AWS Account?

- Use the STS service to assume an IAM Role in their AWS Account to gain temporary credentials

AWS STS (Security Token Service) allows you to get cross-account access through the creation of an IAM Role in your AWS account authorized to assume an IAM Role in another AWS account. See more here: https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html

2. You have an EC2 instance that has an attached IAM role providing it with read/write access to the S3 bucket named my-bucket, and it has been successfully tested. Later, you removed the IAM role from the EC2 instance, but after testing you found that writes stopped working but reads are still working. What is the likely cause for this behavior?

- The S3 bucket policy authorizes reads

When evaluating an IAM policy of an EC2 instance doing actions on S3, the union of both the IAM policy of the EC2 instance and the bucket policy of the S3 bucket are taken into account.

3. What does this IAM policy allow you to do?

`
{
    "Version": "2012-10-17",
    "Id": "Secret Policy",
    "Statement": [
        {
            "Sid": "EC2",
            "Effect": "Allow",
            "Action": "ec2:*",
            "Resource": "*"
        },
        {
            "Sid": "Passrole",
            "Effect": "Allow",
            "Action": [ "iam:PassRole" ],
            "Resource": "arn:aws:iam:::role/RDS-*"
        }
    ]
}
`

- It allows you to assign IAM Roles to EC2 if they start with RDS-

4. Your AWS account is now growing to 200 IAM users where each user has his own data in an S3 bucket named users-data. For each IAM user, you would like to provide personal space in the S3 bucket with the prefix /home/<username>, where they have read/write access. How can you do this efficiently?

- Create one customer-managed policy with dynamic variables and attach it to a group of all the IAM users

5. You are running an on-premises Microsoft Active Directory to manage your users. You have been tasked to to create another AD in AWS and establishes a trust relationship with your on-premises AD. Which AWS Directory service should you use?

- Managed Microsoft AD
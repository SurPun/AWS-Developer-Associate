# Quiz 9: AWS IAM, CLI, & SDK Quiz

1. An application hosted on an EC2 instance wants to upload objects to an S3 bucket using the PutObject API call, but it lacks the required permissions. What should you do?

- Ask an administrator to attach an IAM Policy to the IAM Role on your EC2 instance that authorizes it to do the required API call

IAM Roles are the right way to provide credentials and permissions to an EC2 instance.

2. You and your colleague are working on an application that's interacting with some AWS services through making API calls. Your colleague can run the application on his machine without issues, while you get API Authorization Exceptions. What should you do?

- Compare both your IAM Policy and him IAM Policy in AWS Policy Simulator to understand the differences

3. Your administrator launched a Linux EC2 instance and gives you the EC2 Key Pair so you can SSH into it. After getting into the EC2 instance, you want to get the EC2 instance ID. What is the best way to do this?

- Query the metadata at http://169.254.169.254/latest/meta-data

4. AWS CLI requires .......................... as its runtime.

- Python

5. You're running an application on an on-premises server. The application needs to perform API calls to an S3 bucket. How can you achieve this in the most secure manner?

- Create an IAM user to be used by the application, then generate IAM credentials and put the credentials into environment variables

Here, it's about creating a dedicated IAM user for the application, as using your own personal IAM credentials would blur the lines between actual users and applications. Or, you can run aws configure on the on-premises server.

6. When you have an IAM role attached to your EC2 instance and you run AWS CLI commands from inside this instance, AWS CLI uses the .......................... to get .......................... credentials.

- Instance Metadata, temporary

7. When an IAM role is attached to your EC2 instance, you can retrieve both the IAM role name and the IAM policies attached to the role.

- False

You can retrieve the IAM role name attached to your EC2 instance using the Instance Metadata service, but you can not retrieve the IAM policies themselves.

8. The last API calls you made to AWS KMS begin to throttle, as you have reached the max. allowed API calls per second. What should you do?

- Use Exponential Backoff Strategy

9. Before making API calls against MFA-protected API, you should use ............................... to get temporary credentials.

- STS GetSessionToken

10. AWS CLI uses credentials located in multiple locations and certain locations take precedence over others. Which of the following is the correct order for locations AWS CLI uses to find credentials?

- Command-Line Options —> Environment Variables —> EC2 Instance Profile

https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html#config-settings-and-precedence

11. AWS CLI and AWS SDKs sign API requests for you using your AWS access key. If you're writing your custom code, you must sign AWS API requests using .........................

- Signature Version 4 (SigV4)

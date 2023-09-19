# Quiz 15: CloudFormation Quiz

1. You have put a great deal of expertise into configuring an ELB properly to comply with your organizational policies using CloudFormation. You would like your snippet of code to be re-used by the teams who need to provision an ELB. What should you do?

- Upload the CloudFormation template on S3 and tell people to use it as a CloudFormation Nested Stack

2. What CloudFormation feature helps you analyze the upcoming changes on a CloudFormation stack update without actually executing them?

- ChangeSets

3. A SysOps Administrator created an AWS CloudFormation template for the first time. The stack failed with a status of ROLLBACK_COMPLETE. The Administrator identified and resolved the template issue that caused the failure. How should the Administrator continue with the stack deployment?

- Delete the failed stack and create a new stack

4. You work for a company that uses AWS Organization to manage multiple AWS accounts. You want to create a CloudFormation stack in multiple AWS accounts in multiple AWS Regions. What is the easiest way to achieve this?

- CloudFormation StackSets

5. What CloudFormation feature can you use to detect changes made to your stack resources outside CloudFormation?

- CloudFormation Drift

6. You have 2 CloudFormation templates. Template A contains the networking components (VPC, Subnets, SGs, ...) and template B contains the application infrastructure (EC2 instances, ALB, EBS, ...). You want to attach the SGs in template A to the EC2 instances in template B. How would you achieve this task?

- Export the SGs Ids in the Outputs section from template A, then import exported values in template B using Fn::ImportValue

7. Which of the following are NOT valid CloudFormation Pseudo Parameters?

- AWS::AccountName

8. Your AWS infrastructure created with CloudFormation evolve over time. What should you do to update a CloudFormation stack?

- Update your CloudFormation template locally, then upload and apply it in the CloudFormation console

9. Before a CloudFormation template can be used by CloudFormation, it must be uploaded .............................

- to Amazon S3

CloudFormation references a template from Amazon S3, no matter what. If you upload the template from the AWS console, it gets uploaded to Amazon S3 behind the scenes, and CloudFormation references that template from there.

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

10. When you write a CloudFormation template, you must specify the order in which CloudFormation should create your resources.

- False

11. The following CloudFormation template sections are optional, EXCEPT ........................ is mandatory.

- Resources

12. Which CloudFormation intrinsic function allows you to retrieve the DNS name of an Application Load Balancer created with CloudFormation?

- Fn::GetAtt

13. What is wrong with the following CloudFormation template?

`
Mappings:
  AWSRegionArch2AMI:
    us-east-1:
      HVM64: ami-6869aa05
    us-west-2:
      HVM64: ami-7172b611
    us-west-1:
      HVM64: ami-31490d51
    eu-west-1:
      HVM64: ami-f9dd458a
  EnvironmentToInstanceType:
    development:
      instanceType: t2.micro
    production:
      instanceType: m4.large

Resources:
  EC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !FindInMap [EnvironmentToInstanceType, !Ref 'EnvironmentName', instanceType]
      ImageId: !FindInMap [AWSRegionArch2AMI, !Ref 'AWS::Region', HVM64]
`

- The parameter 'EnvironmentName' is missing

14. The !Ref intrinsic function can be used to reference the following, EXCEPT

- Conditions

15. With the parameter IPAddress value being 10.0.0.1, what is the output of the following intrinsic function?

`
Fn::Join:
  - ''
  - [IPAddress=, !Ref 'IPAddress']
`

- 'IPAddress=10.0.0.1'

16. You're trying to delete a CloudFormation stack, but you can't because other CloudFormation stacks reference its exported outputs. What should you do?

- First, you need to delete the other CloudFormation stacks that reference the exported outputs, then delete it

17. You're trying to create an exported output, but you receive the following error SSHSecurityGroup output already exist. What is a possible cause for this error?

`
Outputs:
  StackSSHSecurityGroup:
    Description: The SSH Security Group for our Company
    Value: !Ref MyCompanyWideSSHSecurityGroup
    Export:
      Name: SSHSecurityGroup
`

- Exported output names must be unique within your region
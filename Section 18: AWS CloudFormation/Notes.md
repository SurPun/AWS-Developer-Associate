# Section 18: AWS CloudFormation

## 197. CloudFormation Overview

Infrastructure as Code

- Currently, we have been doing a lot of manual work
- All this manual work will be very tough to reproduce:
 - In another region
 - in another AWS account
 - Within the same region if everything was deleted

- Wouldn't it be great, if all our infrastructure was... code?
- That code would be deployed and create / update / delete our infrastructure

What is CloudFormation

- CloudFormation is a declarative way of outlining your AWS Infrastructure, for any resources (most of them are supported).
- For example, within a CloudFormation template, you say:
 - I want a security group
 - I want two EC2 machines using this security group
 - I want two Elastic IPs for these EC2 machines
 - I want an s3 bucket
 - I want a load balancer (ELB) in front of these machines

- Then CloudFormation creates those for you, in the right order, with the exact configuration that you specify

Benefits of AWS CloudFormation (1/2)

- Infrastructure as code
 - No resources are manually created, which is excellent for control
 - The code can be version controlled for example using git
 - Changes to the infrastructure are reviewed through code

- Cost
 - Each resources within the stack is staged with an identifier so you can easily see how much a stack costs you
 - You can estimate the costs of your resources using the CloudFormation template
 - Savings strategy: In Dev, you could automation deletion of templates at 5 PM and recreated at 8 AM, safely

Benefits of AWS CloudFormation (2/2)

- Productivity
 - Ability to destroy and re-create an infrastructure on the cloud on the fly
 - Automated generation of Diagram for your templates!
 - Declarative programming (no need to figure out ordering and orchestration)

- Separation of concern: create many stacks for many apps, and many layers. Ex:
 - VPC stacks
 - Network stacks
 - App stacks

- Don't re-invent the wheel
 - Leverage existing templates on the web!
 - Leverage the documentation

How CloudFormation Works

- Templates have to be uploaded in $3 and then referenced in CloudFormation
- To update a template, we can't edit previous ones. We have to re- upload a new version of the template to AWS
- Stacks are identified by a name
- Deleting a stack deletes every single artifact that was created by CloudFormation.

Deploying CloudFormation templates

- Manual way:
 - Editing templates in the CloudFormation Designer
 - Using the console to input parameters, etc

- Automated way:
 - Editing templates in aYAML file
 - Using the AWS CLI (Command Line Interface) to deploy the templates
 - Recommended way when you fully want to automate your flow

CloudFormation Building Blocks

Templates components (one course section for each):

1. Resources: your AWS resources declared in the template (MANDATORY)
2. Parameters: the dynamic inputs for your template
3. Mappings: the static variables for your template
4. Outputs: References to what has been created
5. Conditionals: List of conditions to perform resource creation
6. Metadata

Templates helpers:
1. References
2. Functions

## 200. YAML Crash Course

YAML Crash Course

- YAML and JSON are the languages you can use for CloudFormation.

- JSON is horrible for CF

- YAML is great in so many ways

- Let's learn a bit about it!
    - Key value Pairs
    - Nested objects
    - Support Arrays
    - Multi line strings

## 201. CloudFormation Resources

What are resources?

- Resources are the core of your CloudFormation template (MANDATORY)
- They represent the different AWS Components that will be created and configured
- Resources are declared and can reference each other
- AWS figures out creation, updates and deletes of resources for us
- There are over 224 types of resources (!)
- Resource types identifiers are of the form:
 - AWS: :aws-product-name: :data-type-name

How do i find resources documentation?

- All the resources can be found here:
- http://docs.aws.amazon.com/AW/SCloudFormation/latest/UserGuide/aw s-template-resource-type-ref.html

- Then, we just read the docs
- Example here (for an EC2 instance):
 - http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aw s-properties-ec2-instance.html

FAO for resources

- Can i create a dynamic amount of resources?
 - No, you can’t. Everything in the CloudFormation template has to be declared. You can’t perform code generation there

- Is every AWS Service supported?
 - Almost. Only a select few niches are not there yet
 - You can work around that using AWS Lambda Custom Resources
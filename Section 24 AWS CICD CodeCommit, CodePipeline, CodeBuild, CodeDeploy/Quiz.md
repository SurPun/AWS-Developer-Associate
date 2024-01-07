# Quiz 21: AWS CICD Quiz

1. What is CICD stands for?

- Continuous Integration and Continuous Delivery

2. A company, hosts all their infrastructure in AWS, wants to find an AWS service alternative to GitLab as they want to version control their code entirely in AWS. Which AWS service do you recommend?

- AWS CodeCommit

AWS CodeCommit is a secure, highly scalable, managed source control service that hosts private Git repositories. It is an alternative to GitLab and GitHub

3. You would like to orchestrate your CICD pipeline to deliver all the way to Elastic Beanstalk. Which AWS service do you recommend?

- AWS CodePipeline

AWS CodePipeline is a fully managed continuous delivery (CD) service that helps you automate your release pipeline for fast and reliable application and infrastructure updates. It automates the build, test, and deploy phases of your release process every time there is a code change. It has direct integration with Elastic Beanstalk.

4. Which AWS service helps you deploy your code to a fleet of EC2 instances with a specific strategy (e.g., Blue/Green deployment)?

- AWS CodeDeploy

AWS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of computing services such as EC2, Fargate, Lambda, and your on-premises servers. You can define the strategy you want to execute such as in-place or blue/green deployments.

5. You have a Jenkins Continuous Integration (CI) build server hosted on-premises and you would like to stop it and replace it with an AWS managed service. Which AWS should you choose?

- AWS CodeBuild

AWS CodeBuild is a fully managed continuous integration (CI) service that compiles source code, runs tests, and produces software packages that are ready to deploy. It is an alternative to Jenkins.

6. You plan to create a CICD for your application in AWS. You want to run some automated tests on your application before the deployment process. Which AWS service allows you to do so?

- AWS CodeBuild

7. You're using CodeCommit as your code repository where developers push code changes to it. To prevent developers from committing any secret credentials, you want to automatically trigger code analysis after each commit. How can you achieve this?

- Setup AWS SNS/Lambda integration in CodeCommit

8. AWS CodeCommit supports the following authentication methods, EXCEPT ............................

- WebSoket

9. Your colleague has an IAM user in another AWS Account who wants to access your CodeCommit repository. What should you do?

- Create an IAM role in your AWS account with the required permissions, then tell him to use STS cross-account access to assume this IAM role

10. A CodePipeline pipeline that you manage just failed to deploy your code to Elastic Beanstalk even though the code has been pushed successfully to your CodeCommit repository. The pipeline just working fine 10 minutes ago. What is most likely the reason for this?

- Your CodeBuild stage probably failed some tests

11. Your manager wants to receive emails when your CodePipeline pipeline fails so he can identify and troubleshoot the problems. How can you achieve this?

- Setup an AWS CloudWatch Event Rule

12. Which AWS service allows you to track and audit API calls made to and from AWS CodePipeline?

- AWS CloudTrail

13. The buildspec.yml file must be placed .......................... so CodeBuild can work properly.

- at the root of your code

14. When your CodeBuild build project fails, you can do the following to troubleshoot the issues, EXCEPT ..........................

- SSH into the CodeBuild container to debug from there

CodeBuild containers are deleted at the end of their execution (success or failure). You can't SSH into them, even while they're running.

15. You're using CodeBuild to build your application as part of the CICD process. The build process takes a long time, so you investigated this and found that 15 minutes at each build is spent on pulling dependencies from remote repositories. What should you do to drastically speed up the build process?

- Modify the buildspec.yml to enable Dependencies Caching in Amazon S3

16. (Hard Question - think outside the box!!)

You would like to automatically deploy a Single Page Application (SPA) to the S3 bucket, after generating the static files from a set of markdown files. Which AWS services should you use for this?

- CodePipeline + CodeBuild

CodeBuild can run any commands, so you can use it to run commands including build a static website and copy your static web files to an S3 bucket.

17. What's the proper order of Lifecycle Events in CodeDeploy for an EC2/on-premises deployment?

- ApplicationStop, DownloadBundle, BeforeInstall, Install, AfterInstall, ApplicationStart, ValidateService

18. Which Lifecycle Event hook should be used in the appspec.yml file to ensure the application is properly running after being deployed?

- ValidateService

19. You manage a fleet of EC2 and on-premises instances where you're trying to run your first deployment using AWS CodeDeploy, but it doesn't work. Which of the following could be a possible cause?

- You've probably forgotten to install and start the CodeDeploy agent on the instances

20. You would like to have a one-stop dashboard for all the CICD needs for all of your projects. You don't need heavy control of the individual configuration for all the components in your CICD, but need to be able to get a holistic view of your projects. Which AWS service do you recommend?

- AWS CodeStar

21. CodeBuild containers are run outside of a VPC and it's impossible to connect to resources in your VPC.

- False

You can configure CodeBuild to run its build containers in a VPC, so they can access private resources in a VPC such as databases, internal load balancers, ...

22. CodeDeploy supports the following predefined deployment configurations for EC2/on-premises instances, EXCEPT .......................

- Immutable
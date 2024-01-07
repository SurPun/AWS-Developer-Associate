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

11. 
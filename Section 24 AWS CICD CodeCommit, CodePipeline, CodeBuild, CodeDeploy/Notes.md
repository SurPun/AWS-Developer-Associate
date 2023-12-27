# Section 24: AWS CICD: CodeCommit, CodePipeline, CodeBuild, CodeDeploy

## 363. Introduction to CICD in AWS

CICD — Introduction

- We have learned how to:
 - Create AWS resources, manually (fundamentals)
 - Interact with AWS programmatically (AWS CLI)
 - Deploy code to AWS using Elastic Beanstalk

- All these manual steps make it very likely for us to do mistakes!

- We would like our code “in a repository” and have it deployed onto AWS
 - Automatically
 - The right way
 - Making sure it's tested before being deployed
 - With possibility to go into different stages (dey, test, staging, prod)
 - With manual approval where needed

- To be a proper AWS developer... we need to learn AWS CICD

CICD — Introduction

- This section is all about automating the deployment we've done so far while adding increased safety

- We'll learn about:
 - AWS CodeCommit — storing our code
 - AWS CodePipeline — automating our pipeline from code to Elastic Beanstalk
 - AWS CodeBuild — building and testing our code
 - AWS CodeDeploy — deploying the code to EC2 instances (not Elastic Beanstalk)
 - AWS CodeStar — manage software development activities in one place
 - AWS CodeArtifact — store, publish, and share software packages
 - AWS CodeGuru — automated code reviews using Machine Learning

Continuous Integration (Cl)

- Developers push the code to a code repository often (e.g., GitHub, CodeCommit, Bitbucket...)
- A testing / build server checks the code as soon as It's pushed (CodeBuild, Jenkins Cl, ...)
- The developer gets feedback about the tests and checks that have passed / failed
- Find bugs early, then fix bugs
- Deliver faster as the code is tested
- Deploy often
- Happier developers, as they're unblocked

Continuous Delivery (CD)

- Ensures that the software can be released reliably whenever needed
- Ensures deployments happen often and are quick
- Shift away from “one release every 3 months” to "5 releases a day”
- That usually means automated deployment (e.g., CodeDeploy, Jenkins CD, Spinnaker, ...


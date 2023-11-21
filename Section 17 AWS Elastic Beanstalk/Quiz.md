# Quiz 14: Elastic Beanstalk Quiz

1. You're developing an application and would like to deploy it to Elastic Beanstalk with minimal cost. You should run it in ..................

- Single Instance Mode

The question mentions that you're still in the development stage and you want to reduce costs. Single Instance Mode will create one EC2 instance and one Elastic IP.

2. Elastic Beanstalk application versions can be deployed to ...........................

- Many environments

3. You have been tasked to run an application developed using Rust language on Elastic Beanstalk. After checking, you found that Rust runtime is not currently supported on Elastic Beanstalk. Which of the following is NOT a solution?

- Install scripts and security software using an EC2 User Data script

4. Environments in Elastic Beanstalk must have the following names: dev, test, and prod.

- False

Environments in Elastic Beanstalk can be named freely.

5. You are developing a new application that's hosted on Elastic Beanstalk. As you are in the development process you don't mind downtime so you want your application to be deployed as soon as a new version is available. Which Elastic Beanstalk deployment option should you use?

- All at once

6. A company hosting their website on AWS Elastic Beanstalk. They want a methodology to continuously release new application versions with the ability to roll back very quickly in case if there're any issues. Also, the application must be running at full capacity while releasing new versions. Which Elastic Beanstalk deployment option do you recommend?

- Immutable

In this mode, a full set of new instances running the new version of the application in a separate Auto Scaling Group is launched. To roll back quickly, this mode terminates the ASG holding the new application version, while the current one is untouched and already running at full capacity.

7. You're a DevOps engineer working for a startup company hosting their application on Elastic Beanstalk. The application is in its early phases and it has a lot of new updates every week while being used by a number of users. You want to continuously release new features without application downtime and without incurring extra costs. It's acceptable to temporarily decrease the number of running instances serving users. Which Elastic Beanstalk deployment option should you choose?

- Rolling

8. Which Elastic Beanstalk deployment option allows you to release new versions of your application with minimal added cost while maintaining the full capacity to serve the current users?

- Rolling with Additional Batches

9. To improve your application performance, you want to add an ElastiCache cluster to your application hosted on Elastic Beanstalk. What should you do?

- Create an elasticache.config file in the .ebextensions folder which is at the root of the code zip file and provides appropriate configuration

10. Your deployments on Elastic Beanstalk have been painfully slow. After checking the logs, you realize that this is due to the fact that your application dependencies are resolved on each instance each time you deploy. What can you do to speed up the deployment process with minimal impact?

- Resolve the dependencies beforehand and package them in the zip file uploaded to Elastic Beanstalk

11. Which AWS service does Elastic Beanstalk use under the hood?

- AWS CloudFormation

12. Due to compliance regulations, you have been tasked to enable HTTPS for your application hosted on Elastic Beanstalk. This allows in-flight encryption between your clients and web servers. What must be done to set up HTTPS on Elastic Beanstalk?

- Create an .ebextension/securelistener-alb.config file to configure the Application Load Balancer

13. Which feature in Elastic Beanstalk allows you to automate deletions of old application versions so that new application versions can be created?

- Use a Lifecycle Policy

14. You're using Elastic Beanstalk and you would like to schedule tasks to run periodically and asynchronously. These tasks typically take more than 1 hour to complete. Which Elastic Beanstalk environment should you choose?

- Worker environment and a corn.yaml file

15. You have created a test environment in Elastic Beanstalk and as part of the environment, you have created an RDS DB instance. How can you make sure the database can be used after you delete the environment?

- Make a snapshot of the RDS DB instance before it gets deleted

16. You're running an application on Elastic Beanstalk. You have just finished a major update to your application. You want to deploy the new version then direct a small percentage of traffic to the new version so you can test and fall back if there're any issues. Which Elastic Beanstalk deployment option should you choose?

- Traffic Splitting

17. You have been hired by a company to run some tests on their application hosted on Elastic Beanstalk. You can't run these tests on the current environment as this is the production environment, so you have to create another environment similar to the one already running. Which Elastic Beanstalk feature allows you to do this?

- Elastic Beanstalk Cloning


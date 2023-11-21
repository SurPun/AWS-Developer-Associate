# Quiz 4: High Availability & Scalability

1. Scaling an EC2 instance from r4.large to r4.4xlarge is called .....................

- Vertical Scalability

2. Running an application on an Auto Scaling Group that scales the number of EC2 instances in and out is called .....................

- Horizontal Scalability

3. Elastic Load Balancers provide a .......................

- Static DNS name we can use in our application

Only Network Load Balancer provides both static DNS name and static IP. While, Application Load Balancer provides a static DNS name but it does NOT provide a static IP. The reason being that AWS wants your Elastic Load Balancer to be accessible using a static endpoint, even if the underlying infrastructure that AWS manages changes.

4. You are running a website on 10 EC2 instances fronted by an Elastic Load Balancer. Your users are complaining about the fact that the website always asks them to re-authenticate when they are moving between website pages. You are puzzled because it's working just fine on your machine and in the Dev environment with 1 EC2 instance. What could be the reason?

- The Elastic Load Balancer does not have Sticky Sessions enabled

ELB Sticky Session feature ensures traffic for the same client is always redirected to the same target (e.g., EC2 instance). This helps that the client does not lose his session data.

5. You are using an Application Load Balancer to distribute traffic to your website hosted on EC2 instances. It turns out that your website only sees traffic coming from private IPv4 addresses which are in fact your Application Load Balancer's IP addresses. What should you do to get the IP address of clients connected to your website?

- Modify your website's backend to get the client IP address from X- Forwarded-For header

When using an Application Load Balancer to distribute traffic to your EC2 instances, the IP address you'll receive requests from will be the ALB's private IP addresses. To get the client's IP address, ALB adds an additional header called X-Forwarded-For contains the client's IP address.

6. You hosted an application on a set of EC2 instances fronted by an Elastic Load Balancer. A week later, users begin complaining that sometimes the application just doesn't work. You investigate the issue and found that some EC2 instances crash from time to time. What should you do to protect users from connecting to the EC2 instances that are crashing?

- Enable ELB Health Checks

When you enable ELB Health Checks, your ELB won't send traffic to unhealthy (crashed) EC2 instances.

7. You are working as a Solutions Architect for a company and you are required to design an architecture for a high-performance, low-latency application that will receive millions of requests per second. Which type of Elastic Load Balancer should you choose?

- Network Load Balancer

Network Load Balancer provides the highest performance and lowest latency if your application needs it.

8. Application Load Balancers support the following protocols, EXCEPT:

- TCP

Network Load Balancers support both TCP and UDP protocols.

9. Application Load Balancers can route traffic to different Target Groups based on the following, EXCEPT:

- Client's Location (Geography)

ALBs can route traffic to different Target Groups based on URL Path, Hostname, HTTP Headers, and Query Strings.

10. Registered targets in a Target Groups for an Application Load Balancer can be one of the following, EXCEPT:

- Network load Balancer

11. For compliance purposes, you would like to expose a fixed static IP address to your end-users so that they can write firewall rules that will be stable and approved by regulators. What type of Elastic Load Balancer would you choose?

- Network Load Balancer

Network Load Balancer has one static IP address per AZ and you can attach an Elastic IP address to it. Application Load Balancers and Classic Load Balancers as a static DNS name.

12. You want to create a custom application-based cookie in your Application Load Balancer. Which of the following you can use as a cookie name?

- APPUSERC

The following cookie names are reserved by the ELB (AWSALB, AWSALBAPP, AWSALBTG).

13. You have a Network Load Balancer that distributes traffic across a set of EC2 instances in us-east-1. You have 2 EC2 instances in us-east-1b AZ and 5 EC2 instances in us-east-1e AZ. You have noticed that the CPU utilization is higher in the EC2 instances in us-east-1b AZ. After more investigation, you noticed that the traffic is equally distributed across the two AZs. How would you solve this problem?

- Enable Cross-Zone Load Balancing

When Cross-Zone Load Balancing is enabled, ELB distributes traffic evenly across all registered EC2 instances in all AZs.

14. Which feature in both Application Load Balancers and Network Load Balancers allows you to load multiple SSL certificates on one listener?

- Server Name Indication (SNI)

15. You have an Application Load Balancer that is configured to redirect traffic to 3 Target Groups based on the following hostnames: users.example.com, api.external.example.com, and checkout.example.com. You would like to configure HTTPS for each of these hostnames. How do you configure the ALB to make this work?

- Use Server Name Indication (SNI)

Server Name Indication (SNI) allows you to expose multiple HTTPS applications each with its own SSL certificate on the same listener. Read more here: https://aws.amazon.com/blogs/aws/new-application-load-balancer-sni/

16. You have an application hosted on a set of EC2 instances managed by an Auto Scaling Group that you configured both desired and maximum capacity to 3. Also, you have created a CloudWatch Alarm that is configured to scale out your ASG when CPU Utilization reaches 60%. Your application suddenly received huge traffic and is now running at 80% CPU Utilization. What will happen?

- Nothing

The Auto Scaling Group can't go over the maximum capacity (you configured) during scale-out events.

17. You have an Auto Scaling Group fronted by an Application Load Balancer. You have configured the ASG to use ALB Health Checks, then one EC2 instance has just been reported unhealthy. What will happen to the EC2 instance?

- The ASG will terminate the EC2 instance

You can configure the Auto Scaling Group to determine the EC2 instances' health based on Application Load Balancer Health Checks instead of EC2 Status Checks (default). When an EC2 instance fails the ALB Health Checks, its marked unhealthy and will be terminated while the ASG launches a new EC2 instance.

18. Your boss asked you to scale your Auto Scaling Group based on the number of requests per minute your application makes to your database. What should you do?

- Create a CloudWatch custom metric then create a CloudWatch Alarm on this metric to scale your ASG

There's no CloudWatch Metric for "requests per minute" for backend-to-database connections. You need to create a CloudWatch Custom Metric, then create a CloudWatch Alarm.

19. An application is deployed with an Application Load Balancer and an Auto Scaling Group. Currently, you manually scale the ASG and you would like to define a Scaling Policy that will ensure the average number of connections to your EC2 instances is around 1000. Which Scaling Policy should you use?

- Target Tracking Policy

20. Your application hosted on EC2 instances managed by an Auto Scaling Group suddenly receives a spike in traffic which triggers your ASG to scale out and a new EC2 instance has been launched. The traffic continuously increases but the ASG doesn't launch any new EC2 instances immediately but after 5 minutes. What is a possible cause for this behavior?

- Cooldown Period

For each Auto Scaling Group, there's a Cooldown Period after each scaling activity. In this period, the ASG doesn't launch or terminate EC2 instances. This gives time to metrics to stabilize. The default value for the Cooldown Period is 300 seconds (5 minutes).

# Quiz 6: Route 53

1. You have purchased mycoolcompany.com on Amazon Route 53 Registrar and would like the domain to point to your Elastic Load Balancer my-elb-1234567890.us-west-2.elb.amazonaws.com. Which Route 53 Record type must you use here?

- Alias

2. You have deployed a new Elastic Beanstalk environment and would like to direct 5% of your production traffic to this new environment. This allows you to monitor for CloudWatch metrics and ensuring that there're no bugs exist with your new environment. Which Route 53 Record type allows you to do so?

- Weighted 

Weighted Routing Policy allows you to redirect part of the traffic based on weight (e.g., percentage). It's a common use case to send part of traffic to a new version of your application.

3. You have updated a Route 53 Record's myapp.mydomain.com value to point to a new Elastic Load Balancer, but it looks like users are still redirected to the old ELB. What is a possible cause for this behavior?

- Because of the TTL

Each DNS record has a TTL (Time To Live) which orders clients for how long to cache these values and not overload the DNS Resolver with DNS requests. The TTL value should be set to strike a balance between how long the value should be cached vs. how many requests should go to the DNS Resolver.

4. You have an application that's hosted in two different AWS Regions us-west-1 and eu-west-2. You want your users to get the best possible user experience by minimizing the response time from application servers to your users. Which Route 53 Routing Policy should you choose?

- Latency

Latency Routing Policy will evaluate the latency between your users and AWS Regions, and help them get a DNS response that will minimize their latency (e.g. response time)

5. You have a legal requirement that people in any country but France should NOT be able to access your website. Which Route 53 Routing Policy helps you in achieving this?

- Geolocation

6. You have purchased a domain on GoDaddy and would like to use Route 53 as the DNS Service Provider. What should you do to make this work?

- Create a Public Hosted Zone and update the 3rd party Registrar NS records

Public Hosted Zones are meant to be used for people requesting your website through the Internet. Finally, NS records must be updated on the 3rd party Registrar.

7. Which of the following are NOT valid Route 53 Health Checks?

- Health Check that monitor SQS Queue
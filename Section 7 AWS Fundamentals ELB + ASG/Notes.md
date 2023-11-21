# Section 7: AWS Fundamentals: ELB + ASG

## 57. High Availability and Scalability

- Scalability means that an application / system can handle greater loads
  by adapting.

- There are two kinds of scalability:

  - Vertical Scalability

  - Horizontal Scalability (= elasticity)

- Scalability is linked but different to High Availability

Vertical Scalability

- Increasing the size of the instance

Horizontal Scalability

- Increasing the number of instances.
- Horizontal scaling implies distributed systems

High Availability

- High Availability usually goes hand in hand with horizontal scaling
- High availability means running your application / system in at least 2 data enters (== Availability Zones)
- The goal of high availability is to survive a data center loss

- The high availability can be passive (for RDS Multi AZ example)
- The high availability can be active (for horizontal scaling)

## 58. Elastic Load Balancing (ELB)

- Load Balances are servers that forward traffic to multiple servers (e.g., EC2 instances) downstream

- An Elastic Load Balancer is a managed load balancer

  - AWS takes care of upgrades, maintenance, high availability

- It is integrated with many AWS offerings/services

Health Checks

- Health Checks are crucial for Load Balancers

- They enable the load balancer to know if instances it forwards traffic to are available to reply to requests

- The health check is done on a port and a route (/health is common)

## 60. Application Load Balancer (ALB)

- Application load balancers is layer 7 (HTTP)
- Load balancing to multiple HTTP applications across machines (target groups)
- Load balancing to multiple applications on the same machine (ex: containers)
- Support for HT TP/2 and WebSocket
- Support redirects (from HTTP to HTTPS for example)

Application Load Balancer (v2) (a)

- Routing tables to different target groups:

  - Routing based on path in URL (example.com/users & example.com/posts)
  - Routing based on hostname in URL (one.example.com & otherexample.com)
  - Routing based on Query String, Headers (example.com/users?id= | 23&order=false)

- ALB are a great fit for micro services & container-based applicatio (example: Docker & Amazon ECS)

- Has a port mapping feature to redirect to a dynamic port in ECS

- In comparison, we'd need multiple Classic Load Balancer per application

## 63. Network Load Balancer (NLB)

Network Load Balancer (v2)

- Network load balancers (Layer 4) allow to:

  - Forward TCP & UDP traffic to your instances
  - Handle millions of request per seconds
  - Less latency ~100 ms (vs 400 ms for ALB)

- NLB has one static IP per AZ, and supports assigning Elastic IP (helpful for whitelisting specific IP)
- NLB are used for extreme performance, TCP or UDP traffic
- Not included in the AWS free tier

## 65. Gateway Load Balancer (GWLB)

Gateway Load Balancer

- Deploy, scale, and manage a fleet of 3% party network virtual appliances in AWS
- Example: Firewalls, Intrusion Detection and Prevention Systems, Deep Packet Inspection Systems, payload manipulation, ...
- Operates at Layer 3 (Network Layer) — IP Packets
- Combines the following functions:
  - Transparent Network Gateway — single entry/exit for all traffic
  - Load Balancer — distributes traffic to your virtual appliances
- Uses the GENEVE protocol on port 6081

## 66. Elastic Load Balancer - Sticky Sessions

Sticky Sessions (Session Affinity)

- It is possible to implement stickiness so that the same client is always redirected to the same instance behind a load balancer
- This works for Classic Load Balancer, Application Load Balancer, and Network Load Balancer
- The “cookie” used for stickiness has an expiration date you control
- Use case: make sure the user doesn’t lose his session data
- Enabling stickiness may bring imbalance to the load over the backend EC2 instances

## 67. Elastic Load Balancer - Cross Zone Load Balancing

Cross-Zone Load Balancing

- Application Load Balancer

  - Enabled by default (can be disabled at the Target Group level)
  - No charges for inter AZ data

- Network Load Balancer & Gateway Load Balancer

  - Disabled by default
  - You pay charges ($) for inter AZ data if enabled

- Classic Load Balancer
  - Disabled by default
  - No charges for inter AZ data if enabled

## 68. Elastic Load Balancer - SSL

Elastic Load Balancers — SSL Certificates

- Classic Load Balancer (v1)

  - Support only one SSL certificate
  - Must use multiple CLB for multiple hostname with multiple SSL certificates

- Application Load Balancer (v2)

  - Supports multiple listeners with multiple SSL certificates
  - Uses Server Name Indication (SNI) to make it work

- Network Load Balancer (v2)

  - Supports multiple listeners with multiple SSL certificates
  - Uses Server Name Indication (SNI) to make it work

## 70. Elastic Load Balancer - Connection Draining

Connection Draining

- Feature naming

  - Connection Draining — for CLB
  - Deregistration Delay — for ALB & NLB

- Time to complete “in-flight requests’’ while the instance is de-registering or unhealthy

- Stops sending new requests to the EC2 instance which is de-registering

- Between | to 3600 seconds (default: 300 seconds)

- Can be disabled (set value to 0)

- Set to a low value if your requests are short

## 75. Auto Scaling Groups - Instance Refresh

Auto Scaling — Instance Refresh

- Goal: update launch template and then re-creating all EC2 instances

- For this we can use the native feature of Instance Refresh

- Setting of minimum healthy percentage

- Specify warm-up time (how long until the instance is ready to use)

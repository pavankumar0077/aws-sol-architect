Vertical Scalability
--
- Vertically scalability means increasing the size
of the instance
- For example, your application runs on a
t2.micro
- Scaling that application vertically means
running it on a t2.large
- Districal sea systems such as a database. on
- RDS, ElastiCache are services that can scale
vertically.
 There's usually a limit to how much you can
vertically scalé (hardware limit)

Horizontal Scalability
--
- Horizontal Scalability means increasing the
number of instances / systems for your
application
- Horizontal scaling implies distributed systems.
- This is very common for web applications /
modern applications
- It's easy to horizontally scale thanks the cloud
offerings such as EC2

High Availability & Scalability For EC2
--
- Vertical Scaling: Increase instance size (= scale up / down)
- From: t2.nano - 0.5G of RAM, I vCPU
- To: u-I 2tb I.metal - 12.3 TB of RAM, 448 vCPUs
  
- Horizontal Scaling: Increase number of instances (= scale out / in)
- Auto Scaling Group
- Load Balancer
  
- High Availability: Run instances for the same application across multi AZ
- Auto Scaling Group multi AZ
- Load Balancer multi AZ

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/dcc0ccd2-e842-442a-b3b9-64dfa39b0daf)

Why use a load balancer?
--
- Spread load across multiple downstream instances
- Expose a single point of access (DNS) to your application
- Seamlessly handle failures of downstream instances
- Do regular health checks to your instances
- Provide SSL termination (HTTPS) for your websites
- Enforce stickiness with cookies
- High availability across zones
- Separate public traffic from private traffic

Types of load balancer on AWS
--
- AWS has 4 kinds of managed Load Balancers
- Classic Load Balancer (v| - old generation) - 2009 - CLB
- HTTP, HTTPS, TCP, SSL (secure TCP)
- Application Load Balancer (v2 - new generation) - 2016 - ALB
- НТТР, HTTPS, WebSocket|
- Network Load Balancer (v2 - new generation) - 2017 - NLB
- TCP, TLS (secure TCP), UDP
- Gateway Load Balancer - 2020 - GWLB
- Operates at layer 3 (Network layer) - IP Protocol
- Overall, it is recommended to use the newer generation load balancers as they provide more features
- Some load balancers can be setup as internal (private) or external (public) ELBs

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/1b0a4e24-3a66-41a6-9362-f7a24f003963)

Application Load Balancer (v2)
--
- Application load balancers is Layer 7 (HTTP)
- Load balancing to multiple HT TP applications across machines
(target groups)
- Load balancing to multiple applications on the same machine
(ex: containers)
- Support for HTTP/2 and WebSocket
- Support redirects (from HTTP to HTTPS for example)

- Routing tables to different target groups:
- Routing based on path in URL (example.com/users & example.com/posts)
- Routing based on hostname in URL (one.example.com & other.example.com)
- Routing based on Query String, Headers
(example.com/users?id=|23&order=false)
- ALB are a great fit for micro services & container-based application
(example: Docker & Amazon ECS)
- Has a port mapping feature to redirect to a dynamic port in ECS
- In comparison, we'd need multiple Classic Load Balancer per application

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d5a585da-db4b-44cb-b5cb-d7dc804d216c)

Application Load Balancer (v2)
--
### Target Groups
- EC2 instances (can be managed by an Auto Scaling Group) - TTP
- ECS tasks (managed by ECS itself) — HT TP
- Lambda functions - HTTP request is translated into a JSON event
- IP Addresses - must be private IPs
- ALB can route to multiple target groups
- Health checks are at the target group level

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/527209cf-8b8d-438c-a6c5-5608f8bd51f6)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f4298e07-0f56-4fe2-9d15-0b164eb7f5d9)


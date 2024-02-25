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

ALB
--
- If you want your application to access using ALB and you don't want to access your application directly using ec2 instance then we add security group remove from anywhere and add only ALB security group.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/7be52079-6efa-4d46-8a81-9c38ebdf752e)

- This is the best pratice.

- We can add HTTP listener -- Add RULE
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/15c9b923-0231-4d39-ae94-de441c26ed10)
- We can add conditions
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/5cf297f8-6e4a-4b2c-ac21-c965194c7015) - Host based routing
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/640cab24-ee3b-4d4e-ae07-b608faab6e3c) - Path based routing.
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/1207f31e-259f-4bc5-8f88-faa257127f5e)
- We can add upto 100 conditions rule limits
- We can forward, redirect and fixed respone
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8f3efef2-8335-4d3f-8208-3f6b0008c403)
- We can add Priority -- Lower numberr is the highest priority
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/486fa5cf-bca1-4243-bfc5-bc0845495dfd)

## NETWORK LOAD BALANCCER 
- Network load balancers (Layer 4) allow to:
- Forward TCP & UDP traffic to your instances
- Handle millions of request per seconds
- Less latency ~ 100 ms (vs 400 ms for ALB)
- NLB has one static IP per AZ, and supports assigning Elastic IP
(helpful for whitelisting specific IP)
- NLB are used for extreme performance, TCP or UDP traffic
- Not included in the AWS free tier.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e70fce07-8ead-4a26-afb8-dea179f3e354)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/2ad22a08-a30e-4dc5-b0ff-88f0f871d4ca)

## Gateway Load Balancer
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f4a598b0-00b7-47d4-97f4-ef2a94aa2b54)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/9c795b7a-1945-4d30-afb1-5495f59503ad)

## Sticky Sessions ( SESSION AFFINITY )

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ff6750bc-a1fd-42c6-9852-5aa1c73eb8e9)

Sticky Sessions (Session A
- It is possible to implement stickiness so th
same client is always redirected to the sar
instance behind a load balancer
- This works for Classic Load Balancer, App
Load Balancer, and Network Load Balance
- The "cookie" used for stickiness has an
expiration date you control
- Use case: make sure the user doesn't lose
session data

### Sticky Sessions - Cookie Names

- Application-based Cookies
- Custom cookie
  1.Generated by the target
  2.Can include any custom attributes required by the application
  3.Cookie name must be specified individually for each target group
  4.Don't use AWSALB, AWSALBAPP, or AWSALBTG (reserved for use by the ELB)
- Application cookie
  1.Generated by the load balancer
  2.Cookie name is AWSALBAPP
- Duration-based Cookies
  1.Cookie generated by the load balancer
  2.Cookie name is AWSALB for ALB, AWSELB for CLB

### ADD COOKIE SESSIONS TO ALB
--> Go to Target Group
--> Actions --> Edit Attributes 
--> Find Stickiness 
--> ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d9098ee3-c56d-4ccc-a285-9acf6ad0f6de)
--> ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/899e2258-622b-4a45-9ebd-d4773993b619)

### CROSS ZONE LOAD BALANCING

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b201fb94-0588-4e8e-9887-7cb3bdf9dc97)

- Application Load Balancer
  1.Enabled by default (can be disabled at the Target Group level)
  2.No charges for inter AZ data
- Network Load Balancer & Gateway Load Balancer
  1.Disabled by default
  2.You pay charges ($) for inter AZ data if enabled
- Classic Load Balancer
  1.Disabled by default
  2.No charges for inter AZ data if enabled

### Example - of ALL ALB's

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/18d4d6b8-f3fb-4919-bdf6-a9e9f4ebaff3)

-- ALB --> Attributes --> ON Cross-Zone LB ( THESE IS ARE NLB AND GLB)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d7f916ef-91df-4930-890d-95bff9d61878)

-- ALB --> Attributes --> Cross Zone Load Balancer is BY DEFAULT ON. 
-- We can on and off by going into ALB -- Listeners -- Target group --> Attributes

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/46705c49-98a3-4d8c-b739-34faacadbfc0)

ELB - SSL Certificates 
==
- An be enCrypteate atlast (in-i he encryption lients and your load balancer
- SSL refers to Secure Sockets Layer, used to encrypt connections
- TLS refers to Transport Layer Security, which is a newer version
- Nowadays, TLS certificates are mainly used, but people still refer as SSL
- Public SSL certificates are issued by Certificate Authorities (CA)
- Comodo, Symantec, GoDaddy, GlobalSign, Digicert, Letsencrypt, etc...
- SSL certificates have an expiration date (you set) and must be renewed

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/fe0183a5-0fac-46fd-87a5-3d74ce13eae0)

SSL - SERVER NAME INDICATION (SNI)
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/98d3e14c-1809-4a6f-b1a8-ea74740c02d1)

- Classic Load Balancer (vI)
  1.Support only one SSL certificate
  2.Must use multiple CLB for multiple hostname with multiple SSL certificates
- Application Load Balancer (v2)
  1.Supports multiple listeners with multiple SSL certificates
  2.Uses Server Name Indication (SNI) to make it work
- Network Load Balancer (v2)
  1.Supports multiple listeners with multiple SSL certificates
  2.Uses Server Name Indication (SNI) to make it work

ADD SSL CERTIFICATE TO ALB and NLB
--
--> Goto LB --> DEMOALB --> Add Listener 
--> ADD HTTPS block and port 
--> We have options to Forward, Redirect, Return Fixed Response, Authenticate
--> ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/2bf4036b-9a9a-4cd6-8441-82d5ca29dded)
--> Update with target group
--> Certificate details -- ACM, Manual and etc.
--> ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0727533b-3bcc-4128-a7ea-be5ea827fafa)

ELB - Connection Draining
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ec7d250c-d82b-4ad8-a997-8a8f33025b06)

### AUTO SCALING GROUP ( ASG )

- In real-life, the load on your websites and application can change
- In the cloud, you can create and get rid of servers very quickly
- The goal of an Auto Scaling Group (ASG) is to:
- Scale out (add EC2 instances) to match an increased load
- Scale in (remove EC2 instances) to match a decreased load
- Ensure we have a minimum and a maximum number of EC2 instances running
- Automatically register new instances to a load balancer
- Re-create an EC2 instance in case a previous one is terminated (ex: if unhealthy)
- ASG are free (you only pay for the underlying EC2 instances)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/990941ad-32db-42e3-8493-865d74ed227c)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/cc86e79e-fc81-4786-afa3-86bb1685f6cd)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/13561ff5-386b-4aec-9a16-ff79428f9775)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/cd1efbdc-9a58-400a-bcd8-1c4bbffb6cac)




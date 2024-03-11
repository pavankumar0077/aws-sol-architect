![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/c75d16d7-dbf7-4d83-9e7f-23fc8b4c25a1)

Developer problems on AWS
--
- Managing infrastructure
- Deploying Code
- Configuring all the databases, load balancers, etc
- Scaling concerns
- Most web apps have the same architecture (ALB + ASG)
- All the developers want is for their code to run!
- Possibly, consistently across different applications and environments

Elastic Beanstalk - Overview
--
- Elastic Beanstalk is a developer centric view of deploying an application
on AWS
- It uses all the component's we've seen before: EC2, ASG, ELB, RDS, ...
- Managed service
- Automatically handles capacity provisioning, load balancing, scaling, application
health monitoring, instance configuration, ...
- Just the application code is the responsibility of the developer
- We still have full control over the configuration
- Beanstalk is free but you pay for the underlying instances

ELastic Beanstalk - Components
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/bfa7dff1-fecc-4726-af69-49ac929106dc)

Supported Platforms
--
• Go
• Java SE
• Java with Tomcat
• NET Core on Linux
• NET on Windows Server
• Node.js
• PHP
• Python
• Ruby
• Packer Builder
• Single Container Docker
• Multi-container Docker
• Preconfigured Docker

Web Server Tier vs Worker Tier
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/489416f7-d8ba-4742-a870-f02a418af345)

Elastic Beanstalk - Deployement Modes
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/7c3bfa8d-c2b4-45db-bf9f-03d9f04208ea)

Hands on 
--
Beanstalk with default ooptions --> Create EC2 profile role --> 
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/3a781e5b-f7e3-4d37-9c8a-6c2855f8de18)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8d48f6df-1eeb-4ac9-badb-c0d12cb6bcc2)


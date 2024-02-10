INSTANCE TYPE : https://aws.amazon.com/ec2/instance-types/

REF LINK : https://instances.vantage.sh/

SG
===
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/92986153-a9f7-4b34-a8da-d8e6a58746e1)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/9873d74e-9435-4f12-8cc1-75690d465077)

PORTS
======
Classic Ports to know
--------
- 22 = SSH (Secure Shell) - log into a Linux instance
-  21 = FTP (File Transfer Protocol) - upload files into a file share
-  2 = SFTP (Secure File Transfer Protocol) - upload files using SSH
- 80 = HTTP - – access unsecured websites
- 443 = HTTPS – access secured websites
- 3389 = RDP (Remote Desktop Protocol) - log into a Windows instance

EC2 instances purcharing options:
--
EC2 Instances Purchasing Options
On-Demand Instances - short workload, predictable pricing, pay by second
- Reserved (1 & 3 years)
- Reserved Instances - long workloads
- Convertible Reserved Instances - long workloads with flexible instances
- Savings Plans (I & 3 years) -commitment to an amount of usage, long workload
- Spot Instances - short workloads, cheap, can lose instances (less reliable)
- Dedicated Hosts - book an entire physical server, control instance placement
- Dedicated Instances - no other customers will share your hardware
- Capacity Reservations – reserve capacity in a specific AZ for any duration

EC2 on demand
--
- Pay for what you use:
Linux or Windows - billing per second, after the first minute
--
All other operating systems - billing per hour
- Has the highest cost but no upfront payment
- No long-term commitment
- Recommended for short-term and un-interrupted workloads, where
you can't predict how the application will behave

EC2 Reserved Instances
--
- Up to 72% discount compared to On-demand
- You reserve a specific instance attributes (Instance Type, Region, Tenancy, OS)
- Reservation Period - 1 year (+discount) or 3 years (+++discount)
- Payment Options - No Upfront (+), Partial Upfront (++), All Upfront (+++)
Reserved Instance's Scope - Regional or Zonal (reserve capacity in an AZ)
- Recommended for steady-state usage applications (think database)
- You can buy and sell in the Reserved Instance Marketplace
Convertible Reserved Instance
- Can change the EC2 instance type, instance family, OS, scope and tenancy
Up to 66% discount

EC2 Savings Plans
--
- Get a discount based on long-term usage (up to 72% - same as Rls)
-  Commit to a certain type of usage ($10/hour for I or 3 years)
-  Usage beyond EC2 Savings Plans is billed at the On-Demand price
- locked to a specific instance family & AWS region (e.g., M5 in us-east-1)
- Flexible across:
- Instance Size (e.g., m5.xlarge, m5.2xlarge)
- OS (e.g., Linux, Windows)
- Tenancy (Host, Dedicated, Default)

EC2 Spot Instances
--
- Can get a discount of up to 90% compared to On-demand
- Instances that you can "lose" at any point of time if your max price is less than the
current spot price
- The MOST cost-efficient instances in AWS
Useful for workloads that are resilient to failure
- Batch jobs
- Data analysis
- Image processing
- Any distributed workloads
- Workloads with a flexible start and end time
- Not suitable for critical jobs or databases


EC2 Dedicated Hosts
--
- A physical server with EC2 instance capacity fully dedicated to your use
- Allows you address compliance requirements and use your existing server
bound software licenses (per-socket, per-core, pe—VM software licenses)
Purchasing Options:
--
- On-demand - pay per second for active Dedicated Host
- Reserved - 1 or 3 years (No Upfront, Partial Upfront, All Upfront)
The most expensive option
- Useful for software that have complicated licensing model (BYOL - Bring Your
Own License)
- Or for companies that have strong regulatory or compliance needs

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d4b3b625-7b34-4676-8d3b-2f518e37b5b1)

EC2 Capacity Reservations
--
- Reserve On-Demand instances capacity in a specific AZ for any duration
- You always have access to EC2 capacity when you need it
- No time commitment (create/cancel anytime), no billing discounts
- Combine with Regional Reserved Instances and Savings Plans to benefit
from billing discounts
- You're charged at On-Demand rate whether you run instances or not
- Suitable for short-term, uninterrupted workloads that needs to be in a
specific AZ

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/2e9365f8-25aa-474c-83c2-9022cd26a2b3)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/75207529-4979-4188-b0e5-e31fdb722057)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/21959eb1-98e0-4466-8e98-2b87db6789da)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b910e470-5641-4f5c-b6d8-044ab758ca85)


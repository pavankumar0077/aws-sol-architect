# AWS Snow Family

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e6a88796-1cba-411e-837f-d5933f6471ea)

# Data Migrations with AWS Snow Family

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0dc71e1f-d3b7-45b8-b22d-d1602a9d97cd)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/4accdc5b-c181-417e-8ae4-81df3ee0d1d6)

Snowball Edge (for data transfers)
==
- PrAial data transport solution: move Bs or PBs of data in or out
- Alternative to moving data over the network (and paying network
fees)
- Pay per data transfer job
- Provide block storage and Amazon 53-compatible object storage
- Snowball Edge Storage Optimized
- 80 TB of HDD capacity for block volume and S3 compatible object
storage
- Snowball Edge Compute Optimized
- 42 TB of HDD er 281B. NMe capacity for block volume and 53
compatible object storage
- Use cases: large data cloud migrations, DC decommission, disaster
recovery

AWS Snowcone & Snowcone SSD
--
- Small, portable computing, anywhere, rugged & secure,
withstands harsh environments
- Light (4.5 pounds, 2.1 kg)
- Device used for edge computing, storage, and data
transfer
- Snowcone - 8 TB of HDD Storage
- Snowcone SSD - 14 TB of SSD Storage
- Use Snowcone where Snowball does not fit (space-
constrained environment)
- Must provide your own battery / cables
- Can be send back to AWS offline, or connect it to internet and use AWS DayaSync to send data.

AWS SNOWMOBILE
--
- Transfer exabytes of data (I EB = 1,000 PB = 1,000,000 TBs)
- Each Snowmobile has 100 PB of capacity (use multiple in parallel)
- High security: temperature controlled, GPS, 24/7 video surveillance
- Better than Snowball if you transfer more than 10 PB

Snow Family - Usage Process
--
1. Request Snowball devices from the AWS console for delivery
2. Install the snowball client / AWS OpsHub on your servers
3. Connect the snowball to your servers and copy files using the client
4. Ship back the device when you're done (goes to the right AWS
facility)
5. Data will be loaded into an $3 bucket
6. Snowball is completely wiped

What is Edge Computing ?
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/3e44426e-eb46-4ca4-a5db-de891eaf10ed)

Snow Family - Edge Computing
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/927f207e-51dd-48ca-9614-029b4933994a)

AWS OpsHub
--
- Historical i (Comman tinie derites toul
- Today, you can use AWS OpsHub (a software
manage your Snow Campy Cre/laptop to
- Unlocking and configuring single or clustered devices
- Transferring files
- Lanny Dece managing instances running on Snow
- Monitor device metrics (storage capacity, active
instances on your device)
- Launch compatible AWS services on your devices (ex: EC2, DataSync, NFS)

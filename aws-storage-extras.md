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

Solution Architecture : Snowball into Glacier
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/7dd980b2-3991-4a39-94ae-70d0857f78a5)

Amazon FSx - Overview
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/009c461e-4dca-45ac-a3b3-1c6ecdfa2296)

Amazon FSx for Windows (File Server)
--
- FSx for Windows is a fully managed Windows file system share drive
- Supports SMB protocol & Windows NTFS
- Microsoft Active Directory integration, ACLs, user quotas
- Can be mounted on Linux EC2 instances
- Supports Microsoft's Distributed File System (DFS) Namespaces (group files across multiple FS)
- Scale up to 10s of GB/s, millions of IOPS, 100s PB of data
- Storage Options:
- Can be accessed from your on-premises infrastructure (VPN or Direct Connect)
- Can be configured to be Multi-AZ (high availability)
- Data is backed-up daily to S3

Amazon FSx for Lustre
--
- Lustre is a type of parallel distributed file system, for large-scale computing
- The name Lustre is derived from "Linux" and "cluster
- Machine Learning, High Performance Computing (HPC)
- Video Processing, Financial Modeling, Electronic Design Automation
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- Storage Options:
- SSD - low-latency, IOPS intensive workloads, small & random file operations
- HDD - throughput-intensive workloads, large & sequential file operations
- Seamless integration with S3
- Can "read S3" as a file system (through FSx)
- Can write the output of the computations back to S3 (through FSx)
- Can be used from on-premises servers (VPN or Direct Connect)

Fsx File System Deployment Options
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/99e4034f-243e-480a-9ef1-d1f20679260a)

Amazon FSx for NetApp ONTAP
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/026ebf2e-f56b-4a3f-b858-0daad97a9c95)

Amazon FSx for OpenZFS
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/872ce661-0034-4136-a33a-6b837bf28916)

Hybrid Cloud for Storage
--
- AWS is pushing for "hybrid cloud"
- Part of your infrastructure is on the cloud
- Part of your infrastructure is on-premises
- This can be due to
- Long cloud migrations
- Security requirements
- Compliance requirements
- IT strategy
- S3 is a proprietary storage technology (unlike EFS / NFS), so how do
you expose the S3 data on-premises?

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/be0322b7-84fa-4ecf-a25e-2db0ef1a1246)

AWS Storage Gateway
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e9733962-ec3a-4c21-8d8d-895a13c28e07)

Amazon S3 File Gateway
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ae117d19-7224-40d8-89cc-4386d0dca3bc)

- Configured S3 buckets are accessible using the NFS and SMB protocol
- Most recently used data is cached in the file gateway
- Supports S3 Standard, 53 Standard IA, S3 One Zone A, 53 Intelligent Tiering
- Transition to S3 Glacier using a Lifecycle Policy
- Bucket access using IAM roles for each File Gateway
- SMB Protocol has integration with Active Directory (AD) for user authentication

Amazon FSx File Gateway
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ea265a73-0510-43b3-bf42-ce57e8ef339c)

- Native access to Amazon FSx for Windows File Server
- Local cache for frequently accessed data
- Windows native compatibility (SMB, NTFS, Active Directory...)
- Useful for group file shares and home directories

Volume Gateway
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/bdbd0999-7ef8-43b3-b04a-fdea47a3134e)

- Block storage using iSCSI protocol backed by S3
- Backed by EBS snapshots which can help restore on-premises volumes!
- Cached volumes: low latency access to most recent data
- Stored volumes: entire dataset is on premise, scheduled backups to S3

Tape Gateway
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/94201777-5f04-4487-b967-cc06e5076527)

- Some companies have backup processes using physical tapes (!)
- With Tape Gateway, companies use the same processes but, in the cloud
- Virtual Tape Library (VTL) backed by Amazon 53 and Glacier
- Back up data using existing tape-based processes (and iSCS| interface)
- Works with leading backup software vendors

Storage Gateway - Hardware appliance
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8871c983-1ec4-4b59-a85b-77e7c7a19fa2)

AWS Storage Gatway
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8a231709-1162-4798-a550-52dfbaf1ed55)

AWS TRANSFER FAMILY
--
- Amazon ars sing the ei protocosters into and out of Amazon 53 or
- Supported Protocols
- AWS Transfer for FTP (File Transfer Protocol (FTP))
- AWS Transfer for FTPS (File Transfer Protocol over SSL (FTPS))
- AWS Transfer for SFTP (Secure File Transfer Protocol (SFTP))
- Managed infrastructure, Scalable, Reliable, Highly Available (multi-AZ)
- Pay per provisioned endpoint per hour + data transfers in GB
- Store and manage users' credentials within the service
  Integrate with existing authentication systems (LDAP, Okta, Amazon Cognito, Microsoft Active Directory)
• Usage: sharing files, public datasets, CRM, ERP, ...

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/16751dde-68bc-40be-a32a-25d95aa135ff)

AWS DataSync
--
- Move large amount of data to and from
- On-premises / other cloud to AWS (NFS, SMB, HDFS, S3 API...) - needs agent
- AWS to AWS (different storage services) - no agent needed
- Can synchronize to:
- Amazon 53 (any storage classes - including Glacier)
- Amazon EFS
- Amazon FSx (Windows, Lustre, NetApp, OpenZFS...).
- Replication tasks can be scheduled hourly, daily, weekly
- File permissions and metadata are preserved (NFS POSIX, SMB...)
- One agent task can use 10 Gbps, can setup a bandwidth limit

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/1d654156-442f-431d-b130-44c84119a162)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/de087c57-f41b-4e8f-9b32-3b757f018208)


Storage Comparison
--
- S3: Object Storage
- S3 Glacier: Object Archival
- EBS volumes: Network storage for one EC2 instance at a time
- Instance Storage: Physical storage for your EC2 instance (high IOPS)
- EFS: Network File System for Linux instances, POSIX filesystem
- FSx for Windows: Network File System for Windows servers
- FSx for Lustre: High Performance Computing Linux file system
- FSx for NetApp ONTAP: High OS Compatibility
- FSx for OpenZFS: Managed ZFS file system
- Storage Gateway: S3 & FSx File Gateway, Volume Gateway (cache & stored), Tape Gateway
- Transfer Family: FTP, FTPS, SFTP interface on top of Amazon 53 g
- DataSync: Schedule data sync from on-premises to AWS, or AW
- Snowcone / Snowball / Snowmobile: to move large amount of dically
- Database: for specific workloads, usually with indexing and querying

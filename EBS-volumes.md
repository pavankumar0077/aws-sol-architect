EBS Volume Types
==
- EBS Volumes come in 6 types
- gp2 / gp3 (SSD): General purpose SSD volume that balances price and performance for a wide variety of workloads
- iol /io2 Block Express (SSD): Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads
- stl (HDD): Low cost HDD volume designed for frequently accessed, throughput intensive workloads
- scl (HDD): Lowest cost HDD volume designed for less frequently accessed workloads
- EBS Volumes are characterized in Size | Throughput | IOPS (I/O Ops Per Sec)
- When in doubt always consult the AWS documentation – it’s good!
- Only gp2/gp3 and io1/io2 Block Express can be used as boot volumes

EBS Volume Types Use cases
--
General Purpose SSD
---
- Cost effective storage, low-latency
- System boot volumes, Virtual desktops, Development and test environments
- 1 GiB - 16 TiB
### gp 3:
- Baseline of 3,000 IOPS and throughput of 125 MiB/s
- Can increase IOPS up to 16,000 and throughput up to 1000 MiB/s independently
### gp2:
- Small gp2 volumes can burst IOPS to 3,000
- Size of the volume and IOPS are linked, max IOPS is 16,000
- 3 IOPS per GB, means at 5,334 GB we are at the max IOPS

### Provisioned IOPS (PIOPS) SSD
- Critical business applications with sustained IOPS performance
- Or applications that need more than 16,000 IOPS
- Great for databases workloads (sensitive to storage perf and consistency
- io| (4 GiB - 16 TiB):
- Max PIOPS: 64,000 for Nitro EC2 instances & 32,000 for other
- Can increase PIOPS independently from storage size
- io2 Block Express (4 GiB - 64 TiB):
- Sub-millisecond latency
- Max PIOPS: 256,000 with an IOPS:GiB ratio of 1,000:1
- Supports EBS Multi-attach

### Hard Disk Drives (HDD)
- Cannot be a boot volume
- 125 GiB to 16 TiB
- Throughput Optimized HDD (stl)
- Big Data, Data Warehouses, Log Processing
- Max throughput 500 MiB/s - max lOPS 500
- Cold HDD (sc l):
- For data that is infrequently accessed
- Scenarios where lowest cost is important
- Max throughput 250 MiB/s - max IOPS 250

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8044d963-d703-4cfa-bd39-d0ff6fee8b33)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/2b5791c0-db96-443d-a81d-ac64fa07ca9c)


EBS Encryption
==
- When you create an encrypted EBS volume, you get the following:
- Data at rest is encrypted inside the volume
- All the data in flight moving between the instance and the volume is encrypted
- All snapshots are encrypted
- All volumes created from the snapshot]
- Encryption and decryption are handled transparently (you have nothing to
- Encryption has a minimal impact on latency
- EBS Encryption leverages keys from KMS (AES-256)
- Copying an unencrypted snapshot allows encryption
- Snapshots of encrypted volumes are encrypted

### Encryption: encrypt an unencrypted EBS volume
- Create an EBS snapshot of the volume
- Encrypt the EBS snapshot (using copy )
- Create new ebs volume from the snapshot ( the volume will also be
encrypted)
- Now you can attach the encrypted volume to the original instance

## EFS 
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b9813ba6-a195-4619-906c-8b14bde1a06f)

Amazon EFS - Elastic File System
- Use cases: content management, web serving, data sharing, Wordpress
- Uses NFSv4.I protocol
- Uses security group to control access to EFS
- Compatible with Linux based AMI (not Windows)
- Encryption at rest using KMS
- POSIX file system (~Linux) that has a standard file API
- File system scales automatically, pay-per-use, no capacity planning!


### EFS - Performance & Storage Classes
- EFS Scale
- 1000s of concurrent NFS clients, 10 GB+ /s throughput
- Grow to Petabyte-scale network file system, automatically
- Performance Mode (set at EFS creation time)
- General Purpose (default) - latency-sensitive use cases (web server, CMS, etc...)
- Max I/O - higher latency, throughput, highly parallel (big data, media processing)
- Throughput Mode
- Bursting - 1 TB = 50MiB/s + burst of up to 100MiB/s
- Provisioned - set your throughput regardless of storage size, ex: | GiB/s for
- Elastic - automatically scales throughput up or down based on your workloa
- Up to 3GiB/s for reads and | GiB/s for writes
- Used for unpredictable workloads

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/a5004651-b8c0-4078-9189-c1a2077d6d82)


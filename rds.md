Advantage over using RDS versus deploying
--
### DB on EC2
- RDS is a managed service:
- Automated provisioning, OS patching
- Continuous backups and restore to specific timestamp (Point in Time Restore)!
- Monitoring dashboards
- Read replicas for improved read performance
- Multi AZ setup for DR (Disaster Recovery)
### Maintenance windows for upgrades
- Scaling capability (vertical and horizontal)
- Storage backed by EBS (gp2 or iol)
- BUT you can't SSH into your instances

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0e52db57-25e2-4026-a52b-243187483aca)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0a265c83-3372-4cff-a143-f43239c8658f)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/a7e90ecb-f7a9-437d-888c-7779c60e0691)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/136e8ccf-ed7e-4b1b-a675-71863dbba5f8)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b1404152-390f-4e3c-b589-d5d88495344c)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f0e6cc67-1ea8-427c-87e0-7828c8e164e0)

RDS CUSTOM
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/bfd7712f-e137-4ba4-8bcb-d65a16ced925)

Amazon Aurora
--
- Aurora is a proprietary technology from AWS (not open sourced)
- Postgres and MySQL are both supported as Aurora DB (that means your
drivers will work as if Aurora was a Postgres or MySQL database)
- Aurora is "AWS cloud optimized" and claims 5x performance improvement
over MySQL on RDS, over 3x the performance of Postgres on RDS
- Aurora storage automatically grows in increments of 10GB, up to 128 TB.
- Aurora can have up to 15 replicas and the replication process is faster than
MySQL (sub 10 ms replica lag)
- Failover in Aurora is instantaneous. It's HA native.
- Aurora costs more than RDS (20% more) - but is more efficient

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b5b51ade-42c7-401a-ad48-12e8349f0b77)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/73872ae8-9b1d-4b5f-85c2-441531758521)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/3a243b9d-a06e-496c-b8aa-e5639bff3f3f)

Features of Aurora
--
- Automatic fail-over
- Backup and Recovery
- Isolation and security
- Industry compliance
- Push-button scaling
- Automated Patching with Zero Downtime
- Advanced Monitoring
- Routine Maintenance
- Backtrack: restore data at any point of time without using backups

Advanced Features of Aurora DB
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/18eae6f5-018d-4cb1-9ae0-a6d3d37976ea)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/32321ba8-ee53-4463-b941-e3367cf6fb3e)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/6d5f1272-9b14-4cf1-8d94-c8374dc24dee)

Global Aurora
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b6121e69-6f6c-4da7-8a26-2a7d2bc52b34)
- Aurora Cross Region Read Replicas:
  1. Useful for disaster recovery
- 2. Simple to put in place
- Aurora Global Database (recommended):
  1. Primary Region (read/write)
  2.Up to 5 secondary (read-only) regions, replication lag is less than I second
  3.Up to 16 Read Replicas per secondary region
  4. Helps for decreasing latency
  5. Promoting another region (for disaster recovery) has an RTO of minute
  ### **Typical cross-region replication takes less than 1 second**

 Aurora Machine Learning
 --
 ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e9a3a042-b0c9-4a2f-9713-643227618006)
 
- Enables you to add ML-based predictions to
your applications via SQL
- Simple, optimized, and secure integration
between Aurora and AWS ML services
- Supported services
1. Amazon SageMaker (use with any ML model)
2. Amazon Comprehend (for sentiment analysis)
- You don't need to have ML experience
- Use cases: fraud detection, ads targeting,
sentiment analysis, product recommendations


  

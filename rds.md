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


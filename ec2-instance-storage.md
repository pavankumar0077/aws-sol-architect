What's an EBS Volume? 
--
- An EBS (Elastic Block Store) Volume is a network drive you can attach
to your instances while they run
- It allows your instances to persist data, even after their termination
They can only be mounted to one instance at a time (at the CCP level
They are bound to a specific availability zone
- Analogy: Think of them as a "network USB stick"
- Free tier: 30 GB of free EBS storage of type General Purpose (SSD) or
Magnetic per month

- It's a network drive (i.e. not a physical drive)
- It uses the network to communicate the instance, which means there might be a bit of
latency
- It can be detached from an EC2 instance and attached to another one quickly
- It's locked to an Availability Zone (AZ)
- An EBS Volume in us-east-la cannot be attached to us-east-lb
- To move a volume across, you first need to snapshot it
- Have a provisioned capacity (size in GBs, and IOPS)
- You get billed for all the provisioned capacity
- You can increase the capacity of the drive over time.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/c97630c2-0e96-4a85-9869-4fcdb1270b28)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/1b52ab98-eaf9-4536-9be5-b24559a07d89)

REF LINK : https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html



EBS Snapshots
==

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/3528349b-0a5d-4c53-8745-e227ad2a61f4)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/a8a1e74a-976d-46ef-9d94-37dbf4f41a7c)





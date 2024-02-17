Private vs Public IP (IPv4)
--
Fundamental Differences
Public IP:
- Public IP means the machine can be identified on the internet (WWW)
- Must be unique across the whole web (not two machines can have the same public IP).
Can be geo-located easily
- Private IP:
Private IP means the machine can only be identified on a private network only
The IP must be unique across the private network
BUT two different private networks (two companies) can have the same IPs.
- Machines connect to WWW using an internet gateway (a proxy)
Only a specified range of IPs can be used as private IP

Elastic IP
--
With an Elastic IP address, you can mask the failure of an instance or software
by rapidly remapping the address to another instance in your account.
- You can only have 5 Elastic IP in your account (you can ask AWS to increase
that).
- Overall, try to avoid using Elastic IP:
They often reflect poor architectural decisions
- Instead, use a random public IP and register a DNS name to it
- Or, as we'll see later, use a Load Balancer and don't use a public IP.

Private vs Public IP (IPv4) In AWS EC2 - Hands On
--
- By default, your EC2 machine comes with:
A private IP for the internal AWS Network
A public IP, for the WWW.
- When we are doing SSH into our EC2 machines:
We can't use a private IP, because we are not in the same network
- We can only use the public IP.
- If your machine is stopped and then started,
the public IP can change

NOTE : ONLY PUBLIC IP WE CAN USE TO CONNECT TO THE INSTANCE, PRIVATE IP CAN BE USED IF WE ARE USING VPC AND THAT NETWORK IS DIFFERENT FROM PUBLIC IP.
- ONCE WE ARE IN THE INSTANCE WE CAN USE THE PRIVATE IP ADDRESS.
- EVERY TIME WHEN WE STOP AND START THE INSTANCE PUBLIC IP WILL CHANGE BUT PRIVATE IP WILL REMAIN SAME.
- ELASTIC IP's will get charged if we charged and not used then it will charged as soon as well created ELASTIC IP associate it to EC2 INSTANCE.
- only 5 elastic ip's per region.


Placement Groups
--
- Sometimes you want control over the EC2 Instance placement strategy
- That strategy can be defined using placement groups
- When you create a placement group, you specify one of the following
strategies for the group:
Cluster-clusters instances into a low-latency group in a single Availability Zone
- Spread spreads instances across underlying hardware (max 7 instances per
group per AZ) - critical applications
- Partition—spreads instances across many different partitions (which rely on
different sets of racks) within an AZ. Scales to 100s of EC2 instances per group
(Hadoop, Cassandra, Kafka)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/31e9b40f-9b48-4e1a-9898-504b15daee9d)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/6d51b147-402a-4216-845c-fdce279f3677)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e0573cd3-0a00-45b6-b0a9-b0939dc96107)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/025c086d-0393-4a93-871b-b3fe72861d49)

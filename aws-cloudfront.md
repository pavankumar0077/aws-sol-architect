# AWS CLOUDFRONT

- Content Delivery Network (CDN)
- Improves read performance, content
is cached at the edge
- Improves users experience
- 216 Point of Presence globally (edge
locations)
- DDoS protection (because
worldwide), integration with Shield,
AWS Web Application Firewall

CloudFront - Origins
--
- S3 bucket
- For distributing files and caching them at the edge
- Enhanced security with CloudFront Origin Access Control (OAC)
- OAC is replacing Origin Access Identity (OAI)
- CloudFront can be used as an ingress (to upload files to S3)
  
- Custom Origin (HTTP)
- Application Load Balancer
- EC2 instance
- S3 website (must first enable the bucket as a static S3 websit
- Any HTTP backend you want

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/11bc6856-9ac0-48d5-8115-d3c9245dd6ae)

CloudFront - S3 as an ORGIN
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/a7694f88-0ec6-469a-a8ca-b8e279ad9627)

CloudFront vs 53 Cross Region Replication
--
- **CloudFront:**
- Global Edge network
- Files are cached for a TTL (maybe a day)
- Great for static content that must be available everywhere
  
- **s3 Cross Region Replication:**
- Must be setup for each region you want replication to happen
- Files are updated in near real-time
- Read only
- Great for dynamic content that needs to be available at low-latency in few regions

CloudFront - ALB or EC2 as an Origin
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/cc6b8a33-2f42-4e83-ae27-1d8318aa8e1e)

CloudFront - Geo Restriction
--
- You can restrict who can access your distribution
- Allowlist: Allow your users to access your content only if they're in one of the
countries on a list of approved countries.
- Blocklist: Prevent your users from accessing your content if they're in one of the
countries on a list of banned countries.
- The "country" is determined using a 3rd party Geo-IP database
- Use case: Copyright Laws to control access to content

- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8db1546a-107d-4ea2-8baf-893a395b5f49)
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/c153de58-b938-46e7-8a2f-0cd763b686de)

CloudFront - Price Classes
--
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/951999c8-e929-48b6-beb6-64251da90a63)
- You can reduce the number of edge locations for cost reduction
- ** Three price classes:**
- Price Class All: all regions - best performance
- Price Class 200: most regions, but excludes the most expensive regions
- Price Class 100: only the least expensive regions

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/02d98a56-c463-45e8-9005-58fc3209d458)

CloudFront - Cache Invalidations
--

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/94ec4f5d-df50-4f17-b19a-75e5506e80f9)

- In case you update the back-end
origin, CloudFront doesn't know
about it and will only get the
refreshed content after the T TL has
expired
- However, you can force an entire or
partial cache refresh (thus bypassing
the TTL) by performing a Clou
Invalidation
- You can invalidate all files (*)
special path (/images/*)

AWS Global Accelerator 
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/412fbc0d-729d-403b-b121-3cb62ec70cf2)

- You have deployed an
application and have global
users who want to access it
directly.
- They go over the public
internet, which can add a lot of
latency due to many hal
AWS Global Acceleral
- We wish to go as fast a
possible through AWS
to minimize latency

Unicast IP vs Anycast IP
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b343cf1f-76bc-4d3a-9263-72f53f2651e6)

- Unicast IP: one server holds one IP
address
- Anycast IP: all servers hold the same
IP address and the client is routed to
the nearest one

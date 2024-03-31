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




CloudFront - S3 as an ORGIN
--

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
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/1911b19b-4c7a-41b0-bb35-2af688d4d7a3)

CloudFront - Geo Restriction
--
- You can restrict who can access your distribution
- Allowlist: Allow your users to access your content only if they're in one of the
countries on a list of approved countries.
- Blocklist: Prevent your users from accessing your content if they're in one of the
countries on a list of banned countries.
- The "country" is determined using a 3rd party Geo-IP database
- Use case: Copyright Laws to control access to content

- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b33e72a3-70e0-458b-8b63-7dd945bd0956)
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8178e167-8e03-4e19-8703-495cc720e6c6)


CloudFront - Price Classes
--
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/cbc0ea5d-1309-4354-9ebf-57294690e6e2)
- You can reduce the number of edge locations for cost reduction
- ** Three price classes:**
- Price Class All: all regions - best performance
- Price Class 200: most regions, but excludes the most expensive regions
- Price Class 100: only the least expensive regions

- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/bb64c6b0-1742-46b9-b6e3-05b7aa75a246)


CloudFront - Cache Invalidations
--

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/5a7f71af-d557-4bb1-96df-563f986a72be)

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
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/64646de1-a3e4-40e7-a963-dd401ebc3dcb)

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
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/3e335668-5d02-40d1-ab4a-6bdc1a5de24b)
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/a0fae62a-5477-46a5-9a18-02fd67d9e686)
- Unicast IP: one server holds one IP
address
- Anycast IP: all servers hold the same
IP address and the client is routed to
the nearest one

Aws Global Accelerator
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/81baf970-d39a-402b-8700-c1cc1aef39d7)

- Leverage the AWS internal
network to route to your
application
- 2 Anycast IP are created for your
application
- The Anycast IP send traffic directly
to Edge Locations
- The Edge locations send the traffic
to your application

- Works with Elastic IP, EC2 instances, ALB, NLB, public or private
- 
- **Consistent Performance**
- Intelligent routing to lowest latency and fast regional failover
- No issue with client cache (because the IP doesn't change)
- Internal AWS network
-
- **Health Checks**
- Global Accelerator performs a health check of your applications
- Helps make your application global (failover less than 1 minute for unhealthy)
- Great for disaster recovery (thanks to the health checks)
- 
- **Security**
- only 2 external IP need to be whitelisted
- DDoS protection thanks to AWS Shield

AWS Global Accelerator vs CloudFront
--
- They both use the AWS global network and its edge locations around the world
- Both services integrate with AWS Shield for DDoS protection.
- 
- **CloudFront**
- Improves performance for both cacheable content (such as images and videos)
- Dynamic content (such as API acceleration and dynamic site delivery)
- Content is served at the edge

- **Global Accelerator**
- Improves performance for a wide range of applications over TCP or UDP
- Proxying packets at the edge to applications running in one or more AWS Regions.-
- Good fit for non-HTTP use cases, such as gaming (UDP), loT (MQTT). or Voice over IP
- Good for HIP use cases that require static antic, st regional falover.

Hands on
--
- Crate 2 ec2 instances in 2 regions
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e5fad87d-3726-4c70-b780-5d23b9146bfd)
- Here Client affinity - is nothing but stickyness.
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/70ea1891-a848-4203-ade2-10cf54fe9eb2)
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/683c22d7-203e-4e2c-a4df-7550b1450ae1)
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/43d2fe07-d3ad-4e16-966a-7d39170e5d00)

- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/35e2a7d0-26d3-46b0-be70-970cf6358f49)
- NOW IF WE TRY TO REGION WHICH IS NEAR TO US-EAST-1 OR AP-SOUTH-1, IT WILL WORK WITH THE NEAREST REGION.
- IF HEALTH CHECK FAILS FROM ONE REGION THEN IT WILL WORKS WITH ANOTHER REGION.

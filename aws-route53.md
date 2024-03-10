![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ffdcabf3-1ce2-4330-afd7-50a5c840b067)What is DNS?
--
- Domain Name System which translates the human friendly hostnames
into the machine IP addresses
- www.google.com => 172.217.18.36
- DNS is the backbone of the Internet
- DNS uses hierarchical naming structure
```
.com
example.com
www.example.com
api.example.com
```
DNS Terminologies
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ac0cf77c-a574-4da1-8e6a-a77ff76148f3)

- Domain Registrar: Amazon Route 53, GoDaddy, ...
  1. DNS Records: A, AAAA, CNAME, NS, ...
  2. Zone File: contains DNS records
- Name Server: resolves DNS queries (Authoritative or Non-Authoritative)
-Top Level Domain (TLD): .com, .us, .in,.gov, .org, ...
- Second Level Domain (SLD): amazon.com, google.com, ...

How DNS Works
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/6c9a5e03-df29-4072-aa1e-274161d98dc3)

Amazon Route 53
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0af65f6a-b02e-4705-8910-3d96cd7e44fb)

- A highly available, scalable, fully
managed and Authoritative DNS
- Authoritative the customer (you)
can update the DNS records
- Route 53 is also a Domain Registrar
- Ability to check the health of your
resources
The only AWS service which
provides 100% availability SLA
- Why Route 53? 53 is a reference to
the traditional DNS port

Records
--
- How you want to route traffic for a domain
- Each record contains:
  1.Domain/subdomain Name - e.g., example.com
  2.Record Type-e.g., A or AAAA
  3.Value-e.g., 12.34.56.78
  4.Routing Policy - how Route 53 responds to queries
  5.TTL - amount of time the record cached at DNS Resolvers
- Route 53 supports the following DNS record types:
  1.(must know) A/AAAA/CNAME/NS
  2.(advanced) CAA/DS/MX/NAPTR/PTR/SOA/TXT/SPF/SRV

Route 53 - Record Types
--
- A-maps a hostname to IPv4
- AAAA - maps a hostname to IPv6
- CNAME - maps a hostname to another hostname
  1. The target is a domain name which must have an A or AAAA record
  2. Can't create a CNAME record for the top node of a DNS namespace (Zone
Apex)
  3. Example: you can't create for example.com, but you can create for
www.example.com
- NS-Name Servers for the Hosted Zone
   1.Control how traffic is routed for a domain

Route53 - Hosted Zones
--
- A container for records that define how to route traffic to a domain and
its subdomains
- Public Hosted Zones - contains records that specify how to route
traffic on the Internet (public domain names)
application I.mypublicdomain.com
- **Private Hosted Zones - contain records that specify how you route
traffic within one or more VPCs (private domain names)
application I.company.internal**
- You pay $0.50 per month per hosted zone
- 12 dollars per year.

Route53 - Public vs Priavate Hosted Zones.
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/9ae4116d-fbda-4a2f-98a1-0891beee16fd)

Route53 - Records TTL 
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/5dddbe8a-8074-4e8b-8402-02dc4b73d44f)

CNAME vs ALIAS
--

- AWS Resources (Load Balancer, CloudFront...) expose an AWS hostname:
- lbl-1234.us-east-2.elb.amazonaws.com and you want myapp.mydomain.com
- CNAME:
  1. Points a hostname to any other hostname. (app.mydomain.com => blabla.anything.com)
  2. ONLY FOR NON ROOT DOMAIN (aka. something.mydomain.com)
- Alias:
  1. Points a hostname to an AWS Resource (app.mydomain.com => blabla.amazonaws.com)
  2. Works for ROOT DOMAIN and NON ROOT DOMAIN (aka mydomain.com)
  3. Free of charge

Alias Records
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/570f109a-0190-4174-a593-c9154eb8c777)

- Maps a hostname to an AWS resource
- An extension to DNS functionality
- Automatically recognizes changes in the
resource's IP addresses
- Unlike CNAME, it can be used for the top node
of a DNS namespace (Zone Apex), e.g.:
example.com
- Alias Record is always of type A/AAAA for
AWS resources (IPv4/IPv6)
- You can not set the TTL.

Alias Records Targets
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/58c03f5b-1d3e-45d3-a7a8-815e37f312e1)

Routing Policies
--
- Define how Route 53 responds to DNS queries
- Don't get confused by the word "Routing"
- It's not the same as Load balancer routing which routes the traffic
- DNS does not route any traffic, it only responds to the DNS queries
- Route 53 Supports the following Routing Policies
  
  1. Simple
  
 ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/1922ab5d-a4b9-4859-b5e7-38fd6014c359)
 ```
    1. Typically, route traffic to a single
    resource
    2. Can specify multiple values in the
    same record
    3. If multiple values are returned, a
    random one is chosen by the client
    4. When Alias enabled, specify only
    one AWS resource
    5. Can't be associated with Health
    Checks
```
  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/fd1df143-cfa4-4822-aae0-69154ca94c6f)

  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d9431381-8a18-46fe-82f2-6aa1c272f7a3)

  ### NOTE : If we have multiple records then client i mean broswer will take the decision. 
  
  2. Weighted :
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/66a5fb93-0216-4234-bcf0-bd8c353e0253)

     First record
     --
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/97729aed-7465-4b98-af96-6a393f3f5873)

     Second record
     --
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/093596e8-85a7-4309-a994-9e2068cf06bf)

     Third record
     --
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d75c38fe-c957-4274-9035-3ff86d245d61)

     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/114dfdc7-d84b-42f2-b8f3-a1fd670e5ed9)

  3. Latency based
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ad89b03c-48fd-4fa5-9a7c-8b036678dad4)

     Record 1
     --
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/dbaa1790-9623-498e-a873-05aa2a006606)

     Record 2
     --
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/94a960a3-f9ca-4ebd-b264-416d96161cb0)

     Record 3
     --
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/83bd3068-ed55-4952-81c7-7bb0d4212cfa)

     
  4. Failover
     
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/9f82189f-5fa8-4e5e-be81-0043e6580d6b)

      Record 1
     --
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/2ce68fb6-5304-4bac-8b03-bd37386c1456)

      Record 2
     --
     ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/a8627c30-159e-4b1d-9453-02027a46eac3)
**When record 1 is failover with health checks then record 2 will be routed.**

     
  5. Geolocation

  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/40086be3-5e25-4dc8-92ee-0f6825698fb9)

- Different from Latency-based!
- This routing is based on user location
- Specify location by Continent, Country
or by US State (if there's overlapping,
most precise location selected)
- Should create a "Default" record (in
case there's no match on location)
- Use cases: website localization,
content distribution, load balar
- Can be associated with Health.

    Record 1
  --
  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/37c3bcf6-2b45-4536-a840-4e244c7fdb2a)

  Record 2
  --
  **Add another location**

  Record 3
  --
  **Default location**

  6. IP-Based Routing

  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/9966eeef-3f5b-475a-bd5d-ac8c57f9b40c)

- Routing is based on clients' IP addresses
- You provide a list of CIDRs for your clients
and the corresponding endpoints/locations
(user-IP-to-endpoint mappings)
- Use cases: Optimize performance, reduce
network costs...
- Example: route end users from a particular
ISP to a specific endpoint
  
  7. Multi-Value Answer

 - Use when routing traffic to multiple resources
- Route 53 return multiple values/resources
- Can be associated with Health Checks (return only values for healthy resources)
- Up to 8 healthy records are returned for each Multi-Value query
- Multi-Value is not a substitute for having an ELB

  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b4aaf96a-828e-454e-8681-727e93c22db0)

  **Add three records with multivalue anwser with different ip's**
  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b96d9b38-a12a-4d00-9d12-5ae9fca293c0)

  
  8. Geoproximity (using Route 53 Traffic Flow feature)
 
  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/5e3516dc-0d60-4b2f-aa2d-058b6112050c)

  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/4c5a553c-3200-484e-a6e5-67f0f1fa1f4c)

- Route traffic to your resources based on the geographic location of users and
resources
- Ability to shift more traffic to resources based on the defined bias
- To change the size of the geographic region, specify bias values:
- To expand (I to 99) - more traffic to the resource
- To shrink (-I to -99) - less traffic to the resource
- Resources can be:
- AWS resources (specify AWS region) |
- Non-AWS resources (specify Latitude and Longitude)
- You must use Route 53 Traffic Flow (advanced) to use this feature
  
Route53 - Health Checks
--

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/c83d8dc4-e9b7-46e2-8445-1521e6676685)

- HTTP Health Checks are only for public
resources
- Health Check => Automated DNS Failover:
  1. Health checks that monitor an endpoint
(application, server, other AWS resource)
  2. Health checks that monitor other health
checks (Calculated Health Checks)
  3.Health checks that monitor CloudWatch
Alarms (full control !!) - e,g., throttle
DynamoDB, alarms on RDS, custom
... (helpful for private resources)
- Health Checks are integrated with
metrics

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/fe14b703-b001-4bed-9bcf-7d7bf14a829f)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/27ea5560-00ed-431c-a936-8457757a6204)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0c962887-141e-41a4-bb9a-01128dc99cbb)

Health Checks
--
Route53 --> Health checks --> create health check 

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/a935a30c-fd65-4659-9c89-9ad0c96cdbeb)

**Check security group and give the required ports**
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e99758a6-1104-4cf7-97e0-e336ee07c4af)

**Monitor health check**
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8915caa9-59f8-4d32-81b0-dbaa95a05f9a)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/3c9423db-5827-4b43-94a7-ea55f4b13123)


3rd party domain
--

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f8220f61-79f6-4454-8cb1-ec6052e71713)

- You buy or register your domain name with a Domain Registrar typically by
paying annual charges (e.g, GoDaddy, Amazon Registrar Inc., ...)
- The Domain Registrar usually provides you with a DNS service to manage
your DNS records
- But you can use another DNS service to manage your DINS records
- Example: purchase the domain from GoDaddy and use Route 53 to manage
your DNS records.

**When you want to use Godaddy for domain and Route53 for DNS records management then we have to use Godaddy Name servers in the Route53 Name servers**

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0f29c4b2-06d5-44fa-8b96-8eff5c7d40af)

### 3rd Party Registrar with Amazon Route 53

- If you buy your domain on a 3rd party registrar, you can still use Route
53 as the DNS Service provider
  1. Create a Hosted Zone in Route 53
  2. Update NS Records on 3rd party website to use Route 53 Name
Servers
- Domain Registrar != DNS Service
- But every Domain Registrar usually comes with some DNS fel

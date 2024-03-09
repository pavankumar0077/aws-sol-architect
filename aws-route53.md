What is DNS?
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





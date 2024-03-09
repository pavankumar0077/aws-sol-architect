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



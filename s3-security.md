# Amazon S3 - Object Encryption

### Amazon S3 Encryption - SSE-S3

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/719dc3ff-4fc0-4a1d-b3ce-f217ac06758f)

- Encryption using keys handled, managed, and owned by AWS
- Object is encrypted server-side
- Encryption type is AES-256
- Must set header "X-amz-server-side-encryption": "AES256"
- Enabled by default for new buckets & new obiects.

### Amazon 53 Encryption - SSE-KMS

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/92973aae-adf5-45b3-92ae-8fac9d440187)

- Encryption using keys handled and managed by AWS KMS (Key Management Service)
- KMS advantages: user control + audit key usage using CloudTrail
- Object is encrypted server side
- Must set header "X-amz-server-side-encryption": "aws:kms"

### SSE-KMS Limitation

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/74761e61-36a8-4da4-a913-77016cbae59d)

- If you use SSE-KMS, you may be impacted
by the KMS limits
- When you upload, it calls the
GenerateDataKey KMS API
- When you download, it calls the Decrypt
KMS API
- Count towards the KMS quota per second
(5500, 10000, 30000 req/s based on region)
- You can request a quota increase using the
Service Quotas Console

### Amazon S3 Encryption - SSE-C

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/46c1b7d2-7b28-44ef-bea4-e5dfb9756b4c)

- Server-Side Encryption using keys fully managed by the customer outside of AWS
- Amazon S3 does NOT store the encryption key you provide
- HTTPS must be used
- Encryption key must provided in HTTP headers, for every HTTP request made

### Amazon S3 Encryption - Client-Side Encryption

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/29fd68a2-e853-4571-b87c-f76251346f26)

- Use client libraries such as Amazon S3 Client-Side Encryption Library
- Clients must encrypt data themselves before sending to Amazon 53
- Clients must decrypt data themselves when retrieving from Amazon S3
- Customer fully manages the keys and encryption cycle

### Amazon S3 - Encryption in transit (SSL/TLS)
- Encryption in flight is also called SSL/TLS
- Amazon S3 exposes two endpoints:
- HTTP Endpoint - non encrypted
- HTTPS Endpoint - encryption in flight
- HTTPS is recommended
- HTTPS is mandatory for SSE-C
- Most clients would use the HTTPS endpoint by default

### Amazon S3 - Force Encryption in Transit
### aws:Secure Transport

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/18a96d00-3219-4e2a-9460-16c3ca20bf84)

### S3 Encryption Hands-on

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ecd489c7-6fc5-43a7-b1ea-4ad10f44de26)

- Default encryption is SSE - S3
- We can modify the encryption after creation of the bucket as well.
- By default we have AWS KMS keys available -- If we create our own KMS keys charges will inccur every month.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/28e6bee4-b15c-4ea2-9afc-3fb26ba1c484)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/cbe324d1-e179-4c92-b209-27ecdcbc4394)

- If case we use SSE - KMS, Then we have Bucket key option available
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/eed59493-4c0b-4c2c-8b60-cf1017f9afa0)
- This is to reduce cost by doing less API calls to AWS KMS, This is enabled by default.
- If we use SSE-S3 the Bucket Key is Enabled by Default.

Amazon S3 - Default Encryption vs. Bucket Policies
--
- SSE-S3 encryption is automatically applied to new objects stored in 53 bucket
- Optionally, you can "force encryption" using a bucket policy and refuse any API Call to PUT an S3 object without encryption headers (SSE-KMS or SSE-C)
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/70a53297-1332-4ed9-8ec8-68536eb5f649)
- NOTE : BUCKET POLICIES ARE EVALUATED BEFORE "DEFAULT ENCRYPTION"

S3 CORS
--
What is CORS?
- Cross-Origin Resource Sharing (CORS)
- Origin = scheme (protocol) + host (domain) + port
- example: https://www.example.com (implied port is 443 for HTTPS, 80 for HTTP)
- Web Browser based mechanism to allow requests to other origins while
visiting the main origin
- Same origin: http://example.com/app| & http://example.com/app2
- Different origins: http://www.example.com & http://other.example.com
- The requests won't be fulfilled unless the other origin allows for the
requests, using CORS Headers (example: Access-Control-Allow-Origin)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e50108e0-0124-40e6-a93c-60dfaca591c8)

- If a client makes a cross-origin request on our S3 bucket, we need to enable
the correct CORS headers
- It's a popular exam question
- You can allow for a specific origin or for * (all origins)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/7d7cf77f-a71a-4e2c-a8ae-d8c8c8839bd0)


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

- To allow S3 bucket items to use from different resouces then we need to ALLOW CORS
```
[
    {
        "AllowedHeaders": [
            "Authorization"
        ],
        "AllowedMethods": [
            "GET"
        ],
        "AllowedOrigins": [
            "<url of first bucket with http://...without slash at the end>"
        ],
        "ExposeHeaders": [],
        "MaxAgeSeconds": 3000
    }
]
```

- we can use AllowedOrigins : * TO ALLOW ALL ORIGINS ( WEBISTES ), FOR PROD WE NEED TO USE ONLY KNOW HOSTS.

Amazon S3 - MFA Delete
--
- MFA (Multi-Factor Authentication) - force users to generate a code on a
device (usually a mobile phone or hardware) before doing important
operations on S3
- MFA will be required to:
- Permanently delete an object version
- Suspend Versioning on the bucket
- MFA won't be required to:
- Enable Versioning
- List deleted versions
- To use MFA Delete, Versioning must be enabled on the bucket
- Only the bucket owner (root account) can enable/disable MFA Delete

MFA HANDS ON
--
### NOTE : - We can enable MFA by using CLI as of now, That too from ROOT ACCOUNT
```
# generate root access keys
aws configure --profile root-mfa-delete-demo

# enable mfa delete
aws s3api put-bucket-versioning --bucket mfa-demo-stephane --versioning-configuration Status=Enabled,MFADelete=Enabled --mfa "arn-of-mfa-device mfa-code" --profile root-mfa-delete-demo

# disable mfa delete
aws s3api put-bucket-versioning --bucket mfa-demo-stephane --versioning-configuration Status=Enabled,MFADelete=Disabled --mfa "arn-of-mfa-device mfa-code" --profile root-mfa-delete-demo

# delete the root credentials in the IAM console!!!
```
S3 Access Logs
--
- For audit purpose, you may want to log all access to S3 buckets
- Any request made to S3, from any account, authorized or denied,
will be logged into another S3 bucket
- That data can be analyzed using data analysis tools...
- The target logging bucket must be in the same AWS region
- The log format is at:
https://docs.aws.amazon.com/AmazonS3/latest/dev/LogFormat.html

- Do not set your logging bucket to be the monitored bucket
- It will create a logging loop, and your bucket will grow exponentially

- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f9ad863a-940d-44c7-96b2-6e99672ff500)
- Here TARGET BUCKET FOR LOGGING SHOULD BE DIFFERNT FROM THE BUCKET WHAT WE ARE USING FOR S3 OBJECTS
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0a0107dd-a637-4ccc-bf45-8f6a4da0ae7f)
- access logs
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/571537f9-0fb0-4f64-bc3b-d67626fa110c)

Amazon S3 - Pre-Signed URLs
--

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/9aa760ef-2c28-4b7f-941b-4812fc61f3a4)

- Generate pre-signed URLs using the S3 Console, AWS CL or SDK
- URL Expiration
- S3 Console - I min up to 720 mins (12 hours)
- AWS CLI - configure expiration with -expires-in parameter in seconds (default 3600 secs, max. 604800 secs ~ 168 hours )
- Users given a pre-signed URL inherit the permissions of the user
that generated the ORL for GET / PUT
- Examples:
- Allow only logged-in users to download a premium video from y
bucket|
- Allow an ever-changing list of users to download files by generati
dynamically
- Allow temporarily a user to upload a file to a precise location in
your S3 bucket


Hands on
--
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d1ef5e7f-a350-4082-8ec2-475b99357566)
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/522ee8b7-1cb4-4831-8a63-216f4e26e1dd)

S3 Glacier Valut Lock
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/5ca3b6ef-1a53-4976-a41f-be876f224a2d)

- Adopt a WORM (Write Once Read
Many) model
- Create a Vault Lock Policy
- Lock the policy for future edits
(can no longer be changed or deleted)
- Helpful for compliance and data
retention.

S3 Object Lock (versioning must be enabled)
--
- Adopt a WORM (Write Once Read Many) model
- Block an object version deletion for a specified amount of time
- Retention mode - Compliance:
- Object versions can't be overwritten or deleted by any user, including the root user
- Objects retention modes can't be changed, and retention periods can't be shortened
- Retention mode - Governance:
- Most users can't overwrite or delete an object version or alter its lock settings
- Some users have special permissions to change the retention or delete the object.
- Retention Period: protect the object for a fixed period, it can be extended
- Legal Hold:
- protect the object indefinitely, independent from retention period
- can be freely placed and removed using the s3.PutObjectLegal-old IAM permissions

S3 Access Points
--

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e2d08ca0-b3b9-4cd8-ba38-abb7cb8c2321)

- Access Points simplify security management for S3 Bucket
- Each Access Point has:
- its own DNS name (Internet Origin or VPC Origin)
- an access point policy (similar to bucket policy) - manage security at scale

S3 - Access Points - VPC Origin
--

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b79f4113-9c20-4230-a7c8-0c203e594aa1)

- We can define the access
point to be accessible
only from within the VPC
- You must create a VPC
Endpoint to access the
Access Point (Gateway
or Interface Endpoint)
- The VPC Endpoint Policy
must allow access to the
target bucket and Access
Point

S3 Object Lambda
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/7b51b6bd-8221-483c-906c-4ff5525879b5)

- Use AWS Lambda Functions to
change the object before it is
retrieved by the caller application
- Only one 53 bucket is needed, on
top of which we create 53 Access
Point and S3 Object Lambda Access
Points.
- Use Cases:
- Redacting personally identifiable
nformation for analytics or non-
production environments.
as conting aM do a grats, such
- Resizing and watermarking images on
the fly using caller-specific details, such
as the user who requested the object.

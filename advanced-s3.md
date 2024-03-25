![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/db8069ca-d253-48c3-a4b0-1ebf3ba63c24)

Amazon S3 - Lifecycle Rules
--
- Transition Actions - configure objects to transition to another storage class
- Move objects to Standard IA class 60 days after creation
- Move to Glacier for archiving after 6 months
 
- Expiration actions - configure objects to expire (delete) after some time
- Access log files can be set to delete after a 365 days
- Can be used to delete old versions of files (if versioning is enabled)
- Can be used to delete incomplete Multi-Part uploads

1. Rules can be created for a certain prefix (example: 53://mybucket/m
2. Rules can be created for certain objects Tags (example: Department:Finance)

Amazon S3 - Lifecycle Rules (Scenario 1)
--
- Your application on EC2 creates images thumbnails after profile photos
are uploaded to Amazon S3. These thumbnails can be easily recreated,
and only need to be kept for 60 days. The source images should be able
to be immediately retrieved for these 60 days, and afterwards, the user
can wait up to 6 hours. How would you design this?
- 53 source images can be on Standard, with a lifecycle configurati
transition them to Glacier after 60 days
- $3 thumbnails can be on One-Zone IA, with a lifecycle configura
expire them (delete them) after 60 days


Amazon S3 - Lifecycle Rules (Scenario 2)
--
- A rule in your company states that you should be able to recover your
deleted S3 objects immediately for 30 days, although this may happen
rarely. After this time, and for up to 365 days, deleted objects should be
recoverable within 48 hours.
- Enable S3 Versioning in order to have object versions, so that "deleted
objects" are in fact hidden by a "delete marker" and can be recovered
- Transition the "noncurrent versions" of the object to Standard IA
- Transition afterwards the "noncurrent versions" to Glacier Deep Archive

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/79e06d06-50a9-4a49-ba10-051be1796309)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/129851ee-bc8b-4c56-9bbe-f932854a082c)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/bdf3cf87-7128-453f-919a-6e3bfc40ace5)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/e499177c-1278-4c93-bbb5-a0b80dba6d94)

S3 - Requester Pays
--

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/ef3c08d1-1a25-49ac-82e0-57c5ef9e0277)

- In general, bucket owners pay for all
Amazon 53 storage and data transfer
costs associated with their bucket
- With Requester Pays buckets, the
requester instead of the bucket owner
pays the cost of the request and the
data download from the bucket
- Helpful when you want to share large
datasets with other accounts
- The requester must be authenticated
in AWS (cannot be anonymous)

S3 Event Notifications
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8dbf16c6-d92f-428c-9b73-e991e6b1309d)

- S3:ObjectCreated, S3:ObjectRemoved,
S3: ObjectRestore, S3:Replication...
- Object name filtering possible (*jpg)
- Use case: generate thumbnails of images
uploaded to 53
- Can create as many "S3 events" as desired
- S3 event notifications typically deliver events
in seconds but can sometimes take a minute
or longer.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/fece866f-e881-4b04-a840-a4047a0843d6)

S3 Event Notifications with Amazon EventBridge
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/33b5b806-1c24-48f1-a243-f63e0e69db9a)

• Advanced filtering options with SON rules (metadata, object size, name...)
• Multiple Destinations - ex Step Functions, Kinesis Streams / Firehose...
• EventBridge Capabilities - Archive, Replay Events, Reliable delivery

S3 Event Notification
--
Bucket -- Properites 
- We have 2 options 1. Event notifications and 2. Amazon EventBridge

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/7278ac9e-b516-460b-a9cc-93323c51d6c8)

- Create notification
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/4f90f2e3-5666-4623-9af0-7f6e5f921405)
- Here when we click on create it show error, Be'coz we are not authenticated yet. For that we need to create a poliicy in the SQS queue.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0ef66605-d115-414a-8580-b60f80574bf3)
- Here we need to goto policy generator
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/df3d78ce-5035-4ecf-b367-a990d18dde53)
- Add statement and generate policy.
- Queue is created with default settings and policy changed.
```
{
  "Id": "Policy17113642393",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1711364242311",
      "Action": [
        "sqs:SendMessage"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:sqs:ap-south-1:account-number:DemoS3Notification",
      "Principal": "*"
    }
  ]
}
```

- Check send message in SQS
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/bb47b338-66fc-46b1-a5a2-b2ab3c5d4896)
- Click on poll message and click on message for testing.
- As soon as i uploaded an image in the S3, in SQS poll message i got a message like object is created.
- ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f5d5f3be-8eec-4095-9bb2-dd056aa445f4)

S3 - Baseline Performance
--
- Amazon S3 automatically scales to high request rates, latency 100-200 ms
- Your application can achieve at least 3,500 PUT/COPY/POST/DELETE or
5,500 GET/HEAD requests per second per prefix in a bucket.
- There are no limits to the number of prefixes in a bucket.
- Example (object path => prefix):
- bucket/folder |/sub I/file => /folder |/sub I/|
- bucket/folder |/sub2/file => /folder |/sub2/
- bucket/ I/file => /1/
- bucket/2/file => /2/
- If you spread reads across all four prefixes evenly, you can achieve 22,000
requests per second for GET and HEAD


S3 Performance
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d18ecfd0-5b24-4db5-8195-bd995f49506f)

### Multi-Part upload:
- recommended for files > 100MB,
must use for files > 5GB
- Can help parallelize uploads (speed
up transfers)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/fa7e78ac-242e-40ed-bbd3-77ba900c28bb)

### S3 Transfer Acceleration
- Increase transfer speed by transferring
file to an AWS edge location which will
forward the data to the S3 bucket in the
target region
- Compatible with multi-part upload.

# S3 Performance - S3 Byte-Range Fetches

- Parallelize GETs by requesting specific
byte ranges
- Better resilience in case of failures

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b88ff021-3b5c-4785-b222-76a3c97bb815)

# S3 Select & Glacier Select

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/51f074c7-2bd2-4737-849f-99311642cfe6)

- Retrieve less data using SQL by performing server-side filtering
- Can filter by rows & columns (simple SQL statements)
- Less network transfer, less CPU cost client-side

# S3 Batch Opertaions

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/7b8ba4b9-6dc5-452d-83a5-5488fad04de2)

- Perform bulk operations on existing S3 objects with a
single request, example:
- Modify object metadata & properties
- Copy objects between S3 buckets-
- Encrypt un-encrypted objects
- Modify ACLs, tags
- Restore objects from S3 Glacier
- Invoke Lambda function to perform custom action on
each object
- A job consists of a list of objects, the action to
perform, and optional parameters
- 53 Batch Operations manages retries, tracks progress,
sends completion notifications, generate reports ..
- You can use 53 Inventory to get object list and use S3
Select to filter your objects


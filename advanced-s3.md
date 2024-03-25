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



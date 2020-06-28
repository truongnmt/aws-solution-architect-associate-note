# S3, CloudFront, Snowball, Athena vs Macie

# S3 101

Simple Storage Service 

- Unlimited storage
- Object-based
    - from 0 bytes to 5 TB
    - Key - Value
    - Version ID
    - metadata (data about data we are storing)
    - Subresources
        - Access Control Lists
        - Torrent
    - store files, not suitable to install OS or database
    - Successful uploads will return 200 HTTP Status OK
- Stored in Buckets
- Universal namespace, names must be unique globally
- Control access to buckets using either a bucket ACL or using Bucket Policies

Data consistency work for S3:

- Read after Write consistency  for PUTS of new Object
- **Eventual Consistency** for overwrite PUTS and DELETES (can take some time to propagate), eventually get the newer version, just take a little bit of time to propagate.

Features

- Tiered Storage
- Lifecycle Management
- Versioning
- Encryption
- MFA for delete object
- Secure data using Access Control Lists and Bucket Policies

Classes

- Standard
- IA (Infrequently Accessed)
- One Zone - IA: IA but no multiple Availability Zone
- Intelligent Tiering: using AI automatically moving data to most cost-effective access tier
- Glacier: for archiving, retrieval time is configurable from minutes to hours
- Glacier Deep Archive: lowest-cost storage class where retrieval time of 12 hrs is acceptable

Charges

- Storage
- Requests
- Storage Management Pricing
- Data Transfer
- Transfer Acceleration
    - Enables fast, easy, secure transfers of files over long distances between your end users and an S3 bucket
    - Use Amazon CloudFront's globally distributed edge location

    ![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled.png)

- Cross Region Replication
    - Replicate bucket in another region

# Pricing tier

- S3 Intelligent Tiering
    - Same some money for infrequent access files
    - However it cost to monitoring files and automation (each 1000 objects) so keep that in mind

![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%201.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%201.png)

# Security and Encryption

By default, all newly created buckets are PRIVATE.

Can setup access control using:

- Access Control Lists (set policy up to object level)
- Bucket Policies (set policy for bucket level)

![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%202.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%202.png)

S3 can be configured to create access logs which log all requests made to the S3 bucket.
This can be sent to another bucket and even another bucket in another account

Encryption In Transit

- Go to https, the traffic is encrypted in transit, between your PC and server.
- SSL/TLS

Encryption At Rest (Server Side)

- S3 Managed Keys - SSE - S3: Amz manages all the keys
- AWS Key Management Service, Managed Keys - SSE - KMS
- Server Side Encryption with Customer Provided Keys - SSE - C

Client Side Encryption

- Encrypt the object then upload to S3

# Versioning

- Stores all versions of an object (including all writes and even if you delete an object)
    - Hide versioning and actions/delete →  only create a marker
    - Show versioning and actions/delete → Delete the delete marker will restore the object to latest version
    - Show versioning and actions/delete → Delete the individual version will delete that version
- Great backup tool
- Once enable, Versioning cannot be disabled, only suspended
    - Suspend will suspends the creation of object versions but preserves any existing object versions
- Integrates with Lifecycle rules
- MFA Delete capability
- After WRITE, permission will back to PRIVATE
- Size of the bucket is sum of all versions

# Lifecycle Management and Glacier

Create lifecycle rules to move things around different storage tier and eventually archive to Glacier or delete as well.

- Automates moving objects between the different storage tiers
- Can be used in conjunction with versioning
- Can be applied to current vers and previous vers

# AWS Organizations & Consolidated Billing

An account management service that enables you to consolidate multiple AWS accounts into an organization that you create an centrally manage.

![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%203.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%203.png)

## Consolidated Billing

- Paying account is independent.
- Cannot access resources of the other accounts
- All linked accounts are independent
- One bill per AWS account
- Easy to track charges and allocate costs
- Volumn pricing discount, the more you use the "less" you pay

![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%204.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%204.png)

Tips:

- Always enable MFA on root account
- Always user a strong and complex password on root account
- Paying account should be used for billing purposes only.
Do not deploy resources into the paying account
- Enable/Disable AWS services using Service Control Policies (SCP) either on Orgainzation Unit  or on individual accounts

# Sharing S3 Buckets Across Account

3 ways

- Using Bucket Policies & IAM (applices across the entire bucket). Progarammatic Access Only.
- Using Bucket ACLs & IAM (individual objects). Programmatic Access Only.
- Cross-account IAM Roles. Programatic AND Console access
    - Create new Role
    - Trusted entity: Another AWS Account
    - Add policy AmazonS3FullAccess the new Role

# Cross Region Replication

- Require versioning enabled on both the source and destination buckets
- Files in an exiting bucket are note replicated automatically
- All subsequent updated files will be replicated automatically
- Delete markers are not replicated
- Deleteing individual versions or delete markers will not be replicated

# S3 Transfer Acceleration

User CloudFront Edge Network to accleerate upload to S3.

Instead of uploading directly to S3 bucket, use a distince URL to upload directly to edge location which then transfer that file to S3

![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%205.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%205.png)

Speed Comparison Tool: 
[https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html](https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html)

# CloudFront

A CDN - system of distributed server - deliver content to user based on geographic locations of the user, the origin of the webpage and a content delivery server.

- Edge Location: location where content will be cached. This is separate to an AWS Region/AZ
- Origin: This is the origin of all files that CDN will distribute. This can be an S3 Bucket, EC2 instance, an Elastic Load Balancer or Route53
- Distribution: the name given the CDN which consists of a collection of Edge Locations
- Web Distribution: used for Website
- RTMP: use for media streaming
- Edge location are not just READ only - we can write to them too (ie: put an object on to them)
- Objects are cached for the life of the TTL (Time To Live)
- Can clear/invalidate cached objects, but we will be charged

![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%206.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%206.png)

AWS Edge locations

- Endpoints for AWS which are used for caching content
- Consists of CloudFront, CDN
- There are many more Edge location than Regions

Availability Zone (AZ) vs Edge Location

- A region is a physical location in the world which consists of two or more Availability Zones (AZ's)
- An AZ is one or more discrete data center, each with redundant power, networking and connectivity, housed in separate facilities
- Edge Location are endpoints for AWS for caching content, consists of CloudFront, Amazon CDN

Create a CloudFront Distributions

- Choose origin
- Distribution name

Eg: only paid user can access content

![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%207.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%207.png)

# Snowball

- Petabyte-scale **data transport** solution that use secure appliances to transfer large amounts of data into and out of AWS.
- Transfer data with Snowball is simple, fast, secure, and as little as 1/5 the cost of high-speed internet.
- 50TB or 80TB size
- Use multiple layers of security including tamper-resistant, 256-bit encryption and Trusted Platform Module (TPM)
- After the job done, it will be erased, can't be reused
- Snowball Edge 100TB data transfer device with onboard storage and compute capabilities (eg in the aircraft)
- Snowmobile is an Exabyte-scale data transfer service up to 100PB
- Import/Export to/from S3

# Storage Gateway

Service that connect an on-premise software appliance with cloud-based storage to provide integration between an organization's on premise IT environment and AWS's storage infrastructure.

AWS Storage Gateway's software appliance is available to download

3 different types of Storage Gateway

- File Gateway (NFS & SMB)
    - Files are stored as objects in S3 buckets

    ![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%208.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%208.png)

- Volume Gateway (iSCSI block protocol)
    - Store virtual hard disk drive in S3, it look like Amz EBS snapshots
    - Stored Volumes: store data locally, replicate that volume and async backup that data to AWS in the form of Elastic Block Store (EBS) snapshot
        - **Store the entire dataset**

    ![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%209.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%209.png)

    - Cached Volumes: use S3 as primary data storage, keep frequently accessed data locally in storage gateway.
        - Store data that you write to these volumes in S3 and keep recently read data in your on-premise storage gateway's cache and upload buffer storage
        - Entire dataset is stored on S3, cache the most actively used data

    ![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%2010.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%2010.png)

- Tape Gateway:
    - archive data in AWS Cloud
    - Virtual Tape Library interface let you store data on virtual tape cartridges that create

    ![S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%2011.png](S3%20CloudFront%20Snowball%20Athena%20vs%20Macie%20f715df5f96a1408e991469501b27a745/Untitled%2011.png)

# Athena vs Macie

## Athena

- Turn S3 into giant database, query using standard SQL
- Serverless, nothing to provision, pay per query / per TB scanned
- Works directly with data stored in S3
- Interactive query service

### Use cases

Can be used to query log stored in S3 eg: ELB logs, access logs..

Generate reports on data stored in S3

## Macie

What is PII (Personal Identifiable Information)

- Personal data use to identify individual
- This data could be use to identify criminal, financial fraud

Macie use ML and NLP to discover, classify and protect sensitive data stored in S3

- Use AI to recognize if S3 object contain sensitive data such as PII
- Dashboard, report, alert
- Can analyze CloudTrail logs for suspicious API activity
- Great for PCI-DSS compliance and preventing ID theft

Do read the S3 FAQs before taking exam.
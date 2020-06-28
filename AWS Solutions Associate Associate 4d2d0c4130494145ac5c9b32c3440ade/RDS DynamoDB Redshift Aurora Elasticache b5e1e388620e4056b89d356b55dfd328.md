# RDS, DynamoDB, Redshift, Aurora, Elasticache

RDS (OLTP): Sql server, oracle, mysql, postgres, aurora, mariadb

- Multi AZ: for disaster recovery
- Read Replicas: For performace

With multi AZ: Amz will auto switch to another replica when the other one down

- primary db has write → sync to 2nd database automatically
- can force a failover from one AZ to another by rebooting the RDS instance

![RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled.png](RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled.png)

With Read Replicas

- After Write, primary database will replicate to 2nd database.
- If failure, no auto switch
- manually update in EC2

![RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled%201.png](RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled%201.png)

- Scale out: up performance:
    - Read from replica, write in primary

## Data Warehousing

Used to pull very large and complex data sets, usually used by management to do queries on data

Use for business intelligence, tools like Cognos, Jaspersoft, ...

## OLTP vs OLAP

Different in terms of the types of queries you will run

Online Transaction Processing (OLTP)

- Eg: order number 2121212 pulls up a row of data such as Name, Date, Address ...

Online Analytic Processing (OLAP)

- Much more complex
- Pull large number of records for business analytic, strategy

→ Data Warehousing databases use different type of architecture both from database perspective and infrastructure layer

→ Redshift: Amazon's Data Warehouse Solution

Read Replicas

- Use for scaling, not for DR
- Must have automatic backups turned on in order to deploy a read replica
- have up to 5 read replica copies of any database
- can have read replicas of read replicas (but consider latency)
- each have its own DNS endpoint
- can have read replicas that have Multi-AZ
- can create read replicas of Multi-AZ source databases
- read replicas can be promoted to be their own databases. This breaks the replication
- can have a read replica in a separate region

## ElastiCache

Webservice for in-memory cache in the cloud

Supports 2 open source in memory caching engines

- Memcached
    - for scale horizontally
- Redis
    - multi-az
    - can do backup and restore of Redis

![RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled%202.png](RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled%202.png)

RDS runs on virtual machines

Can't ssh into RDS instance

 

RDS is NOT Serverless (with the exception Aurora)

# RDS - Backups, Multi-AZ & Read Replicas

2 types of backups

- Automated Backup
    - Allow to recover database to any point in time within a "retention period"
    - retention period: 1-35 days
    - take a full daily snapshot
    - store tx logs throughout the day
    - aws choose the mose recent daily backup, then apply transaction logs relevant to that day
    - enabled by default
    - backup data stored in s3
    - get free storage space equal to the size of ur database
    - backup are taken within a defined window
    - during backup, storage IO may be suspended → may got a bit latency
- Database Snapshots
    - done manually, eg: user initiated
    - stored even after you delete the original RDS instance, unlike automated backup

Restored version of the database will be a new RDS instance with a new DNS endpoint

![RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled%203.png](RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled%203.png)

Encryption at rest: supported for MySQL, Oracle, SQL Server, POstgres, Maria, Aurora

- By using AWS Key Management Service (KMS) service
- Once encrypted, data stored at reset  in the underlying storage is encrypted, backup, read replicas and snapshot are also encrypted to

(?)

RDS Reserved instances are available for multi-AZ deployments.

If I wanted to run a database on an EC2 instance, which of the following storage options would Amazon recommend?

- EBS

What data transfer charge is incurred when replicating data from your primary RDS instance to your secondary RDS instance?

- No charge associated with this action

If you are using Amazon RDS Provisioned IOPS storage with a Microsoft SQL Server database engine, what is the maximum size RDS volume you can have by default?

- 16TB

When you add a rule to an RDS DB security group, you must specify a port number or protocol.

- False

# DynamoDB

Amazon's NoSQL Solution

- Stored on SSD
- Spread across 3 geographically distinct data centers
- Eventual Consistent Reads (Default)
    - Consistency across all copies of data is usually reached within a second
    - Repeating a read after short time should return the updated data
    - If your app write to DynamoDB, then wait for more than 1seconds, 
    it will receive the updated data
- Strongly Consistent Reads
    - If your app write to DynamoDB and it need to read that change in less than 1 second
    - → use strongly consistent read
    - return result that reflects all writes that received a successful response prior to the read

# Redshift OLAP

Business intelligent or data warehouse in the cloud

PB scale, $1k/PB per year

Configuration

- Single Node (160Gb)
- Multi-Node
    - Leader Node (manages client connections and receives queries)
    - Compute Node (store data and perform queries and computations)
        - Up to 128 compute nodes

Advanced Compression

- Column data stores
- Use other techniques ..

Massively Parallel Processing (MPP)

- Automatically distributes data and query load across all nodes
- easy to add nodes (compute note?) to data warehouse (scale out)

Available in only 1 AZ

Backup

- Enable by default with 1-35 days retention
- always attempt to maintain at least three copies of your data
- the original and replica backup is in S3
- can async replicate snapshots to S3 in another region for DR

Pricing

- Compute Node Hours (total number of hours all computer nodes run)
    - billed for 1 unit per node per hour
    - 3 node running for a month = 3x24x30 =  2,160 instance hours
    - not charged for leader node hours
- Backup
- Data transfer (only within a VPC, not outside it)

# Security Considerations

Encrypted

- at rest using AES-256
- in transit using SSL

By default Redshift takes care of key management

- AWS KMS
- can manage your own keys through HSM

Availability

- only avail in 1 AZ
- can restore snapshots to new AZs in the event of an outage

# Aurora

A MySQL and PostgresSQL-compatible relational database engine + much more reliable

- 5x better performance than MySQL, 3x better than PostgreSQL
- Start with 10Gb scale in 10GB increment to 64TB
- Scale up to 32vCPUs and 244GB memory

2 copies of data is contained in each availability zone, with minimum of 3 availability zones → 6 copies of data

Can lose a couple of AZ but still not have issue on:

- write availability: loss up to 2 copies
- read availability: loss up to 3 copies

Auto self-healing

- continuously scanned for error and repaired automatically

3 types of Aurora Read Replicas, sit on top of normal Aurora database

- Aurora Replicas 15 can have, automated failover is available
- MySQL Read Replicas 5 ..
- PostgresQL 1 ..

![RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled%204.png](RDS%20DynamoDB%20Redshift%20Aurora%20Elasticache%20b5e1e388620e4056b89d356b55dfd328/Untitled%204.png)

Backup

- Automated backups are alway enabled, backups do not impact database performance
- can take snapshot with aurora, this does not impact on performance
- can share snapshot with other AWS account

MySQL → Aurora

- create Aurora Read Replica
- promote that database to standalone database

Can take snapshot of Aurora database, restore a new database from that snapshot

## Amazon Aurora Serverless

On-demand, auto-scalling

Automatically starts up, shuts down, scales capacity up or down based on application's need

For infrequent, intermittent, or unpredictable workloads

Different with RDS or EC2, pay for instance hours

Serverless pay per invocation basic
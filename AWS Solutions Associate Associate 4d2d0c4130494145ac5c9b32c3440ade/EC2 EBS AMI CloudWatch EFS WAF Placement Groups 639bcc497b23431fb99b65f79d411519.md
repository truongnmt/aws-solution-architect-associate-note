# EC2, EBS, AMI, CloudWatch, EFS, WAF, Placement Groups

Provides resizable compute capacity in the cloud

Virtual machine in the cloud, boot up and down in seconds. → Quickly scale up and down

Different with traditional hardware device, pay up front

Pay as you use, pay for what you use, pay less as you use more

Pricing models

- On demand: fixed rate by the hours, seconds
    - For: short term use, unpredictable workloads cannot be interrupted
    - User for the first time
- Reserved: capacity reservation, contract terms are 1-3 year
    - For: steady use, predictable usage
    - require reserved capacity
    - Standard Reserved Instance
    - Convertible Reserved Instance
    - Scheduled Reserved Instance
- Spot: when AWS has an ecceed resource, they drop the price. You can bid price you want to use, great saving if application have flexible start and end time
    - If terminated by EC2, you will not be charged for a partial hour of usage
    - If terminated by yourself, charged for any hour which instance ran
- Dedicated Hosts: physical EC2 server, can help reduce cost by allowing to use your existing server-bound software license
    - For: goverment, regulatory requirement
- **Termination Protection is turned off by default,** you must turn it on
- On an EBS-backed instance, the **default action is for the root EBS volume to be deleted** when the instance is terminated
- EBS Root volumes of default AMI's CAN be encrypted

# Security Groups

Change rules in security groups, it take effect immediately (eg: remote http port)

Delete all rules in Outbound, → still works, why?

- Security Groups is stateful, whenever create rule in Inbound, Outbound is create automatically
- In the setting, can't block port, IP address → use Network Access Control Lists
- All inbound traffic is blocked by default
- All outbound traffic is allowed
- EC2 instance - security group: N vs M

# EBS 101

Elastic Block Store, virtual disk in the cloud

Each EBS is automatically replicated within its AZ

- General Purpose (SSD)
- Provisioned IOPS (SSD)
- Throughput Optimised Hard Disk Drive
- Cold HDD
- Magnetic

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled.png)

EC2 instance is the same AZ with EBS volume

To move EC2 volume from one AZ to another AZ?

- Create snapshot: like a copy of a volume
- Use that snapshot to create an AMI
- Use that Image (in AMI) to provision EC2 Instance in another AZ

To move EC2 volume from one region to another

- Copy AMI to new region

Terminate EC2 instance 

- By default root volume will be deleted
- Additional volume that are attached to that instance will not be deleted, continue to persisted

Volumes exist on EBS

Snapshots exist on S3

Can create, changing size, performace EBS volume on the fly

First time create will be a bit long

- When save a second snapshot on the first one, it only add, update the changed block
- Snapshots are incremental

Can create AMI's from both volumes and snapshots

# AMI Types

EBS Volumes

- The root device is an Amazon EBS volume created from Amazon EBS snapshot

Instance Store Volumes:

- Ephemeral Storage
- Cannot be stopped, terminate only. Can lose data
- The root device is an instance store volume create from a template stored in Amz S3
- Both can reboot, not lose data
- Be default, both ROOT will be delete when termination. However with EBS volumes, can tell AWS to keep the root volume

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%201.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%201.png)

# ENI vs ENA vs EFA

ENI

- Elastic Network Interface - virtual network card
- Allow primary private address, mac address...
- For basic networking

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%202.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%202.png)

EN

- Enhanced Networking: use single root I/O virtualization provide high-perf networking capabilities
- Just a way of speeding your network essentially
- No additional charge for using but ec2 instance have to support
- Can be enabled using
    - ENA (Elastic Network Adapter): **up to 100 Gbps**
    - Intel 82599 Virtual Function (VF): up to 10 Gbps

    ![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%203.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%203.png)

Elastic Fabric Adapter

- Network device can attach to ec2 instance to accelerate High Performance Computing (HPC) and ML application
- low latency, OS-bypass, allow HPC and ML application to bypass the OS kernel and communicate directly with EFA device

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%204.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%204.png)

# Encrypted Root Device Volumes & Snapshots

Can encrypt when adding a storage

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%205.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%205.png)

To encrypting a root volume when create an instance without encryption

- Create snapshot of unencrypted volume
- Copy snapshot
- "Encrypt this snapshot"
- Create image
- Launch EC2 instance as encrypted root device

Snapshots of encrypted volumes are encrypted automatically

Volumes restored from encrypted snapshots are encrypted automatically

Can share snapshots, to other AWS accounts or made public, but only if they are unencrypted  

# CloudWatch

Monitoring services to monitor AWS resources, as well as the applications that you run on AWS

- Compute
    - EC2 instance
    - Autoscalling Groups
    - Elastic LB
    - Route53 health check
- Storeage & content delivery
    - EBS volumes
    - Storate Gateways
    - CloudFront

CloudWatch & EC2

Host level metrics consist of

- CPU
- entowrk
- disk
- status check

Monitor events every 5 mins by default

- Can have 1 mins intervals by turn on detailed monitoring

Can create alarms which trigger notification (billing alert..)

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%206.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%206.png)

Can create dashboards, dashboards can be global or regionouse

Can configure event, help you respond to state changes in ur AWS resources

Logs - aggregate, monitor and store logs

### AWS Cloud Trail

A CCTV for ur AWS environment

Increase visibility into your user and resources activity by recording AWS Console actions and API calls

Can identify which users and accounts called AWS, source IP address, when the calls were made

# Identity Access Management Roles

Roles are more secure than storing your access key and secret access key on individual EC2 instances

Roles are easier to manage

Roles can be assigned to an ec2 instance after it is create using both console & cmd line

Roles are universal - user in any region

# Using Boot Strap Scripts

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%207.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%207.png)

# Instance Metadata

```jsx
curl http://ip.ip.ip.ip/latest/user-data
```

The above bootstrap script

```jsx
curl http://ip.ip.ip.ip/latest/meta-data/local-ipv4
```

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%208.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%208.png)

- used to get information about instance
- curl metadata
- cur user-data

# Elastic File System

EFS file storage service for ec2 instance.

Similar to EBS, except EBS only mount to 1 ec2 instance

EFS can be shared between ec2 instances

On security group need to add NFS protocol to allow webserver to interact with file system

Support NFSv4 protocol

Mount EFS into EC2 instance:

![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%209.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%209.png)

Only pay for the storage you use (no pre-provisioning required)

Can support thousands of concurrent NFS connections

Data is stored across multiple AZ

Read after Write Consistency

# Amazon FSx for Windows & Amazon FSx for Lustre

Amazon FSx for Windows: 

- a windows file server that run Windows Server Message Block (SMB) based file services
- Designed for WIndows and Windows application
- Support AD users, ACL, groups, policies, DFS

EFS

- Managed NAS filer for EC2 instanced based on NFSv4
- file sharing protocols native to Unix and Linux

Amazon FSx for Lustre

- optimized for coputer-intensive workload, HPC, ML, electronic design automation (EDA)
- massive data sets at 100 Gb/s, millions of IOPS, sub millisecond latencies

# EC2 Placement Groups

A way of placing ec2 placement

3 types

- Clustered Placement Group
    - Grouping of instance within a single AZ
    - Just placing Ec2 instances close to each other so low latency, high network throughput
    - Can't span multiple AZ
- Spread
    - Group of instances that are each placed on distinct underlying hardware
    - Separate rack, power supply
    - Recommend for small number of individual critical instances that should be kept separate from each other
    - Can span multiple AZ but same region
    - can only have 7 running instances per AZ

    ![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%2010.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%2010.png)

- Partitioned
    - divides each group into logical segment called partitions
    - each partition has its own set of racks
    - each rack has its own network and power source
    - isolate impact of hardware failure
    - multiple ec2 instances HDFS, HBase, Cassandra

    ![EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%2011.png](EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519/Untitled%2011.png)

- name of placement group must be unique within aws account
- only certain type of instances can be launched in a placement group (compute optimized, GPU, memory optimize, storage optimized)
- AWS recommend the same instance type within clustered placement group
- can't merge placement groups
- can move an existing instance into placement group, before move, instance must be in stopped state, using AWS CLI or AWS SDK, can do by console yet

Cannot delete a snapshot of root EBS volume

Can attach an EBS volume to more than one EC2 instance at the same time

[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes.html)

A specific type of EC2 can ⚠️

# AWS WAF

Web application firewall, monitor HTTP and HTTPS request that are forwarded to CloudFront, LB or API Gateway

Application level firewall, sit in layer 7 in OSI model

Configure conditions such as what IP addresses, country, values in request headers, string from regex, length request, SQL injection, XSS 

- allow all requests except the ones you specify
- block all requests except the ones you specify
- count the requests that match the properties you specify
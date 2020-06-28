# Test 2

![../VPCs%208e0201fd87d1492792363303ed4fc337/Untitled%201.png](../VPCs%208e0201fd87d1492792363303ed4fc337/Untitled%201.png)

![https://d1.awsstatic.com/security-center/NewSharedResponsibilityModel.749924fb27d7c6de5cd59376dbaab323f86ce5dd.png](https://d1.awsstatic.com/security-center/NewSharedResponsibilityModel.749924fb27d7c6de5cd59376dbaab323f86ce5dd.png)

[EC2, EBS, AMI, CloudWatch, EFS, WAF, Placement Groups](../EC2%20EBS%20AMI%20CloudWatch%20EFS%20WAF%20Placement%20Groups%20639bcc497b23431fb99b65f79d411519.md)

![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-01-19_22-34-15-d1fd30e8eaa8701ddd964e5878e78242.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-01-19_22-34-15-d1fd30e8eaa8701ddd964e5878e78242.png)

![https://udemy-images.s3.amazonaws.com/redactor/raw/2020-02-16_11-15-22-2595be662f78560da845fae54e4f2aca.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2020-02-16_11-15-22-2595be662f78560da845fae54e4f2aca.png)

Security Groups usually control the list of ports that are allowed to be used by your EC2 instances and the NACLs control which network or list of IP addresses can connect to your whole VPC.

By default, security group has no inbound rules, block all inbound rule, includes an outbound rule that allow all outbound traffic.
By default, Network ACL allows **all** inbound and outbound IPv4 traffic

Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover

Here is a list of important information about EBS Volumes:

- When you create an EBS volume in an Availability Zone, it is automatically replicated within that zone to prevent data loss due to a failure of any single hardware component.

- An EBS volume can only be attached to one EC2 instance at a time.

- After you create a volume, you can attach it to any EC2 instance in the same Availability Zone

- An EBS volume is off-instance storage that can persist independently from the life of an instance. You can specify not to terminate the EBS volume when you terminate the EC2 instance during instance creation.

- EBS volumes support live configuration changes while in production which means that you can modify the volume type, volume size, and IOPS capacity without service interruptions.

- Amazon EBS encryption uses 256-bit Advanced Encryption Standard algorithms (AES-256)

- EBS Volumes offer 99.999% SLA.

By default, instances that you launch into a virtual private cloud (VPC) can't communicate with your own network. You can enable access to your network from your VPC by attaching a virtual private gateway to the VPC, creating a custom route table, updating your security group rules, and creating an AWS managed VPN connection.

![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-27_22-45-01-dbcb3de60063eaba73e8d2d12c61d6dc.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-27_22-45-01-dbcb3de60063eaba73e8d2d12c61d6dc.png)

---

**You are instructed by your manager to set up a bastion host in your Amazon VPC and it should only be accessed from the corporate data center via SSH. What is the best way for you to achieve this?**

- ​Create a small EC2 instance with a security group which only allows access on port 22 using your own pre-configured password.
- ​Create a small EC2 instance with a security group which only allows access on port 22 via the IP address of the corporate data center. Use a private key (.pem) file to connect to the bastion host.
- ​Create a large EC2 instance with a security group which only allows access on port 22 using your own pre-configured password.
- ​Create a large EC2 instance with a security group which only allows access on port 22 via the IP address of the corporate data center. Use a private key (.pem) file to connect to the bastion host.
- Answer

    The best way to implement a bastion host is to create a small EC2 instance which should only have a security group from a particular IP address for maximum security. This will block any SSH Brute Force attacks on your bastion host. It is also recommended to use a small instance rather than a large one because this host will only act as a jump server to connect to other instances in your VPC and nothing else.

    ![https://docs.aws.amazon.com/quickstart/latest/linux-bastion/images/linux-bastion-hosts-on-aws-architecture.png](https://docs.aws.amazon.com/quickstart/latest/linux-bastion/images/linux-bastion-hosts-on-aws-architecture.png)

    Therefore, there is no point of allocating a large instance simply because it doesn't need that much computing power to process SSH (port 22) or RDP (port 3389) connections. It is possible to use SSH with an ordinary user ID and a pre-configured password as credentials but it is more secure to use public key pairs for SSH authentication for better security.

    Hence, the right answer for this scenario is the option that says: **Create a small EC2 instance with a security group which only allows access on port 22 via the IP address of the corporate data center. Use a private key (.pem) file to connect to the bastion host**.

    **Creating a large EC2 instance with a security group which only allows access on port 22 using your own pre-configured password** and **creating a small EC2 instance with a security group which only allows access on port 22 using your own pre-configured password** are incorrect because even though you have your own pre-configured password, the SSH connection can still be accessed by anyone over the Internet, which poses as a security vulnerability.

    The option that says: **Create a large EC2 instance with a security group which only allows access on port 22 via the IP address of the corporate data center. Use a private key (.pem) file to connect to the bastion host** is incorrect because you don't need a large instance for a bastion host as it does not require much CPU resources.

⭐️

**A corporate and investment bank has recently decided to adopt a hybrid cloud architecture for their Trade Finance web application which uses an Oracle database with Oracle Real Application Clusters (RAC) configuration. Since Oracle RAC is not supported in RDS, they decided to launch their database in a large On-Demand EC2 instance instead, with multiple EBS Volumes attached. As a Solutions Architect, you are responsible to ensure the security, availability, scalability, and disaster recovery of the whole architecture.In this scenario, which of the following will enable you to take backups of your EBS volumes that are being used by the Oracle database?**

- ​Create snapshots of the EBS Volumes.
- ​Launch the EBS Volumes to a Placement Group which will automatically back up your data.
- ​Use Disk Mirroring, which is also known as RAID 1, that replicates data to two or more disks/EBS Volumes.
- ​EBS-backed EC2 instances.
- Answer

    **Creating snapshots of the EBS Volumes** is correct. You can back up the data on your Amazon EBS volumes to Amazon S3 by taking point-in-time snapshots. Snapshots are *incremental* backups, which means that only the blocks on the device that have changed after your most recent snapshot are saved.

    ![https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/snapshot_1b.png](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/snapshot_1b.png)

    This minimizes the time required to create the snapshot and saves on storage costs by not duplicating data. When you delete a snapshot, only the data unique to that snapshot is removed. Each snapshot contains all of the information needed to restore your data (from the moment the snapshot was taken) to a new EBS volume.

    **EBS-backed EC2 instances** is incorrect since running an EBS-backed EC2 instance does not relate to your problem as you are already running a few of them in the first place.

    **Using Disk Mirroring, which is also known as RAID 1, that replicates data to two or more disks/EBS Volumes** is incorrect. Disk mirroring is not an efficient and cost-optimized solution for your problem. You should use EBS snapshots instead.

    **Launching the EBS Volumes to a Placement Group which will automatically back up your data** is incorrect. A placement group is a logical grouping of instances within a single Availability Zone (AZ) that allows low-latency communication between instances. Hence, this is not an efficient way to back up data.

**You have set up a VPC with public subnet and an Internet gateway. You set up an EC2 instance with a public IP as well. However, you are still not able to connect to the instance via the Internet. You checked its associated security group and it seems okay.What should you do to ensure you can connect to the EC2 instance from the Internet?**

- ​Check the CloudWatch logs as there must be some issue in the EC2 instance.
- ​Set a Secondary Private IP Address to the EC2 instance.
- ​Check the main route table and ensure that the right route entry to the Internet Gateway (IGW) is configured.
- ​Set an Elastic IP Address to the EC2 instance.
- Answer

    The route table entries enable EC2 instances in the subnet to use IPv4 to communicate with other instances in the VPC, and to communicate directly over the Internet. A subnet that's associated with a route table that has a route to an Internet gateway is known as a public subnet.

    If you could not connect to your EC2 instance even if there is already an Internet Gateway in your VPC and there is no issue in the security group, then you must check if the entries in the route table are properly configured.

    **Setting an Elastic IP Address to the EC2 instance** is incorrect since you already have a public IP address for your EC2 instance, and doesn't require an EIP anymore.

    **Setting a Secondary Private IP Address to the EC2 instance** is incorrect because having a secondary private IP address is only used within the VPC, not when connecting to the outside Internet.

    **Checking the CloudWatch logs as there must be some issue in the EC2 instance** is incorrect because it is better to go through your setup and make sure that you didn't miss a step, such as adding a route in the route table, before you check the actual CloudWatch logs to see if an instance has an issue.

**You run a website which accepts high-quality photos and turns them into a downloadable video montage. The website offers a free account and a premium account that guarantees faster processing. All requests by both free and premium members go through a single SQS queue and then processed by a group of EC2 instances which generate the videos. You need to ensure that the premium users who paid for the service have higher priority than your free members. How do you re-design your architecture to address this requirement?**

- ​Use Amazon Kinesis to process the photos and generate the video montage in real time.
- ​For the requests made by premium members, set a higher priority in the SQS queue so it will be processed first compared to the requests made by free members.
- ​Create an SQS queue for free members and another one for premium members. Configure your EC2 instances to consume messages from the premium queue first and if it is empty, poll from the free members' SQS queue.
- ​Use Amazon S3 to store and process the photos and then generate the video montage afterwards.
- Answer

    In this scenario, it is best to create 2 separate SQS queues for each type of members. The SQS queues for the premium members can be polled first by the EC2 Instances and once completed, the messages from the free members can be processed next.

    The option that says: **For the requests made by premium members, set a higher priority in the SQS queue so it will be processed first compared to the requests made by free members** is incorrect as you cannot set a priority to individual items in the SQS queue.

    **Using Amazon Kinesis to process the photos and generate the video montage in real time** is incorrect as Amazon Kinesis is used to process streaming data and it is not applicable in this scenario.

    **Using Amazon S3 to store and process the photos and then generating the video montage afterwards** is incorrect as Amazon S3 is used for durable storage and not for processing data.

⭐️

**An accounting application uses an RDS database configured with Multi-AZ deployments to improve availability. What would happen to RDS if the primary database instance fails?**

- ​The canonical name record (CNAME) is switched from the primary to standby instance.
- ​The IP address of the primary DB instance is switched to the standby DB instance.
- ​A new database instance is created in the standby Availability Zone.
- ​The primary database instance will reboot.

### **Explanation**

- Answer

    In Amazon RDS, failover is automatically handled so that you can resume database operations as quickly as possible without administrative intervention in the event that your primary database instance went down. When failing over, Amazon RDS simply flips the canonical name record (CNAME) for your DB instance to point at the standby, which is in turn promoted to become the new primary.

    ![https://d1nqddva888cns.cloudfront.net/rds_ha_5.png](https://d1nqddva888cns.cloudfront.net/rds_ha_5.png)

    The option that says: ***The IP address of the primary DB instance is switched to the standby DB instance*** is incorrect since IP addresses are per subnet, and subnets cannot span multiple AZs.

    The option that says: ***The primary database instance will reboot*** is incorrect since in the event of a failure, there is no database to reboot with.

    The option that says: ***A new database instance is created in the standby Availability Zone*** is incorrect since with multi-AZ enabled, you already have a standby database in another AZ.

⭐️

**A media company has two VPCs: VPC-1 and VPC-2 with peering connection between each other. VPC-1 only contains private subnets while VPC-2 only contains public subnets. The company uses a single AWS Direct Connect connection and a virtual interface to connect their on-premises network with VPC-1.Which of the following options increase the fault tolerance of the connection to VPC-1? (Select TWO.)**

- [ ]  ​Establish another AWS Direct Connect connection and private virtual interface in the same AWS region as VPC-1.
- [ ]  ​Establish a hardware VPN over the Internet between VPC-1 and the on-premises network.
- [ ]  ​Establish a hardware VPN over the Internet between VPC-2 and the on-premises network.
- [ ]  ​Establish a new AWS Direct Connect connection and private virtual interface in the same region as VPC-2.
- [ ]  ​Use the AWS VPN CloudHub to create a new AWS Direct Connect connection and private virtual interface in the same region as VPC-2.

### **Explanation**

- Answer

    In this scenario, you have two VPCs which have peering connections with each other. Note that a VPC peering connection does not support edge to edge routing. This means that if either VPC in a peering relationship has one of the following connections, you cannot extend the peering relationship to that connection:

    - A VPN connection or an AWS Direct Connect connection to a corporate network

    - An Internet connection through an Internet gateway

    - An Internet connection in a private subnet through a NAT device

    - A gateway VPC endpoint to an AWS service; for example, an endpoint to Amazon S3.

    - (IPv6) A ClassicLink connection. You can enable IPv4 communication between a linked EC2-Classic instance and instances in a VPC on the other side of a VPC peering connection. However, IPv6 is not supported in EC2-Classic, so you cannot extend this connection for IPv6 communication.

    ![https://docs.aws.amazon.com/vpc/latest/peering/images/edge-to-edge-vpn-diagram.png](https://docs.aws.amazon.com/vpc/latest/peering/images/edge-to-edge-vpn-diagram.png)

    For example, if VPC A and VPC B are peered, and VPC A has any of these connections, then instances in VPC B cannot use the connection to access resources on the other side of the connection. Similarly, resources on the other side of a connection cannot use the connection to access VPC B.

    Hence, this means that you cannot use VPC-2 to extend the peering relationship that exists between VPC-1 and the on-premises network. For example, traffic from the corporate network can't directly access VPC-1 by using the VPN connection or the AWS Direct Connect connection to VPC-2, which is why the following options are incorrect:

    ***- Use the AWS VPN CloudHub to create a new AWS Direct Connect connection and private virtual interface in the same region as VPC-2.***

    ***- Establish a hardware VPN over the Internet between VPC-2 and the on-premises network.***

    ***- Establish a new AWS Direct Connect connection and private virtual interface in the same region as VPC-2.***

    You can do the following to provide a highly available, fault-tolerant network connection:

    ***- Establish a hardware VPN over the Internet between the VPC and the on-premises network.***

    ***- Establish another AWS Direct Connect connection and private virtual interface in the same AWS region.***

**You developed a web application and deployed it on a fleet of EC2 instances, which is using Amazon SQS. The requests are saved as messages in the SQS queue which is configured with the maximum message retention period. However, after thirteen days of operation, the web application suddenly crashed and there are 10,000 unprocessed messages that are still waiting in the queue. Since you developed the application, you can easily resolve the issue but you need to send a communication to the users on the issue. What information will you provide and what will happen to the unprocessed messages?**

- ​Tell the users that the application will be operational shortly and all received requests will be processed after the web application is restarted.
- ​Tell the users that unfortunately, they have to resubmit all of the requests since the queue would not be able to process the 10,000 messages together.
- ​Tell the users that unfortunately, they have to resubmit all the requests again.
- ​Tell the users that the application will be operational shortly however, requests sent over three days ago will need to be resubmitted.

### **Explanation**

- Answer

    In this scenario, it is stated that the SQS queue is configured with the maximum message retention period. The maximum message retention in SQS is 14 days that is why the option that says: **Tell the users that the application will be operational shortly and all received requests will be processed after the web application is restarted** is the correct answer i.e. there will be no missing messages.

    The options that say: **Tell the users that unfortunately, they have to resubmit all the requests again** and **Tell the users that the application will be operational shortly, however, requests sent over three days ago will need to be resubmitted** are incorrect as there are no missing messages in the queue thus, there is no need to resubmit any previous requests.

    The option that says: **Tell the users that unfortunately, they have to resubmit all of the requests since the queue would not be able to process the 10,000 messages together** is incorrect as the queue can contain an unlimited number of messages, not just 10,000 messages.

    In Amazon SQS, you can configure the message retention period to a value from 1 minute to 14 days. The default is 4 days. Once the message retention limit is reached, your messages are automatically deleted.

    A single Amazon SQS message queue can contain an unlimited number of messages. However, there is a 120,000 limit for the number of inflight messages for a standard queue and 20,000 for a FIFO queue. Messages are inflight after they have been received from the queue by a consuming component, but have not yet been deleted from the queue.

⭐️

**You are a Solutions Architect of a media company and you are instructed to migrate an on-premises web application architecture to AWS. During your design process, you have to give consideration to current on-premises security and determine which security attributes you are responsible for on AWS.Which of the following does AWS provide for you as part of the shared responsibility model?**

- ​User access to the AWS environment
- ​Instance security
- ​Customer Data
- ​Physical network infrastructure

### **Explanation**

- Answer

    Security and Compliance is a shared responsibility between AWS and the customer. This shared model can help relieve customer’s operational burden as AWS operates, manages and controls the components from the host operating system and virtualization layer down to the physical security of the facilities in which the service operates. The customer assumes responsibility and management of the guest operating system (including updates and security patches), other associated application software as well as the configuration of the AWS provided security group firewall.

    Customers should carefully consider the services they choose as their responsibilities vary depending on the services used, the integration of those services into their IT environment, and applicable laws and regulations. The nature of this shared responsibility also provides the flexibility and customer control that permits the deployment. As shown in the chart below, this differentiation of responsibility is commonly referred to as Security “of” the Cloud versus Security “in” the Cloud.

    **Customer Data** is incorrect since providing you customer data would be a breach in security protocols and data privacy laws.

    **Instance security** is incorrect because it is your responsibility to set up the security tools AWS has provided you to secure your instances in your cloud environment.

    **User access to the AWS environment** is incorrect since it is your responsibility to delegate user access to your cloud environment.

    Refer to this diagram for a better understanding of the shared responsibility model.

    ![https://d1.awsstatic.com/security-center/NewSharedResponsibilityModel.749924fb27d7c6de5cd59376dbaab323f86ce5dd.png](https://d1.awsstatic.com/security-center/NewSharedResponsibilityModel.749924fb27d7c6de5cd59376dbaab323f86ce5dd.png)

⭐️

**A software company has resources hosted in AWS and on-premises servers. You have been requested to create a decoupled architecture for applications which make use of both resources.Which of the following options are valid? (Select TWO.)**

- [ ]  ​Use SQS to utilize both on-premises servers and EC2 instances for your decoupled application
- [ ]  ​Use Amazon Simple Decoupling Service to utilize both on-premises servers and EC2 instances for your decoupled application
- [ ]  ​Use DynamoDB to utilize both on-premises servers and EC2 instances for your decoupled application
- [ ]  ​Use SWF to utilize both on-premises servers and EC2 instances for your decoupled application
- [ ]  ​Use RDS to utilize both on-premises servers and EC2 instances for your decoupled application

### **Explanation**

- Answer

    **Amazon Simple Queue Service (SQS)** and **Amazon Simple Workflow Service (SWF)** are the services that you can use for creating a decoupled architecture in AWS. **Decoupled architecture is a type of computing architecture that enables computing components or layers to execute independently while still interfacing with each other.**

    Amazon SQS offers reliable, highly-scalable hosted queues for storing messages while they travel between applications or microservices. Amazon SQS lets you move data between distributed application components and helps you decouple these components. Amazon SWF is a web service that makes it easy to coordinate work across distributed application components.

    **Using RDS to utilize both on-premises servers and EC2 instances for your decoupled application** and **using DynamoDB to utilize both on-premises servers and EC2 instances for your decoupled application** are incorrect as RDS and DynamoDB are database services.

    **Using Amazon Simple Decoupling Service to utilize both on-premises servers and EC2 instances for your decoupled application** is incorrect because there is no such thing as Amazon Simple Decoupling Service.

⭐️

**You are an AWS Network Engineer working for a utility provider where you are managing a monolithic application with an EC2 instance using a Windows AMI. The legacy application must maintain the same private IP address and MAC address in order for it to work. You want to implement a cost-effective and highly available architecture for your application by launching a standby EC2 instance that is an exact replica of the Windows server. If the primary instance terminates, you can attach the ENI to the standby secondary instance, which allows the traffic flow to resume within a few seconds.When it comes to the ENI attachment to an EC2 instance, what does 'warm attach' refer to?**

- ​Attaching an ENI to an instance when it is idle.
- ​Attaching an ENI to an instance during the launch process.
- ​Attaching an ENI to an instance when it is running.
- ​Attaching an ENI to an instance when it is stopped.

### **Explanation**

- Answer

    You can create a network interface, attach it to an instance, detach it from an instance, and attach it to another instance. The attributes of a network interface follow it as it's attached or detached from an instance and reattached to another instance. When you move a network interface from one instance to another, network traffic is redirected to the new instance.

    If one of your instances serving a particular function fails, its network interface can be attached to a replacement or hot standby instance pre-configured for the same role in order to rapidly recover the service. For example, you can use a network interface as your primary or secondary network interface to a critical service such as a database instance or a NAT instance.

    ![https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/EC2_ENI_management_network.png](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/EC2_ENI_management_network.png)

    If the instance fails, you (or more likely, the code running on your behalf) can attach the network interface to a hot standby instance. Because the interface maintains its private IP addresses, Elastic IP addresses, and MAC address, network traffic begins flowing to the standby instance as soon as you attach the network interface to the replacement instance. Users experience a brief loss of connectivity between the time the instance fails and the time that the network interface is attached to the standby instance, but no changes to the VPC route table or your DNS server are required.

    An elastic network interface (ENI) is a logical networking component in a VPC that represents a virtual network card. You can attach a network interface to an EC2 instance in the following ways:

    **When it's running (hot attach)**

    **When it's stopped (warm attach)**

    **When the instance is being launched (cold attach).**

    Therefore, **attaching an ENI to an instance when it is stopped** is the correct answer.

    **Attaching an ENI to an instance during the launch process** is incorrect because this describes a "cold attach" scenario.

    **Attaching an ENI to an instance when it is running** is incorrect because this describes a "hot attach" scenario.

    **Attaching an ENI to an instance when it is idle** is incorrect because there is no specific name for attaching an ENI to an idle EC2 instance.

⭐️

**You are a Solutions Architect of a multi-national gaming company which develops video games for PS4, Xbox One and Nintendo Switch consoles, plus a number of mobile games for Android and iOS. Due to the wide range of their products and services, you proposed that they use API Gateway. What are the key features of API Gateway that you can tell your client? (Select TWO.)**

- [ ]  ​It automatically provides a query language for your APIs similar to GraphQL.
- [ ]  ​Provides you with static anycast IP addresses that serve as a fixed entry point to your applications hosted in one or more AWS Regions.
- [ ]  ​You pay only for the API calls you receive and the amount of data transferred out.
- [ ]  ​Enables you to run applications requiring high levels of inter-node communications at scale on AWS through its custom-built operating system (OS) bypass hardware interface.
- [ ]  ​Enables you to build RESTful APIs and WebSocket APIs that are optimized for serverless workloads.

### **Explanation**

- Answer

    **Amazon API Gateway** is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale. With a few clicks in the AWS Management Console, you can create an API that acts as a “front door” for applications to access data, business logic, or functionality from your back-end services, such as workloads running on Amazon Elastic Compute Cloud (Amazon EC2), code running on AWS Lambda, or any web application. Since it can use AWS Lambda, you can run your APIs without servers.

    ![https://d1.awsstatic.com/serverless/Serverless%20Migration/Serverlesswebapp.45052e1feb8f1748d96a678311d73434599095b1.png](https://d1.awsstatic.com/serverless/Serverless%20Migration/Serverlesswebapp.45052e1feb8f1748d96a678311d73434599095b1.png)

    Amazon API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, authorization and access control, monitoring, and API version management. Amazon API Gateway has no minimum fees or startup costs. You pay only for the API calls you receive and the amount of data transferred out.

    Hence, the correct answers are:

    ***- Enables you to build RESTful APIs and WebSocket APIs that are optimized for serverless workloads***

    ***- You pay only for the API calls you receive and the amount of data transferred out.***

    The option that says: ***It automatically provides a query language for your APIs similar to GraphQL*** is incorrect because this is not provided by API Gateway.

    The option that says: ***Provides you with static anycast IP addresses that serve as a fixed entry point to your applications hosted in one or more AWS Regions*** is incorrect because this is a capability of AWS Global Accelerator and not API Gateway.

    The option that says: ***Enables you to run applications requiring high levels of inter-node communications at scale on AWS through its custom-built operating system (OS) bypass hardware interface*** is incorrect because this is a capability of Elastic Fabric Adapter and not API Gateway.

⭐️

**You are working for a commercial bank as an AWS Infrastructure Engineer handling the forex trading application of the bank. You have an Auto Scaling group of EC2 instances that allow your company to cope up with the current demand of traffic and achieve cost-efficiency. You want the Auto Scaling group to behave in such a way that it will follow a predefined set of parameters before it scales down the number of EC2 instances, which protects your system from unintended slowdown or unavailability. Which of the following statements are true regarding the cooldown period? (Select TWO.)**

- [ ]  ​It ensures that the Auto Scaling group does not launch or terminate additional EC2 instances before the previous scaling activity takes effect.
- [ ]  ​It ensures that before the Auto Scaling group scales out, the EC2 instances have an ample time to cooldown.
- [ ]  ​It ensures that the Auto Scaling group launches or terminates additional EC2 instances without any downtime.
- [ ]  ​Its default value is 300 seconds.
- [ ]  ​Its default value is 600 seconds.

### **Explanation**

- Answer

    In Auto Scaling, the following statements are correct regarding the cooldown period:

    It ensures that the Auto Scaling group does not launch or terminate additional EC2 instances before the previous scaling activity takes effect.

    Its default value is 300 seconds.

    It is a configurable setting for your Auto Scaling group.

    The following options are incorrect:

    **- It ensures that before the Auto Scaling group scales out, the EC2 instances have an ample time to cooldown.**

    **- It ensures that the Auto Scaling group launches or terminates additional EC2 instances without any downtime.**

    **- Its default value is 600 seconds.**

    These statements are inaccurate and don't depict what the word "cooldown" actually means for Auto Scaling. The cooldown period is a configurable setting for your Auto Scaling group that helps to ensure that it doesn't launch or terminate additional instances before the previous scaling activity takes effect. After the Auto Scaling group dynamically scales using a simple scaling policy, it waits for the cooldown period to complete before resuming scaling activities.

    The figure below demonstrates the scaling cooldown:

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-23_05-13-47-8ff2ec72179862c346ba76ede3994182.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-23_05-13-47-8ff2ec72179862c346ba76ede3994182.png)

⭐️

**You have a static corporate website hosted in a standard S3 bucket and a new web domain name which was registered using Route 53. You are instructed by your manager to integrate these two services in order to successfully launch their corporate website.What are the prerequisites when routing traffic using Amazon Route 53 to a website that is hosted in an Amazon S3 Bucket? (Select TWO.)**

- [ ]  ​The S3 bucket name must be the same as the domain name
- [ ]  ​A registered domain name
- [ ]  ​The Cross-Origin Resource Sharing (CORS) option should be enabled in the S3 bucket
- [ ]  ​The S3 bucket must be in the same region as the hosted zone
- [ ]  ​The record set must be of type "MX"

### **Explanation**

- Answer

    Here are the prerequisites for routing traffic to a website that is hosted in an Amazon S3 Bucket:

    - An S3 bucket that is configured to host a static website. The bucket must have the same name as your domain or subdomain. For example, if you want to use the subdomain portal.tutorialsdojo.com, the name of the bucket must be portal.tutorialsdojo.com.

    - A registered domain name. You can use Route 53 as your domain registrar, or you can use a different registrar.

    - Route 53 as the DNS service for the domain. If you register your domain name by using Route 53, we automatically configure Route 53 as the DNS service for the domain.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-02-13_01-03-54-a79dccacb816c6b4a8da3bd3ac9c2ce6.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-02-13_01-03-54-a79dccacb816c6b4a8da3bd3ac9c2ce6.png)

    The option that says: **The record set must be of type "MX"** is incorrect since an MX record specifies the mail server responsible for accepting email messages on behalf of a domain name. This is not what is being asked by the question.

    The option that says: **The S3 bucket must be in the same region as the hosted zone** is incorrect. There is no constraint that the S3 bucket must be in the same region as the hosted zone, in order for the Route 53 service to route traffic into it.

    The option that says: **The Cross-Origin Resource Sharing (CORS) option should be enabled in the S3 bucket** is incorrect because you only need to enable Cross-Origin Resource Sharing (CORS) when your client web application on one domain interacts with the resources in a different domain.

**A start-up company has an EC2 instance that is hosting a web application. The volume of users is expected to grow in the coming months and hence, you need to add more elasticity and scalability in your AWS architecture to cope with the demand. Which of the following options can satisfy the above requirement for the given scenario? (Select TWO.)**

- [ ]  ​Set up an S3 Cache in front of the EC2 instance.
- [ ]  ​Set up two EC2 instances and then put them behind an Elastic Load balancer (ELB).
- [ ]  ​Set up two EC2 instances deployed using Launch Templates and integrated with AWS Glue.
- [ ]  ​Set up two EC2 instances and use Route 53 to route traffic based on a Weighted Routing Policy.
- [ ]  ​Set up an AWS WAF behind your EC2 Instance.

### **Explanation**

- Answer

    Using an Elastic Load Balancer is an ideal solution for adding elasticity to your application. Alternatively, you can also create a policy in Route 53, such as a Weighted routing policy, to evenly distribute the traffic to 2 or more EC2 instances. Hence, **setting up two EC2 instances and then put them behind an Elastic Load balancer (ELB)** and **setting up two EC2 instances and using Route 53 to route traffic based on a Weighted Routing Policy** are the correct answers.

    ![https://docs.aws.amazon.com/govcloud-us/latest/ug-west/images/r53-cf-elb.png](https://docs.aws.amazon.com/govcloud-us/latest/ug-west/images/r53-cf-elb.png)

    **Setting up an S3 Cache in front of the EC2 instance** is incorrect because doing so does not provide elasticity and scalability to your EC2 instances.

    **Setting up an AWS WAF behind your EC2 Instance** is incorrect because AWS WAF is a web application firewall that helps protect your web applications from common web exploits. This service is more on providing security to your applications.

    **Setting up two EC2 instances deployed using Launch Templates and integrated with AWS Glue** is incorrect because AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics. It does not provide scalability or elasticity to your instances.

⭐️

**A media company is setting up an ECS batch architecture for its image processing application. It will be hosted in an Amazon ECS Cluster with two ECS tasks that will handle image uploads from the users and image processing. The first ECS task will process the user requests, store the image in an S3 input bucket, and push a message to a queue. The second task reads from the queue, parses the message containing the object name, and then downloads the object. Once the image is processed and transformed, it will upload the objects to the S3 output bucket. To complete the architecture, the Solutions Architect must create a queue and the necessary IAM permissions for the ECS tasks.Which of the following should the Architect do next?**

- ​Launch a new Amazon MQ queue and configure the second ECS task to read from it. Create an IAM role that the ECS tasks can assume in order to get access to the S3 buckets and Amazon MQ queue. Set the (`EnableTaskIAMRole`) option to true in the task definition.
- ​Launch a new Amazon Kinesis Data Firehose and configure the second ECS task to read from it. Create an IAM role that the ECS tasks can assume in order to get access to the S3 buckets and Kinesis Data Firehose. Specify the ARN of the IAM Role in the (`taskDefinitionArn`) field of the task definition.
- ​Launch a new Amazon SQS queue and configure the second ECS task to read from it. Create an IAM role that the ECS tasks can assume in order to get access to the S3 buckets and SQS queue. Declare the IAM Role (`taskRoleArn`) in the task definition.
- ​Launch a new Amazon AppStream 2.0 queue and configure the second ECS task to read from it. Create an IAM role that the ECS tasks can assume in order to get access to the S3 buckets and AppStream 2.0 queue. Declare the IAM Role (`taskRoleArn`) in the task definition.

### **Explanation**

- Answer

    Docker containers are particularly suited for batch job workloads. Batch jobs are often short-lived and embarrassingly parallel. You can package your batch processing application into a Docker image so that you can deploy it anywhere, such as in an Amazon ECS task.

    Amazon ECS supports batch jobs. You can use Amazon ECS *Run Task* action to run one or more tasks once. The Run Task action starts the ECS task on an instance that meets the task’s requirements including CPU, memory, and ports.

    ![https://github.com/aws-samples/ecs-refarch-batch-processing/raw/master/images/ECSBatchRefArch.png](https://github.com/aws-samples/ecs-refarch-batch-processing/raw/master/images/ECSBatchRefArch.png)

    For example, you can set up an ECS Batch architecture for an image processing application. You can set up an AWS CloudFormation template that creates an Amazon S3 bucket, an Amazon SQS queue, an Amazon CloudWatch alarm, an ECS cluster, and an ECS task definition. Objects uploaded to the input S3 bucket trigger an event that sends object details to the SQS queue. The ECS task deploys a Docker container that reads from that queue, parses the message containing the object name and then downloads the object. Once transformed it will upload the objects to the S3 output bucket.

    By using the SQS queue as the location for all object details, you can take advantage of its scalability and reliability as the queue will automatically scale based on the incoming messages and message retention can be configured. The ECS Cluster will then be able to scale services up or down based on the number of messages in the queue.

    You have to create an IAM Role that the ECS task assumes in order to get access to the S3 buckets and SQS queue. Note that the permissions of the IAM role don't specify the S3 bucket ARN for the incoming bucket. This is to avoid a circular dependency issue in the CloudFormation template. You should always make sure to assign the least amount of privileges needed to an IAM role.

    Hence, the correct answer is: ***Launch a new Amazon SQS queue and configure the second ECS task to read from it. Create an IAM role that the ECS tasks can assume in order to get access to the S3 buckets and SQS queue. Declare the IAM Role (`taskRoleArn`) in the task definition.***

    The option that says: ***Launch a new Amazon AppStream 2.0 queue and configure the second ECS task to read from it. Create an IAM role that the ECS tasks can assume in order to get access to the S3 buckets and AppStream 2.0 queue. Declare the IAM Role (`taskRoleArn`) in the task definition*** is incorrect because Amazon AppStream 2.0 is a fully managed application streaming service and can't be used as a queue. You have to use Amazon SQS instead.

    The option that says: ***Launch a new Amazon Kinesis Data Firehose and configure the second ECS task to read from it. Create an IAM role that the ECS tasks can assume in order to get access to the S3 buckets and Kinesis Data Firehose. Specify the ARN of the IAM Role in the (`taskDefinitionArn`) field of the task definition*** is incorrect because Amazon Kinesis Data Firehose is a fully managed service for delivering real-time streaming data. Although it can stream data to an S3 bucket, it is not suitable to be used as a queue for a batch application in this scenario. In addition, the ARN of the IAM Role should be declared in the `taskRoleArn` and not in the `taskDefinitionArn` field.

    The option that says: ***Launch a new Amazon MQ queue and configure the second ECS task to read from it. Create an IAM role that the ECS tasks can assume in order to get access to the S3 buckets and Amazon MQ queue. Set the (`EnableTaskIAMRole`) option to true in the task definition*** is incorrect because Amazon MQ is primarily used as a managed message broker service and not a queue. The `EnableTaskIAMRole` option is only applicable for Windows-based ECS Tasks that require extra configuration.

**You are building a cloud infrastructure where you have EC2 instances that require access to various AWS services such as S3 and Redshift. You will also need to provision access to system administrators so they can deploy and test their changes.Which configuration should be used to ensure that the access to your resources are secured and not compromised? (Select TWO.)**

- [ ]  ​Assign an IAM role to the Amazon EC2 instance.
- [ ]  ​Store the AWS Access Keys in the EC2 instance.
- [ ]  ​Enable Multi-Factor Authentication.
- [ ]  ​Store the AWS Access Keys in ACM.
- [ ]  ​Assign an IAM user for each Amazon EC2 Instance.

### **Explanation**

- Answer

    In this scenario, the correct answers are:

    **- Enable Multi-Factor Authentication**

    **- Assign an IAM role to the Amazon EC2 instance**

    **Always remember that you should associate IAM roles to EC2 instances and not an IAM user**, for the purpose of accessing other AWS services. IAM roles are designed so that your applications can securely make API requests from your instances, without requiring you to manage the security credentials that the applications use. Instead of creating and distributing your AWS credentials, you can delegate permission to make API requests using IAM roles.

    ![https://dmhnzl5mp9mj6.cloudfront.net/security_awsblog/images/MFAAPI4.png](https://dmhnzl5mp9mj6.cloudfront.net/security_awsblog/images/MFAAPI4.png)

    AWS Multi-Factor Authentication (MFA) is a simple best practice that adds an extra layer of protection on top of your user name and password. With MFA enabled, when a user signs in to an AWS website, they will be prompted for their user name and password (the first factor—what they know), as well as for an authentication code from their AWS MFA device (the second factor—what they have). Taken together, these multiple factors provide increased security for your AWS account settings and resources. You can enable MFA for your AWS account and for individual IAM users you have created under your account. MFA can also be used to control access to AWS service APIs.

    **Storing the AWS Access Keys in the EC2 instance** is incorrect because this is not recommended by AWS, as it can be compromised. Instead of storing access keys on an EC2 instance for use by applications that run on the instance and make AWS API requests, you can use an IAM role to provide temporary access keys for these applications.

    **Assigning an IAM user for each Amazon EC2 Instance** is incorrect because there is no need to create an IAM user for this scenario since IAM roles already provide greater flexibility and easier management.

    **Storing the AWS Access Keys in ACM** is incorrect because ACM is just a service that lets you easily provision, manage, and deploy public and private SSL/TLS certificates for use with AWS services and your internal connected resources. It is not used as a secure storage for your access keys.

**You have two On-Demand EC2 instances inside your Virtual Private Cloud in the same Availability Zone but are deployed to different subnets. One EC2 instance is running a database and the other EC2 instance a web application that connects with the database. You want to ensure that these two instances can communicate with each other for your system to work properly.What are the things you have to check so that these EC2 instances can communicate inside the VPC? (Select TWO.)**

- [ ]  ​Check if all security groups are set to allow the application host to communicate to the database on the right port and protocol.
- [ ]  ​Check if both instances are the same instance class.
- [ ]  ​Ensure that the EC2 instances are in the same Placement Group.
- [ ]  ​Check the Network ACL if it allows communication between the two subnets.
- [ ]  ​Check if the default route is set to a NAT instance or Internet Gateway (IGW) for them to communicate.

### **Explanation**

- Answer

    First, the Network ACL should be properly set to allow communication between the two subnets. The security group should also be properly configured so that your web server can communicate with the database server. Hence, these are the correct answers:

    **Check if all security groups are set to allow the application host to communicate to the database on the right port and protocol.**

    **Check the Network ACL if it allows communication between the two subnets.**

    The option that says: **Check if both instances are the same instance class** is incorrect because the EC2 instances do not need to be of the same class in order to communicate with each other.

    The option that says: **Check if the default route is set to a NAT instance or Internet Gateway (IGW) for them to communicate** is incorrect because an Internet gateway is primarily used to communicate to the Internet.

    The option that says: **Ensure that the EC2 instances are in the same Placement Group** is incorrect because Placement Group is mainly used to provide low-latency network performance necessary for tightly-coupled node-to-node communication.

**A company has a requirement to move 80 TB data warehouse to the cloud. It would take 2 months to transfer the data given their current bandwidth allocation.Which is the most cost-effective service that would allow you to quickly upload their data into AWS?**

- ​AWS Snowball Edge
- ​AWS Direct Connect
- ​Amazon S3 Multipart Upload
- ​AWS Snowmobile

### **Explanation**

- Answer

    **AWS Snowball Edge** is a type of Snowball device with on-board storage and compute power for select AWS capabilities. Snowball Edge can undertake local processing and edge-computing workloads in addition to transferring data between your local environment and the AWS Cloud.

    Each Snowball Edge device can transport data at speeds faster than the internet. This transport is done by shipping the data in the appliances through a regional carrier. The appliances are rugged shipping containers, complete with E Ink shipping labels. The AWS Snowball Edge device differs from the standard Snowball because it can bring the power of the AWS Cloud to your on-premises location, with local storage and compute functionality.

    Snowball Edge devices have three options for device configurations – storage optimized, compute optimized, and with GPU.

    ![https://docs.aws.amazon.com/snowball/latest/ug/images/SnowballEdgeAppliance.png](https://docs.aws.amazon.com/snowball/latest/ug/images/SnowballEdgeAppliance.png)

    Hence, the correct answer is: **AWS Snowball Edge.**

    **AWS Snowmobile** is incorrect because this is an Exabyte-scale data transfer service used to move extremely large amounts of data to AWS. It is not suitable for transferring a small amount of data, like 80 TB in this scenario. You can transfer up to 100PB per Snowmobile, a 45-foot long ruggedized shipping container, pulled by a semi-trailer truck. A more cost-effective solution here is to order a Snowball Edge device instead.

    **AWS Direct Connect** is incorrect because it is primarily used to establish a dedicated network connection from your premises network to AWS. This is not suitable for one-time data transfer tasks, like what is depicted in the scenario.

    **Amazon S3 Multipart Upload** is incorrect because this feature simply enables you to upload large objects in multiple parts. It still uses the same Internet connection of the company, which means that the transfer will still take time due to its current bandwidth allocation.

**As a Network Architect developing a food ordering application, you need to retrieve the instance ID, public keys, and public IP address of the EC2 server you made for tagging and grouping the attributes into your internal application running on-premises.Which EC2 feature will help you achieve your requirements?**

- ​Resource tags
- ​Amazon Machine Image
- ​Instance metadata
- ​Instance user data

### **Explanation**

- Answer

    Instance metadata is the data about your instance that you can use to configure or manage the running instance. You can get the instance ID, public keys, public IP address and many other information from the instance metadata by firing a URL command in your instance to this URL:

    http://169.254.169.254/latest/meta-data/

    ![https://docs.aws.amazon.com/IAM/latest/UserGuide/images/roles-usingrole-ec2roleinstance.png](https://docs.aws.amazon.com/IAM/latest/UserGuide/images/roles-usingrole-ec2roleinstance.png)

    **Instance user data** is incorrect because this is mainly used to perform common automated configuration tasks and run scripts after the instance starts.

    **Resource tags** is incorrect because these are labels that you assign to an AWS resource. Each tag consists of a key and an optional value, both of which you define.

    **Amazon Machine Image** is incorrect because this mainly provides the information required to launch an instance, which is a virtual server in the cloud.

⭐️

**You have a cryptocurrency exchange portal which is hosted in an Auto Scaling group of EC2 instances behind an Application Load Balancer, and are deployed across multiple AWS regions. Your users can be found all around the globe, but the majority are from Japan and Sweden. Because of the compliance requirements in these two locations, you want your Japanese users to connect to the servers in the `ap-northeast-1` Asia Pacific (Tokyo) region, while your Swedish users should be connected to the servers in the `eu-west-1` EU (Ireland) region.Which of the following services would allow you to easily fulfill this requirement?**

- ​Set up an Application Load Balancers that will automatically route the traffic to the proper AWS region.
- ​Use Route 53 Weighted Routing policy.
- ​Set up a new CloudFront web distribution with the geo-restriction feature enabled.
- ​Use Route 53 Geolocation Routing policy.

### **Explanation**

- Answer

    Geolocation routing lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from. For example, you might want all queries from Europe to be routed to an ELB load balancer in the Frankfurt region.

    When you use geolocation routing, you can localize your content and present some or all of your website in the language of your users. You can also use geolocation routing to restrict distribution of content to only the locations in which you have distribution rights. Another possible use is for balancing load across endpoints in a predictable, easy-to-manage way, so that each user location is consistently routed to the same endpoint.

    ![https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/how-route-53-routes-traffic.png](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/how-route-53-routes-traffic.png)

    **Setting up an Application Load Balancers that will automatically route the traffic to the proper AWS region** is incorrect because Elastic Load Balancers distribute traffic among EC2 instances across multiple Availability Zones but not across AWS regions.

    **Setting up a new CloudFront web distribution with the geo-restriction feature enabled** is incorrect because the CloudFront geo-restriction feature is primarily used to prevent users in specific geographic locations from accessing content that you're distributing through a CloudFront web distribution. It does not let you choose the resources that serve your traffic based on the geographic location of your users, unlike the Geolocation routing policy in Route 53.

    **Using Route 53 Weighted Routing policy** is incorrect because this is not a suitable solution to meet the requirements of this scenario. It just lets you associate multiple resources with a single domain name (tutorialsdojo.com) or subdomain name (forums.tutorialsdojo.com) and choose how much traffic is routed to each resource. You have to use a Geolocation routing policy instead.

**You are helping out a new DevOps Engineer to design her first architecture in AWS. She is planning to develop a highly available and fault-tolerant architecture which is composed of an Elastic Load Balancer and an Auto Scaling group of EC2 instances deployed across multiple Availability Zones. This will be used by an online accounting application which requires path-based routing, host-based routing, and bi-directional communication channels using WebSockets.Which is the most suitable type of Elastic Load Balancer that you should recommend for her to use?**

- ​Application Load Balancer
- ​Network Load Balancer
- ​Either a Classic Load Balancer or a Network Load Balancer
- ​Classic Load Balancer

### **Explanation**

- Answer

    Elastic Load Balancing supports three types of load balancers. You can select the appropriate load balancer based on your application needs.

    If you need flexible application management and TLS termination then we recommend that you use Application Load Balancer. If extreme performance and static IP is needed for your application then we recommend that you use Network Load Balancer. If your application is built within the EC2 Classic network then you should use Classic Load Balancer.

    An Application Load Balancer functions at the application layer, the seventh layer of the Open Systems Interconnection (OSI) model. After the load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply, and then selects a target from the target group for the rule action. You can configure listener rules to route requests to different target groups based on the content of the application traffic. Routing is performed independently for each target group, even when a target is registered with multiple target groups.

    ![https://docs.aws.amazon.com/elasticloadbalancing/latest/application/images/redirect_path.png](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/images/redirect_path.png)

    Application Load Balancers support path-based routing, host-based routing and support for containerized applications hence, **Application Load Balancer** is the correct answer.

    **Network Load Balancer**, **Classic Load Balancer**, and **either a Classic Load Balancer or a Network Load Balancer** are all incorrect as none of these support path-based routing and host-based routing, unlike an Application Load Balancer.

⭐️

**A company is planning to launch an application which requires a data warehouse that will be used for their infrequently accessed data. You need to use an EBS Volume that can handle large, sequential I/O operations.Which of the following is the most cost-effective storage type that you should use to meet the requirement?**

- ​EBS General Purpose SSD (gp2)
- ​Cold HDD (sc1)
- ​Provisioned IOPS SSD (io1)
- ​Throughput Optimized HDD (st1)

### **Explanation**

- Answer

    Cold HDD volumes provide low-cost magnetic storage that defines performance in terms of throughput rather than IOPS. With a lower throughput limit than Throughput Optimized HDD, this is a good fit ideal for large, sequential cold-data workloads. If you require infrequent access to your data and are looking to save costs, Cold HDD provides inexpensive block storage. Take note that bootable Cold HDD volumes are not supported.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-12-17_12-12-20-ce9961d8c4466dd46d97bc76a7004fb6.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-12-17_12-12-20-ce9961d8c4466dd46d97bc76a7004fb6.png)

    Cold HDD provides the lowest cost HDD volume and is designed for less frequently accessed workloads. Hence, **Cold HDD (sc1)** is the correct answer.

    In the exam, always consider the difference between SSD and HDD as shown on the table below. This will allow you to easily eliminate specific EBS-types in the options which are not SSD or not HDD, depending on whether the question asks for a storage type which has ***small, random*** I/O operations or ***large, sequential*** I/O operations.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-01-19_22-34-15-d1fd30e8eaa8701ddd964e5878e78242.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-01-19_22-34-15-d1fd30e8eaa8701ddd964e5878e78242.png)

    **EBS General Purpose SSD (gp2)** is incorrect because a General purpose SSD volume costs more and it is mainly used for a wide variety of workloads. It is recommended to be used as system boot volumes, virtual desktops, low-latency interactive apps, and many more.

    **Provisioned IOPS SSD (io1)** is incorrect because this costs more than Cold HDD and thus, not cost-effective for this scenario. It provides the highest performance SSD volume for mission-critical low-latency or high-throughput workloads, which is not needed in the scenario.

    **Throughput Optimized HDD (st1)** is incorrect because this is primarily used for **frequently** accessed, throughput-intensive workloads. In this scenario, Cold HDD perfectly fits the requirement as it is used for their infrequently accessed data and provides the lowest cost, unlike Throughput Optimized HDD.

**An online events registration system is hosted in AWS and uses ECS to host its front-end tier and a Multi-AZ RDS for its database tier, which also has a standby replica. What are the events that will make Amazon RDS automatically perform a failover to the standby replica? (Select TWO.)**

- [ ]  ​Loss of availability in primary Availability Zone
- [ ]  ​Storage failure on secondary DB instance
- [ ]  ​Storage failure on primary
- [ ]  ​Compute unit failure on secondary DB instance
- [ ]  ​In the event of Read Replica failure

### **Explanation**

- Answer

    **Amazon RDS** provides high availability and failover support for DB instances using Multi-AZ deployments. Amazon RDS uses several different technologies to provide failover support. Multi-AZ deployments for Oracle, PostgreSQL, MySQL, and MariaDB DB instances use Amazon's failover technology. SQL Server DB instances use SQL Server Database Mirroring (DBM).

    In a Multi-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone. The primary DB instance is synchronously replicated across Availability Zones to a standby replica to provide data redundancy, eliminate I/O freezes, and minimize latency spikes during system backups. Running a DB instance with high availability can enhance availability during planned system maintenance, and help protect your databases against DB instance failure and Availability Zone disruption.

    Amazon RDS detects and automatically recovers from the most common failure scenarios for Multi-AZ deployments so that you can resume database operations as quickly as possible without administrative intervention.

    ![https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/con-multi-AZ.png](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/con-multi-AZ.png)

    The high-availability feature is not a scaling solution for read-only scenarios; you cannot use a standby replica to serve read traffic. To service read-only traffic, you should use a Read Replica.

    Amazon RDS automatically performs a failover in the event of any of the following:

    Loss of availability in primary Availability Zone

    Loss of network connectivity to primary

    Compute unit failure on primary

    Storage failure on primary

    The following options are incorrect because all these scenarios do not affect the primary database. Automatic failover only occurs if the primary database is the one that is affected.

    **- Storage failure on secondary DB instance**

    **- In the event of Read Replica failure**

    **- Compute unit failure on secondary DB instance**

⭐️

**[SAA-C02]An application is hosted in AWS Fargate and uses RDS database in Multi-AZ Deployments configuration with several Read Replicas. A Solutions Architect was instructed to ensure that all of their database credentials, API keys, and other secrets are encrypted and rotated on a regular basis to improve data security. The application should also use the latest version of the encrypted credentials when connecting to the RDS database.Which of the following is the MOST appropriate solution to secure the credentials?**

- ​Store the database credentials, API keys, and other secrets to Systems Manager Parameter Store each with a `SecureString` data type. The credentials are automatically rotated by default.
- ​Store the database credentials, API keys, and other secrets to AWS ACM.
- ​Store the database credentials, API keys, and other secrets in AWS KMS.
- ​Use AWS Secrets Manager to store and encrypt the database credentials, API keys, and other secrets. Enable automatic rotation for all of the credentials.

### **Explanation**

- Answer

    **AWS Secrets Manager** is an AWS service that makes it easier for you to manage secrets. *Secrets* can be database credentials, passwords, third-party API keys, and even arbitrary text. You can store and control access to these secrets centrally by using the Secrets Manager console, the Secrets Manager command line interface (CLI), or the Secrets Manager API and SDKs.

    In the past, when you created a custom application that retrieves information from a database, you typically had to embed the credentials (the secret) for accessing the database directly in the application. When it came time to rotate the credentials, you had to do much more than just create new credentials. You had to invest time to update the application to use the new credentials. Then you had to distribute the updated application. If you had multiple applications that shared credentials and you missed updating one of them, the application would break. Because of this risk, many customers have chosen not to regularly rotate their credentials, which effectively substitutes one risk for another.

    ![https://docs.aws.amazon.com/secretsmanager/latest/userguide/images/ASM-Basic-Scenario.png](https://docs.aws.amazon.com/secretsmanager/latest/userguide/images/ASM-Basic-Scenario.png)

    Secrets Manager enables you to replace hardcoded credentials in your code (including passwords), with an API call to Secrets Manager to retrieve the secret programmatically. This helps ensure that the secret can't be compromised by someone examining your code, because the secret simply isn't there. Also, you can configure Secrets Manager to automatically rotate the secret for you according to a schedule that you specify. This enables you to replace long-term secrets with short-term ones, which helps to significantly reduce the risk of compromise.

    Hence, the most appropriate solution for this scenario is: ***Use AWS Secrets Manager to store and encrypt the database credentials, API keys, and other secrets. Enable automatic rotation for all of the credentials.***

    The option that says: ***Store the database credentials, API keys, and other secrets to Systems Manager Parameter Store each with a `SecureString` data type. The credentials are automatically rotated by default*** is incorrect because Systems Manager Parameter Store doesn't rotate its parameters by default.

    The option that says: ***Store the database credentials, API keys, and other secrets to AWS ACM*** is incorrect because it is just a managed private CA service that helps you easily and securely manage the lifecycle of your private certificates to allow SSL communication to your application. This is not a suitable service to store database or any other confidential credentials.

    The option that says: ***Store the database credentials, API keys, and other secrets in AWS KMS*** is incorrect because this only makes it easy for you to create and manage encryption keys and control the use of encryption across a wide range of AWS services. This is primarily used for encryption and not for hosting your credentials.

⭐️

**[SAA-C02] A media company hosts large volumes of archive data that are about 250 TB in size on their internal servers. They have decided to move these data to S3 because of its durability and redundancy. The company currently has a 100 Mbps dedicated line connecting their head office to the Internet.Which of the following is the FASTEST and the MOST cost-effective way to import all these data to Amazon S3?**

- ​Use AWS Snowmobile to transfer the data over to S3.
- ​Establish an AWS Direct Connect connection then transfer the data over to S3.
- ​Upload it directly to S3
- ​Order multiple AWS Snowball devices to upload the files to Amazon S3.

### **Explanation**

- Answer

    AWS Snowball is a petabyte-scale data transport solution that uses secure appliances to transfer large amounts of data into and out of the AWS cloud. Using Snowball addresses common challenges with large-scale data transfers including high network costs, long transfer times, and security concerns. Transferring data with Snowball is simple, fast, secure, and can be as little as one-fifth the cost of high-speed Internet.

    ![https://docs.aws.amazon.com/snowball/latest/ug/images/Snowball-opening-600w.png](https://docs.aws.amazon.com/snowball/latest/ug/images/Snowball-opening-600w.png)

    Snowball is a strong choice for data transfer if you need to more securely and quickly transfer terabytes to many petabytes of data to AWS. Snowball can also be the right choice if you don’t want to make expensive upgrades to your network infrastructure, if you frequently experience large backlogs of data, if you're located in a physically isolated environment, or if you're in an area where high-speed Internet connections are not available or cost-prohibitive.

    As a rule of thumb, if it takes more than one week to upload your data to AWS using the spare capacity of your existing Internet connection, then you should consider using Snowball. For example, if you have a 100 Mb connection that you can solely dedicate to transferring your data and need to transfer 100 TB of data, it takes more than 100 days to complete data transfer over that connection. You can make the same transfer by using multiple Snowballs in about a week.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2020-02-16_11-15-22-2595be662f78560da845fae54e4f2aca.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2020-02-16_11-15-22-2595be662f78560da845fae54e4f2aca.png)

    Hence, ***ordering multiple AWS Snowball devices to upload the files to Amazon S3*** is the correct answer.

    ***Uploading it directly to S3*** is incorrect since this would take too long to finish due to the slow Internet connection of the company.

    ***Establishing an AWS Direct Connect connection then transferring the data over to S3*** is incorrect since provisioning a line for Direct Connect would take too much time and might not give you the fastest data transfer solution. In addition, the scenario didn't warrant an establishment of a dedicated connection from your on-premises data center to AWS. The primary goal is to just do a one-time migration of data to AWS which can be accomplished by using AWS Snowball devices.

    ***Using AWS Snowmobile to transfer the data over to S3*** is incorrect because Snowmobile is more suitable if you need to move extremely large amounts of data to AWS or need to transfer up to 100PB of data. This will be transported on a 45-foot long ruggedized shipping container, pulled by a semi-trailer truck. Take note that you only need to migrate 250 TB of data, hence, this is not the most suitable and cost-effective solution.

**You are working for an online hotel booking firm with terabytes of customer data coming from your websites and applications. There is an annual corporate meeting where you need to present the booking behavior and acquire new insights from your customers’ data. You are looking for a service to perform super-fast analytics on massive data sets in near real-time. Which of the following services gives you the ability to store huge amounts of data and perform quick and flexible queries on it?**

- ​RDS
- ​ElastiCache
- ​DynamoDB
- ​Redshift

### **Explanation**

- Answer

    Amazon Redshift is a fast, scalable data warehouse that makes it simple and cost-effective to analyze all your data across your data warehouse and data lake. Redshift delivers ten times faster performance than other data warehouses by using machine learning, massively parallel query execution, and columnar storage on high-performance disk.

    **DynamoDB** is incorrect. DynamoDB is a NoSQL database which is based on key-value pairs used for fast processing of small data that dynamically grows and changes. But if you need to scan large amounts of data (ie a lot of keys all in one query), the performance will not be optimal.

    **ElastiCache** is incorrect because this is used to increase the performance, speed and redundancy with which applications can retrieve data by providing an in-memory database caching system, and not for database analytical processes.

    **RDS** is incorrect because this is mainly used for On-Line Transaction Processing (OLTP) applications and not for Online Analytics Processing (OLAP).

**Your company has a top priority requirement to monitor a few database metrics and then afterwards, send email notifications to the Operations team in case there is an issue. Which AWS services can accomplish this requirement? (Select TWO.)**

- [ ]  ​Amazon CloudWatch
- [ ]  ​Amazon Simple Notification Service (SNS)
- [ ]  ​Amazon EC2 Instance with a running Berkeley Internet Name Domain (BIND) Server.
- [ ]  ​Amazon Simple Queue Service (SQS)
- [ ]  ​Amazon Simple Email Service

### **Explanation**

- Answer

    ***Amazon CloudWatch*** and ***Amazon Simple Notification Service (SNS)*** are correct. In this requirement, you can use Amazon CloudWatch to monitor the database and then Amazon SNS to send the emails to the Operations team. Take note that you should use SNS instead of SES (Simple Email Service) when you want to monitor your EC2 instances.

    ![https://d1.awsstatic.com/product-marketing/cloudwatch/product-page-diagram_Cloudwatch_v4.55c15d1cc086395cbd5ad279a2f1fc37e8452e77.png](https://d1.awsstatic.com/product-marketing/cloudwatch/product-page-diagram_Cloudwatch_v4.55c15d1cc086395cbd5ad279a2f1fc37e8452e77.png)

    CloudWatch collects monitoring and operational data in the form of logs, metrics, and events, providing you with a unified view of AWS resources, applications, and services that run on AWS, and on-premises servers.

    SNS is a highly available, durable, secure, fully managed pub/sub messaging service that enables you to decouple microservices, distributed systems, and serverless applications.

    ***Amazon Simple Email Service*** is incorrect. SES is a cloud-based email sending service designed to send notification and transactional emails.

    ***Amazon Simple Queue Service (SQS)*** is incorrect. SQS is a fully-managed message queuing service. It does not monitor applications nor send email notifications unlike SES.

    ***Amazon EC2 Instance with a running Berkeley Internet Name Domain (BIND) Server*** is incorrect because BIND is primarily used as a Domain Name System (DNS) web service. This is only applicable if you have a private hosted zone in your AWS account. It does not monitor applications nor send email notifications.

**A music publishing company is building a multitier web application that requires a key-value store which will save the document models. Each model is composed of band ID, album ID, song ID, composer ID, lyrics, and other data. The web tier will be hosted in an Amazon ECS cluster with AWS Fargate launch type.Which of the following is the MOST suitable setup for the database-tier?**

- ​Use Amazon WorkDocs to store the document models.
- ​Launch an Amazon Aurora Serverless database.
- ​Launch a DynamoDB table.
- ​Launch an Amazon RDS database with Read Replicas.

### **Explanation**

- Answer

    Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed cloud database and supports both document and key-value store models. Its flexible data model, reliable performance, and automatic scaling of throughput capacity makes it a great fit for mobile, web, gaming, ad tech, IoT, and many other applications.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-23_05-24-29-74b3e6dadc8ce683ccd2a5bd00f99889.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-23_05-24-29-74b3e6dadc8ce683ccd2a5bd00f99889.png)

    Hence, the correct answer is: ***Launch a DynamoDB table*.**

    The option that says: ***Launch an Amazon RDS database with Read Replicas*** is incorrect because this is a relational database. This is not suitable to be used as a key-value store. A better option is to use DynamoDB as it supports both document and key-value store models.

    The option that says: ***Use Amazon WorkDocs to store the document models*** is incorrect because Amazon WorkDocs simply enables you to share content, provide rich feedback, and collaboratively edit documents. It is not a key-value store like DynamoDB.

    The option that says: ***Launch an Amazon Aurora Serverless database*** is incorrect because this type of database is not suitable to be used as a key-value store. Amazon Aurora Serverless is an on-demand, auto-scaling configuration for Amazon Aurora where the database will automatically start-up, shut down, and scale capacity up or down based on your application's needs. It enables you to run your database in the cloud without managing any database instances. It's a simple, cost-effective option for infrequent, intermittent, or unpredictable workloads and not as a key-value store.

⭐️

**A startup company has a serverless architecture that uses AWS Lambda, API Gateway, and DynamoDB. They received an urgent feature request from their client last month and now, it is ready to be pushed to production. The company is using AWS CodeDeploy as their deployment service.Which of the following configuration types will allow you to specify the percentage of traffic shifted to your updated Lambda function version before the remaining traffic is shifted in the second increment?**

- ​Blue/Green
- ​Canary
- ​Linear
- ​All-at-once

### **Explanation**

- Answer

    If you're using the AWS Lambda compute platform, you must choose one of the following deployment configuration types to specify how traffic is shifted from the original AWS Lambda function version to the new AWS Lambda function version:

    **Canary**: Traffic is shifted in two increments. You can choose from predefined canary options that specify the percentage of traffic shifted to your updated Lambda function version in the first increment and the interval, in minutes, before the remaining traffic is shifted in the second increment.

    **Linear**: Traffic is shifted in equal increments with an equal number of minutes between each increment. You can choose from predefined linear options that specify the percentage of traffic shifted in each increment and the number of minutes between each increment.

    **All-at-once**: All traffic is shifted from the original Lambda function to the updated Lambda function version at once.

    ![https://d2908q01vomqb2.cloudfront.net/7719a1c782a1ba91c031a682a0a2f8658209adbf/2018/01/11/solution-overview-1024x514.png](https://d2908q01vomqb2.cloudfront.net/7719a1c782a1ba91c031a682a0a2f8658209adbf/2018/01/11/solution-overview-1024x514.png)

    **Blue/Green** is incorrect because this is not a predefined deployment type configuration for an AWS Lambda Compute Platform. You can only choose Canary, Linear, and All-at-once.

    **Linear** is incorrect because this type of deployment shifts the traffic in equal increments with an equal number of minutes between each increment. You can't specify the percentage of traffic shifted to your updated Lambda function version before the remaining traffic is shifted in the second increment, unlike Canary.

    **All-at-once** is incorrect because there are no increments for this type of deployment. All traffic is shifted from the original Lambda function to the updated Lambda function version at once.

**You are working as a Cloud Consultant for a government agency with a mandate of improving traffic planning, maintenance of roadways and preventing accidents. There is a need to manage traffic infrastructure in real time, alert traffic engineers and emergency response teams when problems are detected, and automatically change traffic signals to get emergency personnel to accident scenes faster by using sensors and smart devices. Which AWS service will allow the developers of the agency to connect the said devices to your cloud-based applications?**

- ​AWS IoT Core
- ​Container service
- ​CloudFormation
- ​Elastic Beanstalk

### **Explanation**

- Answer

    AWS IoT Core is a managed cloud service that lets connected devices easily and securely interact with cloud applications and other devices. AWS IoT Core provides secure communication and data processing across different kinds of connected devices and locations so you can easily build IoT applications.

    ![https://d1.awsstatic.com/IoT/diagrams/AWS%20IoT%20Core%20-%20Process%20and%20Act.2b1f03813fbd3b4416e45c096336497f22954520.png](https://d1.awsstatic.com/IoT/diagrams/AWS%20IoT%20Core%20-%20Process%20and%20Act.2b1f03813fbd3b4416e45c096336497f22954520.png)

    **CloudFormation** is incorrect because this is mainly used for creating and managing the architecture and not for handling connected devices. You have to use AWS IoT Core instead.

    **Elastic Beanstalk** is incorrect because this is mainly used as a substitute to Infrastructure-as-a-Service with Platform-as-a-Service, which reduces management complexity without restricting choice or control and not for handling connected devices.

    **Container service** is incorrect because this is mainly used for creating and managing docker instances and not for handling devices.

**Your company is running a multi-tier web application farm in a virtual private cloud (VPC) that is not connected to their corporate network. They are connecting to the VPC over the Internet to manage the fleet of Amazon EC2 instances running in both the public and private subnets. You have added a bastion host with Microsoft Remote Desktop Protocol (RDP) access to the application instance security groups, but the company wants to further limit administrative access to all of the instances in the VPC.Which of the following bastion host deployment options will meet this requirement?**

- ​Deploy a Windows Bastion host with an Elastic IP address in the private subnet, and restrict RDP access to the bastion from only the corporate public IP addresses.
- ​Deploy a Windows Bastion host on the corporate network that has RDP access to all EC2 instances in the VPC.
- ​Deploy a Windows Bastion host with an Elastic IP address in the public subnet and allow RDP access to bastion only from the corporate IP addresses.
- ​Deploy a Windows Bastion host with an Elastic IP address in the public subnet and allow SSH access to the bastion from anywhere.

### **Explanation**

- Answer

    The correct answer is to deploy a Windows Bastion host with an Elastic IP address in the public subnet and allow RDP access to bastion only from the corporate IP addresses.

    A bastion host is a special purpose computer on a network specifically designed and configured to withstand attacks. If you have a bastion host in AWS, it is basically just an EC2 instance. It should be in a public subnet with either a public or Elastic IP address with sufficient RDP or SSH access defined in the security group. Users log on to the bastion host via SSH or RDP and then use that session to manage other hosts in the private subnets.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-02-13_01-07-49-c56d7bdad437af14a0a3b8a17c9dcfd2.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-02-13_01-07-49-c56d7bdad437af14a0a3b8a17c9dcfd2.png)

    **Deploying a Windows Bastion host on the corporate network that has RDP access to all EC2 instances in the VPC** is incorrect since you do not deploy the Bastion host to your corporate network. It should be in the public subnet of a VPC.

    **Deploying a Windows Bastion host with an Elastic IP address in the private subnet, and restricting RDP access to the bastion from only the corporate public IP addresses** is incorrect since it should be deployed in a public subnet, not a private subnet.

    **Deploying a Windows Bastion host with an Elastic IP address in the public subnet and allowing SSH access to the bastion from anywhere** is incorrect. Since it is a Windows bastion, you should allow RDP access and not SSH as this is mainly used for Linux-based systems.

**You have a new, dynamic web app written in MEAN stack that is going to be launched in the next month. There is a probability that the traffic will be quite high in the first couple of weeks. In the event of a load failure, how can you set up DNS failover to a static website?**

- ​Use Route 53 with the failover option to a static S3 website bucket or CloudFront distribution.
- ​Add more servers in case the application fails.
- ​Duplicate the exact application architecture in another region and configure DNS weight-based routing.
- ​Enable failover to an application hosted in an on-premises data center.

### **Explanation**

- Answer

    For this scenario, **using Route 53 with the failover option to a static S3 website bucket or CloudFront distribution** is correct. You can create a new Route 53 with the failover option to a static S3 website bucket or CloudFront distribution as an alternative.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-02-13_01-05-29-0096a577e991922c675f02801d48a8a4.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-02-13_01-05-29-0096a577e991922c675f02801d48a8a4.png)

    **Duplicating the exact application architecture in another region and configuring DNS weight-based routing** is incorrect because running a duplicate system is not a cost-effective solution. Remember that you are trying to build a failover mechanism for your web app, not a distributed setup.

    **Enabling failover to an application hosted in an on-premises data center** is incorrect because, although you can set up failover to your on-premises data center, you are not maximizing the AWS environment such as using Route 53 failover.

    **Adding more servers in case the application fails** is incorrect because this is not the best way to handle a failover event. If you add more servers only in case the application fails, then there would be a period of downtime in which your application is unavailable. Since there are no running servers on that period, your application will be unavailable for a certain period of time until your new server is up and running.

⭐️

**You are a Solutions Architect working for a large insurance company that deployed their production environment on a custom Virtual Private Cloud in AWS with a default configuration. The VPC consists of two private subnets and one public subnet. Inside the public subnet is a group of EC2 instances which are created by an Auto Scaling group and all of the instances are in the same Security Group. Your development team has created a new application which will be accessed by mobile devices via a custom port. This application has been deployed to the production environment and you need to open this port globally to the Internet.Which of the following is the correct procedure to meet this requirement?**

- ​Open the custom port on the Network Access Control List of your VPC. Your EC2 instances will be able to use this port immediately.
- ​Open the custom port on the Security Group. Your EC2 instances will be able to use this port immediately.
- ​Open the custom port on the Security Group. Your EC2 instances will be able to use this port after 60 minutes.
- ​Open the custom port on the Network Access Control List of your VPC. Your EC2 instances will be able to use this port after a reboot.

### **Explanation**

- Answer

    To allow the custom port, you have to change the Inbound Rules in your Security Group to allow traffic coming from the mobile devices. **Security Groups usually control the list of ports that are allowed to be used by your EC2 instances and the NACLs control which network or list of IP addresses can connect to your whole VPC.**

    ![https://docs.aws.amazon.com/vpc/latest/userguide/images/nacl-example-diagram.png](https://docs.aws.amazon.com/vpc/latest/userguide/images/nacl-example-diagram.png)

    When you create a security group, it has no inbound rules. Therefore, no inbound traffic originating from another host to your instance is allowed until you add inbound rules to the security group. By default, a security group includes an outbound rule that allows all outbound traffic. You can remove the rule and add outbound rules that allow specific outbound traffic only. If your security group has no outbound rules, no outbound traffic originating from your instance is allowed.

    The option that says: **Open the custom port on the Security Group. Your EC2 instances will be able to use this port after 60 minutes** and **Open the custom port on the Network Access Control List of your VPC. Your EC2 instances will be able to use this port after a reboot** are both incorrect because any changes to the Security Groups or Network Access Control Lists are applied immediately and not after 60 minutes or after the instance reboot.

    The option that says: **Open the custom port on the Network Access Control List of your VPC. Your EC2 instances will be able to use this port immediately** is incorrect because the scenario says that VPC is using a default configuration. Since by default, Network ACL allows **all** inbound and outbound IPv4 traffic, then there is no point of explicitly allowing the port in the Network ACL. Security Groups, on the other hand, does not allow incoming traffic by default, unlike Network ACL.

⭐️

**You are working for a litigation firm as the Data Engineer for their case history application. You need to keep track of all the cases your firm has handled. The static assets like .jpg, .png, and .pdf files are stored in S3 for cost efficiency and high durability. As these files are critical to your business, you want to keep track of what's happening in your S3 bucket. You found out that S3 has an event notification whenever a delete or write operation happens within the S3 bucket. What are the possible Event Notification destinations available for S3 buckets? (Select TWO.)**

- [ ]  ​SES
- [ ]  ​Kinesis
- [ ]  ​SWF
- [ ]  ​Lambda function
- [ ]  ​SQS

### **Explanation**

- Answer

    The Amazon S3 notification feature enables you to receive notifications when certain events happen in your bucket. To enable notifications, you must first add a notification configuration identifying the events you want Amazon S3 to publish, and the destinations where you want Amazon S3 to send the event notifications.

    Amazon S3 supports the following destinations where it can publish events:**Amazon Simple Notification Service (Amazon SNS) topic -** A web service that coordinates and manages the delivery or sending of messages to subscribing endpoints or clients.

    **Amazon Simple Queue Service (Amazon SQS) queue -** Offers reliable and scalable hosted queues for storing messages as they travel between computer.

    **AWS Lambda -** AWS Lambda is a compute service where you can upload your code and the service can run the code on your behalf using the AWS infrastructure. You package up and upload your custom code to AWS Lambda when you create a Lambda function

    **Kinesis** is incorrect because this is used to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information, and not used for event notifications. You have to use SNS, SQS or Lambda.

    **SES** is incorrect because this is mainly used for sending emails designed to help digital marketers and application developers send marketing, notification, and transactional emails, and not for sending event notifications from S3. You have to use SNS, SQS or Lambda.

    **SWF** is incorrect because this is mainly used to build applications that use Amazon's cloud to coordinate work across distributed components and not used as a way to trigger event notifications from S3. You have to use SNS, SQS or Lambda.

    Here’s what you need to do in order to start using this new feature with your application:

    Create the queue, topic, or Lambda function (which I’ll call the target for brevity) if necessary.

    Grant S3 permission to publish to the target or invoke the Lambda function. For SNS or SQS, you do this by applying an appropriate policy to the topic or the queue. For Lambda, you must create and supply an IAM role, then associate it with the Lambda function.

    Arrange for your application to be invoked in response to activity on the target. As you will see in a moment, you have several options here.

    Set the bucket’s Notification Configuration to point to the target.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-23_07-00-07-8b41add7c02e86428c5743b6790ac876.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-23_07-00-07-8b41add7c02e86428c5743b6790ac876.png)

⭐️

**As a Junior Software Engineer, you are developing a hotel reservations application and are given the task of improving the database aspect of the app. You found out that RDS does not satisfy the needs of your application because it does not scale as easily compared with DynamoDB. You need to demonstrate to your Senior Software Engineer the advantages of using DynamoDB over RDS. What are the valid use cases for Amazon DynamoDB? (Select TWO.)**

- [ ]  ​Running a database with a well-defined schema and enforces referential integrity in relationships between tables.
- [ ]  ​Storing large amounts of infrequently accessed data.
- [ ]  ​Storing BLOB data.
- [ ]  ​Storing metadata for Amazon S3 objects.
- [ ]  ​Managing web sessions.

### **Explanation**

- Answer

    **DynamoDB** is a NoSQL database that supports key-value and document data structures. A key-value store is a database service that provides support for storing, querying, and updating collections of objects that are identified using a key and values that contain the actual content being stored. Meanwhile, a document data store provides support for storing, querying, and updating items in a document format such as JSON, XML, and HTML.

    **Managing web sessions** is correct because the DynamoDB Time-to-Live (TTL) mechanism enables you to manage web sessions of your application easily. It lets you set a specific timestamp to delete expired items from your tables. Once the timestamp expires, the corresponding item is marked as expired and is subsequently deleted from the table. By using this functionality, you do not have to track expired data and delete it manually. TTL can help you reduce storage usage and reduce the cost of storing data that is no longer relevant.

    **Storing metadata for Amazon S3 objects** is correct because the Amazon DynamoDB stores structured data indexed by primary key and allow low latency read and write access to items ranging from 1 byte up to 400KB. Amazon S3 stores unstructured blobs and is suited for storing large objects up to 5 TB. In order to optimize your costs across AWS services, large objects or infrequently accessed data sets should be stored in Amazon S3, while smaller data elements or file pointers (possibly to Amazon S3 objects) are best saved in Amazon DynamoDB.

    To speed up access to relevant data, you can pair Amazon S3 with a search engine such as Amazon CloudSearch or a database such as Amazon DynamoDB or Amazon RDS. In these scenarios, Amazon S3 stores the actual information, and the search engine or database serves as the repository for associated metadata such as the object name, size, keywords, and so on. Metadata in the database can easily be indexed and queried, making it very efficient to locate an object’s reference by using a search engine or a database query. This result can be used to pinpoint and retrieve the object itself from Amazon S3.

    The option that says: **Running a database with a well-defined schema and enforces referential integrity in relationships between tables** is incorrect since DynamoDB is a NoSQL database solution and not a relational database. RDS is more suitable for a relational model that normalizes data into tables that are composed of rows and columns. An RDS database enforces referential integrity in relationships between tables, unlike a DynamoDB table.

    **Storing large amounts of infrequently accessed data** is incorrect because DynamoDB is not meant to store large amounts of infrequently accessed data, due to factors like sizing, scaling, and cost. Amazon Glacier would be a better option for this scenario.

    **Storing BLOB data** is incorrect because BLOB data is too large a chunk of data to be put into a NoSQL database such as DynamoDB.

⭐️

**You have a data analytics application that updates a real-time, foreign exchange dashboard and another separate application that archives data to Amazon Redshift. Both applications are configured to consume data from the same stream concurrently and independently by using Amazon Kinesis Data Streams. However, you noticed that there are a lot of occurrences where a shard iterator expires unexpectedly. Upon checking, you found out that the DynamoDB table used by Kinesis does not have enough capacity to store the lease data. Which of the following is the most suitable solution to rectify this issue?**

- ​Use Amazon Kinesis Data Analytics to properly support the data analytics application instead of Kinesis Data Stream.
- ​Enable In-Memory Acceleration with DynamoDB Accelerator (DAX).
- ​Upgrade the storage capacity of the DynamoDB table.
- ​Increase the write capacity assigned to the shard table.

### **Explanation**

- Answer

    A new shard iterator is returned by every **GetRecords** request (as `NextShardIterator`), which you then use in the next **GetRecords** request (as `ShardIterator`). Typically, this shard iterator does not expire before you use it. However, you may find that shard iterators expire because you have not called **GetRecords** for more than 5 minutes, or because you've performed a restart of your consumer application.

    ![https://docs.aws.amazon.com/streams/latest/dev/images/architecture.png](https://docs.aws.amazon.com/streams/latest/dev/images/architecture.png)

    If the shard iterator expires immediately before you can use it, this might indicate that the DynamoDB table used by Kinesis does not have enough capacity to store the lease data. This situation is more likely to happen if you have a large number of shards. To solve this problem, increase the write capacity assigned to the shard table.

    Hence, **increasing the write capacity assigned to the shard table** is the correct answer.

    **Upgrading the storage capacity of the DynamoDB table** is incorrect because DynamoDB is a fully managed service which automatically scales its storage, without setting it up manually. The scenario refers to the **write capacity** of the shard table when it says that the DynamoDB table used by Kinesis does not have enough *capacity* to store the lease data.

    **Enabling In-Memory Acceleration with DynamoDB Accelerator (DAX)** is incorrect because the DAX feature is primarily used for read performance improvement of your DynamoDB table from *milliseconds* response time to *microseconds*. It does not have any relationship with Amazon Kinesis Data Stream in this scenario.

    **Using Amazon Kinesis Data Analytics to properly support the data analytics application instead of Kinesis Data Stream** is incorrect because although Amazon Kinesis Data Analytics can support a data analytics application, it is still not a suitable solution for this issue. You simply need to increase the write capacity assigned to the shard table in order to rectify the problem which is why switching to Amazon Kinesis Data Analytics is not necessary.

⭐️

**A web application, which is used by your clients around the world, is hosted in an Auto Scaling group of EC2 instances behind a Classic Load Balancer. You need to secure your application by allowing multiple domains to serve SSL traffic over the same IP address.Which of the following should you do to meet the above requirement?**

- ​Use Server Name Indication (SNI) on your Classic Load Balancer by adding multiple SSL certificates to allow multiple domains to serve SSL traffic.
- ​Use an Elastic IP and upload multiple 3rd party certificates in your Classic Load Balancer using the AWS Certificate Manager.
- ​It is not possible to allow multiple domains to serve SSL traffic over the same IP address in AWS
- ​Generate an SSL certificate with AWS Certificate Manager and create a CloudFront web distribution. Associate the certificate with your web distribution and enable the support for Server Name Indication (SNI).

### **Explanation**

- Answer

    SNI Custom SSL relies on the SNI extension of the Transport Layer Security protocol, which allows multiple domains to serve SSL traffic over the same IP address by including the hostname which the viewers are trying to connect to.

    Amazon CloudFront delivers your content from each edge location and offers the same security as the Dedicated IP Custom SSL feature. SNI Custom SSL works with most modern browsers, including Chrome version 6 and later (running on Windows XP and later or OS X 10.5.7 and later), Safari version 3 and later (running on Windows Vista and later or Mac OS X 10.5.6. and later), Firefox 2.0 and later, and Internet Explorer 7 and later (running on Windows Vista and later).

    ![https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2016/10/17/image12_new_a.png](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2016/10/17/image12_new_a.png)

    Some users may not be able to access your content because some older browsers do not support SNI and will not be able to establish a connection with CloudFront to load the HTTPS version of your content. If you need to support non-SNI compliant browsers for HTTPS content, it is recommended to use the Dedicated IP Custom SSL feature.

    **Using Server Name Indication (SNI) on your Classic Load Balancer by adding multiple SSL certificates to allow multiple domains to serve SSL traffic** is incorrect because a Classic Load Balancer does not support Server Name Indication (SNI). You have to use an Application Load Balancer instead or a CloudFront web distribution to allow the SNI feature.

    **Using an Elastic IP and uploading multiple 3rd party certificates in your Classic Load Balancer using the AWS Certificate Manager** is incorrect because just like in the above, a Classic Load Balancer does not support Server Name Indication (SNI) and the use of an Elastic IP is not a suitable solution to allow multiple domains to serve SSL traffic. You have to use Server Name Indication (SNI).

    The option that says: **It is not possible to allow multiple domains to serve SSL traffic over the same IP address in AWS** is incorrect because AWS does support the use of Server Name Indication (SNI).

**The operations team of your company asked you for a way to monitor the health of your production EC2 instances in AWS. You told them to use the CloudWatch service.Which of the following metrics is not available by default in CloudWatch?**

- ​CPU Usage
- ​Memory Usage
- ​Disk Read operations
- ​Network In and Out

### **Explanation**

- Answer

    Memory Usage is a metric not available by default in CloudWatch. You need to add a custom metric for it to work.

**A San Francisco-based tech startup is building a cross-platform mobile app that can notify the user with upcoming astronomical events such as eclipses, blue moon, novae or a meteor shower. Your mobile app authenticates with the Identity Provider (IdP) using the provider's SDK and Amazon Cognito. Once the end user is authenticated with the IdP, the OAuth or OpenID Connect token returned from the IdP is passed by your app to Amazon Cognito.Which of the following is returned for the user to provide a set of temporary, limited-privilege AWS credentials?**

- ​Cognito ID
- ​Cognito API
- ​Cognito Key Pair
- ​Cognito SDK

### **Explanation**

- Answer

    You can use Amazon Cognito to deliver temporary, limited-privilege credentials to your application so that your users can access AWS resources. Amazon Cognito identity pools support both authenticated and unauthenticated identities. You can retrieve a unique Amazon Cognito identifier (identity ID) for your end user immediately if you're allowing unauthenticated users or after you've set the login tokens in the credentials provider if you're authenticating users.

    That is why the correct answer for this question is **Cognito ID**.

    **Cognito SDK** is incorrect because this is not a unique Amazon Cognito identifier but a software development kit that is available in various programming languages.

    **Cognito Key Pair** is incorrect because this is not a unique Amazon Cognito identifier but a cryptography key.

    **Cognito API** is incorrect because this is not a unique Amazon Cognito identifier and is primarily used as an Application Programming Interface.

⭐️

**A company has an enterprise web application hosted in an AWS Fargate cluster with an Amazon FSx for Lustre filesystem for its high performance computing workloads. A warm standby environment is running in another AWS region for disaster recovery. A Solutions Architect was assigned to design a system that will automatically route the live traffic to the disaster recovery (DR) environment only in the event that the primary application st ack experiences an outage.What should the Architect do to satisfy this requirement?**

- ​Set up a Weighted routing policy configuration in Route 53 by adding health checks on both the primary stack and the DR environment. Configure the network access control list and the route table to allow Route 53 to send requests to the endpoints specified in the health checks. Enable the `Evaluate Target Health` option by setting it to `Yes`.
- ​Set up a failover routing policy configuration in Route 53 by adding a health check on the primary service endpoint. Configure Route 53 to direct the DNS queries to the secondary record when the primary resource is unhealthy. Configure the network access control list and the route table to allow Route 53 to send requests to the endpoints specified in the health checks. Enable the `Evaluate Target Health` option by setting it to `Yes`.
- ​Set up a CloudWatch Events rule to monitor the primary Route 53 DNS endpoint and create a custom Lambda function. Execute the `ChangeResourceRecordSets` API call using the function to initiate the failover to the secondary DNS record.
- ​Set up a CloudWatch Alarm to monitor the primary Route 53 DNS endpoint and create a custom Lambda function. Execute the `ChangeResourceRecordSets` API call using the function to initiate the failover to the secondary DNS record.

### **Explanation**

- Answer

    Use an active-passive failover configuration when you want a primary resource or group of resources to be available majority of the time and you want a secondary resource or group of resources to be on standby in case all the primary resources become unavailable. When responding to queries, Route 53 includes only the healthy primary resources. If all the primary resources are unhealthy, Route 53 begins to include only the healthy secondary resources in response to DNS queries.

    To create an active-passive failover configuration with one primary record and one secondary record, you just create the records and specify **Failover** for the routing policy. When the primary resource is healthy, Route 53 responds to DNS queries using the primary record. When the primary resource is unhealthy, Route 53 responds to DNS queries using the secondary record.

    You can configure a health check that monitors an endpoint that you specify either by IP address or by domain name. At regular intervals that you specify, Route 53 submits automated requests over the Internet to your application, server, or other resource to verify that it's reachable, available, and functional. Optionally, you can configure the health check to make requests similar to those that your users make, such as requesting a web page from a specific URL.

    ![https://media.amazonwebservices.com/blog/2013/route_53_elb_config_1.png](https://media.amazonwebservices.com/blog/2013/route_53_elb_config_1.png)

    When Route 53 checks the health of an endpoint, it sends an HTTP, HTTPS, or TCP request to the IP address and port that you specified when you created the health check. For a health check to succeed, your router and firewall rules must allow inbound traffic from the IP addresses that the Route 53 health checkers use.

    Hence, the correct answer is: **Set up a failover routing policy configuration in Route 53 by adding a health check on the primary service endpoint. Configure Route 53 to direct the DNS queries to the secondary record when the primary resource is unhealthy. Configure the network access control list and the route table to allow Route 53 to send requests to the endpoints specified in the health checks. Enable the *`Evaluate Target Health`* option by setting it to *`Yes.`***

    The option that says: **Set up a Weighted routing policy configuration in Route 53 by adding health checks on both the primary stack and the DR environment. Configure the network access control list and the route table to allow Route 53 to send requests to the endpoints specified in the health checks. Enable the `Evaluate Target Health` option by setting it to `Yes`** is incorrect because Weighted routing simply lets you associate multiple resources with a single domain name (tutorialsdojo.com) or subdomain name (blog.tutorialsdojo.com) and choose how much traffic is routed to each resource. This can be useful for a variety of purposes, including load balancing and testing new versions of software, but not for a failover configuration. Remember that the scenario says that the solution should automatically route the live traffic to the disaster recovery (DR) environment only in the event that the primary application stack experiences an outage. This configuration is incorrectly distributing the traffic on both the primary and DR environment.

    The option that says: **Set up a CloudWatch Alarm to monitor the primary Route 53 DNS endpoint and create a custom Lambda function. Execute the `ChangeResourceRecordSets` API call using the function to initiate the failover to the secondary DNS record** is incorrect because setting up a CloudWatch Alarm and using the Route 53 API is not applicable nor useful at all in this scenario. Remember that CloudWatch Alam is primarily used for monitoring CloudWatch metrics. You have to use a Failover routing policy instead.

    The option that says: **Set up a CloudWatch Events rule to monitor the primary Route 53 DNS endpoint and create a custom Lambda function. Execute the`ChangeResourceRecordSets` API call using the function to initiate the failover to the secondary DNS record** is incorrect because the Amazon CloudWatch Events service is commonly used to deliver a near real-time stream of system events that describe changes in **some** Amazon Web Services (AWS) resources. There is no direct way for CloudWatch Events to monitor the status of your Route 53 endpoints. You have to configure a health check and a failover configuration in Route 53 instead to satisfy the requirement in this scenario.

⭐️

**You are developing a meal planning application that provides meal recommendations for the week as well as the food consumption of your users. Your application resides on an EC2 instance which requires access to various AWS services for its day-to-day operations. Which of the following is the best way to allow your EC2 instance to access your S3 bucket and other AWS services?**

- ​Add the API Credentials in the Security Group and assign it to the EC2 instance.
- ​Store the API credentials in the EC2 instance.
- ​Create a role in IAM and assign it to the EC2 instance.
- ​Store the API credentials in a bastion host.

### **Explanation**

- Answer

    The best practice in handling API Credentials is to create a new role in the Identity Access Management (IAM) service and then assign it to a specific EC2 instance. In this way, you have a secure and centralized way of storing and managing your credentials.

    **Storing the API credentials in the EC2 instance**, **adding the API Credentials in the Security Group and assigning it to the EC2 instance**, and **storing the API credentials in a bastion host** are incorrect because it is not secure to store nor use the API credentials from an EC2 instance. You should use IAM service instead.

**A digital media company shares static content to its premium users around the world and also to their partners who syndicate their media files. The company is looking for ways to reduce its server costs and securely deliver their data to their customers globally with low latency.Which combination of services should be used to provide the MOST suitable and cost-effective architecture? (Select TWO.)**

- [ ]  ​AWS Global Accelerator
- [ ]  ​Amazon S3
- [ ]  ​AWS Fargate
- [ ]  ​AWS Lambda
- [ ]  ​Amazon CloudFront

### **Explanation**

- Answer

    Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.

    CloudFront is integrated with AWS – both physical locations that are directly connected to the AWS global infrastructure, as well as other AWS services. CloudFront works seamlessly with services including AWS Shield for DDoS mitigation, Amazon S3, Elastic Load Balancing or Amazon EC2 as origins for your applications, and Lambda@Edge to run custom code closer to customers’ users and to customize the user experience. Lastly, if you use AWS origins such as Amazon S3, Amazon EC2 or Elastic Load Balancing, you don’t pay for any data transferred between these services and CloudFront.

    ![https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2018/06/27/4-v-2.png](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2018/06/27/4-v-2.png)

    Amazon S3 is object storage built to store and retrieve any amount of data from anywhere on the Internet. It’s a simple storage service that offers an extremely durable, highly available, and infinitely scalable data storage infrastructure at very low costs.

    AWS Global Accelerator and Amazon CloudFront are separate services that use the AWS global network and its edge locations around the world. CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery). Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. Both services integrate with AWS Shield for DDoS protection.

    Hence, the correct options are ***Amazon CloudFront** and **Amazon S3*.**

    ***AWS Fargate*** is incorrect because this service is just a serverless compute engine for containers that work with both Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS). Although this service is more cost-effective than its server-based counterpart, Amazon S3 still costs way less than Fargate, especially for storing static content.

    ***AWS Lambda*** is incorrect because this simply lets you run your code serverless, without provisioning or managing servers. Although this is also a cost-effective service since you have to pay only for the compute time you consume, you can't use this to store static content or as a Content Delivery Network (CDN). A better combination is Amazon CloudFront and Amazon S3.

    ***AWS Global Accelerator*** is incorrect because this service is more suitable for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. Moreover, there is no direct way that you can integrate AWS Global Accelerator with Amazon S3. It's more suitable to use Amazon CloudFront instead in this scenario.

⭐️

**You are an IT Consultant for an advertising company that is currently working on a proof of concept project that automatically provides SEO analytics for their clients. Your company has a VPC in AWS that operates in dual-stack mode in which IPv4 and IPv6 communication is allowed. You deployed the application to an Auto Scaling group of EC2 instances with an Application Load Balancer in front that evenly distributes the incoming traffic. You are ready to go live but you need to point your domain name (tutorialsdojo.com) to the Application Load Balancer. In Route 53, which record types will you use to point the DNS name of the Application Load Balancer? (Select TWO.)**

- [ ]  ​Alias with a type "AAAA" record set
- [ ]  ​Non-Alias with a type "A" record set
- [ ]  ​Alias with a type "CNAME" record set
- [ ]  ​Alias with a type "A" record set
- [ ]  ​Alias with a type of “MX” record set

### **Explanation**

- Answer

    **Alias with a type "AAAA" record set** and **Alias with a type "A" record set** are correct. To route domain traffic to an ELB load balancer, use Amazon Route 53 to create an alias record that points to your load balancer. An alias record is a Route 53 extension to DNS. It's similar to a CNAME record, but you can create an alias record both for the root domain, such as tutorialsdojo.com, and for subdomains, such as portal.tutorialsdojo.com. (You can create CNAME records only for subdomains.) To enable IPv6 resolution, you would need to create a second resource record, tutorialsdojo.com ALIAS AAAA -> myelb.us-west-2.elb.amazonnaws.com, this is assuming your Elastic Load Balancer has IPv6 support.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-08-30_17-37-24-0de42a388340542c43e306b5844130d2.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-08-30_17-37-24-0de42a388340542c43e306b5844130d2.png)

    **Non-Alias with a type "A" record set** is incorrect because you only use Non-Alias with a type “A” record set for IP addresses.

    **Alias with a type "CNAME" record set** is incorrect because you can't create a CNAME record at the zone apex. For example, if you register the DNS name tutorialsdojo.com, the zone apex is tutorialsdojo.com.

    **Alias with a type of “MX” record set** is incorrect because an MX record is primarily used for mail servers. It includes a priority number and a domain name, for example: `10 mailserver.tutorialsdojo.com`.

**To protect your enterprise applications against unauthorized access, you configured multiple rules for your Network ACLs in your VPC. How are the access rules evaluated?**

- ​By default, all Network ACL Rules are evaluated before any traffic is allowed or denied.
- ​Network ACL Rules are evaluated by rule number, from lowest to highest, and executed after all rules are checked for conflicting allow/deny rules.
- ​Network ACL Rules are evaluated by rule number, from highest to lowest and are executed immediately when a matching allow/deny rule is found.
- ​Network ACL Rules are evaluated by rule number, from lowest to highest, and executed immediately when a matching allow/deny rule is found.

### **Explanation**

- Answer

    A **network access control list (ACL)** is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. You might set up network ACLs with rules similar to your security groups in order to add an additional layer of security to your VPC.

    Network ACL Rules are evaluated by rule number, from lowest to highest, and executed immediately when a matching allow/deny rule is found.

    ![https://docs.aws.amazon.com/vpc/latest/userguide/images/nacl-example-diagram.png](https://docs.aws.amazon.com/vpc/latest/userguide/images/nacl-example-diagram.png)

    The option that says: **Network ACL Rules are evaluated by rule number, from highest to lowest and are executed immediately when a matching allow/deny rule is found** is incorrect since rules are evaluated from lowest to highest, not the other way around.

    The option that says: **By default, all Network ACL Rules are evaluated before any traffic is allowed or denied** is incorrect because the Network ACL Rules are evaluated by rule number, from lowest to highest, and executed immediately when a matching allow/deny rule is found.

    The option that says: **Network ACL Rules are evaluated by rule number, from lowest to highest, and executed after all rules are checked for conflicting allow/deny rules** is incorrect since rules are executed immediately when a match is found and not after all rules are checked for conflicting allow/deny rules.

 

⭐️

**As part of the Business Continuity Plan of your company, your IT Director instructed you to set up an automated backup of all of the EBS Volumes for your EC2 instances as soon as possible. What is the fastest and most cost-effective solution to automatically back up all of your EBS Volumes?**

- ​For an automated solution, create a scheduled job that calls the "create-snapshot" command via the AWS CLI to take a snapshot of production EBS volumes periodically.
- ​Set your Amazon Storage Gateway with EBS volumes as the data source and store the backups in your on-premises servers through the storage gateway.
- ​Use an EBS-cycle policy in Amazon S3 to automatically back up the EBS volumes.
- ​Use Amazon Data Lifecycle Manager (Amazon DLM) to automate the creation of EBS snapshots.

### **Explanation**

- Answer

    You can use Amazon Data Lifecycle Manager (Amazon DLM) to automate the creation, retention, and deletion of snapshots taken to back up your Amazon EBS volumes. Automating snapshot management helps you to:

    - Protect valuable data by enforcing a regular backup schedule.

    - Retain backups as required by auditors or internal compliance.

    - Reduce storage costs by deleting outdated backups.

    Combined with the monitoring features of Amazon CloudWatch Events and AWS CloudTrail, Amazon DLM provides a complete backup solution for EBS volumes at no additional cost.

    Hence, **using Amazon Data Lifecycle Manager (Amazon DLM) to automate the creation of EBS snapshots** is the correct answer as it is the fastest and most cost-effective solution that provides an automated way of backing up your EBS volumes.

    The option that says: **For an automated solution, create a scheduled job that calls the "create-snapshot" command via the AWS CLI to take a snapshot of production EBS volumes periodically** is incorrect because even though this is a valid solution, you would still need additional time to create a scheduled job that calls the "create-snapshot" command. It would be better to use Amazon Data Lifecycle Manager (Amazon DLM) instead as this provides you the fastest solution which enables you to automate the creation, retention, and deletion of the EBS snapshots without having to write custom shell scripts or creating scheduled jobs.

    **Setting your Amazon Storage Gateway with EBS volumes as the data source and storing the backups in your on-premises servers through the storage gateway** is incorrect as the Amazon Storage Gateway is used only for creating a backup of data from your on-premises server and not from the Amazon Virtual Private Cloud.

    **Using an EBS-cycle policy in Amazon S3 to automatically back up the EBS volumes** is incorrect as there is no such thing as EBS-cycle policy in Amazon S3.

⭐️

**You are a Solutions Architect working with a company that uses Chef Configuration management in their datacenter. Which service is designed to let the customer leverage existing Chef recipes in AWS?**

- ​AWS Elastic Beanstalk
- ​AWS CloudFormation
- ​Amazon Simple Workflow Service
- ​AWS OpsWorks

### **Explanation**

- Answer

    AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet. Chef and Puppet are automation platforms that allow you to use code to automate the configurations of your servers. OpsWorks lets you use Chef and Puppet to automate how servers are configured, deployed, and managed across your Amazon EC2 instances or on-premises compute environments. OpsWorks has three offerings - AWS Opsworks for Chef Automate, AWS OpsWorks for Puppet Enterprise, and AWS OpsWorks Stacks.

    ![https://media.amazonwebservices.com/blog/2016/opsworks_chef_auto_welcome_1.png](https://media.amazonwebservices.com/blog/2016/opsworks_chef_auto_welcome_1.png)

    **Amazon Simple Workflow Service** is incorrect because AWS SWF is a fully-managed state tracker and task coordinator in the Cloud. It does not let you leverage Chef recipes.

    **AWS Elastic Beanstalk** is incorrect because this handles an application's deployment details of capacity provisioning, load balancing, auto-scaling, and application health monitoring. It does not let you leverage Chef recipes just like Amazon SWF.

    **AWS CloudFormation** is incorrect because this is a service that lets you create a collection of related AWS resources and provision them in a predictable fashion using infrastructure as code. It does not let you leverage Chef recipes just like Amazon SWF and AWS Elastic Beanstalk.

**One of your EC2 instances is reporting an unhealthy system status check. The operations team is looking for an easier way to monitor and repair these instances instead of fixing them manually.How will you automate the monitoring and repair of the system status check failure in an AWS environment?**

- ​Write a python script that queries the EC2 API for each instance status check
- ​Create CloudWatch alarms that stop and start the instance based on status check alarms.
- ​Buy and implement a third party monitoring tool.
- ​Write a shell script that periodically shuts down and starts instances based on certain stats.

### **Explanation**

- Answer

    Using Amazon CloudWatch alarm actions, you can create alarms that automatically stop, terminate, reboot, or recover your EC2 instances. You can use the stop or terminate actions to help you save money when you no longer need an instance to be running. You can use the reboot and recover actions to automatically reboot those instances or recover them onto new hardware if a system impairment occurs.

    **Writing a python script that queries the EC2 API for each instance status check**, **writing a shell script that periodically shuts down and starts instances based on certain stats**, and **buying and implementing a third party monitoring tool** are all incorrect because it is unnecessary to go through such lengths when CloudWatch Alarms already has such a feature for you, offered at a low cost.

**You work for a leading university as an AWS Infrastructure Engineer and also as a professor to aspiring AWS architects. As a way to familiarize your students with AWS, you gave them a project to host their applications to an EC2 instance. One of your students created an instance to host their online enrollment system project but is having a hard time connecting to their newly created EC2 instance. Your students have explored all of the troubleshooting guides by AWS and narrowed it down to login issues. Which of the following can you use to log into an EC2 instance?**

- ​EC2 Connection Strings
- ​Custom EC2 password
- ​Access Keys
- ​Key Pairs

### **Explanation**

- Answer

    Amazon EC2 uses public–key cryptography to encrypt and decrypt login information. Public–key cryptography uses a public key to encrypt a piece of data, such as a password, then the recipient uses the private key to decrypt the data. The public and private keys are known as a *key pair*.

    To log in to your instance, you must create a key pair, specify the name of the key pair when you launch the instance, and provide the private key when you connect to the instance. On a Linux instance, the public key content is placed in an entry within `~/.ssh/authorized_keys`. This is done at boot time and enables you to securely access your instance using the private key instead of a password.

    **Custom EC2 password** and **EC2 Connection Strings** are incorrect as both do not exist.

    **Access Keys** is incorrect as these are used for API calls and not for logging in to EC2.

⭐️

**Your customer is building an internal application that serves as a repository for images uploaded by a couple of users. Whenever a user uploads an image, it would be sent to Kinesis for processing before it is stored in an S3 bucket. Afterwards, if the upload was successful, the application will return a prompt telling the user that the upload is successful. The entire processing typically takes about 5 minutes to finish.Which of the following options will allow you to asynchronously process the request to the application in the most cost-effective manner?**

- ​Create a Lambda function that will asynchronously process the requests.
- ​Use a combination of SNS to buffer the requests and then asynchronously process them using On-Demand EC2 Instances.
- ​Use a combination of SQS to queue the requests and then asynchronously process them using On-Demand EC2 Instances.
- ​Use a combination of Lambda and Step Functions to orchestrate service components and asynchronously process the requests.

### **Explanation**

- Answer

    AWS Lambda supports synchronous and asynchronous invocation of a Lambda function. You can control the invocation type only when you invoke a Lambda function. When you use an AWS service as a trigger, the invocation type is predetermined for each service. You have no control over the invocation type that these event sources use when they invoke your Lambda function. Since the processing only takes 5 minutes, Lambda is also a cost-effective choice.

    ![https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-RealTimeStreamProcessing.d79d55b5f3a5d6b58142a6c0fc8a29eadc81c02b.png](https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-RealTimeStreamProcessing.d79d55b5f3a5d6b58142a6c0fc8a29eadc81c02b.png)

    **Using a combination of Lambda and Step Functions to orchestrate service components and asynchronously process the requests** is incorrect because the AWS Step Functions service lets you coordinate multiple AWS services into serverless workflows so you can build and update apps quickly. Although this can be a valid solution, it is not cost-effective since the application does not have a lot of components to orchestrate. Lambda functions can effectively meet the requirements in this scenario without using Step Functions. This service is not as cost-effective as Lambda.

    **Using a combination of SQS to queue the requests and then asynchronously processing them using On-Demand EC2 Instances** and **Using a combination of SNS to buffer the requests and then asynchronously processing them using On-Demand EC2 Instances** are both incorrect as using On-Demand EC2 instances is not cost-effective. It is better to use a Lambda function instead.

⭐️

**Your company just recently adopted a hybrid architecture that integrates their on-premises data center to their AWS cloud. You are assigned to configure the VPC as well as to implement the required IAM users, IAM roles, IAM groups and IAM policies.In this scenario, what is a best practice when creating IAM policies?**

- ​Use the principle of least privilege which means granting only the least number of people with full root access.
- ​Grant all permissions to any EC2 user.
- ​Use the principle of least privilege which means granting only the permissions required to perform a task.
- ​Determine what users need to do and then craft policies for them that let the users perform those tasks including additional administrative operations.

### **Explanation**

- Answer

    One of the best practices in Amazon IAM is to **grant least privilege**.

    When you create IAM policies, follow the standard security advice of granting *least privilege*—that is, granting only the permissions required to perform a task. Determine what users need to do and then craft policies for them that let the users perform *only* those tasks. Therefore, **using the principle of least privilege which means granting only the permissions required to perform a task** is the correct answer.

    Start with a minimum set of permissions and grant additional permissions as necessary.

    Defining the right set of permissions requires some understanding of the user's objectives. Determine what is required for the specific task, what actions a particular service supports, and what permissions are required in order to perform those actions.

    **Granting all permissions to any EC2 user** is incorrect since you don't want your users to gain access to everything and perform unnecessary actions. Doing so is not a good security practice.

    **Using the principle of least privilege which means granting only the least number of people with full root access** is incorrect because this is not the correct definition of what the principle of least privilege is.

    **Determining what users need to do and then craft policies for them that let the users perform those tasks including additional administrative operations** is incorrect as well since there are some users who you should not give administrative access to. You should follow the principle of least privilege when providing permissions and accesses to your resources.

**You are building a transcription service for a company in which a fleet of EC2 worker instances processes an uploaded audio file and generates a text file as an output. You must store both of these frequently accessed files in the same durable storage until the text file is retrieved by the uploader. Due to an expected surge in demand, you have to ensure that the storage is scalable and can be retrieved within minutes.Which storage option in AWS can you use in this situation, which is both cost-efficient and scalable?**

- ​A single Amazon S3 bucket
- ​Multiple Amazon EBS volume with snapshots
- ​Amazon S3 Glacier Deep Archive
- ​Multiple instance stores

### **Explanation**

- Answer

    In this scenario, the best option is to use Amazon S3. It’s a simple storage service that offers a highly-scalable, reliable, and low-latency data storage infrastructure at very low costs.

    **Multiple Amazon EBS volume with snapshots** and **Multiple instance stores** are incorrect because these services do not provide durable storage.

    **Amazon S3 Glacier Deep Archive** is incorrect because this is mainly used for data archives with data retrieval times that can take more than 12 hours. Hence, it is not suitable for the transcription service where the data are stored and frequently accessed.

⭐️

**You are working for a central bank as the Principal AWS Solutions Architect. Due to compliance requirements and security concerns, you are tasked to implement strict access to the central bank's AWS resources using the AWS Identity and Access Management service. Which of the following can you manage in the IAM dashboard? (Select TWO.)**

- [ ]  ​Network Access Control List
- [ ]  ​Cost Allocation Reports
- [ ]  ​Identity providers
- [ ]  ​Groups
- [ ]  ​Security Groups

### **Explanation**

- Answer

    AWS Identity and Access Management (IAM) is a web service for securely controlling access to AWS services. With IAM, you can centrally manage users, security credentials such as access keys, and permissions that control which AWS resources users and applications can access.

    ![https://docs.aws.amazon.com/IAM/latest/UserGuide/images/intro-diagram%20_policies_800.png](https://docs.aws.amazon.com/IAM/latest/UserGuide/images/intro-diagram%20_policies_800.png)

    **Groups** is correct because an IAM group is a collection of IAM users. Groups let you specify permissions for multiple users, which can make it easier to manage the permissions for those users.

    **Identity providers** is correct as you can manage identity providers using IAM Dashboard instead of creating IAM users in your AWS account. With an identity provider (IdP), you can manage your user identities outside of AWS and give these external user identities permission to use AWS resources in your account.

    **Cost Allocation Reports** is incorrect because these are under AWS Billing and Cost Management.

    **Security Groups** is incorrect because this can be managed in the EC2 console and not in the IAM dashboard.

    **Network Access Control List** is incorrect because this is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets while security groups act as virtual firewall for your instance to control inbound and outbound traffic, both of which cannot be managed in the IAM dashboard.

**One member of your DevOps team consulted you about a connectivity problem in one of your Amazon EC2 instances. The application architecture is initially set up with four EC2 instances, each with an EIP address that all belong to a public non-default subnet. You launched another instance to handle the increasing workload of your application. The EC2 instances also belong to the same security group. Everything works well as expected except for one of the EC2 instances which is not able to send nor receive traffic over the Internet.Which of the following is the MOST likely reason for this issue?**

- ​The EC2 instance does not have a private IP address associated with it.
- ​The EC2 instance is running in an Availability Zone that is not connected to an Internet gateway.
- ​The EC2 instance does not have a public IP address associated with it.
- ​The route table is not properly configured to allow traffic to and from the Internet through the Internet gateway.

### **Explanation**

- Answer

    IP addresses enable resources in your VPC to communicate with each other, and with resources over the Internet. Amazon EC2 and Amazon VPC support the IPv4 and IPv6 addressing protocols.

    By default, Amazon EC2 and Amazon VPC use the IPv4 addressing protocol. When you create a VPC, you must assign it an IPv4 CIDR block (a range of private IPv4 addresses). Private IPv4 addresses are not reachable over the Internet. To connect to your instance over the Internet, or to enable communication between your instances and other AWS services that have public endpoints, you can assign a globally-unique public IPv4 address to your instance.

    You can optionally associate an IPv6 CIDR block with your VPC and subnets, and assign IPv6 addresses from that block to the resources in your VPC. IPv6 addresses are public and reachable over the Internet.

    ![https://docs.aws.amazon.com/vpc/latest/userguide/images/case-1.png](https://docs.aws.amazon.com/vpc/latest/userguide/images/case-1.png)

    All subnets have a modifiable attribute that determines whether a network interface created in that subnet is assigned a public IPv4 address and, if applicable, an IPv6 address. This includes the primary network interface (eth0) that's created for an instance when you launch an instance in that subnet. Regardless of the subnet attribute, you can still override this setting for a specific instance during launch.

    By default, nondefault subnets have the IPv4 public addressing attribute set to **`false`**, and default subnets have this attribute set to `true`. An exception is a nondefault subnet created by the Amazon EC2 launch instance wizard — the wizard sets the attribute to `true`. You can modify this attribute using the Amazon VPC console.

    In this scenario, there are 5 EC2 instances that belong to the same security group that should be able to connect to the Internet. The main route table is properly configured but there is a problem connecting to one instance. Since the other four instances are working fine, we can assume that the security group and the route table are correctly configured. One possible reason for this issue is that the problematic instance does not have a public or an EIP address.

    Take note as well that the four EC2 instances all belong to a public **non-default** subnet. Which means that a new EC2 instance will not have a public IP address by default since the since IPv4 public addressing attribute is initially set to `false.`

    Hence, the correct answer is the option that says: ***The EC2 instance does not have a public IP address associated with it.***

    The option that says: ***The route table is not properly configured to allow traffic to and from the Internet through the Internet gateway*** is incorrect because the other three instances, which are associated with the same route table and security group, do not have any issues.

    The option that says: ***The EC2 instance is running in an Availability Zone that is not connected to an Internet gateway*** is incorrect because there is no relationship between the Availability Zone and the Internet Gateway (IGW) that may have caused the issue.

⭐️

**You are working for a University as their AWS Consultant. They want to have a disaster recovery strategy in AWS for mission-critical applications after suffering a disastrous outage wherein they lost student and employee records. They don't want this to happen again but at the same time want to minimize the monthly costs. You are instructed to set up a minimal version of the application that is always available in case of any outages. The DR site should only run the most critical core elements of your system in AWS to save cost which can be rapidly upgraded to a full-scale production environment in the event of system outages.Which of the following disaster recovery architectures is the most cost-effective type to use in this scenario?**

- ​Pilot Light
- ​Backup & Restore
- ​Multi Site
- ​Warm Standby

### **Explanation**

- Answer

    The correct answer is **Pilot Light**.

    The term pilot light is often used to describe a DR scenario in which a minimal version of an environment is always running in the cloud. The idea of the pilot light is an analogy that comes from the gas heater. In a gas heater, a small flame that’s always on can quickly ignite the entire furnace to heat up a house. This scenario is similar to a backup-and-restore scenario.

    For example, with AWS you can maintain a pilot light by configuring and running the most critical core elements of your system in AWS. When the time comes for recovery, you can rapidly provision a full-scale production environment around the critical core.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-02-13_01-09-16-5d7907b9394b71dc4064a6e8abae0647.jpg](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-02-13_01-09-16-5d7907b9394b71dc4064a6e8abae0647.jpg)

    **Backup & Restore** is incorrect because you are running mission-critical applications, and the speed of recovery from backup and restore solution might not meet your RTO and RPO.

    **Warm Standby** is incorrect. Warm standby is a method of redundancy in which the scaled-down secondary system runs in the background of the primary system. Doing so would not optimize your savings as much as running a pilot light recovery since some of your services are always running in the background.

    **Multi Site** is incorrect as well. Multi-site is the most expensive solution out of disaster recovery solutions. You are trying to save monthly costs so this should be the least probable choice for you.

⭐️

**You are working as a Solutions Architect for an investment bank and your Chief Technical Officer intends to migrate all of your applications to AWS. You are looking for block storage to store all of your data and have decided to go with EBS volumes. Your boss is worried that EBS volumes are not appropriate for your workloads due to compliance requirements, downtime scenarios, and IOPS performance. Which of the following are valid points in proving that EBS is the best service to use for your migration? (Select TWO.)**

- [ ]  ​When you create an EBS volume in an Availability Zone, it is automatically replicated on a separate AWS region to prevent data loss due to a failure of any single hardware component.
- [ ]  ​EBS volumes can be attached to any EC2 Instance in any Availability Zone.
- [ ]  ​An EBS volume is off-instance storage that can persist independently from the life of an instance.
- [ ]  ​EBS volumes support live configuration changes while in production which means that you can modify the volume type, volume size, and IOPS capacity without service interruptions.
- [ ]  ​Amazon EBS provides the ability to create snapshots (backups) of any EBS volume and write a copy of the data in the volume to Amazon RDS, where it is stored redundantly in multiple Availability Zones

### **Explanation**

- Answer

    An Amazon EBS volume is a durable, block-level storage device that you can attach to a single EC2 instance. You can use EBS volumes as primary storage for data that requires frequent updates, such as the system drive for an instance or storage for a database application. You can also use them for throughput-intensive applications that perform continuous disk scans. EBS volumes persist independently from the running life of an EC2 instance.

    Here is a list of important information about EBS Volumes:

    - When you create an EBS volume in an Availability Zone, it is automatically replicated within that zone to prevent data loss due to a failure of any single hardware component.

    - An EBS volume can only be attached to one EC2 instance at a time.

    - After you create a volume, you can attach it to any EC2 instance in the same Availability Zone

    - An EBS volume is off-instance storage that can persist independently from the life of an instance. You can specify not to terminate the EBS volume when you terminate the EC2 instance during instance creation.

    - EBS volumes support live configuration changes while in production which means that you can modify the volume type, volume size, and IOPS capacity without service interruptions.

    - Amazon EBS encryption uses 256-bit Advanced Encryption Standard algorithms (AES-256)

    - EBS Volumes offer 99.999% SLA.

    The option that says: **When you create an EBS volume in an Availability Zone, it is automatically replicated on a separate AWS region to prevent data loss due to a failure of any single hardware component** is incorrect because when you create an EBS volume in an Availability Zone, it is automatically replicated within that zone only, and not on a separate AWS region, to prevent data loss due to a failure of any single hardware component.

    The option that says: **EBS volumes can be attached to any EC2 Instance in any Availability Zone** is incorrect as EBS volumes can only be attached to an EC2 instance in the same Availability Zone.

    The option that says: **Amazon EBS provides the ability to create snapshots (backups) of any EBS volume and write a copy of the data in the volume to Amazon RDS, where it is stored redundantly in multiple Availability Zones** is almost correct. But instead of storing the volume to Amazon RDS, the EBS Volume snapshots are actually sent to Amazon S3.

⭐️

**In Elastic Load Balancing, there are various security features that you can use such as Server Order Preference, Predefined Security Policy, Perfect Forward Secrecy and many others. Perfect Forward Secrecy is a feature that provides additional safeguards against the eavesdropping of encrypted data through the use of a unique random session key. This prevents the decoding of captured data, even if the secret long-term key is compromised. Perfect Forward Secrecy is used to offer SSL/TLS cipher suites for which two AWS services?**

- ​Trusted Advisor and GovCloud
- ​CloudTrail and CloudWatch
- ​EC2 and S3
- ​CloudFront and Elastic Load Balancing

### **Explanation**

- Answer

    Perfect Forward Secrecy is a feature that provides additional safeguards against the eavesdropping of encrypted data, through the use of a unique random session key. This prevents the decoding of captured data, even if the secret long-term key is compromised.

    CloudFront and Elastic Load Balancing are the two AWS services that support Perfect Forward Secrecy. Hence, the correct answer is: **CloudFront and Elastic Load Balancing**.

    **EC2 and S3**, **CloudTrail and CloudWatch**, and **Trusted Advisor and GovCloud** are incorrect since these services do not use Perfect Forward Secrecy. SSL/TLS is commonly used when you have sensitive data travelling through the public network.

⭐️

**A company is hosting its web application in an Auto Scaling group of EC2 instances behind an Application Load Balancer. Recently, the Solutions Architect identified a series of SQL injection attempts and cross-site scripting attacks to the application, which had adversely affected their production data.Which of the following should the Architect implement to mitigate this kind of attack?**

- ​Block all the IP addresses where the SQL injection and cross-site scripting attacks originated using the Network Access Control List.
- ​Set up security rules that block SQL injection and cross-site scripting attacks in AWS Web Application Firewall (WAF). Associate the rules to the Application Load Balancer.
- ​Use Amazon Guard​Duty to prevent any further SQL injection and cross-site scripting attacks in your application.
- ​Using AWS Firewall Manager, set up security rules that block SQL injection and cross-site scripting attacks. Associate the rules to the Application Load Balancer.

### **Explanation**

- Answer

    **AWS WAF** is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon API Gateway API, Amazon CloudFront or an Application Load Balancer. AWS WAF also lets you control access to your content. Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings, API Gateway, CloudFront or an Application Load Balancer responds to requests either with the requested content or with an HTTP 403 status code (Forbidden). You also can configure CloudFront to return a custom error page when a request is blocked.

    ![https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2018/11/19/waf-archs2-1024x354.png](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2018/11/19/waf-archs2-1024x354.png)

    At the simplest level, AWS WAF lets you choose one of the following behaviors:

    **Allow all requests except the ones that you specify** – This is useful when you want CloudFront or an Application Load Balancer to serve content for a public website, but you also want to block requests from attackers.

    **Block all requests except the ones that you specify** – This is useful when you want to serve content for a restricted website whose users are readily identifiable by properties in web requests, such as the IP addresses that they use to browse to the website.

    **Count the requests that match the properties that you specify** – When you want to allow or block requests based on new properties in web requests, you first can configure AWS WAF to count the requests that match those properties without allowing or blocking those requests. This lets you confirm that you didn't accidentally configure AWS WAF to block all the traffic to your website. When you're confident that you specified the correct properties, you can change the behavior to allow or block requests.

    Hence, the correct answer in this scenario is: ***Set up security rules that block SQL injection and cross-site scripting attacks in AWS Web Application Firewall (WAF). Associate the rules to the Application Load Balancer.***

    ***Using Amazon Guard​Duty to prevent any further SQL injection and cross-site scripting attacks in your application*** is incorrect because Amazon Guard​Duty is just a threat detection service that continuously monitors for malicious activity and unauthorized behavior to protect your AWS accounts and workloads.

    ***Using AWS Firewall Manager to set up security rules that block SQL injection and cross-site scripting attacks, then associating the rules to the Application Load Balancer*** is incorrect because the AWS Firewall Manager just simplifies your AWS WAF and AWS Shield Advanced administration and maintenance tasks across multiple accounts and resources.

    ***Blocking all the IP addresses where the SQL injection and cross-site scripting attacks originated using the Network Access Control List*** is incorrect because this is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. NACLs are not effective in blocking SQL injection and cross-site scripting attacks

**You are working for an advertising company as their Senior Solutions Architect handling the S3 storage data. Your company has terabytes of data sitting on AWS S3 standard storage class, which accumulates significant operational costs. The management wants to cut down on the cost of their cloud infrastructure so you were instructed to switch to Glacier to lessen the cost per GB storage. The Amazon Glacier storage service is primarily used for which use case? (Select TWO.)**

- [ ]  ​Used for active database storage
- [ ]  ​Storing infrequently accessed data
- [ ]  ​Storing cached session data
- [ ]  ​Used as a data warehouse
- [ ]  ​Storing Data archives

### **Explanation**

- Answer

    Amazon S3 Glacier is an extremely low-cost storage service that provides secure, durable, and flexible storage for data backup and archival. Amazon Glacier is designed to store data that is infrequently accessed. Amazon Glacier enables customers to offload the administrative burdens of operating and scaling storage to AWS so that they don’t have to worry about capacity planning, hardware provisioning, data replication, hardware failure detection and repair, or time-consuming hardware migrations.

    **Storing cached session data** is incorrect because this is the main use case for ElastiCache and not Amazon Glacier.

    The option that says: **Used for active database storage** is incorrect because you should use RDS or DynamoDB for your active database storage as S3, in general, is used for storing your data or files.

    The option that says: **Used as a data warehouse** is incorrect because storing it for data warehousing is the main use case of Amazon Redshift. It does not meet the requirement of being able to archive your infrequently accessed data. You can use S3 standard instead for frequently accessed data or Glacier for infrequently accessed data and archiving.

    It is advisable to transition the standard data to infrequent access first then transition it to Amazon Glacier. You can specify in the lifecycle rule the time it will sit in standard tier and infrequent access. You can also delete the objects after a certain amount of time.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-11-12_21-01-50-8e238b3286aa6c7c72f18b468ce19ead.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-11-12_21-01-50-8e238b3286aa6c7c72f18b468ce19ead.png)

    In transitioning S3 standard to Glacier you need to tell S3 which objects are to be archived to the new Glacier storage option, and under what conditions. You do this by setting up a lifecycle rule using the following elements:

    A prefix to specify which objects in the bucket are subject to the policy.

    A relative or absolute time specifier and a time period for transitioning objects to Glacier. The time periods are interpreted with respect to the object’s creation date. They can be relative (migrate items that are older than a certain number of days) or absolute (migrate items on a specific date)

    An object age at which the object will be deleted from S3. This is measured from the original PUT of the object into the service, and the clock is not reset by a transition to Glacier.

    You can create a lifecycle rule in the AWS Management Console.

**A start-up company that offers an intuitive financial data analytics service has consulted you about their AWS architecture. They have a fleet of Amazon EC2 worker instances that process financial data and then outputs reports which are used by their clients. You must store the generated report files in a durable storage. The number of files to be stored can grow over time as the start-up company is expanding rapidly overseas and hence, they also need a way to distribute the reports faster to clients located across the globe. Which of the following is a cost-efficient and scalable storage option that you should use for this scenario?**

- ​Use Amazon Glacier as the data storage and ElastiCache as the CDN.
- ​Use multiple EC2 instance stores for data storage and ElastiCache as the CDN.
- ​Use Amazon S3 as the data storage and CloudFront as the CDN.
- ​Use Amazon Redshift as the data storage and CloudFront as the CDN.

### **Explanation**

- Answer

    A Content Delivery Network (CDN) is a critical component of nearly any modern web application. It used to be that CDN merely improved the delivery of content by replicating commonly requested files (static content) across a globally distributed set of caching servers. However, CDNs have become much more useful over time.

    For caching, a CDN will reduce the load on an application origin and improve the experience of the requestor by delivering a local copy of the content from a nearby cache edge, or Point of Presence (PoP). The application origin is off the hook for opening the connection and delivering the content directly as the CDN takes care of the heavy lifting. The end result is that the application origins don’t need to scale to meet demands for static content.

    ![https://d1.awsstatic.com/product-marketing/Cloudfront-cdn-diagram-v2.1a4a693fc371d29d794d318a01dfe1aecc4c658e.PNG](https://d1.awsstatic.com/product-marketing/Cloudfront-cdn-diagram-v2.1a4a693fc371d29d794d318a01dfe1aecc4c658e.PNG)

    Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment. CloudFront is integrated with AWS – both physical locations that are directly connected to the AWS global infrastructure, as well as other AWS services.

    ***Amazon S3*** offers a highly durable, scalable, and secure destination for backing up and archiving your critical data. This is the correct option as the start-up company is looking for a durable storage to store the audio and text files. In addition, ElastiCache is only used for caching and not specifically as a Global Content Delivery Network (CDN).

    ***Using Amazon Redshift as the data storage and CloudFront as the CDN*** is incorrect as Amazon Redshift is usually used as a Data Warehouse.

    ***Using Amazon S3 Glacier as the data storage and ElastiCache as the CDN*** is incorrect as Amazon S3 Glacier is usually used for data archives.

    ***Using multiple EC2 instance stores for data storage and ElastiCache as the CDN*** is incorrect as data stored in an instance store is not durable.

**You have built a web application that checks for new items in an S3 bucket once every hour. If new items exist, a message is added to an SQS queue. You have a fleet of EC2 instances which retrieve messages from the SQS queue, process the file, and finally, send you and the user an email confirmation that the item has been successfully processed. Your officemate uploaded one test file to the S3 bucket and after a couple of hours, you noticed that you and your officemate have 50 emails from your application with the same message.Which of the following is most likely the root cause why the application has sent you and the user multiple emails?**

- ​The sqsSendEmailMessage attribute of the SQS queue is configured to 50.
- ​Your application does not issue a delete command to the SQS queue after processing the message, which is why this message went back to the queue and was processed multiple times.
- ​By default, SQS automatically deletes the messages that were processed by the consumers. It might be possible that your officemate has submitted the request 50 times which is why you received a lot of emails.
- ​There is a bug in the application.

### **Explanation**

- Answer

    In this scenario, the main culprit is that your application does not issue a delete command to the SQS queue after processing the message, which is why this message went back to the queue and was processed multiple times.

    The option that says: **The sqsSendEmailMessage attribute of the SQS queue is configured to 50** is incorrect as there is no sqsSendEmailMessage attribute in SQS.

    The option that says: **There is a bug in the application** is a valid answer but since the scenario did not mention that the EC2 instances deleted the processed messages, the most likely cause of the problem is that the application does not issue a delete command to the SQS queue as mentioned above.

    The option that says: **By default, SQS automatically deletes the messages that were processed by the consumers. It might be possible that your officemate has submitted the request 50 times which is why you received a lot of emails** is incorrect as SQS does not automatically delete the messages.

⭐️

**Your fellow AWS Engineer has created a new Standard-class S3 bucket to store financial reports that are not frequently accessed but should be immediately available when an auditor requests for it. To save costs, you changed the storage class of the S3 bucket from Standard to Infrequent Access storage class. In Amazon S3 Standard - Infrequent Access storage class, which of the following statements are true? (Select TWO.)**

- [ ]  ​Ideal to use for data archiving.
- [ ]  ​It is designed for data that requires rapid access when needed.
- [ ]  ​It is designed for data that is accessed less frequently.
- [ ]  ​It is the best storage option to store noncritical and reproducible data
- [ ]  ​It provides high latency and low throughput performance

### **Explanation**

- Answer

    Amazon S3 Standard - Infrequent Access (Standard - IA) is an Amazon S3 storage class for data that is accessed less frequently, but requires rapid access when needed. Standard - IA offers the high durability, throughput, and low latency of Amazon S3 Standard, with a low per GB storage price and per GB retrieval fee.

    This combination of low cost and high performance make Standard - IA ideal for long-term storage, backups, and as a data store for disaster recovery. The Standard - IA storage class is set at the object level and can exist in the same bucket as Standard, allowing you to use lifecycle policies to automatically transition objects between storage classes without any application changes.

    **Key Features:**

    - Same low latency and high throughput performance of Standard

    - Designed for durability of 99.999999999% of objects

    - Designed for 99.9% availability over a given year

    - Backed with the Amazon S3 Service Level Agreement for availability

    - Supports SSL encryption of data in transit and at rest

    - Lifecycle management for automatic migration of objects

    The option that says: **It is the best storage option to store noncritical and reproducible data** is incorrect as it actually refers to Amazon S3 - Reduced Redundancy Storage (RRS). In addition, RRS will be completely deprecated soon and AWS recommends to use S3 IA One-Zone instead.

    The option that says: **It provides high latency and low throughput performance** is incorrect as it should be "low latency" and "high throughput" instead. S3 automatically scales performance to meet user demands.

    The option that says: **Ideal to use for data archiving** is incorrect because this statement refers to Amazon S3 Glacier. Glacier is a secure, durable, and extremely low-cost cloud storage service for data archiving and long-term backup.

**For data privacy, a healthcare company has been asked to comply with the Health Insurance Portability and Accountability Act (HIPAA). They have been told that all of the data being backed up or stored on Amazon S3 must be encrypted.What is the best option to do this? (Select TWO.)**

- [ ]  ​Enable Server-Side Encryption on an S3 bucket to make use of AES-256 encryption.
- [ ]  ​Enable Server-Side Encryption on an S3 bucket to make use of AES-128 encryption.
- [ ]  ​Before sending the data to Amazon S3 over HTTPS, encrypt the data locally first using your own encryption keys.
- [ ]  ​Store the data in encrypted EBS snapshots.
- [ ]  ​Store the data on EBS volumes with encryption enabled instead of using Amazon S3.

### **Explanation**

- Answer

    Server-side encryption is about data encryption at rest—that is, Amazon S3 encrypts your data at the object level as it writes it to disks in its data centers and decrypts it for you when you access it. As long as you authenticate your request and you have access permissions, there is no difference in the way you access encrypted or unencrypted objects. For example, if you share your objects using a pre-signed URL, that URL works the same way for both encrypted and unencrypted objects.

    ![https://d1.awsstatic.com/security-center/SecurityBlog/bucket_policies_defense_s3.43e6c93a095f2f55b33b30276f4782ab9ec79f47.png](https://d1.awsstatic.com/security-center/SecurityBlog/bucket_policies_defense_s3.43e6c93a095f2f55b33b30276f4782ab9ec79f47.png)

    You have three mutually exclusive options depending on how you choose to manage the encryption keys:

    Use Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)

    Use Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS)

    Use Server-Side Encryption with Customer-Provided Keys (SSE-C)

    The options that say: **Before sending the data to Amazon S3 over HTTPS, encrypt the data locally first using your own encryption keys** and **Enable Server-Side Encryption on an S3 bucket to make use of AES-256 encryption** are correct because these options are using client-side encryption and Amazon S3-Managed Keys (SSE-S3) respectively. *Client-side encryption* is the act of encrypting data before sending it to Amazon S3 while SSE-S3 uses AES-256 encryption.

    **Storing the data on EBS volumes with encryption enabled instead of using Amazon S3** and **storing the data in encrypted EBS snapshots** are incorrect because both options use EBS encryption and not S3.

    **Enabling Server-Side Encryption on an S3 bucket to make use of AES-128 encryption** is incorrect as S3 doesn't provide AES-128 encryption, only AES-256.

**You are working as a Solutions Architect for a leading commercial bank which has recently adopted a hybrid cloud architecture. You have to ensure that the required data security is in place on all of their AWS resources to meet the strict financial regulatory requirements. In the AWS Shared Responsibility Model, which security aspects are the responsibilities of the customer? (Select TWO.)**

- [ ]  ​IAM Policies and Credentials Management
- [ ]  ​Virtualization infrastructure
- [ ]  ​OS Patching of an EC2 instance
- [ ]  ​Physical security of hardware
- [ ]  ​Managing the underlying network infrastructure

### **Explanation**

- Answer

    Security and Compliance is a shared responsibility between AWS and the customer. This shared model can help relieve customer’s operational burden as AWS operates, manages and controls the components from the host operating system and virtualization layer down to the physical security of the facilities in which the service operates. The customer assumes responsibility and management of the guest operating system (including updates and security patches), other associated application software as well as the configuration of the AWS provided security group firewall.

    Customers should carefully consider the services they choose as their responsibilities vary depending on the services used, the integration of those services into their IT environment, and applicable laws and regulations. The nature of this shared responsibility also provides the flexibility and customer control that permits the deployment. This differentiation of responsibility is commonly referred to as Security “**of**” the Cloud versus Security “**in**” the Cloud.

    The shared responsibility model for infrastructure services, such as Amazon Elastic Compute Cloud (Amazon EC2) for example, specifies that AWS manages the security of the following assets:

    Facilities

    Physical security of hardware

    Network infrastructure

    Virtualization infrastructure

    You as the customer are responsible for the security of the following assets:

    Amazon Machine Images (AMIs)

    Operating systems

    Applications

    Data in transit

    Data at rest

    Data stores

    Credentials

    Policies and configuration

    For a better understanding about this topic, refer to the AWS Security Best Practices whitepaper on the reference link below and also the Shared Responsibility Model diagram:

    ![https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg](https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg)

⭐️

**You work for an Intelligence Agency as its Principal Consultant developing a missile tracking application, which is hosted on both development and production AWS accounts. Alice, the Intelligence agency’s Junior Developer, only has access to the development account. She has received security clearance to access the agency’s production account but the access is only temporary and only write access to EC2 and S3 is allowed.Which of the following allows you to issue short-lived access tokens that acts as temporary security credentials to allow access to your AWS resources?**

- ​Use AWS Cognito to issue JSON Web Tokens (JWT)
- ​Use AWS STS
- ​Use AWS SSO
- ​All of the given options are correct.

### **Explanation**

- Answer

    AWS Security Token Service (AWS STS) is the service that you can use to create and provide trusted users with temporary security credentials that can control access to your AWS resources. Temporary security credentials work almost identically to the long-term access key credentials that your IAM users can use.

    In this diagram, IAM user Alice in the Dev account (the role-assuming account) needs to access the Prod account (the role-owning account). Here’s how it works:

    Alice in the Dev account assumes an IAM role (WriteAccess) in the Prod account by calling AssumeRole.

    STS returns a set of temporary security credentials.

    Alice uses the temporary security credentials to access services and resources in the Prod account. Alice could, for example, make calls to Amazon S3 and Amazon EC2, which are granted by the WriteAccess role.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-23_06-52-31-201df4af92968773479c7a09268baf1e.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-23_06-52-31-201df4af92968773479c7a09268baf1e.png)

    **Using AWS Cognito to issue JSON Web Tokens (JWT)** is incorrect because the Amazon Cognito service is primarily used for user authentication and not for providing access to your AWS resources. A JSON Web Token (JWT) is meant to be used for user authentication and session management.

    **Using AWS SSO** is incorrect because although the AWS SSO service uses STS, it does not issue short-lived credentials by itself. AWS Single Sign-On (SSO) is a cloud SSO service that makes it easy to centrally manage SSO access to multiple AWS accounts and business applications.

    The option that says **All of the given options are correct** is incorrect as only STS has the ability to provide temporary security credentials.

⭐️

**Your client is an insurance company that utilizes SAP HANA for their day-to-day ERP operations. Since you can’t migrate this database due to customer preferences, you need to integrate it with your current AWS workload in your VPC in which you are required to establish a site-to-site VPN connection. What needs to be configured outside of the VPC for you to have a successful site-to-site VPN connection?**

- ​An EIP to the Virtual Private Gateway
- ​A dedicated NAT instance in a public subnet
- ​An Internet-routable IP address (static) of the customer gateway's external interface for the on-premises network
- ​The main route table in your VPC to route traffic through a NAT instance

### **Explanation**

- Answer

    By default, instances that you launch into a virtual private cloud (VPC) can't communicate with your own network. You can enable access to your network from your VPC by attaching a virtual private gateway to the VPC, creating a custom route table, updating your security group rules, and creating an AWS managed VPN connection.

    Although the term *VPN connection* is a general term, in the Amazon VPC documentation, a VPN connection refers to the connection between your VPC and your own network. AWS supports Internet Protocol security (IPsec) VPN connections.

    A *customer gateway* is a physical device or software application on your side of the VPN connection.

    To create a VPN connection, you must create a customer gateway resource in AWS, which provides information to AWS about your customer gateway device. Next, you have to set up an Internet-routable IP address (static) of the customer gateway's external interface.

    The following diagram illustrates single VPN connections. The VPC has an attached virtual private gateway, and your remote network includes a customer gateway, which you must configure to enable the VPN connection. You set up the routing so that any traffic from the VPC bound for your network is routed to the virtual private gateway.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-27_22-45-01-dbcb3de60063eaba73e8d2d12c61d6dc.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-10-27_22-45-01-dbcb3de60063eaba73e8d2d12c61d6dc.png)

    ***A dedicated NAT instance in a public subnet** and **the main route table in your VPC to route traffic through a NAT instance*** are incorrect since you don't need a NAT instance for you to be able to create a VPN connection.

    ***An EIP to the Virtual Private Gateway*** is incorrect since you do not attach an EIP to a VPG.
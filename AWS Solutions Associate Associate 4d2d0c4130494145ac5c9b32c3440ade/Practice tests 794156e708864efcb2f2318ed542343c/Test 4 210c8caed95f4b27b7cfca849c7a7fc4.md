# Test 4

**This practice test covers the following domains:**

- Design Resilient Architectures

- Define Performant Architecture

- Specify Secure Applications and Architectures

- Design Cost-Optimized Architectures

- Define Operationally-Excellent Architecture

On-Demand EC2 ?

Globalaccelerator vs cloudfront

Redshift Spectrum

Athena

Incur cost

Amazon VPC pricing

EBS VOlumes attached to stopped EC2 instances

Public Data Set

**A web application is hosted in an Auto Scaling group of EC2 instances deployed across multiple Availability Zones in front of an Application Load Balancer. You need to implement an SSL solution for your system to improve its security which is why you requested an SSL/TLS certificate from a third-party certificate authority (CA). Where can you safely import the SSL/TLS certificate of your application? (Select TWO.)**

- [ ]  ​IAM certificate store
- [ ]  ​AWS Certificate Manager
- [ ]  ​An S3 bucket configured with server-side encryption with customer-provided encryption keys (SSE-C)
- [ ]  ​A private S3 bucket with versioning enabled
- [ ]  ​CloudFront

### **Explanation**

adfasdfasdf

- Answer

    If you got your certificate from a third-party CA, import the certificate into ACM or upload it to the IAM certificate store. Hence, **AWS Certificate Manager** and **IAM certificate store** are the correct answers.

    ![https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2016/10/11/image1_numbereddiagram_b.png](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2016/10/11/image1_numbereddiagram_b.png)

    ACM lets you import third-party certificates from the ACM console, as well as programmatically. If ACM is not available in your region, use AWS CLI to upload your third-party certificate to the IAM certificate store.

    **A private S3 bucket with versioning enabled** and **an S3 bucket configured with server-side encryption with customer-provided encryption keys (SSE-C)** are both incorrect as S3 is not a suitable service to store the SSL certificate.

    **CloudFront** is incorrect because although you can upload certificates to CloudFront, it doesn't mean that you can import SSL certificates on it. You would not be able to export the certificate that you have loaded in CloudFront nor assign them to your EC2 or ELB instances as it would be tied to a single CloudFront distribution.

**A bank portal application is hosted in an Auto Scaling group of EC2 instances behind a Classic Load Balancer (CLB). You are required to set up the architecture so that any back-end EC2 instances that you de-register should complete the in-progress requests first before the de-registration process takes effect. Conversely, if a back-end instance fails health checks, the load balancer should not send any new requests to the unhealthy instance but should allow existing requests to complete.How will you configure your load balancer to satisfy the above requirement?**

- ​Configure Connection Draining
- ​Configure both Cross-Zone Load Balancing and Sticky Sessions
- ​Configure Sticky Sessions
- ​Configure Proxy Protocol

### **Explanation**

- Answer

    To ensure that a Classic Load Balancer stops sending requests to instances that are de-registering or unhealthy while keeping the existing connections open, use connection draining. This enables the load balancer to complete in-flight requests made to instances that are de-registering or unhealthy. Hence, **configuring Connection Draining** is the correct answer.

    When you enable connection draining, you can specify a maximum time for the load balancer to keep connections alive before reporting the instance as de-registered. The maximum timeout value can be set between 1 and 3,600 seconds (the default is 300 seconds). When the maximum time limit is reached, the load balancer forcibly closes connections to the de-registering instance.

    **Configuring Sticky Sessions** is incorrect because the sticky sessions feature is mainly used to ensure that all requests from the user during the session are sent to the same instance.

    **Configuring both Cross-Zone Load Balancing and Sticky Sessions** is incorrect because this will still not satisfy the requirement. Cross-Zone load balancing is mainly used to distribute requests evenly across the registered instances in all enabled Availability Zones. You have to enable Connection Draining.

    **Configuring Proxy Protocol** is incorrect because this is an Internet protocol used to carry connection information from the source requesting the connection to the destination for which the connection was requested.

**A Solutions Architect is designing the cloud architecture for the enterprise application suite of the company. Both the web and application tiers need to access the Internet to fetch data from public APIs. However, these servers should be inaccessible from the Internet.Which of the following steps should the Architect implement to meet the above requirements?**

- ​Deploy a NAT gateway in the private subnet and add a route to it from the public subnet where the web and application tiers are hosted.
- ​Deploy a NAT gateway in the public subnet and add a route to it from the private subnet where the web and application tiers are hosted.**(Correct)**
- ​Deploy the web and application tier instances to a public subnet and then allocate an Elastic IP address to each EC2 instance.
- ​Deploy the web and application tier instances to a private subnet and then allocate an Elastic IP address to each EC2 instance.

### **Explanation**

- Answer

    [VPCs](../VPCs%208e0201fd87d1492792363303ed4fc337.md)

    You can use a network address translation (NAT) gateway to enable instances in a private subnet to connect to the internet or other AWS services, but prevent the internet from initiating a connection with those instances. You are charged for creating and using a NAT gateway in your account.

    NAT gateway hourly usage and data processing rates apply. Amazon EC2 charges for data transfer also apply. NAT gateways are not supported for IPv6 traffic—use an egress-only internet gateway instead.

    ![https://docs.aws.amazon.com/vpc/latest/userguide/images/nat-gateway-diagram.png](https://docs.aws.amazon.com/vpc/latest/userguide/images/nat-gateway-diagram.png)

    To create a NAT gateway, you must specify the public subnet in which the NAT gateway should reside. You must also specify an Elastic IP address to associate with the NAT gateway when you create it. The Elastic IP address cannot be changed once you associate it with the NAT Gateway.

    After you've created a NAT gateway, you must update the route table associated with one or more of your private subnets to point Internet-bound traffic to the NAT gateway. This enables instances in your private subnets to communicate with the internet. Each NAT gateway is created in a specific Availability Zone and implemented with redundancy in that zone. You have a limit on the number of NAT gateways you can create in an Availability Zone.

    Hence, the correct answer is to **deploy a NAT gateway in the public subnet and add a route to it from the private subnet where the web and application tiers are hosted.**

    **Deploying the web and application tier instances to a private subnet and then allocating an Elastic IP address to each EC2 instance** is incorrect because an Elastic IP address is just a static, public IPv4 address. In this scenario, you have to use a NAT Gateway instead.

    **Deploying a NAT gateway in the private subnet and adding a route to it from the public subnet where the web and application tiers are hosted** is incorrect because you have to deploy a NAT gateway in the public subnet instead and not on a private one.

    **Deploying the web and application tier instances to a public subnet and then allocating an Elastic IP address to each EC2 instance** is incorrect because having an EIP address is irrelevant as it is only a static, public IPv4 address. Moreover, you should deploy the web and application tier in the private subnet instead of a public subnet to make it inaccessible from the Internet and then just add a NAT Gateway to allow outbound Internet connection.

**You have a web-based order processing system which is currently using a standard queue in Amazon SQS. The support team noticed that there are a lot of cases where an order was processed twice. This issue has caused a lot of trouble in your processing and made your customers very unhappy. Your IT Manager has asked you to ensure that this issue will not recur.What can you do to prevent this from happening again in the future? (Select TWO.)**

- [ ]  ​Alter the retention period in Amazon SQS.
- [ ]  ​Change the message size in SQS.
- [ ]  ​Alter the visibility timeout of SQS.
- [ ]  ​Use an Amazon SQS FIFO Queue instead.
- [ ]  ​Replace Amazon SQS and instead, use Amazon Simple Workflow service.

### **Explanation**

- Answer

    Amazon SQS FIFO (First-In-First-Out) Queues have all the capabilities of the standard queue with additional capabilities designed to enhance messaging between applications when the order of operations and events is critical, or where **duplicates can't be tolerated**, for example:

    - Ensure that user-entered commands are executed in the right order.- Display the correct product price by sending price modifications in the right order.- Prevent a student from enrolling in a course before registering for an account.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2020-03-09_11-14-42-e24d31f607e373f989c2829e2805b01e.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2020-03-09_11-14-42-e24d31f607e373f989c2829e2805b01e.png)

    Amazon SWF provides useful guarantees around task assignments. It ensures that a task is never duplicated and is assigned only once. Thus, even though you may have multiple workers for a particular activity type (or a number of instances of a decider), Amazon SWF will give a specific task to only one worker (or one decider instance). Additionally, Amazon SWF keeps at most one decision task outstanding at a time for a workflow execution. Thus, you can run multiple decider instances without worrying about two instances operating on the same execution simultaneously. These facilities enable you to coordinate your workflow without worrying about duplicate, lost, or conflicting tasks.

    The main issue in this scenario is that the order management system produces duplicate orders at times. Since the company is using SQS, there is a possibility that a message can have a duplicate in case an EC2 instance failed to delete the already processed message. To prevent this issue from happening, you have to use Amazon Simple Workflow service instead of SQS.

    Therefore, the correct answers are:

    **- *Replace Amazon SQS and instead, use Amazon Simple Workflow service.***

    ***- Use an Amazon SQS FIFO Queue instead.***

    ***Altering the retention period in Amazon SQS*** is incorrect because the retention period simply specifies if the Amazon SQS should delete the messages that have been in a queue for a certain period of time.

    ***Altering the visibility timeout of SQS*** is incorrect because for standard queues, the visibility timeout isn't a guarantee against receiving a message twice. To avoid duplicate SQS messages, it is better to design your applications to be *idempotent* (they should not be affected adversely when processing the same message more than once).

    ***Changing the message size in SQS*** is incorrect because this is not related at all in this scenario.

**A financial firm is designing an application architecture for its online trading platform that must have high availability and fault tolerance. Their Solutions Architect configured the application to use an Amazon S3 bucket located in the us-east-1 region to store large amounts of intraday financial data. The stored financial data in the bucket must not be affected even if there is an outage in one of the Availability Zones or if there's a regional service failure.What should the Architect do to avoid any costly service disruptions and ensure data durability?**

- ​Create a new S3 bucket in another region and configure Cross-Account Access to the bucket located in us-east-1.
- ​Enable Cross-Region Replication.
- ​Copy the S3 bucket to an EBS-backed EC2 instance.
- ​Create a Lifecycle Policy to regularly backup the S3 bucket to Amazon Glacier.

### **Explanation**

- Answer

    In this scenario, you need to enable Cross-Region Replication to ensure that your S3 bucket would not be affected even if there is an outage in one of the Availability Zones or a regional service failure in us-east-1. When you upload your data in S3, your objects are redundantly stored on multiple devices across multiple facilities within the region only, where you created the bucket. Thus, if there is an outage on the entire region, your S3 bucket will be unavailable if you do not enable Cross-Region Replication, which should make your data available to another region.

    ![https://d1.awsstatic.com/product-marketing/S3/S3_Replication_Diagram.7860a04edc2ba93d290ffb9a21a9718574dc08e4.jpg](https://d1.awsstatic.com/product-marketing/S3/S3_Replication_Diagram.7860a04edc2ba93d290ffb9a21a9718574dc08e4.jpg)

    Note that an Availability Zone (AZ) is more related with Amazon EC2 instances rather than Amazon S3 so if there is any outage in the AZ, the S3 bucket is usually not affected but only the EC2 instances deployed on that zone.

    Hence, the correct answer is: ***Enable Cross-Region Replication*.**

    The option that says: ***Copy the S3 bucket to an EBS-backed EC2 instance*** is incorrect because EBS is not as durable as Amazon S3. Moreover, if the Availability Zone where the volume is hosted goes down then the data will also be inaccessible.

    The option that says: ***Create a Lifecycle Policy to regularly backup the S3 bucket to Amazon Glacier*** is incorrect because Glacier is primarily used for data archival. You also need to replicate your data to another region for better durability.

    The option that says: ***Create a new S3 bucket in another region and configure Cross-Account Access to the bucket located in us-east-1*** is incorrect because Cross-Account Access in Amazon S3 is primarily used if you want to grant access to your objects to another AWS account, and not just to another AWS Region. For example, Account `MANILA` can grant another AWS account (Account `CEBU)` permission to access its resources such as buckets and objects. S3 Cross-Account Access does not replicate data from one region to another. A better solution is to enable Cross-Region Replication (CRR) instead.

**[SAA-C02] A Fortune 500 company which has numerous offices and customers around the globe has hired you as their Principal Architect. You have staff and customers that upload gigabytes to terabytes of data to a centralized S3 bucket from the regional data centers, across continents, all over the world on a regular basis. At the end of the financial year, there are thousands of data being uploaded to the central S3 bucket which is in ap-southeast-2 (Sydney) region and a lot of employees are starting to complain about the slow upload times. You were instructed by the CTO to resolve this issue as soon as possible to avoid any delays in processing their global end of financial year (EOFY) reports. Which feature in Amazon S3 enables fast, easy, and secure transfer of your files over long distances between your client and your Amazon S3 bucket?**

- ​Cross-Region Replication
- ​Multipart Upload
- ​AWS Global Accelerator
- ​Transfer Acceleration

### **Explanation**

- Answer

    **Amazon S3 Transfer Acceleration** enables fast, easy, and secure transfer of files over long distances between your client and your Amazon S3 bucket. Transfer Acceleration leverages Amazon CloudFront's globally distributed AWS Edge Locations. As data arrives at an AWS Edge Location, data is routed to your Amazon S3 bucket over an optimized network path.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2020-01-05_10-40-22-9f9d508726b9e9828a384a704259745e.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2020-01-05_10-40-22-9f9d508726b9e9828a384a704259745e.png)

    Amazon S3 Transfer Acceleration can speed up content transfers to and from Amazon S3 by as much as 50-500% for long-distance transfer of larger objects. Customers who have either web or mobile applications with widespread users or applications hosted far away from their S3 bucket can experience long and variable upload and download speeds over the Internet. S3 Transfer Acceleration (S3TA) reduces the variability in Internet routing, congestion and speeds that can affect transfers, and logically shortens the distance to S3 for remote applications. S3TA improves transfer performance by routing traffic through Amazon CloudFront’s globally distributed Edge Locations and over AWS backbone networks, and by using network protocol optimizations.

    Hence, **Transfer Acceleration** is the correct answer.

    **AWS Global Accelerator** is incorrect because this service is primarily used to optimize the path from your users to your applications which improves the performance of your TCP and UDP traffic. Using Amazon S3 Transfer Acceleration is a more suitable service for this scenario.

    **Cross-Region Replication** is incorrect because this simply enables you to automatically copy S3 objects from one bucket to another bucket that is placed in a different AWS Region or within the same Region.

    **Multipart Upload** is incorrect because this feature simply allows you to upload a single object as a set of parts. You can upload these object parts independently and in any order. If transmission of any part fails, you can retransmit that part without affecting other parts. After all parts of your object are uploaded, Amazon S3 assembles these parts and creates the object. In general, when your object size reaches 100 MB, you should consider using multipart uploads instead of uploading the object in a single operation.

**[SAA-C02] A company is using the AWS Directory Service to integrate their on-premises Microsoft Active Directory (AD) domain with their Amazon EC2 instances via an AD connector. The below identity-based policy is attached to the IAM Identities that use the AWS Directory service:{ "Version":"2012-10-17", "Statement":[ { "Sid":"DirectoryTutorialsDojo1234", "Effect":"Allow", "Action":[ "ds:*" ], "Resource":"arn:aws:ds:us-east-1:987654321012:directory/d-1234567890" }, { "Effect":"Allow", "Action":[ "ec2:*" ], "Resource":"*" } ]}Which of the following BEST describes what the above resource policy does?**

- ​Allows all AWS Directory Service (`ds`) calls as long as the resource contains the directory ID: `DirectoryTutorialsDojo1234`
- ​Allows all AWS Directory Service (`ds`) calls as long as the resource contains the directory ID: `987654321012`
- ​Allows all AWS Directory Service (`ds`) calls as long as the resource contains the directory ID: `d-1234567890`
- ​Allows all AWS Directory Service (`ds`) calls as long as the resource contains the directory name of: `DirectoryTutorialsDojo1234`

### **Explanation**

- Answer

    AWS Directory Service provides multiple ways to use Amazon Cloud Directory and Microsoft Active Directory (AD) with other AWS services. Directories store information about users, groups, and devices, and administrators use them to manage access to information and resources. AWS Directory Service provides multiple directory choices for customers who want to use existing Microsoft AD or Lightweight Directory Access Protocol (LDAP)–aware applications in the cloud. It also offers those same choices to developers who need a directory to manage users, groups, devices, and access.

    ![https://d1.awsstatic.com/Products/product-name/diagrams/directory_service_howitworks.80bfccbf2f5d1d63558ec3c086aff247147258f1.png](https://d1.awsstatic.com/Products/product-name/diagrams/directory_service_howitworks.80bfccbf2f5d1d63558ec3c086aff247147258f1.png)

    Every AWS resource is owned by an AWS account, and permissions to create or access the resources are governed by permissions policies. An account administrator can attach permissions policies to IAM identities (that is, users, groups, and roles), and some services (such as AWS Lambda) also support attaching permissions policies to resources.

    The following resource policy example allows all `ds` calls as long as the resource contains the directory ID "`d-1234567890`".

    ```
    {
     "Version":"2012-10-17",
     "Statement":[
        {
            "Sid":"VisualEditor0",
            "Effect":"Allow",
            "Action":[
                "ds:*"
             ],
                     "Resource":"arn:aws:ds:us-east-1:123456789012:directory/d-1234567890"
        },
        {
        "Effect":"Allow",
        "Action":[
            "ec2:*"
        ],
        "Resource":"*"
        }
      ]
    }
    ```

    Hence, the correct answer is the option that says: **Allows all AWS Directory Service `(ds)` calls as long as the resource contains the directory ID: `d-1234567890`**.

    The option that says: **Allows all AWS Directory Service `(ds)` calls as long as the resource contains the directory ID: `DirectoryTutorialsDojo1234`** is incorrect because `DirectoryTutorialsDojo1234` is the Statement ID (SID) and not the Directory ID.

    The option that says: **Allows all AWS Directory Service `(ds)` calls as long as the resource contains the directory ID: `987654321012`** is incorrect because the numbers: `987654321012` is the Account ID and not the Directory ID.

    The option that says: **Allows all AWS Directory Service `(ds)` calls as long as the resource contains the directory name of: `DirectoryTutorialsDojo1234`** is incorrect because `DirectoryTutorialsDojo1234` is the Statement ID (SID) and not the Directory name.

**You are a Solutions Architect working for a large multinational investment bank. They have a web application that requires a minimum of 4 EC2 instances to run to ensure that it can cater to its users across the globe. You are instructed to ensure fault tolerance of this system.Which of the following is the best option?**

- ​Deploy an Auto Scaling group with 2 instances in each of 3 Availability Zones behind an Application Load Balancer.
- ​Deploy an Auto Scaling group with 2 instances in each of 2 Availability Zones behind an Application Load Balancer.
- ​Deploy an Auto Scaling group with 1 instance in each of 4 Availability Zones behind an Application Load Balancer.
- ​Deploy an Auto Scaling group with 4 instances in one Availability Zone behind an Application Load Balancer.

### **Explanation**

- Answer

    Fault Tolerance is the ability of a system to remain in operation even if some of the components used to build the system fail. In AWS, this means that in the event of server fault or system failures, the number of running EC2 instances should not fall below the minimum number of instances required by the system for it to work properly. So if the application requires a minimum of 4 instances, there should be at least 4 instances running in case there is an outage in one of the Availability Zones or if there are server issues.

    One of the differences between Fault Tolerance and High Availability is that, the former refers to the minimum number of running instances. For example, you have a system that requires a minimum of 4 running instances and currently has 6 running instances deployed in two Availability Zones. There was a component failure in one of the Availability Zones which knocks out 3 instances. In this case, the system can still be regarded as Highly Available since there are still instances running that can accomodate the requests. However, it is not Fault Tolerant since the required minimum of four instances have not been met.

    As such, ***deploying an Auto Scaling group with 2 instances in each of 3 Availability Zones behind an Application Load Balancer*** is the correct answer because even if there was an outage in one of the Availability Zones, the system still satisfies the requirement of a minimum of 4 running instances.

    ***Deploying an Auto Scaling group with 2 instances in each of 2 Availability Zones behind an Application Load Balancer*** is incorrect because if one Availability Zone went out, there will only be 2 running instances available out of the required 4 minimum instances. Although the Auto Scaling group can spin up another 2 instances, the fault tolerance of the web application has already been compromised.

    ***Deploying an Auto Scaling group with 4 instances in one Availability Zone behind an Application Load Balancer*** is incorrect because if the Availability Zone went out, there will be no running instance available to accommodate the request.

    ***Deploying an Auto Scaling group with 1 instance in each of 4 Availability Zones behind an Application Load Balancer*** is incorrect because if one Availability Zone went out, there will only be 3 instances available to accommodate the request.

**A data analytics company has been building its new generation big data and analytics platform on their AWS cloud infrastructure. They need a storage service that provides the scale and performance that their big data applications require such as high throughput to compute nodes coupled with read-after-write consistency and low-latency file operations. In addition, their data needs to be stored redundantly across multiple AZs and allows concurrent connections from multiple EC2 instances hosted on multiple AZs. Which of the following AWS storage services will you use to meet this requirement?**

- ​Glacier
- ​S3
- ​EFS
- ​EBS

### **Explanation**

- Answer

    In this question, you should take note of the two keywords/phrases: "file operation" and "allows concurrent connections from multiple EC2 instances". There are various AWS storage options that you can choose but whenever these criteria show up, always consider using EFS instead of using EBS Volumes which is mainly used as a "block" storage and can only have one connection to one EC2 instance at a time. Amazon EFS provides the scale and performance required for big data applications that require high throughput to compute nodes coupled with read-after-write consistency and low-latency file operations.

    **Amazon EFS** is a fully-managed service that makes it easy to set up and scale file storage in the Amazon Cloud. With a few clicks in the AWS Management Console, you can create file systems that are accessible to Amazon EC2 instances via a file system interface (using standard operating system file I/O APIs) and supports full file system access semantics (such as strong consistency and file locking).

    Amazon EFS file systems can automatically scale from gigabytes to petabytes of data without needing to provision storage. Tens, hundreds, or even thousands of Amazon EC2 instances can access an Amazon EFS file system at the same time, and Amazon EFS provides consistent performance to each Amazon EC2 instance. Amazon EFS is designed to be highly durable and highly available.

    **EBS** is incorrect because it does not allow concurrent connections from multiple EC2 instances hosted on multiple AZs and it does not store data redundantly across multiple AZs by default, unlike EFS.

    **S3** is incorrect because although it can handle concurrent connections from multiple EC2 instances, it does not have the ability to provide low-latency file operations, which is required in this scenario.

    **Glacier** is incorrect because this is an archiving storage solution and is not applicable in this scenario.

**There are a few, easily reproducible but confidential files that your client wants to store in AWS without worrying about storage capacity. For the first month, all of these files will be accessed frequently but after that, they will rarely be accessed at all. The old files will only be accessed by developers so there is no set retrieval time requirement. However, the files under a specific `tutorialsdojo-finance` prefix in the S3 bucket will be used for post-processing that requires millisecond retrieval time.Given these conditions, which of the following options would be the most cost-effective solution for your client's storage needs?**

- ​Store the files in S3 then after a month, change the storage class of the bucket to S3-IA using lifecycle policy.
- ​Store the files in S3 then after a month, change the storage class of the `tutorialsdojo-finance` prefix to S3-IA while the remaining go to Glacier using lifecycle policy.
- ​Store the files in S3 then after a month, change the storage class of the bucket to Intelligent-Tiering using lifecycle policy.
- ​Store the files in S3 then after a month, change the storage class of the `tutorialsdojo-finance` prefix to One Zone-IA while the remaining go to Glacier using lifecycle policy.

### **Explanation**

- Answer

    Initially, the files will be accessed frequently, and S3 is a durable and highly available storage solution for that. After a month has passed, the files won't be accessed frequently anymore, so it is a good idea to use lifecycle policies to move them to a storage class that would have a lower cost for storing them.

    ![https://docs.aws.amazon.com/AmazonS3/latest/dev/images/SupportedTransitionsWaterfallModel.png](https://docs.aws.amazon.com/AmazonS3/latest/dev/images/SupportedTransitionsWaterfallModel.png)

    Since the files are easily reproducible and some of them are needed to be retrieved quickly based on a specific prefix filter (`tutorialsdojo-finance`), S3-One Zone IA would be a good choice for storing them. The other files that do not contain such prefix would then be moved to Glacier for low cost archival. This setup would also be the most cost-effective for the client.

    Hence, the correct answer is to **store the files in S3 then after a month, change the storage class of the `tutorialsdojo-finance` prefix to One Zone-IA while the remaining go to Glacier using lifecycle policy**.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-04-02_04-26-21-158b6e1eb7ef7be3b91049e88f056f3a.gif](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-04-02_04-26-21-158b6e1eb7ef7be3b91049e88f056f3a.gif)

    **Storing the files in S3 then after a month, changing the storage class of the bucket to S3-IA using lifecycle policy** is incorrect because although it is valid to move the files to S3-IA, this solution still costs more compared with using a combination of S3-One Zone IA and Glacier.

    **Storing the files in S3 then after a month, changing the storage class of the bucket to Intelligent-Tiering using lifecycle policy** is incorrect because while S3 Intelligent-Tiering can automatically move data between two access tiers (frequent access and infrequent access) when access patterns change, it is more suitable for scenarios where you don't know the access patterns of your data. It may take some time for S3 Intellgent-Tiering to analyze the access patterns before it moves the data to a cheaper storage class like S3-IA which means you may still end up paying more in the beginning. In addition, you already know the access patterns of the files which means you can directly change the storage class immediately and save cost right away.

    **Storing the files in S3 then after a month, changing the storage class of the `tutorialsdojo-finance` prefix to S3-IA while the remaining go to Glacier using lifecycle policy** is incorrect because although S3-IA costs less than S3 Standard storage class, it is still more expensive than S3-One Zone IA. Remember that the files are easily reproducible so you can safely move the data to S3-One Zone IA and in case there is an outage, you can simply generate the missing data again.

The FTP protocol uses TCP via ports 20 and 21.

**You are working for a tech company which currently has an on-premises infrastructure. They are currently running low on storage and want to have the ability to extend their storage using AWS cloud.Which AWS service can help you achieve this requirement?**

- ​Amazon EC2
- ​Amazon Elastic Block Storage
- ​Amazon Storage Gateway
- ​Amazon SQS

### **Explanation**

- Answer

    AWS Storage Gateway connects an on-premises software appliance with cloud-based storage to provide seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure. You can use the service to store data in the AWS Cloud for scalable and cost-effective storage that helps maintain data security.

    ![https://docs.aws.amazon.com/storagegateway/latest/userguide/images/aws-storage-gateway-stored-diagram.png](https://docs.aws.amazon.com/storagegateway/latest/userguide/images/aws-storage-gateway-stored-diagram.png)

    **Amazon EC2** is incorrect since this is a compute service, not a storage service.

    **Amazon Elastic Block Storage** is incorrect since EBS is primarily used as a storage of your EC2 instances.

    **Amazon SQS** is incorrect since this is a message queuing service, and does not extend your on-premises storage capacity.

**You have a requirement to integrate the Lightweight Directory Access Protocol (LDAP) directory service of your on-premises data center to your AWS VPC using IAM. The identity store which is currently being used is not compatible with SAML. Which of the following provides the most valid approach to implement the integration?**

- ​Use an IAM policy that references the LDAP identifiers and AWS credentials.
- ​Develop an on-premises custom identity broker application and use STS to issue short-lived AWS credentials.
- ​Use IAM roles to rotate the IAM credentials whenever LDAP credentials are updated.
- ​Use AWS Single Sign-On (SSO) service to enable single sign-on between AWS and your LDAP.

### **Explanation**

- Answer

    If your identity store is not compatible with SAML 2.0, then you can build a custom identity broker application to perform a similar function. The broker application authenticates users, requests temporary credentials for users from AWS, and then provides them to the user to access AWS resources.

    The application verifies that employees are signed into the existing corporate network's identity and authentication system, which might use LDAP, Active Directory, or another system. The identity broker application then obtains temporary security credentials for the employees.

    To get temporary security credentials, the identity broker application calls either **`AssumeRole`** or **`GetFederationToken`** to obtain temporary security credentials, depending on how you want to manage the policies for users and when the temporary credentials should expire. The call returns temporary security credentials consisting of an AWS access key ID, a secret access key, and a session token. The identity broker application makes these temporary security credentials available to the internal company application. The app can then use the temporary credentials to make calls to AWS directly. The app caches the credentials until they expire, and then requests a new set of temporary credentials.

    ![https://docs.aws.amazon.com/IAM/latest/UserGuide/images/enterprise-authentication-with-identity-broker-application.diagram.png](https://docs.aws.amazon.com/IAM/latest/UserGuide/images/enterprise-authentication-with-identity-broker-application.diagram.png)

    **Using an IAM policy that references the LDAP identifiers and AWS credentials** is incorrect because using an IAM policy is not enough to integrate your LDAP service to IAM. You need to use SAML, STS or a custom identity broker.

    **Using AWS Single Sign-On (SSO) service to enable single sign-on between AWS and your LDAP** is incorrect because the scenario did not require SSO and in addition, the identity store that you are using is not SAML-compatible.

    **Using IAM roles to rotate the IAM credentials whenever LDAP credentials are updated** is incorrect because manually rotating the IAM credentials is not an optimal solution to integrate your on-premises and VPC network. You need to use SAML, STS or a custom identity broker.

**Your company has a two-tier environment in its on-premises data center which is composed of an application tier and database tier. You are instructed to migrate their environment to the AWS cloud, and to design the subnets in their VPC with the following requirements:a) There is an application load balancer that would distribute the incoming traffic among the servers in the application tier.b) The application tier and the database tier must not be accessible from the public Internet. The application tier should only accept traffic coming from the load balancer.c) The database tier contains very sensitive data. It must not share the same subnet with other AWS resources and its custom route table with other instances in the environment.d) The environment must be highly available and scalable to handle a surge of incoming traffic over the Internet.How many subnets should you create to meet the above requirements?**

- ​4
- ​3
- ​6
- ​2

### **Explanation**

- Answer

    The given scenario indicated 4 requirements that should be met in order to successfully migrate their two-tier environment from their on-premises data center to AWS Cloud. The first requirement means that you have to use an application load balancer (ALB) to distribute the incoming traffic to your application servers.

    The second requirement specifies that both your application and database tier should not be accessible from the public Internet. This means that you could create a single private subnet for both of your application and database tier. However, the third requirement mentioned that the database tier should not share the same subnet with other AWS resources to protect its sensitive data. This means that you should provision one private subnet for your application tier and another private subnet for your database tier.

    **The last requirement alludes to the need for using at least two Availability Zones to achieve high availability. This means that you have to distribute your application servers to two AZs as well as your database which can be set up with a master-slave configuration to properly replicate the data between two zones.**

    **If you have more than one private subnet in the same Availability Zone that contains instances that need to be registered with the load balancer, you only need to create one public subnet**. You need only one public subnet per Availability Zone; you can add the private instances in all the private subnets that reside in that particular Availability Zone.

    ![https://i.udemycdn.com/redactor/raw/2019-11-15_05-21-05-c823048b82f65f434901a13b2ecdbfce.png](https://i.udemycdn.com/redactor/raw/2019-11-15_05-21-05-c823048b82f65f434901a13b2ecdbfce.png)

    **Since you have a public internet-facing load balancer that has a group of backend Amazon EC2 instances that are deployed in a private subnet, you must create the corresponding public subnets in the same Availability Zones**. This new public subnet is on top of the private subnet that is used by your private EC2 instances. Lastly, you should associate these public subnets to the internet-facing load balancer to complete the setup.

    To summarize, we need to have one private subnet for the application tier and another one for the database tier. We then need to create another public subnet in the same Availability Zone where the private EC2 instances are hosted, in order to properly connect the public Internet-facing load balancer to your instances. This means that we have to use a total of 3 subnets consisting of 2 private subnets and 1 public subnet.

    To meet the requirement of high availability, we have to deploy the stack to two Availability Zones. This means that you have to double the number of subnets you are using. Take note as well that you must create the corresponding public subnet in the same Availability Zone of your private EC2 servers in order for it to properly communicate with the load balancer.

    Hence, the correct answer is 6 subnets.

**You are working as a Solutions Architect for a leading data analytics company in which you are tasked to process real-time streaming data of your users across the globe. This will enable you to track and analyze globally-distributed user activity on your website and mobile applications, including click stream analysis. Your cloud architecture should process the data in close geographical proximity to your users and to respond to user requests at low latencies.Which of the following options is the most ideal solution that you should implement?**

- ​Use a CloudFront web distribution and Route 53 with a Geoproximity routing policy in order to process the data in close geographical proximity to users and respond to user requests at low latencies. Process real-time streaming data using Kinesis and durably store the results to an Amazon S3 bucket.
- ​Integrate CloudFront with Lambda@Edge in order to process the data in close geographical proximity to users and respond to user requests at low latencies. Process real-time streaming data using Amazon Athena and durably store the results to an Amazon S3 bucket.
- ​Integrate CloudFront with Lambda@Edge in order to process the data in close geographical proximity to users and respond to user requests at low latencies. Process real-time streaming data using Kinesis and durably store the results to an Amazon S3 bucket.
- ​Use a CloudFront web distribution and Route 53 with a latency-based routing policy, in order to process the data in close geographical proximity to users and respond to user requests at low latencies. Process real-time streaming data using Kinesis and durably store the results to an Amazon S3 bucket.

### **Explanation**

- Answer

    Lambda@Edge is a feature of Amazon CloudFront that lets you run code closer to users of your application, which improves performance and reduces latency. With Lambda@Edge, you don't have to provision or manage infrastructure in multiple locations around the world. You pay only for the compute time you consume - there is no charge when your code is not running.

    With Lambda@Edge, you can enrich your web applications by making them globally distributed and improving their performance — all with zero server administration. Lambda@Edge runs your code in response to events generated by the Amazon CloudFront content delivery network (CDN). Just upload your code to AWS Lambda, which takes care of everything required to run and scale your code with high availability at an AWS location closest to your end user.

    ![https://d1.awsstatic.com/products/cloudfront/AWS-Lambda-at-Edge_User-Tracking-Analytics-diagram%20Oct%202018.5cc920f99c9450467b7290c20a8a4eb7c444e915.png](https://d1.awsstatic.com/products/cloudfront/AWS-Lambda-at-Edge_User-Tracking-Analytics-diagram%20Oct%202018.5cc920f99c9450467b7290c20a8a4eb7c444e915.png)

    By using Lambda@Edge and Kinesis together, you can process real-time streaming data so that you can track and analyze globally-distributed user activity on your website and mobile applications, including clickstream analysis. Hence, the correct answer in this scenario is the option that says: **Integrate CloudFront with Lambda@Edge in order to process the data in close geographical proximity to users and respond to user requests at low latencies. Process real-time streaming data using Kinesis and durably store the results to an Amazon S3 bucket.**

    The options that say: **Use a CloudFront web distribution and Route 53 with a latency-based routing policy, in order to process the data in close geographical proximity to users and respond to user requests at low latencies. Process real-time streaming data using Kinesis and durably store the results to an Amazon S3 bucket** and **Use a CloudFront web distribution and Route 53 with a Geoproximity routing policy in order to process the data in close geographical proximity to users and respond to user requests at low latencies. Process real-time streaming data using Kinesis and durably store the results to an Amazon S3 bucket** are both incorrect because you can only route traffic using Route 53 since it does not have any computing capability. This solution would not be able to process and return the data in close geographical proximity to your users since it is not using Lambda@Edge.

    The option that says: **Integrate CloudFront with Lambda@Edge in order to process the data in close geographical proximity to users and respond to user requests at low latencies. Process real-time streaming data using Amazon Athena and durably store the results to an Amazon S3 bucket** is incorrect because although using Lambda@Edge is correct, Amazon Athena is just an interactive query service that enables you to easily analyze data in Amazon S3 using standard SQL. Kinesis should be used to process the streaming data in real-time.

**You have a distributed application in AWS that periodically processes large volumes of data across multiple instances. You designed the application to recover gracefully from any instance failures. You are required to launch the application in the most cost-effective way.Which type of EC2 instance will meet your requirements?**

- ​Dedicated instances
- ​Spot Instances
- ​Reserved instances
- ​On-Demand instances

### **Explanation**

- Answer

    You require an EC2 instance that is the most cost-effective among other types. In addition, the application it will host is designed to gracefully recover in case of instance failures.

    In terms of cost-effectiveness, Spot and Reserved instances are the top options. And since the application can gracefully recover from instance failures, the Spot instance is the best option for this case as it is the cheapest type of EC2 instance. Remember that when you use Spot Instances, there will be interruptions. Amazon EC2 can interrupt your Spot Instance when the Spot price exceeds your maximum price, when the demand for Spot Instances rise, or when the supply of Spot Instances decreases. This makes **Spot Instances** the correct answer.

    **Reserved instances** is incorrect because although you could also use reserved instances to save costs, it entails a commitment of 1-year or 3-year terms of usage. Since your processes only run periodically, you won't be able to maximize the discounted price of using reserved instances.

    **Dedicated instances** and **On-Demand instances** are also incorrect because Dedicated and on-demand instances are not a cost-effective solution to use for your application.

**[SAA-C02] An online trading platform with thousands of clients across the globe is hosted in AWS. To reduce latency, you have to direct user traffic to the nearest application endpoint to the client. The traffic should be routed to the closest edge location via an Anycast static IP address. AWS Shield should also be integrated into the solution for DDoS protection.Which of the following is the MOST suitable service that the Solutions Architect should use to satisfy the above requirements?**

- ​AWS Global Accelerator
- ​Amazon CloudFront
- ​AWS WAF
- ​AWS PrivateLink

### **Explanation**

- Answer

    **AWS Global Accelerator** is a service that improves the availability and performance of your applications with local or global users. It provides static IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions, such as your Application Load Balancers, Network Load Balancers or Amazon EC2 instances.

    AWS Global Accelerator uses the AWS global network to optimize the path from your users to your applications, improving the performance of your TCP and UDP traffic. AWS Global Accelerator continually monitors the health of your application endpoints and will detect an unhealthy endpoint and redirect traffic to healthy endpoints in less than 1 minute.

    ![https://d1.awsstatic.com/r2018/b/ubiquity/global-accelerator-how-it-works.feb297eb78d8cc55205874a1691e0ea2bc8bdbf1.png](https://d1.awsstatic.com/r2018/b/ubiquity/global-accelerator-how-it-works.feb297eb78d8cc55205874a1691e0ea2bc8bdbf1.png)

    Many applications, such as gaming, media, mobile applications, and financial applications, need very low latency for a great user experience. To improve the user experience, AWS Global Accelerator directs user traffic to the nearest application endpoint to the client, thus reducing internet latency and jitter. It routes the traffic to the closest edge location via Anycast, then by routing it to the closest regional endpoint over the AWS global network. AWS Global Accelerator quickly reacts to changes in network performance to improve your users’ application performance.

    **AWS Global Accelerator and Amazon CloudFront are separate services that use the AWS global network and its edge locations around the world**. CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery). Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. Both services integrate with AWS Shield for DDoS protection.

    Hence, the correct answer is ***AWS Global Accelerator***.

    ***Amazon CloudFront*** is incorrect because although this service uses edge locations, it doesn't have the capability to route the traffic to the closest edge location via an Anycast static IP address.

    ***AWS WAF*** is incorrect because the this service is just a web application firewall that helps protect your web applications or APIs against common web exploits that may affect availability, compromise security, or consume excessive resources

    ***AWS PrivateLink*** is incorrect because this service simply provides private connectivity between VPCs, AWS services, and on-premises applications, securely on the Amazon network. It doesn't route traffic to the closest edge location via an Anycast static IP address.

**You are employed by a large electronics company that uses Amazon Simple Storage Service. For reporting purposes, they want to track and log every request access to their S3 buckets including the requester, bucket name, request time, request action, referrer, turnaround time, and error code information. The solution should also provide more visibility into the object-level operations of the bucket.Which is the best solution among the following options that can satisfy the requirement?**

- ​Enable Amazon S3 Event Notifications for PUT and POST.
- ​Enable AWS CloudTrail to audit all Amazon S3 bucket access.
- ​Enable the Requester Pays option to track access via AWS Billing.
- ​Enable server access logging for all required Amazon S3 buckets.

### **Explanation**

- Answer

    You can use AWS CloudTrail logs together with server access logs for Amazon S3. CloudTrail logs provide you with detailed API tracking for Amazon S3 **bucket-level and object-level** operations, while server access logs for Amazon S3 provide you visibility into **object-level** operations on your data in Amazon S3.

    ![https://docs.aws.amazon.com/AmazonS3/latest/user-guide/images/bucket-logging-box.png](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/images/bucket-logging-box.png)

    You can also use CloudTrail logs together with CloudWatch for Amazon S3. CloudTrail integration with CloudWatch Logs delivers S3 bucket-level API activity captured by CloudTrail to a CloudWatch log stream in the CloudWatch log group you specify. You can create CloudWatch alarms for monitoring specific API activity and receive email notifications when the specific API activity occurs

    For this scenario, you can use CloudTrail and the Server Access Logging feature of Amazon S3. However, the question mentioned that it needs detailed information about every access request sent to the S3 bucket including the referrer and turn-around time information. These two records are not available in CloudTrail which is why the correct answer is to **enable server access logging for all required Amazon S3 buckets**.

    **Enabling the Requester Pays option to track access via AWS Billing** is incorrect because this action refers to AWS billing and not for logging.

    **Enabling Amazon S3 Event Notifications for PUT and POST** is incorrect because we are looking for a logging solution and not an event notification.

**To save cost, a company decided to change their third-party data analytics tool to a cheaper solution. They sent a full data export on a CSV file which contains all of their analytics information. You then save the CSV file to an S3 bucket for storage. Your manager asked you to do some validation on the provided data export. In this scenario, what is the most cost-effective and easiest way to analyze export data using a standard SQL?**

- ​Create a migration tool to load the CSV export file from S3 to a DynamoDB instance. Once the data has been loaded, run queries using DynamoDB.
- ​Use a migration tool to load the CSV export file from S3 to a database which is designed for online analytic processing (OLAP) such as AWS RedShift. Run some queries once the data has been loaded to complete your validation.
- ​To be able to run SQL queries, use AWS Athena to analyze the export data file in S3.
- ​Use mysqldump client utility to load the CSV export file from S3 to a MySQL RDS instance. Run some SQL queries once the data has been loaded to complete your validation.

### **Explanation**

- Answer

    Amazon Athena is an interactive query service that makes it easy to analyze data directly in Amazon Simple Storage Service (Amazon S3) **using standard SQL**. With a few actions in the AWS Management Console, you can point Athena at your data stored in Amazon S3 and begin using standard SQL to run ad-hoc queries and get results in seconds.

    Athena is serverless, so there is no infrastructure to set up or manage, and you pay only for the queries you run. Athena scales automatically—executing queries in parallel—so results are fast, even with large datasets and complex queries.

    Athena helps you analyze unstructured, semi-structured, and structured data stored in Amazon S3. Examples include CSV, JSON, or columnar data formats such as Apache Parquet and Apache ORC. You can use Athena to run ad-hoc queries using ANSI SQL, without the need to aggregate or load the data into Athena.

    Hence, the most cost-effective and appropriate answer in this scenario is the option that says: **To be able to run SQL queries, use Amazon Athena to analyze the export data file in S3.**

    The rest of the options are all incorrect because it is not necessary to set up a database to be able to analyze the CSV export file. You can use a cost-effective option (AWS Athena), which is a serverless service that enables you to pay only for the queries you run.

**You are a Big Data Engineer who is assigned to handle the online enrollment system database of a prestigious university, which is hosted in RDS. You are required to monitor the database metrics in Amazon CloudWatch to ensure the availability of the enrollment system.What are the enhanced monitoring metrics that Amazon CloudWatch gathers from Amazon RDS DB instances which provide a more accurate information? (Select TWO.)**

- [ ]  ​CPU Utilization
- [ ]  ​RDS child processes.
- [ ]  ​Freeable Memory
- [ ]  ​Database Connections
- [ ]  ​OS processes

### **Explanation**

- Answer

    **Amazon RDS** provides metrics in real time for the operating system (OS) that your DB instance runs on. You can view the metrics for your DB instance using the console, or consume the Enhanced Monitoring JSON output from CloudWatch Logs in a monitoring system of your choice.

    **CloudWatch** gathers metrics about CPU utilization from the hypervisor for a DB instance, and Enhanced Monitoring gathers its metrics from an agent on the instance. As a result, you might find differences between the measurements, because the hypervisor layer performs a small amount of work. The differences can be greater if your DB instances use smaller instance classes, because then there are likely more virtual machines (VMs) that are managed by the hypervisor layer on a single physical instance. Enhanced Monitoring metrics are useful when you want to see how different processes or threads on a DB instance use the CPU.

    ![https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/metrics1.png](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/images/metrics1.png)

    In RDS, the Enhanced Monitoring metrics shown in the Process List view are organized as follows:

    **RDS child processes** – Shows a summary of the RDS processes that support the DB instance, for example `aurora` for Amazon Aurora DB clusters and `mysqld` for MySQL DB instances. Process threads appear nested beneath the parent process. Process threads show CPU utilization only as other metrics are the same for all threads for the process. The console displays a maximum of 100 processes and threads. The results are a combination of the top CPU consuming and memory consuming processes and threads. If there are more than 50 processes and more than 50 threads, the console displays the top 50 consumers in each category. This display helps you identify which processes are having the greatest impact on performance.

    ***RDS processes*** – Shows a summary of the resources used by the RDS management agent, diagnostics monitoring processes, and other AWS processes that are required to support RDS DB instances.

    ***OS processes*** – Shows a summary of the kernel and system processes, which generally have minimal impact on performance.

    ***CPU Utilization, Database Connections,*** and ***Freeable Memory*** are incorrect because these are just the regular items provided by Amazon RDS Metrics in CloudWatch. Remember that the scenario is asking for the Enhanced Monitoring metrics.

**You have an Auto Scaling group which is configured to launch new `t2.micro` EC2 instances when there is a significant load increase in the application. To cope with the demand, you now need to replace those instances with a larger `t2.2xlarge` instance type. How would you implement this change?**

- ​Change the instance type of each EC2 instance manually.
- ​Create a new launch configuration with the new instance type and update the Auto Scaling Group.
- ​Create another Auto Scaling Group and attach the new instance type.
- ​Just change the instance type to `t2.2xlarge` in the current launch configuration

### **Explanation**

- Answer

    You can only specify one launch configuration for an Auto Scaling group at a time, and you can't modify a launch configuration after you've created it. Therefore, if you want to change the launch configuration for an Auto Scaling group, you must create a launch configuration and then update your Auto Scaling group with the new launch configuration.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2020-02-16_08-38-47-aa6b38010545d6907cd3f2c5e02249ac.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2020-02-16_08-38-47-aa6b38010545d6907cd3f2c5e02249ac.png)

    Hence, the correct answer is: **Create a new launch configuration with the new instance type and update the Auto Scaling Group.**

    The option that says: **Just change the instance type to t2.2xlarge in the current launch configuration** **is incorrect because you can't change your launch configuration once it is created. You have to create a new one instead.The option that says: **Create another Auto Scaling Group and attach the new instance type** is incorrect because you can't directly attach or declare the new instance type to your Auto Scaling group. You have to create a new launch configuration first, with a new instance type, then attach it to your existing Auto Scaling group.The option that says: **Change the instance type of each EC2 instance manually** is incorrect because you can't directly change the instance type of your EC2 instance. This should be done by creating a brand new launch configuration then attaching it to your existing Auto Scaling group.

**A financial company instructed you to automate the recurring tasks in your department such as patch management, infrastructure selection, and data synchronization to improve their current processes. You need to have a service which can coordinate multiple AWS services into serverless workflows. Which of the following is the most cost-effective service to use in this scenario?**

- ​AWS Step Functions
- ​AWS Batch
- ​AWS Lambda
- ​SWF

### **Explanation**

- Answer

    **AWS Step Functions** provides serverless orchestration for modern applications. Orchestration centrally manages a workflow by breaking it into multiple steps, adding flow logic, and tracking the inputs and outputs between the steps. As your applications execute, Step Functions maintains application state, tracking exactly which workflow step your application is in, and stores an event log of data that is passed between application components. That means that if networks fail or components hang, your application can pick up right where it left off.

    Application development is faster and more intuitive with Step Functions, because you can define and manage the workflow of your application independently from its business logic. Making changes to one does not affect the other. You can easily update and modify workflows in one place, without having to struggle with managing, monitoring and maintaining multiple point-to-point integrations. Step Functions frees your functions and containers from excess code, so your applications are faster to write, more resilient, and easier to maintain.

    **SWF** is incorrect because this is a fully-managed state tracker and task coordinator service. It does not provide serverless orchestration to multiple AWS resources.

    **AWS Lambda** is incorrect because although Lambda is used for serverless computing, it does not provide a direct way to coordinate multiple AWS services into serverless workflows.

    **AWS Batch** is incorrect because this is primarily used to efficiently run hundreds of thousands of batch computing jobs in AWS.

**A leading IT consulting company has an application which processes a large stream of financial data by an Amazon ECS Cluster then stores the result to a DynamoDB table. You have to design a solution to detect new entries in the DynamoDB table then automatically trigger a Lambda function to run some tests to verify the processed data.What solution can be easily implemented to alert the Lambda function of new entries while requiring minimal configuration change to your architecture?**

- ​Use CloudWatch Alarms to trigger the Lambda function whenever a new entry is created in the DynamoDB table.
- ​Enable DynamoDB Streams to capture table activity and automatically trigger the Lambda function.
- ​Invoke the Lambda functions using SNS each time that the ECS Cluster successfully processed financial data.
- ​Use Systems Manager Automation to detect new entries in the DynamoDB table then automatically invoke the Lambda function for processing.

### **Explanation**

- Answer

    Amazon DynamoDB is integrated with AWS Lambda so that you can create *triggers*—pieces of code that automatically respond to events in DynamoDB Streams. With triggers, you can build applications that react to data modifications in DynamoDB tables.

    If you enable DynamoDB Streams on a table, you can associate the stream ARN with a Lambda function that you write. Immediately after an item in the table is modified, a new record appears in the table's stream. AWS Lambda polls the stream and invokes your Lambda function synchronously when it detects new stream records.

    ![https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/images/StreamsAndTriggers.png](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/images/StreamsAndTriggers.png)

    You can create a Lambda function which can perform a specific action that you specify, such as sending a notification or initiating a workflow. For instance, you can set up a Lambda function to simply copy each stream record to persistent storage, such as EFS or S3, to create a permanent audit trail of write activity in your table.

    Suppose you have a mobile gaming app that writes to a `TutorialsDojoCourses` table. Whenever the `TopCourse` attribute of the `TutorialsDojoScores` table is updated, a corresponding stream record is written to the table's stream. This event could then trigger a Lambda function that posts a congratulatory message on a social media network. (The function would simply ignore any stream records that are not updates to `TutorialsDojoCourses` or that do not modify the `TopCourse` attribute.)

    Hence, **enabling DynamoDB Streams to capture table activity and automatically trigger the Lambda function** is the correct answer because the requirement can be met with minimal configuration change using DynamoDB streams which can automatically trigger Lambda functions whenever there is a new entry.

    **Using CloudWatch Alarms to trigger the Lambda function whenever a new entry is created in the DynamoDB table** is incorrect because CloudWatch Alarms only monitor service metrics, not changes in DynamoDB table data.

    **Invoking the Lambda functions using SNS each time that the ECS Cluster successfully processed financial data** is incorrect because you don't need to create an SNS topic just to invoke Lambda functions. You can enable DynamoDB streams instead to meet the requirement with less configuration.

    **Using Systems Manager Automation to detect new entries in the DynamoDB table then automatically invoking the Lambda function for processing** is incorrect because the Systems Manager Automation service is primarily used to simplify common maintenance and deployment tasks of Amazon EC2 instances and other AWS resources. It does not have the capability to detect new entries in a DynamoDB table.

**A Solutions Architect is designing a monitoring application which generates audit logs of all operational activities of the company's cloud infrastructure. Their IT Security and Compliance team mandates that the application retain the logs for 5 years before the data can be deleted.How can the Architect meet the above requirement?**

- ​Store the audit logs in an EFS volume and use Network File System version 4 (NFSv4) file-locking mechanism.
- ​Store the audit logs in an EBS volume and then take EBS snapshots every month.
- ​Store the audit logs in a Glacier vault and use the Vault Lock feature.
- ​Store the audit logs in an Amazon S3 bucket and enable Multi-Factor Authentication Delete (MFA Delete) on the S3 bucket.

### **Explanation**

- Answer

    An Amazon S3 Glacier (Glacier) vault can have one resource-based vault access policy and one Vault Lock policy attached to it. A *Vault Lock policy* is a vault access policy that you can lock. Using a Vault Lock policy can help you enforce regulatory and compliance requirements. Amazon S3 Glacier provides a set of API operations for you to manage the Vault Lock policies.

    ![https://media.amazonwebservices.com/blog/2015/glacier_lock_policy_4.png](https://media.amazonwebservices.com/blog/2015/glacier_lock_policy_4.png)

    As an example of a Vault Lock policy, suppose that you are required to retain archives for one year before you can delete them. To implement this requirement, you can create a Vault Lock policy that denies users permissions to delete an archive until the archive has existed for one year. You can test this policy before locking it down. After you lock the policy, the policy becomes immutable. For more information about the locking process, see Amazon S3 Glacier Vault Lock. If you want to manage other user permissions that can be changed, you can use the vault access policy

    Amazon S3 Glacier supports the following archive operations: Upload, Download, and Delete. Archives are immutable and cannot be modified. Hence, the correct answer is to **store the audit logs in a Glacier vault and use the Vault Lock feature**.

    **Storing the audit logs in an EBS volume and then taking EBS snapshots every month** is incorrect because this is not a suitable and secure solution. Anyone who has access to the EBS Volume can simply delete and modify the audit logs. Snapshots can be deleted too.

    **Storing the audit logs in an Amazon S3 bucket and enabling Multi-Factor Authentication Delete (MFA Delete) on the S3 bucket** is incorrect because this would still not meet the requirement. If someone has access to the S3 bucket and also has the proper MFA privileges then the audit logs can be edited.

    **Storing the audit logs in an EFS volume and using Network File System version 4 (NFSv4) file-locking mechanism** is incorrect because the data integrity of the audit logs can still be compromised if it is stored in an EFS volume with Network File System version 4 (NFSv4) file-locking mechanism and hence, not suitable as storage for the files. Although it will provide some sort of security, the file lock can still be overridden and the audit logs might be edited by someone else.

**A popular augmented reality (AR) mobile game is heavily using a RESTful API which is hosted in AWS. The API uses Amazon API Gateway and a DynamoDB table with a preconfigured read and write capacity. Based on your systems monitoring, the DynamoDB table begins to throttle requests during high peak loads which causes the slow performance of the game. Which of the following can you do to improve the performance of your app?**

- ​Add the DynamoDB table to an Auto Scaling Group.
- ​Integrate an Application Load Balancer with your DynamoDB table.
- ​Create an SQS queue in front of the DynamoDB table.
- ​Use DynamoDB Auto Scaling

### **Explanation**

- Answer

    DynamoDB auto scaling uses the AWS Application Auto Scaling service to dynamically adjust provisioned throughput capacity on your behalf, in response to actual traffic patterns. This enables a table or a global secondary index to increase its provisioned read and write capacity to handle sudden increases in traffic, without throttling. When the workload decreases, Application Auto Scaling decreases the throughput so that you don't pay for unused provisioned capacity.

    **Using DynamoDB Auto Scaling** is the best answer. DynamoDB Auto Scaling uses the AWS Application Auto Scaling service to dynamically adjust provisioned throughput capacity on your behalf.

    **Integrating an Application Load Balancer with your DynamoDB table** is incorrect because an Application Load Balancer is not suitable to be used with DynamoDB and in addition, this will not increase the throughput of your DynamoDB table.

    **Adding the DynamoDB table to an Auto Scaling Group** is incorrect because you usually put EC2 instances on an Auto Scaling Group, and not a DynamoDB table.

    **Creating an SQS queue in front of the DynamoDB table** is incorrect because this is not a design principle for high throughput DynamoDB table. Using SQS is for handling queuing and polling the request. This will not increase the throughput of DynamoDB which is required in this situation.

**[SAA-C02] An automotive company is working on an autonomous vehicle development and deployment project using AWS. The solution requires High Performance Computing (HPC) in order to collect, store and manage massive amounts of data as well as to support deep learning frameworks. The Linux EC2 instances that will be used should have a lower latency and higher throughput than the TCP transport traditionally used in cloud-based HPC systems. It should also enhance the performance of inter-instance communication and must include an OS-bypass functionality to allow the HPC to communicate directly with the network interface hardware to provide low-latency, reliable transport functionality.Which of the following is the MOST suitable solution that you should implement to achieve the above requirements?**

- ​Attach an Elastic Network Adapter (ENA) on each Amazon EC2 instance to accelerate High Performance Computing (HPC).
- ​Attach an Elastic Fabric Adapter (EFA) on each Amazon EC2 instance to accelerate High Performance Computing (HPC).
- ​Attach an Elastic Network Interface (ENI) on each Amazon EC2 instance to accelerate High Performance Computing (HPC).
- ​Attach a Private Virtual Interface (VIF) on each Amazon EC2 instance to accelerate High Performance Computing (HPC).

### **Explanation**

- Answer

    **An Elastic Fabric Adapter (EFA)** is a network device that you can attach to your Amazon EC2 instance to accelerate High Performance Computing (HPC) and machine learning applications. EFA enables you to achieve the application performance of an on-premises HPC cluster, with the scalability, flexibility, and elasticity provided by the AWS Cloud.

    EFA provides lower and more consistent latency and higher throughput than the TCP transport traditionally used in cloud-based HPC systems. It enhances the performance of inter-instance communication that is critical for scaling HPC and machine learning applications. It is optimized to work on the existing AWS network infrastructure and it can scale depending on application requirements.

    EFA integrates with Libfabric 1.9.0 and it supports Open MPI 4.0.2 and Intel MPI 2019 Update 6 for HPC applications, and Nvidia Collective Communications Library (NCCL) for machine learning applications.

    ![https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/efa_stack.png](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/efa_stack.png)

    The OS-bypass capabilities of EFAs are not supported on Windows instances. If you attach an EFA to a Windows instance, the instance functions as an Elastic Network Adapter, without the added EFA capabilities.

    Elastic Network Adapters (ENAs) provide traditional IP networking features that are required to support VPC networking. EFAs provide all of the same traditional IP networking features as ENAs, and they also support OS-bypass capabilities. OS-bypass enables HPC and machine learning applications to bypass the operating system kernel and to communicate directly with the EFA device.

    Hence, the correct answer is to ***attach an Elastic Fabric Adapter (EFA) on each Amazon EC2 instance to accelerate High Performance Computing (HPC)**.*

    ***Attaching an Elastic Network Adapter (ENA) on each Amazon EC2 instance to accelerate High Performance Computing (HPC)*** is incorrect because Elastic Network Adapter (ENA) doesn't have OS-bypass capabilities, unlike EFA.

    ***Attaching an Elastic Network Interface (ENI) on each Amazon EC2 instance to accelerate High Performance Computing (HPC)*** is incorrect because an Elastic Network Interface (ENI) is simply a logical networking component in a VPC that represents a virtual network card. It doesn't have OS-bypass capabilities that allow the HPC to communicate directly with the network interface hardware to provide low-latency, reliable transport functionality.

    ***Attaching a Private Virtual Interface (VIF) on each Amazon EC2 instance to accelerate High Performance Computing (HPC)*** is incorrect because Private Virtual Interface just allows you to connect to your VPC resources on your private IP address or endpoint.

**You are the technical lead of the Cloud Infrastructure team in your company and you were consulted by a software developer regarding the required AWS resources of the web application that he is building. He knows that an Instance Store only provides ephemeral storage where the data is automatically deleted when the instance is terminated. To ensure that the data of his web application persists, the app should be launched in an EC2 instance that has a durable, block-level storage volume attached. He knows that they need to use an EBS volume, but they are not sure what type they need to use. In this scenario, which of the following is true about Amazon EBS volume types and their respective usage? (Select TWO.)**

- [ ]  ​Reduced Redundancy Storage volumes offer consistent and low-latency performance, and are designed for I/O intensive applications such as large relational or NoSQL databases.
- [ ]  ​Magnetic volumes provide the lowest cost per gigabyte of all EBS volume types and are ideal for workloads where data is accessed infrequently, and applications where the lowest storage cost is important.
- [ ]  ​Spot volumes provide the lowest cost per gigabyte of all EBS volume types and are ideal for workloads where data is accessed infrequently, and applications where the lowest storage cost is important.
- [ ]  ​Single root I/O virtualization (SR-IOV) volumes are suitable for a broad range of workloads, including small to medium sized databases, development and test environments, and boot volumes.
- [ ]  ​Provisioned IOPS volumes offer storage with consistent and low-latency performance, and are designed for I/O intensive applications such as large relational or NoSQL databases.

### **Explanation**

- Answer

    **Amazon EBS** provides three volume types to best meet the needs of your workloads: General Purpose (SSD), Provisioned IOPS (SSD), and Magnetic.

    ![https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/overview_getting_started.png](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/overview_getting_started.png)

    General Purpose (SSD) is the new, SSD-backed, general purpose EBS volume type that we recommend as the default choice for customers. General Purpose (SSD) volumes are suitable for a broad range of workloads, including small to medium sized databases, development, and test environments, and boot volumes.

    Provisioned IOPS (SSD) volumes offer storage with consistent and low-latency performance and are designed for I/O intensive applications such as large relational or NoSQL databases. Magnetic volumes provide the lowest cost per gigabyte of all EBS volume types.

    Magnetic volumes are ideal for workloads where data are accessed infrequently, and applications where the lowest storage cost is important. Take note that this is a Previous Generation Volume. The latest low-cost magnetic storage types are Cold HDD (sc1) and Throughput Optimized HDD (st1) volumes.

    Hence, the correct answers are:

    ***Provisioned IOPS volumes offer storage with consistent and low-latency performance, and are designed for I/O intensive applications such as large relational or NoSQL databases.***

    ***Magnetic volumes provide the lowest cost per gigabyte of all EBS volume types and are ideal for workloads where data is accessed infrequently, and applications where the lowest storage cost is important.***

    The option that says: ***Spot volumes provide the lowest cost per gigabyte of all EBS volume types and are ideal for workloads where data is accessed infrequently, and applications where the lowest storage cost is important*** is incorrect because there is no EBS type called a "Spot volume" however, there is an Instance purchasing option for Spot Instances.

    The option that says: ***Reduced Redundancy Storage volumes offer consistent and low-latency performance, and are designed for I/O intensive applications such as large relational or NoSQL databases*** is incorrect because there is no such thing as Reduced Redundancy Storage volumes. In Amazon S3, there is an obsolete storage type named: Reduced Redundancy Storage (RRS), but not in EBS.

    The option that says: ***Single root I/O virtualization (SR-IOV) volumes are suitable for a broad range of workloads, including small to medium sized databases, development and test environments, and boot volumes*** is incorrect because SR-IOV is related with Enhanced Networking on Linux and not in EBS.

**You are planning to reduce the amount of data that Amazon S3 transfers to your servers in order to lower your operating costs as well as to lower the latency of retrieving the data. To accomplish this, you need to use simple structured query language (SQL) statements to filter the contents of Amazon S3 objects and retrieve just the subset of data that you need. Which of the following services will help you accomplish this requirement?**

- ​AWS Step Functions
- ​RDS
- ​Redshift Spectrum
- ​S3 Select

### **Explanation**

- Answer

    With Amazon S3 Select, you can use simple structured query language (SQL) statements to filter the contents of Amazon S3 objects and retrieve just the subset of data that you need. By using Amazon S3 Select to filter this data, you can reduce the amount of data that Amazon S3 transfers, which reduces the cost and latency to retrieve this data.

    ![https://media.amazonwebservices.com/blog/2018/sel_select_us_airports_2.png](https://media.amazonwebservices.com/blog/2018/sel_select_us_airports_2.png)

    Amazon S3 Select works on objects stored in CSV, JSON, or Apache Parquet format. It also works with objects that are compressed with GZIP or BZIP2 (for CSV and JSON objects only), and server-side encrypted objects. You can specify the format of the results as either CSV or JSON, and you can determine how the records in the result are delimited.

    **RDS** is incorrect because although RDS is an SQL database where you can perform SQL operations, it is still not valid because you want to apply SQL transactions on S3 itself, and not on the database, which RDS cannot do.

    **Redshift Spectrum** is incorrect because although Amazon Redshift Spectrum provides a similar in-query functionality like S3 Select, this service is more suitable for querying your data from the Redshift external tables hosted in S3. The Redshift queries are run on your cluster resources against local disk. Redshift Spectrum queries run using per-query scale-out resources against data in S3 which can entail additional costs compared with S3 Select.

    **AWS Step Functions** is incorrect because this only lets you coordinate multiple AWS services into serverless workflows so you can build and update apps quickly.

**You had recently set up a CloudWatch Alarm that performs status checks on your EBS volume. However, you noticed that the volume check has a status of `insufficient-data`. What does this status mean?**

- ​All EBS Volume checks have been completed.
- ​The EBS Volume is severely degraded or the volume performance is well below expectations.
- ​The check on the EBS volume is still in progress.
- ​All EBS Volume checks have failed.

### **Explanation**

- Answer

    Volume status checks are automated tests that run every 5 minutes and return a pass or fail status. You can view the results of volume status checks to identify any impaired volumes and take any necessary actions.

    If all checks pass, the status of the volume is **`ok`**. The option that says: **All EBS Volume checks have been completed** is therefore incorrect.

    If a check fails, the status of the volume is **`impaired`**. The option that says: **All EBS Volume checks have failed** is therefore incorrect.

    If the volume is severely degraded or the volume performance is well below expectations, then the status is **`warning`**. The option that says: **The EBS Volume is severely degraded or the volume performance is well below expectations** is therefore incorrect.

    If the status is **`insufficient-data`**, the checks may still be in progress on the volume. The option that says: **The check on the EBS volume is still in progress** is therefore correct.

**A data analytics company, which uses machine learning to collect and analyze consumer data, is using Redshift cluster as their data warehouse. You are instructed to implement a disaster recovery plan for their systems to ensure business continuity even in the event of an AWS region outage. Which of the following is the best approach to meet this requirement?**

- ​Use Automated snapshots of your Redshift Cluster.
- ​Do nothing because Amazon Redshift is a highly available, fully-managed data warehouse which can withstand an outage of an entire AWS region.
- ​Enable Cross-Region Snapshots Copy in your Amazon Redshift Cluster.
- ​Create a scheduled job that will automatically take the snapshot of your Redshift Cluster and store it to an S3 bucket. Restore the snapshot in case of an AWS region outage.

### **Explanation**

- Answer

    You can configure Amazon Redshift to copy snapshots for a cluster to another region. To configure cross-region snapshot copy, you need to enable this copy feature for each cluster and configure where to copy snapshots and how long to keep copied automated snapshots in the destination region. When cross-region copy is enabled for a cluster, all new manual and automatic snapshots are copied to the specified region.

    ![https://docs.aws.amazon.com/redshift/latest/mgmt/images/rs-mgmt-restore-table-from-snapshot.png](https://docs.aws.amazon.com/redshift/latest/mgmt/images/rs-mgmt-restore-table-from-snapshot.png)

    The option that says: **Create a scheduled job that will automatically take the snapshot of your Redshift Cluster and store it to an S3 bucket. Restore the snapshot in case of an AWS region outage** is incorrect because although this option is possible, this entails a lot of manual work and hence, not the best option. You should configure cross-region snapshot copy instead.

    The option that says: **Do nothing because Amazon Redshift is a highly available, fully-managed data warehouse which can withstand an outage of an entire AWS region** is incorrect because although Amazon Redshift is a fully-managed data warehouse, you will still need to configure cross-region snapshot copy to ensure that your data is properly replicated to another region.

    **Using Automated snapshots of your Redshift Cluster** is incorrect because using automated snapshots is not enough and will not be available in case the entire AWS region is down.

**To save costs, your manager instructed you to analyze and review the setup of your AWS cloud infrastructure. You should also provide an estimate of how much your company will pay for all of the AWS resources that they are using. In this scenario, which of the following will incur costs? (Select TWO.)**

- [ ]  ​A running EC2 Instance
- [ ]  ​Public Data Set
- [ ]  ​EBS Volumes attached to stopped EC2 Instances
- [ ]  ​Using an Amazon VPC
- [ ]  ​A stopped On-Demand EC2 Instance

### **Explanation**

- Answer

    Billing commences when Amazon EC2 initiates the boot sequence of an AMI instance. Billing ends when the instance terminates, which could occur through a web services command, by running "shutdown -h", or through instance failure. When you stop an instance, AWS shuts it down but don't charge hourly usage for a stopped instance or data transfer fees, but AWS does charge for the storage of any Amazon EBS volumes.

    Hence, **a running EC2 Instance** and **EBS Volumes attached to stopped EC2 Instances** are the right answers and conversely, **a stopped On-Demand EC2 Instance** is incorrect as there is no charge for a terminated EC2 instance that you have shut down.

    **Using Amazon VPC** is incorrect because there are no additional charges for creating and using the VPC itself. Usage charges for other Amazon Web Services, including Amazon EC2, still apply at published rates for those resources, including data transfer charges.

    **Public Data Set** is incorrect due to the fact that Amazon stores the data sets at no charge to the community and, as with all AWS services, you pay only for the compute and storage you use for your own applications.

**You are working as a Solutions Architect for a startup in which you are tasked to develop a custom messaging service that will also be used to train their AI for an automatic response feature which they plan to implement in the future. Based on their research and tests, the service can receive up to thousands of messages a day, and all of these data are to be sent to Amazon EMR for further processing. It is crucial that none of the messages will be lost, no duplicates will be produced and that they are processed in EMR in the same order as their arrival.Which of the following options should you implement to meet the startup's requirements?**

- ​Set up a default Amazon SQS queue to handle the messages.
- ​Create an Amazon Kinesis Data Stream to collect the messages.
- ​Set up an Amazon SNS Topic to handle the messages.
- ​Create a pipeline using AWS Data Pipeline to handle the messages.

### **Explanation**

- Answer

    Two important requirements that the chosen AWS service should fulfill is that data should not go missing, is durable, and streams data in the sequence of arrival. Kinesis can do the job just fine because of its architecture. A Kinesis data stream is a set of shards that has a sequence of data records, and each data record has a sequence number that is assigned by Kinesis Data Streams. Kinesis can also easily handle the high volume of messages being sent to the service.

    ![https://d1.awsstatic.com/Products/product-name/diagrams/product-page-diagram_Amazon-Kinesis-Data-Streams.074de94302fd60948e1ad070e425eeda73d350e7.png](https://d1.awsstatic.com/Products/product-name/diagrams/product-page-diagram_Amazon-Kinesis-Data-Streams.074de94302fd60948e1ad070e425eeda73d350e7.png)

    Amazon Kinesis Data Streams enables real-time processing of streaming big data. It provides ordering of records, as well as the ability to read and/or replay records in the same order to multiple Amazon Kinesis Applications. The Amazon Kinesis Client Library (KCL) delivers all records for a given partition key to the same record processor, making it easier to build multiple applications reading from the same Amazon Kinesis data stream (for example, to perform counting, aggregation, and filtering).

    **Setting up a default Amazon SQS queue to handle the messages** is incorrect because although SQS is a valid messaging service, it is not suitable for scenarios where you need to process the data based on the order they were received. Take note that a default queue in SQS is just a standard queue and not a FIFO (First-In-First-Out) queue. In addition, SQS does not guarantee that no duplicates will be sent.

    **Setting up an Amazon SNS Topic to handle the messages** is incorrect because SNS is a pub-sub messaging service in AWS. SNS might not be capable of handling such a large volume of messages being received and sent at a time. It does not also guarantee that the data will be transmitted in the same order they were received.

    **Creating a pipeline using AWS Data Pipeline to handle the messages** is incorrect because this is primarily used as a cloud-based data workflow service that helps you process and move data between different AWS services and on-premises data sources. It is not suitable for collecting data from distributed sources such as users, IoT devices, or clickstreams.

**A multinational company with multiple on-premises data centers around the globe is heavily using AWS to serve its clients worldwide. The company already has hundreds of VPCs with multiple VPN connections to their data centers that span to multiple AWS Regions. As the number of its workloads running on AWS grows, the company must be able to scale its networks across multiple accounts and Amazon VPCs to keep up. A Solutions Architect is tasked to interconnect all of the company's on-premises networks, VPNs, and VPCs into a single gateway, that includes support for inter-region peering across multiple AWS regions.Which of the following is the BEST solution that the Architect should set up to support the required interconnectivity?**

- ​Set up an AWS VPN CloudHub for inter-region VPC access and a Direct Connect gateway for the VPN connections to the on-premises data centers. Create a virtual private gateway in each VPC, then create a private virtual interface for each AWS Direct Connect connection to the Direct Connect gateway.
- ​Enable inter-region VPC peering that allows peering relationships to be established between multiple VPCs across different AWS regions. Set up a networking configuration that ensures that the traffic will always stay on the global AWS backbone and never traverse the public Internet.
- ​Set up an AWS Transit Gateway to implement a hub-and-spoke network topology in each region that routes all traffic through a network transit center. Route traffic between VPCs and the on-premises data centers over AWS Site-to-Site VPNs.
- ​Set up an AWS Direct Connect Gateway to achieve inter-region VPC access to all of the AWS resources and on-premises data centers. Set up a link aggregation group (LAG) to aggregate multiple connections at a single AWS Direct Connect endpoint in order to treat them as a single, managed connection. Launch a virtual private gateway in each VPC and then create a public virtual interface for each AWS Direct Connect connection to the Direct Connect Gateway.

### **Explanation**

- Answer

    AWS Transit Gateway is a service that enables customers to connect their Amazon Virtual Private Clouds (VPCs) and their on-premises networks to a single gateway. As you grow the number of workloads running on AWS, you need to be able to scale your networks across multiple accounts and Amazon VPCs to keep up with the growth. Today, you can connect pairs of Amazon VPCs using peering. However, managing point-to-point connectivity across many Amazon VPCs, without the ability to centrally manage the connectivity policies, can be operationally costly and cumbersome. For on-premises connectivity, you need to attach your AWS VPN to each individual Amazon VPC. This solution can be time consuming to build and hard to manage when the number of VPCs grows into the hundreds.

    With AWS Transit Gateway, you only have to create and manage a single connection from the central gateway in to each Amazon VPC, on-premises data center, or remote office across your network. Transit Gateway acts as a hub that controls how traffic is routed among all the connected networks which act like spokes. This hub and spoke model significantly simplifies management and reduces operational costs because each network only has to connect to the Transit Gateway and not to every other network. Any new VPC is simply connected to the Transit Gateway and is then automatically available to every other network that is connected to the Transit Gateway. This ease of connectivity makes it easy to scale your network as you grow.

    ![https://d1.awsstatic.com/product-marketing/transit-gateway/tgw-after.d85d3e2cb67fd2ed1a3be645d443e9f5910409fd.png](https://d1.awsstatic.com/product-marketing/transit-gateway/tgw-after.d85d3e2cb67fd2ed1a3be645d443e9f5910409fd.png)

    It acts as a Regional virtual router for traffic flowing between your virtual private clouds (VPC) and VPN connections. A transit gateway scales elastically based on the volume of network traffic. Routing through a transit gateway operates at layer 3, where the packets are sent to a specific next-hop attachment, based on their destination IP addresses.

    A transit gateway attachment is both a source and a destination of packets. You can attach the following resources to your transit gateway:

    - One or more VPCs

    - One or more VPN connections

    - One or more AWS Direct Connect gateways

    - One or more transit gateway peering connections

    If you attach a transit gateway peering connection, the transit gateway must be in a different Region.

    Hence, the correct answer is: ***Set up an AWS Transit Gateway to implement a hub-and-spoke network topology in each region that routes all traffic through a network transit center. Route traffic between VPCs and the on-premises data centers over AWS Site-to-Site VPNs.***

    The option that says: ***Set up an AWS Direct Connect Gateway to achieve inter-region VPC access to all of the AWS resources and on-premises data centers. Set up a link aggregation group (LAG) to aggregate multiple connections at a single AWS Direct Connect endpoint in order to treat them as a single, managed connection. Launch a virtual private gateway in each VPC and then create a public virtual interface for each AWS Direct Connect connection to the Direct Connect Gateway*** is incorrect because you can only create a **private** virtual interface to a Direct Connect gateway and not a **public** virtual interface. Using a link aggregation group (LAG) is also irrelevant in this scenario because it is just a logical interface that uses the Link Aggregation Control Protocol (LACP) to aggregate multiple connections at a single AWS Direct Connect endpoint, allowing you to treat them as a single, managed connection. Ultimately, an AWS Direct Connect Gateway is quite limited as opposed to a Transit Gateway as it can only manage a single connection for multiple VPCs or VPNs that are in the same Region. Remember that the multinational company has several VPCs and VPN connections in multiple AWS Regions.

    The option that says: ***Enable inter-region VPC peering which allows peering relationships to be established between VPCs across different AWS regions. This will ensure that the traffic will always stay on the global AWS backbone and will never traverse the public Internet*** is incorrect because this solution would require a lot of manual setup and management overhead to successfully build a functional, error-free inter-region VPC network compared with just using a Transit Gateway. Although the Inter-Region VPC Peering provides a cost-effective way to share resources between regions or replicate data for geographic redundancy, its connections are not dedicated and highly available. Moreover, it doesn't support the company's on-premises data centers in multiple AWS Regions.

    The option that says: ***Set up an AWS VPN CloudHub for inter-region VPC access and a Direct Connect gateway for the VPN connections to the on-premises data centers. Create a virtual private gateway in each VPC, then create a private virtual interface for each AWS Direct Connect connection to the Direct Connect gateway*** is incorrect because this solution doesn't meet the requirement of interconnecting all of the company's on-premises networks, VPNs, and VPCs into a **single** gateway, that includes support for inter-region peering across multiple AWS regions. As its name implies, the AWS VPN CloudHub is only for **VPNs** and not for VPCs. It is also not capable of managing hundreds of VPCs with multiple VPN connections to their data centers that span to multiple AWS Regions.

Flow Logs are used in VPC and not on specific EC2 instance.

**A company is looking to store their confidential financial files in AWS which are accessed every week. The Architect was instructed to set up the storage system which uses envelope encryption and automates key rotation. It should also provide an audit trail which shows who used the encryption key and by whom for security purposes.Which of the following should the Architect implement to satisfy the requirement in the most cost-effective way? (Select TWO.)**

- [ ]  ​Amazon Certificate Manager
- [ ]  ​Configure Server-Side Encryption with Customer-Provided Keys (SSE-C).
- [ ]  ​Use Amazon S3 to store the data.
- [ ]  ​Use Amazon S3 Glacier Deep Archive to store the data.
- [ ]  ​Configure Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS).
- [ ]  ​Configure Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3).

### **Explanation**

- Answer

    Server-side encryption is the encryption of data at its destination by the application or service that receives it. AWS Key Management Service (AWS KMS) is a service that combines secure, highly available hardware and software to provide a key management system scaled for the cloud. Amazon S3 uses AWS KMS customer master keys (CMKs) to encrypt your Amazon S3 objects. SSE-KMS encrypts only the object data. Any object metadata is not encrypted. If you use customer-managed CMKs, you use AWS KMS via the AWS Management Console or AWS KMS APIs to centrally create encryption keys, define the policies that control how keys can be used, and audit key usage to prove that they are being used correctly. You can use these keys to protect your data in Amazon S3 buckets.

    ![https://docs.aws.amazon.com/kms/latest/developerguide/images/key-hierarchy-cmk.png](https://docs.aws.amazon.com/kms/latest/developerguide/images/key-hierarchy-cmk.png)

    A customer master key (CMK) is a logical representation of a master key. The CMK includes metadata, such as the key ID, creation date, description, and key state. The CMK also contains the key material used to encrypt and decrypt data. You can use a CMK to encrypt and decrypt up to 4 KB (4096 bytes) of data. **Typically, you use CMKs to generate, encrypt, and decrypt the data keys that you use outside of AWS KMS to encrypt your data**. This strategy is known as **envelope encryption.**

    You have three mutually exclusive options depending on how you choose to manage the encryption keys:

    **Use Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)** – Each object is encrypted with a unique key. As an additional safeguard, it encrypts the key itself with a master key that it regularly rotates. Amazon S3 server-side encryption uses one of the strongest block ciphers available, 256-bit Advanced Encryption Standard (AES-256), to encrypt your data.

    **Use Server-Side Encryption with Customer Master Keys (CMKs) Stored in AWS Key Management Service (SSE-KMS)** – Similar to SSE-S3, but with some additional benefits and charges for using this service. There are separate permissions for the use of a CMK that provides added protection against unauthorized access of your objects in Amazon S3. SSE-KMS also provides you with an audit trail that shows when your CMK was used and by whom. Additionally, you can create and manage customer-managed CMKs or use AWS managed CMKs that are unique to you, your service, and your Region.

    **Use Server-Side Encryption with Customer-Provided Keys (SSE-C)** – You manage the encryption keys and Amazon S3 manages the encryption, as it writes to disks, and decryption when you access your objects.

    In the scenario, the company needs to store financial files in AWS which are accessed every week and the solution should use envelope encryption. This requirement can be fulfilled by using an Amazon S3 configured with Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS). Hence, **using Amazon S3 to store the data** and **configuring Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS)** are the correct answers.

    **Using Amazon S3 Glacier Deep Archive to store the data** is incorrect because although this provides the most cost-effective storage solution, it is not the appropriate service to use if the files being stored are frequently accessed every week.

    **Configuring Server-Side Encryption with Customer-Provided Keys (SSE-C)** and **configuring Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)** are incorrect because although you can configure automatic key rotation, these two do not provide you with an audit trail that shows when your CMK was used and by whom, unlike Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS).

**An application is using a RESTful API hosted in AWS which uses Amazon API Gateway and AWS Lambda. There is a requirement to trace and analyze user requests as they travel through your Amazon API Gateway APIs to the underlying services. Which of the following is the most suitable service to use to meet this requirement?**

- ​CloudTrail
- ​CloudWatch
- ​VPC Flow Logs
- ​AWS X-Ray

### **Explanation**

- Answer

    You can use [AWS X-Ray](https://docs.aws.amazon.com/xray/latest/devguide/xray-services-apigateway.html) to trace and analyze user requests as they travel through your Amazon API Gateway APIs to the underlying services. API Gateway supports AWS X-Ray tracing for all API Gateway endpoint types: regional, edge-optimized, and private. You can use AWS X-Ray with Amazon API Gateway in all regions where X-Ray is available.

    X-Ray gives you an end-to-end view of an entire request, so you can analyze latencies in your APIs and their backend services. You can use an X-Ray service map to view the latency of an entire request and that of the downstream services that are integrated with X-Ray. And you can configure sampling rules to tell X-Ray which requests to record, at what sampling rates, according to criteria that you specify. If you call an API Gateway API from a service that's already being traced, API Gateway passes the trace through, even if X-Ray tracing is not enabled on the API.

    You can enable X-Ray for an API stage by using the API Gateway management console, or by using the API Gateway API or CLI.

    ![https://docs.aws.amazon.com/apigateway/latest/developerguide/images/apigateway-xray-traceview-1.png](https://docs.aws.amazon.com/apigateway/latest/developerguide/images/apigateway-xray-traceview-1.png)

    ***VPC Flow Logs*** is incorrect because this is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your entire VPC. Although it can capture some details about the incoming user requests, it is still better to use AWS X-Ray as it provides a better way to debug and analyze your microservices applications with request tracing so you can find the root cause of your issues and performance.

    ***CloudWatch*** is incorrect because this is a monitoring and management service. It does not have the capability to trace and analyze user requests as they travel through your Amazon API Gateway APIs.

    ***CloudTrail*** is incorrect because this is primarily used for IT audits and API logging of all of your AWS resources. It does not have the capability to trace and analyze user requests as they travel through your Amazon API Gateway APIs, unlike AWS X-Ray.

**An auto-scaling group of Linux EC2 instances is created with basic monitoring enabled in CloudWatch. You noticed that your application is slow so you asked one of your engineers to check all of your EC2 instances. After checking your instances, you noticed that the auto scaling group is not launching more instances as it should be, even though the servers already have high memory usage.Which of the following are possible solutions that an Architect can implement to solve this issue? (Select TWO.)**

- [ ]  ​Install CloudWatch monitoring scripts in the instances. Send custom metrics to CloudWatch which will trigger your Auto Scaling group to scale up.
- [ ]  ​Enable detailed monitoring on the instances.
- [ ]  ​Install AWS SDK in the EC2 instances. Create a script that will trigger the Auto Scaling event if there is a high memory usage.
- [ ]  ​Modify the scaling policy to increase the threshold to scale up the number of instances.
- [ ]  ​Install the CloudWatch agent to the EC2 instances which will trigger your Auto Scaling group to scale up.

### **Explanation**

- Answer

    The Amazon CloudWatch Monitoring Scripts for Amazon Elastic Compute Cloud (Amazon EC2) Linux-based instances demonstrate how to produce and consume Amazon CloudWatch custom metrics. These sample Perl scripts comprise a fully functional example that reports memory, swap, and disk space utilization metrics for a Linux instance.

    ![https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/aeb-container-cw.png](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/aeb-container-cw.png)

    The premise of the scenario is that the EC2 servers have **high memory** usage, but since this specific metric is not tracked by the Auto Scaling group by default, the scaling up activity is not being triggered. Remember that by default, CloudWatch doesn't monitor memory usage but only the CPU utilization, Network utilization, Disk performance and Disk Reads/Writes.

    This is the reason why you have to install CloudWatch Monitoring Scripts in your EC2 instances to collect and monitor the custom metric (memory usage), which will be used by your Auto Scaling Group as a trigger for scaling activities.

    CloudWatch does not monitor EC2 memory usage as well as disk space utilization. You would have to collect the metrics using a script or by using a CloudWatch agent then send the data to CloudWatch. Hence, the correct answers are:

    ***- Install CloudWatch monitoring scripts in the instances. Send custom metrics to CloudWatch which will trigger your Auto Scaling group to scale up.***

    ***- Install the CloudWatch agent to the EC2 instances which will trigger your Auto Scaling group to scale up.***

    The option that says: ***Install AWS SDK in the EC2 instances. Create a script that will trigger the Auto Scaling event if there is a high memory usage*** is incorrect because AWS SDK is a set of programming tools that allow you to create applications that run using Amazon cloud services. You would have to program the alert which is not the best strategy for this scenario.

    The option that says: ***Enable detailed monitoring on the instances*** is incorrect because detailed monitoring does not provide metrics for memory usage. CloudWatch does not monitor memory usage in its default set of EC2 metrics and **detailed monitoring just provides a higher frequency of metrics (1-minute frequency).**

    The option that says: ***Modify the scaling policy to increase the threshold to scale up the number of instances*** is incorrect because you are already maxing out your usage, which should in effect cause an auto-scaling event.

**A real-time data analytics application is using AWS Lambda to process data and store results in JSON format to an S3 bucket. To speed up the existing workflow, you have to use a service where you can run sophisticated Big Data analytics on your data without moving them into a separate analytics system. Which of the following group of services can you use to meet this requirement?**

- ​S3 Select, Amazon Athena, Amazon Redshift Spectrum
- ​Amazon X-Ray, Amazon Neptune, DynamoDB
- ​Amazon Glue, Glacier Select, Amazon Redshift
- ​S3 Select, Amazon Neptune, DynamoDB DAX

### **Explanation**

- Answer

    Amazon S3 allows you to run sophisticated Big Data analytics on your data without moving the data into a separate analytics system. In AWS, there is a suite of tools that make analyzing and processing large amounts of data in the cloud faster, including ways to optimize and integrate existing workflows with Amazon S3:

    **1. S3 Select**

    Amazon S3 Select is designed to help analyze and process data within an object in Amazon S3 buckets, faster and cheaper. It works by providing the ability to retrieve a subset of data from an object in Amazon S3 using simple SQL expressions. Your applications no longer have to use compute resources to scan and filter the data from an object, potentially increasing query performance by up to 400%, and reducing query costs as much as 80%. You simply change your application to use SELECT instead of GET to take advantage of S3 Select.

    **2. Amazon Athena**

    Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL expressions. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries you run. Athena is easy to use. Simply point to your data in Amazon S3, define the schema, and start querying using standard SQL expressions. Most results are delivered within seconds. With Athena, there’s no need for complex ETL jobs to prepare your data for analysis. This makes it easy for anyone with SQL skills to quickly analyze large-scale datasets.

    **3. Amazon Redshift Spectrum**

    Amazon Redshift also includes Redshift Spectrum, allowing you to directly run SQL queries against exabytes of unstructured data in Amazon S3. No loading or transformation is required, and you can use open data formats, including Avro, CSV, Grok, ORC, Parquet, RCFile, RegexSerDe, SequenceFile, TextFile, and TSV. Redshift Spectrum automatically scales query compute capacity based on the data being retrieved, so queries against Amazon S3 run fast, regardless of data set size.

**You are working for a media company and you need to configure an Amazon S3 bucket to serve static assets for your public-facing web application. Which methods ensure that all of the objects uploaded to the S3 bucket can be read publicly all over the Internet? (Select TWO.)**

- [ ]  ​Create an IAM role to set the objects inside the S3 bucket to public read.
- [ ]  ​Configure the S3 bucket policy to set all objects to public read.
- [ ]  ​Grant public read access to the object when uploading it using the S3 Console.
- [ ]  ​Do nothing. Amazon S3 objects are already public by default.
- [ ]  ​Configure the ACL of the S3 bucket to set all objects to be publicly readable and writeable.

### **Explanation**

- Answer

    By default, all Amazon S3 resources such as buckets, objects, and related subresources are private which means that only the AWS account holder (resource owner) that created it has access to the resource. The resource owner can optionally grant access permissions to others by writing an access policy. In S3, you also set the permissions of the object during upload to make it public.

    Amazon S3 offers access policy options broadly categorized as resource-based policies and user policies. Access policies you attach to your resources (buckets and objects) are referred to as resource-based policies.

    For example, bucket policies and access control lists (ACLs) are resource-based policies. You can also attach access policies to users in your account. These are called user policies. You may choose to use resource-based policies, user policies, or some combination of these to manage permissions to your Amazon S3 resources.

    You can also manage the public permissions of your objects during upload. Under *Manage public permissions* you can grant read access to your objects to the general public (everyone in the world), for all of the files that you're uploading. Granting public read access is applicable to a small subset of use cases such as when buckets are used for websites.

    ![https://i.udemycdn.com/redactor/raw/2020-05-22_03-44-35-8faafd3a03fc514d237f5eb8ded2faee.png](https://i.udemycdn.com/redactor/raw/2020-05-22_03-44-35-8faafd3a03fc514d237f5eb8ded2faee.png)

    Hence, the correct answers are:

    **Grant public read access to the object when uploading it using the S3 Console.**

    **Configure the S3 bucket policy to set all objects to public read.**

    **Configuring the ACL of the S3 bucket to set all objects to be publicly readable and writeable** is incorrect as ACLs are primarily used to grant basic read/write permissions to AWS accounts and are not suitable for providing public access over the Internet.

    **Creating an IAM role to set the objects inside the S3 bucket to public read** is incorrect. You can create an IAM role and attach it to an EC2 instance in order to retrieve objects from the S3 bucket or add new ones. **An IAM Role, in itself, cannot directly make the S3 objects public or change the permissions of each individual object.**

    The option that says: **Do nothing. Amazon S3 objects are already public by default** is incorrect because by default, all the S3 resources are private, so only the AWS account that created the resources can access them.

**You are working as a Solutions Architect for a financial firm which is building an internal application that processes loans, accruals, and interest rates for their clients. They require a storage service that is able to handle future increases in storage capacity of up to 16 TB and can provide the lowest-latency access to their data. Their web application will be hosted in a single m5ad.24xlarge Reserved EC2 instance which will process and store data to the storage service.Which of the following would be the most suitable storage service that you should use to meet this requirement?**

- ​Storage Gateway
- ​S3
- ​EFS
- ​EBS

### **Explanation**

- Answer

    Amazon Web Services (AWS) offers cloud storage services to support a wide range of storage workloads such as Amazon S3, EFS and EBS. Amazon EFS is a file storage service for use with Amazon EC2. Amazon EFS provides a file system interface, file system access semantics (such as strong consistency and file locking), and concurrently-accessible storage for up to thousands of Amazon EC2 instances. Amazon S3 is an object storage service. Amazon S3 makes data available through an Internet API that can be accessed anywhere. Amazon EBS is a block-level storage service for use with Amazon EC2. Amazon EBS can deliver performance for workloads that require the **lowest-latency access to data** from a single EC2 instance. You can also increase EBS storage for up to 16TB or add new volumes for additional storage.

    In this scenario, the company is looking for a storage service which can provide the lowest-latency access to their data which will be fetched by a single m5ad.24xlarge Reserved EC2 instance. This type of workloads can be supported better by using either EFS or EBS but in this case, the latter is the most suitable storage service. As mentioned above, EBS provides the *lowest-latency* access to the data for your EC2 instance since the volume is directly attached to the instance. In addition, the scenario does not require concurrently-accessible storage since they only have one instance.

    Hence, the correct answer is **EBS**.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2019-01-27_08-08-30-95c0c6fa077cd4d2c0dc4dd23c98ef09.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2019-01-27_08-08-30-95c0c6fa077cd4d2c0dc4dd23c98ef09.png)

    **Storage Gateway** is incorrect since this is primarily used to extend your on-premises storage to your AWS Cloud.

    **S3** is incorrect because although this is also highly available and highly scalable, it still **does not provide the lowest-latency access to the data**, unlike EBS. Remember that **S3 does not reside within your VPC by default**, which means the data will **traverse the public Internet** that may result to higher latency. You can set up a VPC Endpoint for S3 yet still, its latency is greater than that of EBS.

    **EFS** is incorrect because the scenario does not require concurrently-accessible storage since the internal application is only hosted in one instance. Although EFS can provide low latency data access to the EC2 instance as compared with S3, the storage service that can provide the lowest latency access is still EBS.

**[SAA-C02] A newly hired Solutions Architect is checking all of the security groups and network access control list rules of the company's AWS resources. For security purposes, the MS SQL connection via port 1433 of the database tier should be secured. Below is the security group configuration of their Microsoft SQL Server database:**

![https://udemy-images.s3.amazonaws.com/redactor/raw/2020-01-11_08-59-07-8cf0adda84f8f9ecd6201220e6901cc5.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2020-01-11_08-59-07-8cf0adda84f8f9ecd6201220e6901cc5.png)

**The application tier hosted in an Auto Scaling group of EC2 instances is the only identified resource that needs to connect to the database. The Architect should ensure that the architecture complies with the best practice of granting least privilege.**

**Which of the following changes should be made to the security group configuration?**

- ​For the MS SQL rule, change the `Source` to the EC2 instance IDs of the underlying instances of the Auto Scaling group.
- ​For the MS SQL rule, change the `Source` to the Network ACL ID attached to the application tier.
- ​For the MS SQL rule, change the `Source` to the security group ID attached to the application tier.
- ​For the MS SQL rule, change the `Source` to the static AnyCast IP address attached to the application tier.

### **Explanation**

- Answer

    A **security group** acts as a virtual firewall for your instance to control inbound and outbound traffic. When you launch an instance in a VPC, you can assign up to five security groups to the instance. Security groups act at the instance level, not the subnet level. Therefore, each instance in a subnet in your VPC can be assigned to a different set of security groups.

    If you launch an instance using the Amazon EC2 API or a command line tool and you don't specify a security group, the instance is automatically assigned to the default security group for the VPC. If you launch an instance using the Amazon EC2 console, you have an option to create a new security group for the instance.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2020-01-11_09-55-33-102a3438068e9bb4c45fa670155c2044.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2020-01-11_09-55-33-102a3438068e9bb4c45fa670155c2044.png)

    For each security group, you add *rules* that control the inbound traffic to instances, and a separate set of rules that control the outbound traffic. This section describes the basic things that you need to know about security groups for your VPC and their rules.

    Amazon security groups and network ACLs don't filter traffic to or from link-local addresses (`169.254.0.0/16`) or AWS reserved IPv4 addresses (these are the first four IPv4 addresses of the subnet, including the Amazon DNS server address for the VPC). Similarly, flow logs do not capture IP traffic to or from these addresses.

    In the scenario, the security group configuration allows any server (0.0.0.0/0) from anywhere to establish an MS SQL connection to the database via the 1433 port. The most suitable solution here is to change the **`Source`** field to the security group ID attached to the application tier.

    Hence, the correct answer is the option that says: **For the MS SQL rule, change the `Source` to the security group ID attached to the application tier**.

    The option that says: **For the MS SQL rule, change the `Source` to the EC2 instance IDs of the underlying instances of the Auto Scaling group** is incorrect because using the EC2 instance IDs of the underlying instances of the Auto Scaling group as the source can cause intermittent issues. New instances will be added and old instances will be removed from the Auto Scaling group over time, which means that you have to manually update the security group setting once again. A better solution is to use the security group ID of the Auto Scaling group of EC2 instances.

    The option that says: **For the MS SQL rule, change the `Source` to the static AnyCast IP address attached to the application tier** is incorrect because a static AnyCast IP address is primarily used for AWS Global Accelerator and not for security group configurations.

    The option that says: **For the MS SQL rule, change the `Source` to the Network ACL ID attached to the application tier** is incorrect because you have to use the security group ID instead of the Network ACL ID of the application tier. Take note that the Network ACL covers the entire subnet which means that other applications that use the same subnet will also be affected.

**You launched an EC2 instance in your newly created VPC. You have noticed that the generated instance does not have an associated DNS hostname.Which of the following options could be a valid reason for this issue?**

- ​The newly created VPC has an invalid CIDR block.
- ​Amazon Route53 is not enabled.
- ​The DNS resolution and DNS hostname of the VPC configuration should be enabled.
- ​The security group of the EC2 instance needs to be modified.

### **Explanation**

- Answer

    When you launch an EC2 instance into a default VPC, AWS provides it with public and private DNS hostnames that correspond to the public IPv4 and private IPv4 addresses for the instance.

    However, when you launch an instance into a non-default VPC, AWS provides the instance with a private DNS hostname only. New instances will only be provided with public DNS hostname depending on these two DNS attributes: the **DNS resolution** and **DNS hostnames**, that you have specified for your VPC, and if your instance has a public IPv4 address.

    In this case, the new EC2 instance does not automatically get a DNS hostname because the **DNS resolution** and **DNS hostnames** attributes are disabled in the newly created VPC.

    The option that says: **The newly created VPC has an invalid CIDR block** is incorrect since it's very unlikely that a VPC has an invalid CIDR block because of AWS validation schemes.

    The option that says: **Amazon Route 53 is not enabled** is incorrect since Route 53 does not need to be enabled. Route 53 is the DNS service of AWS, but the VPC is the one that enables assigning of instance hostnames.

    The option that says: **The security group of the EC2 instance needs to be modified** is incorrect since security groups are just firewalls for your instances. They filter traffic based on a set of security group rules.

**A company has an OLTP (Online Transactional Processing) application that is hosted in an Amazon ECS cluster using the Fargate launch type. It has an Amazon RDS database that stores data of its production website. The Data Analytics team needs to run queries against the database to track and audit all user transactions. These query operations against the production database must not impact application performance in any way.Which of the following is the MOST suitable and cost-effective solution that you should implement?**

- ​Set up a new Amazon Redshift database cluster. Migrate the product database into Redshift and allow the Data Analytics team to fetch data from it.
- ​Upgrade the instance type of the RDS database to a large instance.
- ​Set up a new Amazon RDS Read Replica of the production database. Direct the Data Analytics team to query the production data from the replica.
- ​Set up a Multi-AZ deployments configuration of your production database in RDS. Direct the Data Analytics team to query the production data from the standby instance.

### **Explanation**

- Answer

    Amazon RDS Read Replicas provide enhanced performance and durability for database (DB) instances. This feature makes it easy to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads.

    You can create one or more replicas of a given source DB Instance and serve high-volume application read traffic from multiple copies of your data, thereby increasing aggregate read throughput. Read replicas can also be promoted when needed to become standalone DB instances. Read replicas are available in Amazon RDS for MySQL, MariaDB, Oracle and PostgreSQL, as well as Amazon Aurora.

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2020-01-16_09-06-35-c09d77a9e6c2998538885b574784c9df.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2020-01-16_09-06-35-c09d77a9e6c2998538885b574784c9df.png)

    You can reduce the load on your source DB instance by routing read queries from your applications to the read replica. These replicas allow you to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads.

    Because read replicas can be promoted to master status, they are useful as part of a sharding implementation. To shard your database, add a read replica and promote it to master status, then, from each of the resulting DB Instances, delete the data that belongs to the other shard.

    Hence, the correct answer is: **Set up a new Amazon RDS Read Replica of the production database. Direct the Data Analytics team to query the production data from the replica.**

    The option that says: **Set up a new Amazon Redshift database cluster. Migrate the product database into Redshift and allow the Data Analytics team to fetch data from it** is incorrect because Redshift is primarily used for OLAP (Online Analytical Processing) applications and not for OLTP.

    The option that says: **Set up a Multi-AZ deployments configuration of your production database in RDS. Direct the Data Analytics team to query the production data from the standby instance** is incorrect because you can't directly connect to the standby instance. This is only used in the event of a database failover when your primary instance encountered an outage.

    The option that says: **Upgrade the instance type of the RDS database to a large instance** is incorrect because this entails a significant amount of cost. Moreover, the production database could still be affected by the queries done by the Data Analytics team. A better solution for this scenario is to use a Read Replica instead.

**[SAA-C02] A company has a High Performance Computing (HPC) cluster that is composed of EC2 Instances with Provisioned IOPS volume to process transaction-intensive, low-latency workloads. The Solutions Architect must maintain high IOPS while keeping the latency down by setting the optimal queue length for the volume. The size of each volume is 10 GiB.Which of the following is the MOST suitable configuration that the Architect should set up?**

- ​Set the IOPS to 500 then maintain a low queue length.
- ​Set the IOPS to 400 then maintain a low queue length.
- ​Set the IOPS to 600 then maintain a high queue length.
- ​Set the IOPS to 800 then maintain a low queue length.

### **Explanation**

- Answer

    Provisioned IOPS SSD (`io1`) volumes are designed to meet the needs of I/O-intensive workloads, particularly database workloads, that are sensitive to storage performance and consistency. Unlike `gp2`, which uses a bucket and credit model to calculate performance, an `io1` volume allows you to specify a consistent IOPS rate when you create the volume, and Amazon EBS delivers within 10 percent of the provisioned IOPS performance 99.9 percent of the time over a given year.

    An `io1` volume can range in size from 4 GiB to 16 TiB. You can provision from 100 IOPS up to 64,000 IOPS per volume on [Nitro system](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html#ec2-nitro-instances) instance families and up to 32,000 on other instance families. **The maximum ratio of provisioned IOPS to requested volume size (in GiB) is 50:1.**

    For example, a 100 GiB volume can be provisioned with up to 5,000 IOPS. On a supported instance type, any volume 1,280 GiB in size or greater allows provisioning up to the 64,000 IOPS maximum (50 × 1,280 GiB = 64,000).

    ![https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/io1_throughput.png](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/io1_throughput.png)

    An `io1` volume provisioned with up to 32,000 IOPS supports a maximum I/O size of 256 KiB and yields as much as 500 MiB/s of throughput. With the I/O size at the maximum, peak throughput is reached at 2,000 IOPS. A volume provisioned with more than 32,000 IOPS (up to the cap of 64,000 IOPS) supports a maximum I/O size of 16 KiB and yields as much as 1,000 MiB/s of throughput.

    The volume queue length is the number of pending I/O requests for a device. Latency is the true end-to-end client time of an I/O operation, in other words, the time elapsed between sending an I/O to EBS and receiving an acknowledgement from EBS that the I/O read or write is complete. Queue length must be correctly calibrated with I/O size and latency to avoid creating bottlenecks either on the guest operating system or on the network link to EBS.

    Optimal queue length varies for each workload, depending on your particular application's sensitivity to IOPS and latency. If your workload is not delivering enough I/O requests to fully use the performance available to your EBS volume then your volume might not deliver the IOPS or throughput that you have provisioned.

    Transaction-intensive applications are sensitive to increased I/O latency and are well-suited for SSD-backed `io1` and `gp2` volumes. You can maintain high IOPS while keeping latency down by maintaining a low queue length and a high number of IOPS available to the volume. Consistently driving more IOPS to a volume than it has available can cause increased I/O latency.

    Throughput-intensive applications are less sensitive to increased I/O latency, and are well-suited for HDD-backed `st1` and `sc1` volumes. You can maintain high throughput to HDD-backed volumes by maintaining a high queue length when performing large, sequential I/O.

    Therefore, for instance, a 10 GiB volume can be provisioned with up to **500** IOPS. Any volume 640 GiB in size or greater allows provisioning up to a maximum of 32,000 IOPS (50 × 640 GiB = 32,000). Hence, the correct answer is to **set the IOPS to 500 then maintain a low queue length**.

    **Setting the IOPS to 400 then maintaining a low queue length** is incorrect because although a value of 400 is an acceptable value, it is not the maximum value for the IOPS. You will not fully utilize the available IOPS that the volume can offer if you just set it to 400.

    The options that say: **Set the IOPS to 600 then maintain a high queue length** and **Set the IOPS to 800 then maintain a low queue length** are both incorrect because the maximum IOPS for the 10 GiB volume is only 500. Therefore, any value greater than the maximum amount, such as 600 or 800, is wrong. Moreover, you should keep the latency down by maintaining a low queue length, and not higher.
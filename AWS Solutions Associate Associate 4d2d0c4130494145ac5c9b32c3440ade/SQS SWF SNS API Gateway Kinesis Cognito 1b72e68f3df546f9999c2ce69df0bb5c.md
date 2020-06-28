# SQS, SWF, SNS, API Gateway, Kinesis, Cognito

# SQS

Web service that give you access to a message queue that can be used to store messages while waiting for a computer to process them

Distributed queue system that enables web service applications to quickly and reliably queue message that one component in the application generates to be consumed by another component.

A queue is a temporary repository for messages that are awaiting processing

***Decouple*** the components of an application so they run independently, easing message management between components

Any component of a distributed application can store messages in a fail-safe queue

Messages can contain up to 256 KB of text in any format. (not hard limit, it's store on S3 so can go up to TB)

Any component can later retrieve the messages programmatically using the Amz SQS API

- (SQS) Pull-based, not pushed-based (SNS), require a compute component (EC2) pulling the message out of queue
- **Messages can be kept in the queue from 1 minute to 14 days, default retention period is 4 days**
- Messages will be processed/delivered at least once
- Visibility timeout
    - Amount of time that the message is invisible in the SQS queue after a reader picks up that message
    - The job is done before the visibility timeout expires, the message will then be deleted
    - If not, the message will become visible again and another reader will process it
    - This could result in the same message being delivered twice
    - Eg: if message is being delivered twice? Why? Visibility timeout is not long enough, the job is taking longer time to process than visibility timeout. → increase it
    - **Maximum: 12hrs**
- Amz SQS long polling: a way to retrieve messages from Amz SQS queues
    - The regular short polling return immediately (even if the message queue being polled is empty)
    - Long polling doesn't return a response until a message arrives in the message queue or times out
    - Eg: queue mostly empty, EC2 polling queue will create a charge. How to reduce bill? → long poll

## Queue Types

- Standard queues (default)
    - has nearly-unlimited number of tx/s
    - Occasionally more than one copy of a message might be delivered **out of order**
    - Multiples copies of the same message may be delivered twice

    ![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled.png)

- FIFO queues
    - Exactly-once processing
    - Exact order
    - Support message groups: multiple ordered message groups within a single queue
    - Limited to 300 TPS

    ![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%201.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%201.png)

- Charge

[https://www.slideshare.net/AmazonWebServicesJapan/aws-31275003](https://www.slideshare.net/AmazonWebServicesJapan/aws-31275003)

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%202.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%202.png)

# SWF

Amazon Simple Workflow Service (Amz SWF)

Designed as a tasks coordination 

Task is a invocation of various processing steps in an application which can be performed by code, web service calls, human actions, scripts.

Eg: Amz use inside warehouse, user order involve series of actions, take money from card, warehouse worker take order and labeling package, ... 

SWF vs SQS

- SQS has a retention period up to 14 days
- **SWF workflow execution can last up to 1 year**
- SWF: task-oriented API, SQS: message-oritented API
- SWF: task is assigned only once and is never duplicated, SQS: need to handle duplicated messages and may also need to ensure that a message is processed only once
- SWF: keep track of all task and events in an application
- SQS: DIY application-level tracking

SWF Actors

- Workflow Starters: an application that can initiate (start) a workflow
- Deciders: control the flow of activity tasks in a workflow execution, If smt finished (or failed) in a workflow, a Decider decides what to do next
- Activity Workers: carry out the activity tasks

# SNS

Simple Notification Service , setup operate send notifications from the cloud

Provides dev highly scalable, flexible, cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications.

Push notification to devices, SMS or email to SQS queues to any HTTP endpoint

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%203.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%203.png)

Group multiple recipients using topics.

Recipients subscribe to topics, topics is an "access point"

Eg: Billing Topic, Alert Topic

- Defining policies that determine which publishers and subscribers can communicate with the topic
- SNS matches the topic to a list of subs who have subscribed to that topic

One topic can support deliveries to multiple endpoint types

- Group mobile: iOS, Android, SMS recipients

When publish, SNS delivers formatted copies to subscriber

All messages are stored across multiple AZ

Benefits

- Instantaneous, push-based delivery (no polling)
- Simple APIs and easy integration with application
- Flexible message delivery over multiple transport protocols
- Inexpensive, pay-as-you-go model with no up-front costs
- Point-and-click interface in Console

SNS vs SQS

- Both meassing services in AWS
- SNS: Push
- SQS: Polls (Pulls) - EC2 polling to queue

Charge:

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%204.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%204.png)

[https://www.slideshare.net/AmazonWebServicesJapan/aws-31275003](https://www.slideshare.net/AmazonWebServicesJapan/aws-31275003)

- Auth
- 

# Elastic Transcoder

- Media Transcoder in the cloud
- Covert media to format that will play on smartphones, tablets, PCs...
- Provides transcoding presets already
- Pay based on minute transcode and resolution transcode

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%205.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%205.png)

# API Gateway

A "front door" to your AWS Services.

- Expose HTTPS endpoints to define a RESTful API
- Serverless-ly connect to services like Lambda & DynamoDB
- Send each API endpoint to a different target
- Low cost, auto scale
- Track and control usage by API key
- Throttle requests to prevent attacks
- Connect to CloudWatch to log all request
- Maintain multiple version of APIt
- If we using Js/AJAX that use multiple domains with API Gateway, ensure that you have enabled CORS on API Gateway

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%206.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%206.png)

API Gate way Caching

- Cache endpoint's response
- Reduce number of calls, improve latency of requests to API
- Caches responses from endpoint for a specified time-to-live (TTL), in seconds
- API Gateway responds to the request by looking up the cache instead of making request to endpoint

# Kinesis

Streaming data is data that generated continuously, simultaneously, in small sizes Kilobytes

- Stock Prices
- Game data (as gamer plays, LOL, Dota..)
- Social network data (hashtags, comments, tweet...)
- Geospatial data (uber, grab, ..)
- iOT sensor data

Kinesis is a platform allow sending streaming data to Kinesis

- Kinesis Streams

    ![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%207.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%207.png)

    - Shards:
        - Read: 5tps, 2MB/s
        - Write: 1000 tps, 1MB/s

- Kinesis Firehose
    - Data comes in, no persistent storage
    - Have a lambda function do smt with it
    - Output it to some where

    ![https://udemy-images.s3.amazonaws.com/redactor/raw/2018-11-12_21-25-45-a0789b019c82e01bc6cbc2830a24f90f.png](https://udemy-images.s3.amazonaws.com/redactor/raw/2018-11-12_21-25-45-a0789b019c82e01bc6cbc2830a24f90f.png)

    ![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%208.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%208.png)

- Kinesis Analytics
    - Work with both above Kinesis type
    - Analyze data on the fly and store data some where

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%209.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%209.png)

# Web Identity Federation - Cognito

Give user access to AWS resources after they have successfully authenticated with web-based identity provider like Amazon, Fb or GG

After successfull authentication, user receives Authn code from Web ID provider, which can trade for temporary AWS security credentials.

Feature:

- Sign up and sign in to your apps
- Access for guest user
- Sync user data for multiple devices

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%2010.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%2010.png)

Cognito User Pools

- User Poll: user name, email address, ...
- Identity Pool: actual granting of authentication to

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%2011.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%2011.png)

Cognito Synchronisation

- Track the association between user identity and the various different devices they sign-in from
- Use Push Synchronization to push updates and sync user data across multiple devices
- Use SNS to send notification to all devices associated with user identity whenever data stored in the cloud changes (email address change, password, setting in app... )

![SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%2012.png](SQS%20SWF%20SNS%20API%20Gateway%20Kinesis%20Cognito%201b72e68f3df546f9999c2ce69df0bb5c/Untitled%2012.png)
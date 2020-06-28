# HA Architecture

# Elastic Load Balancer

Balance the network load across multiple web server 

3 types

- Application LB
    - best suited for LB of HTTP and HTTPS traffic
    - operate at Layer 7 and are application-aware
- Network LB
    - best suited for LB of TCP traffic where extreme performance is required
    - operate at Layer 4 (connection level)
    - capable of handling millions of requests per second, while maintaining ultra-low latencies
- Classic LB
    - legacy Elastic Load Balancers
    - can load balance HTTP/HTTPS application and user layer 7, can also use layer 4 LB
    - if don't care how traffic is routed, just use basic round robin, should use this cause a bit cheaper

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled.png)

EC2 instance will log the ELB IP instead of user IP, so do look for X-Forwarded-For header

- 504 Error means the gateway has timed out. This means that the application not responding within the idle timeout period
- Troubleshoot the application, is it the Web Server or Database Server
- Instances monitored by ELB are reported as: InService, or OutofService
- LB have their own DNS name, you are never given an IP address

Target group: your LB routes requests to the targets in a target group using the target group settings that you specify, perform health check ..

Basically, group of EC2 instances for American customers, another group for European customers, having different language, currency setting, can create ALB to detect those and send request to the right group

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%201.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%201.png)

## Sticky Sessions

Classic LB routes each request independently to the registered EC2 instance with the smallest load

Allow to bind a user's session to a specific EC2 instance. This ensure that all requests from the user during the session are sent to the same instance

Can enable Sticky Sessions for ALB as well, but traffic will be sent at the Target Group Level

Can be useful if you are storing information locally to that instance

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%202.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%202.png)

## Cross Zone LB

Load balance across multiple AZ

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%203.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%203.png)

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%204.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%204.png)

## Path Patterns

Create a listener with rules to forward requests based on the URL path

If you are running micro-services, you can route traffic to multiple back-end services using path-based routing

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%205.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%205.png)

# Auto Scalling

Has 3 Components

- Groups
    - Logical component: webserver group or Application group or database group ...
- Configuration Templates
    - Each group use a launch template or launch configuration as a configuration template for its EC2 instance
    - Can specify information such as AMI ID, instance type, key pair, SG, ...
- Scaling Options
    - Maintain current instance levels at all times
    - scale manually
    - scale based on a schedule
    - scale based on demand
    - use predictive scaling

 

# HA Architecture

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%206.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%206.png)

- always design for failure
- use multiple AZ's and multiple regions where ever you can
- know the difference between multi-az and read replicas for RDS
- know the difference between scaling out and scaling up
    - scaling out: use ASG
    - scaling up: increase the resource of each EC2 instance
- read the question carefully and always consider the cost element
- know the different S3 storage classes

Sample HA Wordpress

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%207.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%207.png)

# CloudFormation

- scripting your cloud environment
- json
- quick start is a bunch of CloudFormation templates already built by AWS SA allow you to create complex env very quickly

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%208.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%208.png)

# Elastic Beanstack

- quickly deploy and manage app without worry ab the infra
- upload app then auto handle details of capacity provisioning, LB, scaling, app health check
- like heroku

![HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%209.png](HA%20Architecture%20bf45df6b19904351a163b8bf327ccf43/Untitled%209.png)

- Availability when user need
- Durability refers to the on-going existence of the object or resource
- Resiliency can be described as the ability to a system to self heal after damage or an event
- Reliability is closely related to availability, however a system can be 'available' but not be working properly. Reliability is the probability that a system will work as designed
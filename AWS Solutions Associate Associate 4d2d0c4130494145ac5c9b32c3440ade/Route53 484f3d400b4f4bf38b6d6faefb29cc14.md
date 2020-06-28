# Route53

# DNS

Used to convert human friendly domain names into an IP address, like a yellow phone book

IPv4 space is a 32 bit has over 4 billion different address

IPv6 was created to solve this depletion and has an address space of 128 bits

## Top Level Domains

Last word in domain name: .com, .edu

The second word is second level domain name (optional, depends on the domain name): .co.uk, .gov.uk

These top level domain names are controlled by Internet Assigned Numbers Authority (IANA) in a root zone database

Can view this database by visit:

[https://www.iana.org/domains/root/db](https://www.iana.org/domains/root/db)

## Domain Registrars

Because all domain name have to be unique, there needs to be a way to make sure this is not duplicated.

→ Domain registrars

A registrar is an authority that can assign domain names directly under one ore more top-level domain

These domains are registered with InterNIC, a service of ICANN, which enforces uniqueness of domain name across the Internet

Each domain name becomes registered in a central database known as WhoIS database

Popular domain registrar: Amazon, GoDaddy, ..

## Start Of Authority Record (SOA)

After bought a domain name, every DNS address begin with a start of SOA record.

Stores information about

- The name of the server that supplied the data for the zone
- The admin of the zone
- Current version of data file
- Default number of seconds for the TTL file on resource records

## NS Records

Name Server Records

This record indicates which DNS server is authoritative for that domain 
(which server contain the actual DNS records)

[Example of an NS record](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Example%20of%20an%20NS%20record%205cd76c8da95c4a3f8529fa092cda04b7.csv)

Top Level Domain servers uses NS records to direct traffic to Content DNS server which contains the authoritative DNS records

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled.png)

- type address into browser
- browser doesn't know IP address for that domain
- browser go to Top Level Domain (TLD) server and query for authoritative DNS records:
    - browser: "I got this domain, I need to know the IP address of it"
- TLD server doesn't contain the IP address: has something similar to this:
    - domainxxx.com. 123123123 IN NS ns.awsdns.com
    - ns.awsdns.com: NS Records
- Go to NS Records, give Start Of Authority
- SOA contains DNS records

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%201.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%201.png)

How a DNS Server works - [https://www.youtube.com/watch?v=mpQZVYPuDGU](https://www.youtube.com/watch?v=mpQZVYPuDGU) 

(?) ☝️How did the TLD server know which authoratative Name Server to use?

- → Domain Registrar
- Domain Registrar has right and authority to assign which Name Server they should use
[ns1.exampleserver.com](ns1.exampleserver.com), [ns2.exampleserver.com](http://ns1.exampleserver.com/), ...
- Registrar tell the Registry to update the TLD Name Servers

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%202.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%202.png)

## A Records

A for Address, used to translate the name of the domain to an IP address.

For example: [example.com](http://example.com) → 123.10.10.10

## TTL

Length that DNS record is cached on either Resolving Server of the user local PC, in seconds

Default: 48 hrs

## CName

A Canonical Name (CName) is used to resolve one domain name to another

For eg: [m.example.com](http://m.example.com) is used for when user browser to domain name on their mobile devices

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%203.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%203.png)

Instead of 2 separate IP addresses, we map one pointing to another

## Alias Records

Map resource record sets in your hosted zone to ELB, CloudFront distributions or S3 buckets that are configured as website

Works like a CNAME record in that you can map one DNS name (www.example.com) to another 'target' DNS name elb1234.elb.amazonaws.com)

Key difference: A CNAME can't be used for naked domain names (zone apex record, domain without www)

Can't have a CNAME for http://example.com, it must be either an A record or an Alias

## Tips

It can take up to 3 days to register depending on the circumstances

ELBs do not have pre-defined IPv4 addresses, you resolve to them using a DNS name

## Routing Policies

### Simple Policy

Route53 returns all values to the user in a random order

Can only have one record with multiple IP addresses

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%204.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%204.png)

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%205.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%205.png)

### Weighted Routing Policy

Split traffic based on weight

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%206.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%206.png)

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%207.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%207.png)

**Tips**

Health Checks

- Can set health checks on individual record sets
- If a record set fails a health check it will be removed from Route53 unit till passes the health check
- Can set notifications to alert if a health check is failed

### Latency-based

Route traffic based on the lowest network latency

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%208.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%208.png)

Send request to EU-WEST-2 since it has a much lower latency

### Failover

Used when you want to create an active/passive setup

Normally, traffics are sent to primary site

Eg: set primary site to be in EU-WEST-2 and secondary DR Site in AP-SOUTHEAST-2

Route 53 will monitor the health of primary site using a health check

A health check monitors the health of your end points

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%209.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%209.png)

### Geolocation

Traffic will be sent based on the geographic location of your users

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%2010.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%2010.png)

### Geoproximity (Traffic Flow only)

Lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources.

Can choose to route more traffic or less to a given resource by specifying a value - bias

A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.

Must use Route 53 traffic flow

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%2011.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%2011.png)

### Multivalue Answer

Return multiple values, such as IP address**es** for your web servers, in response to DNS queries

Route53 returns only values for healthy resources

Similar to simple routing however it allows you to put health checks on each record set

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%2012.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%2012.png)

QA:

True or False: There is a limit to the number of domain names that you can manage using Route 53.

- True and False. With Route 53, there is a default limit of 50 domain names. However, this limit can be increased by contacting AWS support.

![Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%2013.png](Route53%20484f3d400b4f4bf38b6d6faefb29cc14/Untitled%2013.png)
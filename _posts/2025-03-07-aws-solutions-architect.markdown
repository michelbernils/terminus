---
layout: post
title:  "AWS Solutions Architect"
date:   2025-03-07 22:00:00 -0300
categories: AWS Solutions Architect
---

# Zones
1. Region: Isolated geographic area, each region consist of multiple data centers and is designed to provide low-latency and high availability.
  * eg: us-east-1.
1. Availability-Zone (AZs): Each region consist of multiple AZs which are physically separate data centers.
  * eg: us-east-1a, us-east-1b.
1. Edge-Location: data centers strategically positioned around the world to process requests closer to the end users.
  * eg: 450 Edges locations worldwide.

# IAM
Service that helps you securely control access to AWS resources.

### Access Methods
1. CLI (Need roles to access)
1. CloudShell
1. Console
1. API Calls (Need roles to access)

### What can I create with IAM
1. Users.
  * Assign each user a specific access.
1. Groups.
  * Users that share the same resources.
1. Roles.
  * Grant permissions to resources without using long-term credentials like passwords or access keys.
  * Uses STS
1. Policies.
  * JSON based permission rules attached to users, groups, or roles.  
  * Identity based policies (applied to Users, Groups, or Roles).  
  * Resource based policies (applied to AWS resources like S3, Lambda, etc.).  

### STS (Security Token Service)
AWS STS generates temporary security credentials for IAM roles, these credentials automatically expire (no need for manual rotation).  

1. Grants temporary, limited-time access to AWS resources.  
1. For cross-account access (users in one account assume a role in another).  
1. When using federated authentication (e.g., integrating AWS with Google, Okta, etc.).  

# S3
Object-based storage, it manages data as objects opposed to other storage architectures.

1. S3 provides *unlimited storage.
1. You don't need to think about the underlying infrastructure. (serverless service)
1. The S3 console provides an interface for you to upload and access your data.
1. You can store an individual object from 0 bytes to 5 terabytes in size.
1. There are 3 types of encryption: Server Side with S3 Managed Keys, Server-side encryption with AWS Keys management, Dual layer encryption.
1. You can by default create only 100 buckets.
  * You can make a request to increase it to 1000.
1. No max bucket size and no limit to the number of objects in the bucket.
  * files larger than 100MB should use multi-part upload.
1. S3 Object: object that contains your data.
  * Key: this is the name of the object.
  * Value: the data itself made up of a sequence of bytes.
  * Version-ID: when versioning enabled, the version of the object.
  * Metadata: additional information attached to the object.
1. S3 Bucket: Buckets hold objects. Buckets can also have folder which in turn hold objects.
  * S3 is a universal namespace, so buckets names must be uniques. (think like having a domain-name)

### Bucket Types
1. General purpose bucket
  * Organizes data in a flat hierarchy.
  * The original S3 bucket type.
  * Can be used for all the storage classes except S3 Express One Zone storage class.
1. Directory bucket
  * Organizes data folder hierarchy.
  * Only to be used with S3 Express One Zone storage class.
  * Single digit millisecond performance on PUT and GET.
  * 10 directory buckets per account.

### Object Overview
1. ETags: A way to detect when the contents of an object has changed without downloading the content.
1. Checksums: ensures the integrity of a file being uploaded or downloaded.
  * CRC32
  * CRC32C
  * SHA1
  * SHA256
1. Object Prefixes: simulates file-system folders in flat in a flat hierarchy.
  * /assets/images/andrew.png (all objects are stored flats, so the prefixes are a way to organize them)
1. Object Metadata: attach data alongside the content, to describe the content of the data.
1. Objects Tags: benefits resource tagging but at the object level.
1. Object Locking: makes data file immutable.
1. Object Versioning: have multiple version of a data file.

### Object WORM
Write once read many, good for financial companies, where the object stored cannot be altered.

### Object Lock
Prevent a deletion of objects in a bucket.
1. Can only be turned on when the bucket is created.
  * SEC 17a-4, CTCC, FINRA
1. Can only be made via s3-cli.

### URI
Way to reference the address of a bucket and a object.

### CLI
1. S3: high-level way to interact with s3 objects and buckets.
1. S3api: low-level way to interact with s3 objects and buckets.
1. S3control: manage s3 access points, s3 outposts buckets, s3 batch operations, storage lens.
1. s3outposts: manage end-points for s3 outposts.

### Request Styles
1. Virtual-hosted-style requests: the bucket name is a subdomain on the host.
1. Path-style requests: the bucket name is the request path.

### Classes Overview
1. Outpost: Object storage to your on-premises AWS Outposts environment
1. Standard: high durability, Availability, and performance object storage for frequently accessed data.
1. Intelligent-Tiring: Automatically reduces your storage costs on a granular object level by automatically moving data to the most cost-effective access tier based on access frequency
1. Express-one-zone: SIngle digit ms performance, special bucket-type, one AZ, 50% less than standard cost.
1. Standard-IA (Infrequent Access): Data that is accessed less frequently, but requires rapid access when needed
1. Glacier Instant Retrieve: Archive storage class that delivers the lowest-cost storage for long-lived data that is rarely accessed and requires retrieval in milliseconds
1. Glacier Flexible Retrieve: Archive data that is accessed 1—2 times per year and is retrieved asynchronously
1. Glacier Deep Archive: Archive data that is very rarely accessed and very low cost

### Standard
1. Durability: 11 9s. (99,999999999%)
1. Availability: 4 9s. (99,99%)
1. Redundancy: 3 or more availability zones.
1. Retrieval Time: Within milliseconds. (low latency)
1. Throughput: Optimized for data that is frequently accessed or real-time access.
1. Use-Cases: Wide variety of things.
1. Pricing:
  * Storage per GB.
  * Per Requests.
  * No Retrieval Fee.

### Standard Infrequent Access
1. Durability: 11 9s. (99,999999999%)
1. Availability: 3 9s. (99,9%)
1. Redundancy: 3 or more availability zones.
1. Retrieval Time: Within milliseconds. (low latency)
1. Throughput: Optimized for rapid access , although the data is accessed less frequently compared to S3 Standard
1. Use-Cases: Ideal for data that are less frequent but requires quick access when needed.
1. Pricing:
  * Storage per GB.
  * Per Requests.
  * Has Retrieval Fee.

### Express One Zone
1. 10x faster then standard.
1. Request cost 50% lower than the S3 Standard.
1. Data is stored in one AZ (Availability Zone)
1. Data is stored in a new bucket style, directory bucket.

### One Zone IA
1. Durability: 11 9s. (99,999999999%)
1. Availability: 99,5%
1. Cost-Effective: cost 20% less from Standard IA
1. Redundancy: 1 availability zone.
1. Retrieval Time: within milliseconds. (low latency)
1. Use-Cases: Secondary backup.
1. Pricing:
  * Storage per GB.
  * Per Requests.
  * Has Retrieval Fee.
  * Has a minimum storage duration charge of 30 days.

### Security Overview
1. Bucket Policies: Define permissions for an entire S3 bucket using JSON-based access policy language.
1. Access Control Lists (ACLs): Provide a legacy method to manage access permissions on individual objects and buckets.
1. AWS PrivateLink for Amazon S3: Enables private network access to S3, bypassing the public internet for enhanced security.
1. Cross-Origin Resource Sharing (CORS): Allows restricted resources on a web page from another domain to be requested.
1. Amazon S3 Block Public Access: Offers settings to easily block public access to all your S3 resources.
1. IAM Access Analyzer for S3: Analyzes resource policies to help identify and mitigate potential access risks.
1. Internet Traffic Privacy: Ensures data privacy by encrypting data moving between AWS services and the Internet.
1. Object Ownership: Manages data ownership between AWS accounts when objects are uploaded to S3 buckets.
1. Access Points: Simplifies managing data access at scale for shared datasets in S3.
1. Access Grants: Providing access to S3 data via a directory services e.g. Active Directory.
1. Versioning: Preserves, retrieves, and restores every version of every object stored in an S3 bucket.
1. MFA Delete: Adds an additional layer of security by requiring MFA for the deletion of S3 objects.
1. Object Tags: Provides a way to categorize storage by assigning key-value pairs to S3 objects.
1. In-Transit Encryption: Protects data by encrypting it as it travels to and from S3 over the internet.
1. Server-Side Encryption: Automatically encrypts data when writing it to S3 and decrypts it when downloading.
1. Client-Side Encryption: Encrypts data client-side before uploading to S3 and decrypts it after downloading.
1. Compliance Validation for Amazon S3: Ensures S3 services meet compliance requirements like HIPAA, GDPR, etc.
1. Infrastructure Security: Protects the underlying infrastructure of the S3 service, ensuring data integrity and availability.

### Block Public Access
Is a feature that comes by default, to block all public access to the bucket.
1. New access controls lists (acls) 
1. Any access controls lists
1. New bucket policies or access points.
1. Any bucket policies or access points.

### Bucket Policies
Resource-based policy to grant an s3 bucket and bucket objects to other principles eg. AWS Accounts, Users, AWS Services.

# Snowball Family
Petabyte scale data transfer service, move data into AWS via physical briefcase computer.

### Snowball
1. Low-cost
1. Faster
1. Comes in two sizes
  * 50 TB
  * 80 TB
1. Can import and export from S3.

### Snowball Edge
1. LCD Display
1. Can use clusters in groups of 5 to 10.
1. Comes ins two sizes
  * 100 TB (83 TB of usable space)
  * 100 TB Clustered (45 TB per node)

### Snowmobile
45-foot-long ruggedize shipping container, pulled by a semi-trailer truck.
1. Transfer up to 100 PB per Snowmobile.
1. GPS Tracking
1. Alarm Monitoring
1. 24/7 video surveillance
1. An escort security vehicle while in transit.

# AWS API (Go back and watch it again)

### Access Keys
Is a key and secret required to have programmatic access to AWS resources when interacting with AWS API outside the AWS Management Console.
  * Commonly known as AWS Credentials.
  * Never share your access keys and secrets.
  * Never commit access keys to a codebase.
  * You can have two active access keys.
  * Access keys have whatever access a user has to AWS resources

### STS
Web service that enables you to request temporary, limited-privileged credentials for IAM users or federated users.

1. STS will return:
  * AccessKeyID
  * SecretAccessKey
  * SessionToken
  * Expiration

1. You can use this following API actions to obtain STS.
  * AssumeRole
  * AssumeRoleWithWebIdentity
  * AssumeRoleWithSAML
  * DecodeAuthorizationMessage
  * GetAccessInfo
  * GetCallerIdentity
  * GetFederationToken
  * GetSessionToken

# VPC (Virtual Private Cloud)
Is a isolated virtual network, resembles a traditional network you'd operate in your own datacenter.
  * Launching a virtual machine. (EC2)
  * ENIs (Elastic Network Interfaces) is used within a VPC.
  * VPC is tightly coupled with EC2.
  * All VPC commands are under EC2.

### Core Components
1. Internet Gateways (IGW): A gateway that connects your VPC out to the internet.
1. Virtual Private Network (VPN Gateway): A gateway that connects to a private external network.
1. Route Tables: Determines where to route traffic within a VPC.
1. NAT Gateway: Allows private instances to connect to services outside the VPC.
1. Network Access Control Lists (NACLs): Acts as a stateless virtual firewall for compute within a VPC.
1. Security Groups: Act as a stateful virtual firewall for compute within a VPC.
1. Public Subnets: Allows instances to have public IP Addresses. 
1. Private Subnets: Subnets that disallows instances to have public IP Addresses.
1. VPC Endpoints: Privately connect to AWS support services.
1. VPC Peering: Connect to VPCs to other VPCs.

### Key Features
1. VPCs are region specific. They do not spam regions 
  * You can use VPC Peering to connect to VPC across regions.
1. You can create up to 5 VPC per regions.
1. Every region comes with a default VPC.
1. You can have 200 subnets per VPC.
1. Up to 5 IPv4 (Adjust to 50)
1. Up to 5 IPv6 (Adjust to 50)
1. Most components cost-nothing
  * VPCs, Route Tables, NACLs, Internet Gateways, Security Groups and SUbnets.
1. Some things cost money
  * VPC Endpoints, VPN Gateway, Customer Gateway, IPv4 Access.


# Lake Formation
Data lake to centrally govern, secure and globally share data for analytics and machine learning.

1. Manage fine-grained access control for your data lake data on Amazon S3.
1. Manage metadata in AWS Glue Data Catalog.
1. Lake formation provide its own permissions model that augments the IAM Permission model.
  * Thought a simple grant or revoke mechanism similar to RDBMS.
1. Allow you to share data internally and externally across multiple AWS Accounts, AWS Organizations or directly with IAM.
1. Permissions are enforced using granular controls at the column, row, and cell-levels across.
  * Athena
  * Quicksight
  * Redshift 
  * EMR
  * Glue

### Data Lake Recap
Centralized data repository for unstructured data or semi-structured data.
  * Data lake generally uses objects (blobs) or file as its storages medium.


# Route 53
1. Managed DNS (Domain Name System)
1. DNS is a collection of rules and records which helps clients understand how to reach a server through URLs.
1. Most commons records are:
  * A: URL to IPv4
  * AAAA: URL to IPv6
  * CNAME: URL to URL
  * Alias: URL to AWS Resource

1. Diagrams
  * A record:
    - Web-browser -> DNS Request to Route 53 -> Sends back the a A record -> Web-browser makes a HTTP Request to the server -> Server return an HTTP Response.
  * AAAA Record:

1. Advanced features:
  * Load Balancing (through DNS - also called Client load balancing)
  * Health checks
  * Routing Policy: simple, failover, geolocation, latency, weighted, multi-value 

1. Overview
  * public domains that you own or buy.
  * private domain names that can be resolved by your instances in your VPCs.

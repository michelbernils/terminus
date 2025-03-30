---
layout: post
title:  "AWS Cloud Practitioner"
date:   2025-03-07 22:00:00 -0300
categories: aws practitioner
---
## What is Cloud Computing?

Before -> Server Rooms
After -> Data Centers

Advantages

1. Low cost
1. Global scaling
1. Performance
1. Flexibility
1. Speed
1. Productivity
1. Security

Cloud types

1. IaaS -> Infrastructure as a service
    * Server, Virtual Machine and Storage
1. PaaS -> Platform as a service
    * Hosting and Operational System 
1. SaaS -> Software as a service
    * Applications and e-mail services

Public cloud -> AWS, GCP, Azure
Private cloud -> Banks and Government
Hybrid cloud -> Public and Private mixed


## AWS Support

There are four levels of support.

1. Developer
    * Recommended if you are experimenting or testing AWS.
    * General support.
1. Business 
    * Minimum recommended level for those with production workloads on AWS.
    * Contextual to your use cases.
1. Enterprise on-ramp
    * Recommended for those with business-critical or essential production workloads on AWS.
    * Annual consultative review and guidance according to applications.
1. Enterprise
    * Recommended for those with business and/or mission-critical workloads on AWS.
    * Consultative reviews and guidance based on applications.

### IAM (Identity and Access Management)
* Users: Individual entities with their own credentials and permissions.
* Groups: Collections of users that share common permissions.
* Roles: Identities with specific permissions that can be assumed by users, services, or applications to access resources temporarily.
* Policies: Define and attach policies (JSON documents) to users, groups, or roles that specify what actions are allowed or denied on AWS resources.

### IAM Identity Center
AWS IAM Identity Center is a service designed to simplify the process of managing user access to AWS accounts and third-party applications. It enables Single Sign-On (SSO), allowing users to log in once to access multiple applications and AWS resources without needing to re-authenticate.

### Organizations
AWS Organizations is a service that allows you to create and manage a hierarchy of AWS accounts, streamline billing, and enforce governance across multiple accounts within your organization. It is designed to simplify account management and provide a centralized approach to governance and security.

1. Centralized account management.
1. Hierarchical access control.
1. Service control.

What are Organizational Units (OUs)?

Organizational Units (OUs) are a way to organize and manage AWS accounts within AWS Organizations. They allow you to create a hierarchical structure for your accounts, grouping them based on business needs, projects, environments, or other criteria.

### CloudTrail
Service that enables governance, compliance, operational auditing, and auditing of your AWS account.

1. Report
    * Credential Report (CC): List users and information.
    * Access Advisor (AA): User level.

### Structure
1. Global Infrastructure
    * Region: Physical location around the world where we cluster data centers. eg: us-west-1
    * Availability Zone: Discrete data centers with redundant power, networking, and connectivity in an AWS Region. eg: us-west-la
    * Local Zone: Infrastructure closer to your end users and business centers.
    * Wavelength Zone: Optimized for mobile apps.
    * Outposts: Use AWS products locally.

### AWS Share Responsibility
1. Amazon: Compute, Storage, Database, Networking.
1. Customer: Platform Application, Identity and Access Management.

### Pricing Calculator
Calculate how much the selected service will cost.

## Virtualization

### Elastic Compute Cloud (EC2)
1. Rent virtual servers to run applications in the cloud.
    * Scalability: You can easily scale your EC2 instances up or down based on demand.
    * Customizability: You can choose the instance type, operating system, storage, and networking configurations.
    * Pay-as-you-go Pricing: You only pay for the compute capacity you use, with no upfront costs.
    * Security: Offers security measures like virtual private clouds (VPC), firewalls, and encryption.
    * Flexibility: Supports various operating systems (Linux, Windows, etc.) and integrations with other AWS services.

1. EC2 Types
    * Elastic Block Store (EBS): 

1. EC2 Values
    * On-Demand: $$$$
    * Saving Plans: $$ (1 to 3 years)
    * Spot: $ (90%)
    * Dedicated Host: $$$$$ (Gov or Banks)
    * Capacity on demand: $$$ 
    * Reserved Instances: For a fixed period of time.

1. EC2 Security Groups
    * Security firewall that protects the EC2 instance.
    * Can be used to block outside access.

1. Snapshots
    * Creates an registry of the EC2, can be use to move server to other regions.

1. EBS (Elastic Block Store)
    * HDD: Hard Disk (Slow + More space)
    * Solid State Drive (Fast + Less space)

1. AMI (Amazon Machine Image) 
    * An image of an EC2

1. EFS (Elastic File System)
    * Shared with other regions and EC2 instances.

1. FSx
    * A managed file system service that provides different types of file systems, including FSx for Windows File Server and FSx for Lustre.

1. Scalability
    * Vertical: Type + T2.Micro -> T2.Large
    * Horizontal: + Instances.

1. Elasticity
    * Adapt automatically (Load Balance)

1. Availability
    * Always available

1. Auto-Scaling
    * Instance Model: Script
    * AutoScaling:  % of Traffic or Possible instances

1. ELB, ALB, NLB, CLB
    * ELB (Elastic Load Balance): Directs the traffic (APP -> DNS -> Load Balance -> Server1/Server2)
    * ALB (Apply Load Balance): HTTP/HTTPS
    * NLB (Network load balance): TCP or UDP
    * CLB (Classic Load Balance): HTTP, HTTPs, TCP, SSL

## Storage

### AWS Simple Storage Service (S3)

Object storage service. 

1. S3 Standard: high durability, Availability, and performance object storage for frequently accessed data.
1. S3 Intelligent-Tiring: Automatically reduces your storage costs on a granular object level by automatically moving data to the most cost-effective access tier based on access frequency
1. S3 Standard-IA: Data that is accessed less frequently, but requires rapid access when needed
1. S3 Glacier Instant Retrieve: Archive storage class that delivers the lowest-cost storage for long-lived data that is rarely accessed and requires retrieval in milliseconds
1. S3 Glacier Flexible Retrieve: Archive data that is accessed 1—2 times per year and is retrieved asynchronously
1. S3 Glacier Deep Archive: Archive data that is very rarely accessed and very low cost
1. S3 Outpost: Amazon S3 on Outposts delivers object storage to your on-premises AWS Outposts environment

### S3 Transfer Acceleration
Speed up content transfers to and from Amazon S3 by as much as 50-500% for long-distance transfer of larger objects.
Versioning: Files with the same name.

### S3 Data Replication 
1. Buckets in the same AWS Region: S3 Same-Region Replication (SRR)
1. Buckets in different AWS Region: S3 Cross-Region Replication (CRR)

### Storage Gateway
1. Hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage. 

### Snow
1. Snowcone: Device up to 8TB storage, can be sent back to Amazon and use DataSync to sent data.
1. Snowmobile: A truck goes to your company gets your data and then uploads it to AWS. 
1. Snowball: A device bigger than Snowcone but has the same functionality.

## Databases
Relational: Tables
No-Relational: Document, Hashmap, etc

### RDS
1. Service to manage relational database
    * Scalability
    * High Availability 
    * Security
    * Performance

### Aurora
Relational database

### Elasticache
1. In-memory database (cache)
    * Redis
    * Memcache 

### DynamoDB
1. Non-Relational Database
    * 3 Availability-Zones.
    * Serverless.

### Neptune

1. Database focused on social media
    * Uses Graph.
    * 3 Availability Zones.
    * 15 Read Replicas.

## ETL Tool

### Glue
1. ETL (Extract, TRansform, Load) Tool
    * RDS -> Glue -> Redshift.
    
## Network

### VPC 
1. Virtual Private Cloud
    * Subnet.
    * Internal.
1. NACL
    * Additional layer of security for controlling traffic in and out of subnets within an Amazon Virtual Private Cloud (VPC).
1. VPC Peering
    * Networking connection between two Virtual Private Clouds (VPCs) that enables them to communicate with each other as if they were part of the same network. 
1. VPC End-Points
    * Establish private connections between your VPC and other AWS services without needing an internet gateway.
1. VPC Flow Logs
    * Capture and monitor network traffic going into and out of your Virtual Private Cloud (VPC).

### Transit
Simplifies network architecture by acting as a central hub to connect multiple Amazon VPCs, on-premises networks, and AWS accounts in a scalable, centralized, and managed manner.

### VPC Cloud Log
Creates an s3 that will keep all the logs stored.

### Direct Connect
Dedicated link between AWS and the company.

### Client VPN
Managed, scalable, and secure solution that allows you to establish a secure VPN (Virtual Private Network) connection to your AWS resources or your on-premises network from remote devices like laptops or mobile devices.

### Private Link
Secure, private connectivity between Virtual Private Clouds (VPCs), AWS services, and on-premises networks without exposing the traffic to the public internet.

## Content Delivery

### Route 53
1. Route 53 translates domain names (like example.com) into IP addresses (like 192.0.2.1) that computers use to connect to each other over the internet.
1. Domain Registration: You can register domain names directly through Route 53. This simplifies the process of buying, managing, and configuring DNS settings for domain names.
1. Route 53 allows you to route end-user traffic to AWS services (like EC2 instances, S3 buckets, or load balancers) and external resources.
1. Supports different routing policies like Simple, Latency-based, Failover, Weighted, and Geo-location-based routing to manage how traffic is directed.
1. Policies:
    * Simple Routing: Basic routing where a single record responds to queries.
    * Weighted Routing: Distributes traffic across multiple resources based on assigned weights.
    * Latency Routing: Routes traffic to the resource with the lowest network latency relative to the user’s location.
    * Failover Routing: Directs traffic to a primary resource and shifts to a backup if the primary becomes unavailable.
    * Geolocation Routing: Routes traffic based on the user's geographic location.
    * Geoproximity Routing: Routes traffic based on the user’s geographic location and the proximity of AWS resources.
    * Multi-Value Answer: Returns multiple values (IP addresses) in response to a DNS query, allowing clients to choose one.

## AWS Cloud Acceleration

### CloudFront
1. Fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency.
    * Instead of accessing your s3 bucket directly you can use a cloudfront first. (Content -> Cloudfront -> S3).

## Container

### ECS
1. Fully managed container orchestration service. It allows you to run Docker containers in a highly scalable, managed environment, without needing to install and manage the underlying infrastructure.
    * Task (JSON).
    * ECR (Elastic Container Registry).

### EKS
1. Fully managed Kubernetes service. It allows you to run Kubernetes, an open-source container orchestration platform, on AWS without having to install and maintain your own Kubernetes control plane.
    * Removes the complexity of using Kubernetes.

## Real time steaming data (AWS Kinesis family)

### Kinesis Data Streams
Ingesting and processing real-time, continuous data streams.

## Message Services

### SQS (Simple Queue Service)
Fully managed message queuing service.

### SNS (Simple Notification Service)
Fully managed pub/sub messaging service.

## Data Processing: 

### Batch
Batch processing, good to be used in ML, Data Analysis, CI/CD Pipelines.

## Other Services

### Cognito
1. AWS Cognito is a service provided by Amazon Web Services that enables developers to add user sign-up, sign-in, and access control to web and mobile applications.

### STS (Security Token Service)
Security Token Service (STS) is a web service that enables you to request temporary, limited-privilege credentials for AWS Identity and Access Management (IAM) users or federated users.

### Device Farm
Cloud-based application testing service that allows developers to test their mobile and web applications on a wide variety of physical devices.

### App Sync
1. Syncs mobile and app, when you have an update it updates both of them.
    * Uses GraphQL.

### Amplify
Amplify is a development platform that enables developers to build and deploy scalable full-stack applications powered by AWS.

### Amplify Studio
Create mobile application

### Amplify Hosting
Hosts applications

### IOT Core
Bridge to connect devices and AWS services

### Step Functions
1. Coordinates functions
    * Parallel State: two servers in parallel. 
    * Sequence: Initialize and execute.

### App Flow
AWS AppFlow is a fully managed integration service that enables users to securely transfer data between various SaaS applications and AWS services.

### Backup
Centralized backup service.

### Workspace
Desktop manager service.

### LightSail
Accelerate the lunch of an application (VPS + Web Server).

### Lambda
Serverless computing service that allows you to run code in response to events without provisioning or managing servers.

### Fargate
Serverless compute engine for running containers automatically. 

### Device Farm
Testing service that lets you run your mobile and web apps on real devices in the cloud.

### Workspace
managed, secure Desktop-as-a-Service (DaaS) solution that provides virtual cloud desktops. It allows you to provision Windows or Linux desktops in the cloud, enabling users to access their applications, documents, and resources from anywhere, on any supported device.

## Billing

### Control Tower
1. Service that helps you set up and govern a secure, multi-account AWS environment based on best practices. It provides automated account provisioning, centralized governance, and compliance controls, making it easier to manage multiple AWS accounts.
    * Big companies.
    * Companies that have multiple accounts.
    * Simplify the process of creating multiple accounts.

### RAM (Resource Access Manager)
Service that allows you to securely share your AWS resources with other AWS accounts or within your organization. 

### Service Catalog
Allows organizations to create, manage, and distribute catalogs of approved AWS resources and services. It enables administrators to control which services and configurations are available to users, ensuring compliance with organizational standards and governance policies.

### Trusted Advisor
1. Online resource that provides real-time guidance to help you provision your resources following AWS best practices. It analyzes your AWS environment and offers recommendations across several categories, including:
    * Cost Optimization: Identifies opportunities to reduce costs, such as underutilized or idle resources.
    * Performance: Suggests improvements to enhance the performance of your applications.
    * Security: Highlights security best practices, including potential vulnerabilities and necessary updates.
    * Fault Tolerance: Recommends enhancements to improve your application's resilience and uptime.
    * Service Limits: Monitors your usage against AWS service limits and alerts you when you approach them.

## Machine Learning/Artificial Intelligence

### Transcribe
1. It is a speech-to-text service that converts spoken language into written text.
    * ASR (Automatic Speak Recognition)
    * Multilingual

### Rekognition
Text, objects, persons recognition.

### Translation
1. Fully managed neural machine translation service that provides high-quality language translation in real-time
    * Text -> EN -> PT -> Website
    * Text -> PT -> EN -> Website

### Polly
Text-to-speech (TTS) service that converts text into lifelike speech.

### Comprehend
1. Natural language processing (NLP) service that uses machine learning to analyze and extract insights from text.
    * Can be used to analyze sentiments.

### Lex
1. Service for building conversational interfaces using voice and text
    * ASR: Speech to text.
    * NLU: Natural Language understand.
    * Used by Amazon Alexa.
    * Chatbot.

### Kendra
1. Intelligent search service powered by machine learning, designed to provide more relevant and accurate search results for enterprise applications.
    * Salesforce -> Study -> Return
    * S3 -> Study -> Return
    * One Drive -> Study -> Return

### Textrack
Fully managed machine learning service that automatically extracts text, handwriting, and data from scanned documents and images

### Sagemaker
Comprehensive platform for building, training, and deploying machine learning models at scale.

## Best Practice

### AWS Well-Architected Framework
The AWS Well-Architected Framework is a set of best practices and guidelines designed to help cloud architects build secure, high-performing, resilient, and efficient infrastructure for applications. It consists of five pillars, each focusing on different aspects of architecture. Here’s a brief overview of each pillar:

1. Operational Excellence
    1. Focus: Operations and monitoring of workloads.
    1. Key Concepts: 
        * Monitoring and logging
        * Incident response
        * Continuous improvement
        * Automation of operational tasks

1. Security
    1. Focus: Protecting data, systems, and assets.
    1. Key Concepts: 
        * Identity and access management
        * Data protection
        * Incident response and security monitoring
        * Compliance and governance

1. Reliability
    1. Focus: Ensuring workloads can recover from failures and meet availability requirements.
    1. Key Concepts: 
        * Distributed system design
        * Backup and recovery
        * Fault tolerance
        * Change management

1. Performance Efficiency
    1. Focus: Efficiently using resources to meet system requirements and performance goals.
    1. Key Concepts: 
        * Selecting the right resource types and sizes
        * Monitoring performance
        * Evolving with technology advancements
        * Scaling based on demand

1. Cost Optimization
    1. Focus: Minimizing costs while maximizing the value of resources.
    1. Key Concepts: 
        * Avoiding unnecessary expenses
        * Analyzing spend patterns
        * Scaling resources to demand
        * Taking advantage of pricing models and services

### CAF (Cloud Adoption Framework)
1. The AWS CAF provides guidance to organizations on how to adopt cloud computing effectively. It helps organizations develop a comprehensive cloud adoption strategy by focusing on key areas that influence successful cloud adoption.
    * Business: Aligning cloud initiatives with business goals and outcomes.
    * People: Developing skills and creating a culture to support cloud adoption.
    * Governance: Establishing governance frameworks to manage cloud usage and compliance.
    * Platform: Building a secure and scalable cloud architecture.
    * Security: Integrating security into all stages of cloud adoption.
    * Operations: Managing cloud operations efficiently and effectively.

### Eco System
1. Community and Knowledge Sharing
    * Blog.
    * Re:Post (Forum).
    * Whitepapers (Guides).
    * Partners Solutions (Other companies solutions using AWS).

### IQ
1. Helps from a specialist
    * Freelance

### AMS (Managed Services)
1. AWS Managed Services (AMS) is a service that helps organizations manage their AWS infrastructure in a secure and compliant manner. AMS provides operational support, best practices, and governance, enabling businesses to focus on innovation while AWS handles day-to-day operations.
    * Hight cost due to Amazon being responsible for everything.

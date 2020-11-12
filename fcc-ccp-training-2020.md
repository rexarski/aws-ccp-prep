# freeCodeCamp - AWS Certified Cloud Practitioner Training 2020

- CCP = Certified Cloud Practitioner
- **Not a gilded title, not too much value on resumes**
- direct prepare for the Solution Architect Associate

$100 USD, 90 min, 65 questions, 70% passing score, valid for 3 years.

## Content Outline

- cloud concepts 28%
- security 24%
- technology 36%
- billing and pricing 12%
- response types
  - choose 1 out of 4
  - choose 2 out of 5 or 3 out of 6
- white papers (super boring, not ideal review content for ccp test)
  - July 2019 Overview of Amazon Web Services
    - [latest version](whitepaper/aws-overview.pdf) updated in August 2020
  - ~~Oct 2018 Architecting for the Cloud: AWS Best Practices~~
    - archived, now upgraded to [AWS Well-Architected Framework](whitepaper/AWS_Well-Architected_Framework.pdf) (August 2020)
  - June 2018 [How AWS Pricing Works](whitepaper/aws_pricing_overview.pdf)
  - March 2018 [Cost Management in the AWS Cloud](whitepaper/aws-tco-2-cost-management.pdf)

## Cloud Concepts

### What is cloud computing

The practice of using a network of remote servers hosted on the Internet to store, manage, and process data, rather than a local server or a personal computer.

### Six advantages and benefits of cloud computing

1. Trade capital expense for variable expense. -> No upfront-cost. Pay on-demand.
2. Benefit from massive economies of scale. -> Sharing the cost with other customers.
3. Stop guessing capacity. -> Instead of paying for idle or underutilized servers.
4. Increase speed and agility. -> Within a few clicks in minutes.
5. Stop spending money on running and maintaining data centres. -> Focus on your own customers.
6. Go global in minutes. -> Multiple regions around the world with a few clicks.

### Types of cloud computing

- **SaaS** aka *software as a service* for customers. A completed product that is run and managed by the service provider. Example: Gmail, Office 365.
- **PaaS** aka *platform as a service* for developers. Removes the need for your organization to manage the underlying infrastructure. Focus on deployment and management of your applications.
- **IaaS** aka *infrastructure as a service* for admins. The basic building blocks for cloud IT. Provides access to networking features, computers and data storage space. Example: AWS, GCP, Azure.

### Cloud computing deployment models

- cloud: fully utilizing cloud computing, e.g. start-ups, SaaS offerings, new projects and companies.
- hybrid: using both cloud and on-premise ,e.g., banks, FinTech, investment management, large professional service providers, legacy on-premise.
- on-premise: deploying resources on-premises, using virtualization and resource management tools, is sometimes called “private cloud”, e.g. public sector (government), super sensitive data (hospitals), large enterprise with heavy regulation (insurance companies).

## AWS Global Infrastructure

### Where does all this cloud computing run

*As per today (2020-10-28), 24 launched regions, 3 announced regions, 77 availability zones.*

For current [statistics](https://aws.amazon.com/about-aws/global-infrastructure/?p=ngi&loc=1).

- **Regions:** physical location in the word with multiple Availability Zones.
- **Availability Zones:** one or more discrete data centers.
- **Edge Location:** datacenter owned by a trusted partner of AWS.

### Regions

- A geographically distinct location which has multiple datacenters (AZs).
- Each region has at least 2 AZs.
- Every region is physically isolated from and independent of every other region in terms of location, power, water supply.
- Not all services are available in all regions.
- The largest region is US-EAST, US-EAST-1 (North Virginia) is the region where you can see all your billing information.

### Availability Zones (AZs)

- A datacenter owned and operated by AWS in which AWS services run.
- AZs are represented by a Region Code, followed by a letter identifier e.g. us-east-1a.
- Multi-AZ distributing -> handle requests when one goes down.
- < 10ms latency between AZs.

### Edge locations

- A lot of them.
- A datacenter owned by a trusted partner of AWS which has a direct connection to the AWS network.
- These serve requests for CloudFront and Route 53. Requests going to either of these services will be routed to the nearest edge location automatically.
- S3 Transfer Acceleration traffic and API Gateway endpoint traffic also use the AWS Edge Network.
- Low latency.

### GovCloud Regions 🇺🇸

- AWS GovCloud Regions allow customers to host sensitive **Controlled Unclassified Information** and other types of regulated workloads.
- Only operated by employees who are U.S. citizens, on U.S. soil.
- Only accessible to U.S. entities and root account holders who pass a screening process.

## Getting Started

- Creating an AWS account ✅
- Billing preferences, budgets and alarms ✅
  - Billing preferences -> keep yourself in the loop
  - AWS Budgets -> create a new budget (cost budget)
  - CloudWatch -> set billing alarm
- Change IAM users sign-in link
  - Identity and Access Management (IAM)
- Activate MFA on root account
  - Multi-factor authorization (MFA)
- Create individual IAM user
  - We do not want to be using root account which should be rarely used.
- Set a password policy

## Hands On

### Elastic Cloud Compute (EC2)

- When creating, we can assign a role in IAM called `AmazonEC2RoleforSSM` (Simple System Manager).
- SSM does not require key pairs to log in.

### Session managers

- How to get into the server
  - SSH; or
  - EC2 Instance Connect (browser-based SSH connection); or
  - System Manager's Session Manager
    - Search "sm" in AWS, find the "Session Manager" in the sidebar, create a session.
    - `sudo su - ec2-user` to be ec2-user instead root user.
    - Session history will be recorded.

### AMI

- Amazon Machine Image (AMI)
  - Like a snapshot. In EC2, select an instance, use "Actions-Image-Create Image".
  - Can launch an instance from an image.

### Auto Scaling Groups

- Benefits of Auto Scaling
  - Auto Provisioning: Keep your Auto Scaling group healthy and balanced, whether you need one instance or 1,000.
  - Adjustable Capacity: Maintain a fixed group size or adjust dynamically based on Amazon CloudWatch metrics.
  - Launch Template Support: Provision instances easily using EC2 Launch Templates.

### Elastic Load Balancer

- ELB
  - Put an ELB in front of your instances. When traffic comes, it flows through ELB first, and will be evenly distributed to multiple instances (say they are in different AZs), to prevent some server downtime.
  - Application LB ✅
  - Network LB
  - Classic LB
  - When configuring routing, need to create a target group with target type (instance, IP or Lambda function)

### S3

- Simple Storage Service (S3)
  - Nothing else to talk about here.

### CloudFront

- Create a distribution.
  - Origin from previous S3 bucket.
  - A distribution is gonna copy the file from S3 and move it around the world in order to keep the access to file super fast.

### RDS

- Relational Databases
  - Database engine options
    - Amazon Aurora
    - MySQL
    - MariaDB
    - PostgreSQL
    - Oracle
    - Microsoft SQL Server
  - Templates
    - Production (roughly $600/month)
    - Dev/Test (roughly $260/month)
    - Free Tier ($0 for a while)

### Lambda

- Run functions between AWS services in other languages.

## EC2 Pricing Models

- Intro (4 models)
  - On-Demand (least commitment)
    - low cost and flexible
    - only pay per hour
    - short-term, spiky, unpredictable workloads
    - cannot be interrupted
    - for first time apps
  - Spot (up to 90% off, biggest savings)
    - request spare computing capacity
    - flexible start and end times
    - can handle interruptions (server randomly stopping and starting)
    - for non-critical background jobs
  - Reserved (up to 75% off, best long-term)
    - steady state or predictable usage
    - commit to EC2 over a 1 or 3 year term
    - can resell unused reserved instances
  - Dedicated (most expensive)
    - dedicated servers
    - can be on-demand or served (up to 70% off)
    - when you need a guarantee of isolate hardware (enterprise requirements)
- On-Demand Instances, least commitment
  - by default pricing
  - no up-front payment, no long-term commitment
  - charged by the hour or by the minute
  - for applications where the workload is for **short-term**, **spikey** or **unpredictable**.
- Reserved Instances (RI), best long-term
  - for applications that have a **steady-state**, or require **reserved capacity**.
  - Reduced pricing is based on **Term x Offering Class x Payment Option**.
    - Terms: 1 year or 3 year contract.
    - Payment options: all upfront, partial upfront, and no upfront.
    - Offering class:
      - **Standard** - up to 75% reduced pricing compared to on-demand, cannot change RI attributes.
      - **Convertible** - up to 54% reduced pricing compared to on-demand, allows RI attributes changing if greater or equal in value.
      - **Scheduled** - reserve instances for specific time periods. Savings vary.
  - RIs can be shared between multiple accounts within an organization.
  - Unused RIs can be sold in **Reserved Instance Marketplace**.
- Spot Instances, biggest savings
  - **unused compute capacity**
  - spot instances -> a discount of 90% compared to on-demand pricing
  - spot instances can be terminated if the computing capacity is needed by on-demand customers
  - Designed for applications that have flexible start and end times or applications that are only feasible at very low compute costs.
  - AWS Batch is an easy and convenient way to use Spot Pricing.
    - Instances can be terminated by AWS at anytime.
    - If terminated by AWS, don't get charged for partial hour.
    - If terminated by you, get charged for any hour that it ran.
- Dedicated Host Instances, most expensive
  - when you have strict **server-bound licensing** that won't support multi-tenancy or cloud deployment
    - multi-tenant (virtual isolation)
    - single tenant (physical isolation)
      - "dedicated hardware"
- EC2 Pricing Cheatsheet (summary)
  - EC2 has for 4 pricing models, **On-Demand, Spot, Reserved Instance (RI)** and **Dedicated**.
  - **On-Demand** (least commitment)
    - low cost and flexible
    - only pay per hour
    - **Use case:** short-term, spiky, unpredictable workloads, first time apps
    - ideal when your workloads cannot be interrupted
  - **Reserved Instances** up to 75% (best long-term value)
    - **Use case:** steady state or predictable usage
    - can resell unused reserved instances (Reserved Instance Marketplace)
    - Reduced pricing is based on **Term x Offering Class x Payment Option**
    - **Payment Terms:** 1 year or 3 year
    - **Payment Options:** all upfront, partial upfront, and no upfront
    - **Class Offerings:**
      - **Standard** Up to 75% reduced pricing compared to on-demand. Cannot change RI attributes.
      - **Convertible** Up to 54% reduced pricing compared to on-demand. Allows you to change RI Attributes if greater or equal in value.
      - **Scheduled** You reserve instances for specific time periods e.g. once a week for a few hours. Savings vary.
  - **Spot pricing** up to 90% off (biggest savings)
    - request spare computing capacity
    - flexible start and end times
    - **Use case:** can handle interruptions (server randomly stopping and starting)
    - **Use case:** for non-critical background jobs
    - Instances can be terminated by AWS at any time
    - If your instance is **terminated by AWS**, you don't get charged for a partial hour of usage.
    - If **you terminate** an instance you will still be charged for any hour that it ran.
  - **Dedicated Hosting** (most expensive)
    - Dedicated servers
    - can be on-demand or reserved (up to 70% off)
    - **Use case:** when you need a guarantee of isolate hardware (enterprise requirements)

## Billing and Pricing

- Free Services, certain services are free, but the resources they setup will cost you. They can provision AWS services which cost money*.
  - IAM - Identity Access Management ✅
  - Amazon VPC ✅
  - Auto Scaling* ✅
  - CloudFormation* ✅
  - Elastic Beanstalk* ✅
  - Opsworks*
  - Amplify*
  - AppSync*
  - CodeStar*
  - Organizations & Consolidated Billing
  - AWS Cost Explorer
- ✅ likely to be tested
- AWS Support Plans
  - basic
    - email support only
    - for billing and account
    - 7 trusted advisor checks
    - price: $0 USD/month
  - developer
    - tech support via email ~ 24 hours until reply
    - no third party support
    - general guidance < 24 hrs
    - system impaired < 12 hrs
    - 7 trusted advisor checks
    - price: $20 USD/month
  - business
    - tech support via email ~24 hours until reply
    - tech support via chat, phone, anytime 24/7
    - general guidance < 24 hrs
    - system impaired < 12 hrs
    - production system impaired < 4 hrs
    - production system DOWN < 1 hrs
    - all trusted advisor checks
    - price: $100 USD/month
  - enterprise
    - tech support via email ~24 hours until reply
    - tech support via chat, phone, anytime 24/7
    - general guidance < 24 hrs
    - system impaired < 12 hrs
    - production system impaired < 4 hrs
    - production system DOWN < 1 hrs
    - business-critical system DOWN < 15 m
    - personal concierge
    - TAM (technical account manager)
    - all trusted advisor checks
    - price: $15,000 USD/month
- AWS Marketplace
  - a curated digital catalogue with thousands of software listings from independent software vendors.
  - free or with an associated charge -> becomes a part of the AWS bill.
  - sales channel for ISV (Independent Software Vendors) -> sell your solutions to other AWS customers
  - prodcuts can be offered as:
    - Amazon Machine Images (AMIs)
    - AWS CloudFormation templates
    - Software as a service (SaaS) Offerings
    - Web ACL (Access Control List)
    - AWS WAF (Web Application Firewall) rules
- AWS Trusted Advisor
  - Free - 7 Trusted Advisor Checks
  - Business, Enterprise - All Trusted Advisor Checks
  - Advises you on **security, saving money, performance, service limits** and **fault tolerance**.
  - Like an automated checklist of best practices on AWS.
  - Commonly Used ones:
    - Cost Optimization
      - Idle Load Balancers
      - Unassociated Elastic IP Addresses
    - Performance
      - High Utilization Amazon EC2 Instances
    - Security
      - MFA (Multi-factor Authentication) on Root Account
      - IAM Access Key Rotation
    - Fault Tolerance
      - Amazon RDS Backups
    - Service Limits
      - VPC (Virtual Private Cloud)
  - How to use it?
    - Go to [Trusted Advisor Dashboard](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/)
    - Set up email notification preferences
- Consolidated Billing
  - One bill for all of your accounts.
    - Coinsolidate your billing and payment methods **across** multiple AWS accounts into one bill.
    - For billing AWS treats all the accounts in an organization as if they were one account.
    - You can designate one **master account** that pays the charges of all the other **member accounts**.
    - Consolidated billing is offered at no additional cost.
    - Use **Cost Explorer** to visualize usage for each consolidated billing.
- Consolidated Billing Volume Discounts
  - The more you use, the more you save. (Tiers up.)
- AWS Cost Explorer
  - Visualize, understand and manage your AWS costs and usage over time within an AWS organization costs will be consolidated in the **master account.**
  - default report
  - forecasting
  - filter and grouping
- AWS Budgets
  - first 2 budgets are free of charge, each budge is $0.02 per day ~ 0.60 USD/month.
  - 20,000 budgets limit.
  - Plan your **service usage, service costs and Instance reservations**.
  - Set up alerts if you exceed or are approaching your defined budget.
  - Create **Cost, Usage** or **Reservation** Budgets.
  - Can be tracked at the monthly, quarterly, or yearly levels, with customizable start and end dates.
  - Alerts support **EC2, RDS, Redshift** and **ElastiCache** reservations.
  - Buget based on a fixed cost or plan you upfront based on your chosen level.
  - Managed in **AWS Budget** dashboard or via **Budgets API**.
  - Get notified by email or **Chatbot**.
- TCO Calculator
  - The **TCO (Total Cost of Ownership)** Calculator allos you to estimate how much you would save when moving to AWS from on-premise.
  - a **detailed set of reports** that **can be used in executive presentations**.
  - for **approximation purposes** only.
- AWS Landing Zone
  - helps enterprises quickly set-up a secure, AWS multi-account, provides you with a **baseline environment** to get started with a **multi-account architecture**.
  - AWS Account Vending Machine (AVM)
    - automatically provisions and configures new accounts via Secure Catalog Template.
    - uses Single Sign-on (SSO) for managing and accessing accounts.
- Resource Groups and Tagging
  - **Tags** are words or phrases act as metadata for organizing your AWS resources.
  - **Resource Groups** are a collection of resources that share one or more tags.
- AWS QuickStart
  - **Prebuilt templates** by AWS and AWS Partners to help you deploy popular stacks on AWS.
  - A Quick Start is composed of 3 parts:
    - A reference architecture for the deployment.
    - **AWS CloudFormation** templates that automate and configure the deployment.
    - A deployment guide explaining the architecture and implementation in detail.
- AWS Cost and Usage Report
  - Generate a **detailed spreadsheet** enabling you to better analyze and understand your AWS costs.
  - Places the reports in S3.
  - Use Athena to turn the report into a queryable database.
  - Use QuickSight to visualize your billing data as graphs.

## Technology Overview

- AWS Organizations and Accounts
  - **Organizations** allow yo uto centrally manage billing, control access, compliance, security, and share resource access your AWS accounts.
  - **Root Account User** is a single sign-in identity that has complete access to all AWS services and resources in an account. Each account has a Root Account User.
  - **Organization Units** are a group of AWS accounts within an organization which can also contain other organizational units - creating a hierarchy.
  - **Service Control Policies** give central control over the allowed permissions for all accounts in your organization, helping to ensure your accounts stay within your organization's guidelines.
  - In IAM or AWS Organizations
    - create organization
    - verify master account
      - root->master account
    - create organizational unit
    - create another (developer) account
    - add accounts to organizational unit
    - change/create control policies, add/remove/change resources
- AWS Networking
  - **Region** is the geographical location of your network.
  - **AZ** is the data center of your AWS resources.
  - **VPC (Virtual Private Cloud)** is a logically isolated section of the AWS Cloud where you can launch AWS resources.
    - public and private
  - **Internet Gateway** enables access to the Internet.
  - **Route Tables** determine where network traffic from your subnets are directed.
  - **NACLs (Network Access Control List)** acts as a firewall at the subnet level.
  - **Security Groups** act as firewall at the instance level.
  - **Subnets** is a logical partition of an IP network into multiple, smaller network segments.
- Database Services
  - DynamoDB - NoSQL **key/value** database, e.g. Cassandra.
  - DocumentDB - NoSQL **document** database that is MongoDB compatible.
  - RDS - **Relational** database service that supports multiple engines
    - Engines: MySQL, Postgres, MariaDB, Oracle, Microsoft SQL Server, Aurora
    - Aurora - MySQL (5x faster) and PSQL (3x faster) database **fully managed**
    - AUrora Serverless - only runs when you need it, like AWS Lambda
  - Neptune - Managed **Graph** database
  - Redshift - **Columnar** database, **petabyte** warehouse
    - 1000 TB = 1 PB
  - ElastiCache - **Redis**, or **Memcached** database
- Provisioning Services
  - what is provisioning?
    - the allocation or creation of resources and services to a customer
  - some provisioning services
    - **Elastic Beanstalk** - service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker.
    - **OpsWorks** - configuration management service that provides managed instances of **Chef** and **Puppet**.
    - **CloudFormation**- infrastructure as code, **JSON** or **YAML**.
    - **AWS QuickStart** - pre-made packages that can launch and configure your AWS compute, network, storage, and other services required to deploy a workload on AWS.
    - **AWS Marketplace** - a digital catalogue of thousands of software listings from independent software vendors you can use to find, buy, test, and deploy software.
- Computing Services
  - **EC2** Elastic Compute Cloud, highly configurable server e.g. CPU, Memory, Network, OS.
  - **ECS** Elastic Container Service **Docker as a Service** highly scalable, high-performance container orchestration service that supports Docker containers, pay for EC2 instances.
  - **Fargate** Microservices where you don't think about the infrastructure. Pay per task.
  - **EKS** Kubernetes as a Service easy to deploy, manage, and scale containerized applications using Kubernetes.
  - **Lambda** serverless functions run code without provisioning or managing servers. You pay only for the compute time you consume.
  - **Elastic Beanstalk** orchestrates various AWS services, including EC2, S3, Simple Notification Service (SNS), CloudWatch, Autoscaling, and Elastic Load Balancers.
  - **AWS Batch** plans, schedules, and executes your batch computing workloads across the full range of AWS compute services and features, such as **Amazon EC2** and **Spot Instances**.
- Storage Services
  - **S3 - Simple Storage Service** - **object** storage
  - **S3 Glacier** - low cost storage for **archiving and long-term backup**
  - **Storage Gateway** - hybrid cloud storage with local caching
    - File Gateway
    - Volume Gateway
    - Tape Gateway
  - **EBS - Elastic Block Storage** - hard drive in the cloud you attach to EC2 instances
    - SSD, IOPS SSD, Throughout HHD, Cold HHD
  - **EFS - Elastic File Storage** - file storage mountable to multiple EC2 instances at the same time
  - **Snowball** - Physically migrate lots of data via a computer suitcase 50-80 TB
    - **Snowball Edge** A better version of Snowball - 100 TB
    - **Snowmobile** Shipping container, pulled by a semi-trailer truck - 100 PB
- Business Centric Services
  - **Amazon Connect** - **Call Center** - Cloud-based call center service you can setup in just a few clicks - based on the same proven system used by the Amazon customer service teams.
  - **WorkSpaces** - **Virtual Remote Desktop** - Secure managed service for provisioning either Windows or Linux desktops in just a few minutes which quickly scales up to thousands of desktops.
  - **WorkDocs** - A content creation and collaboratio service - easily create, edit, and share content saved centrally in AWS. **(the AWS version of Sharepoint)**
  - **Chime** - AWS Platform for **online meetings, video conferencing,** and business calling which elastically scales to meet your capacity needs.
  - **WorkMail** - Managed **business mail**, contacts, and calendar service with support for existing desktop and mobile email client applications. (IMAP)
  - **Pinpoint** - Marketing campaign management system you can **use for sending targeted email,** SMS, push notifications, and voice messages.
  - **SES - Simple Email Service** - A cloud-based email sending service designed for marketers and application developers to **send marketing, notification, and emails**.
  - **QuickSight** - A Business Intelligence (BI) service. Connect multiple datasource, and quickly visualize data in the form of graphs with little to no programming knowledge.
- Enterprise Integration
  - **Direct Connect** dedicated Gigabit network connection from your premises to AWS Imagine having a direct fibre optic cable running straight to AWS.
  - **VPN** establish a **secure** connection to your AWS network
    - Site-to-site VPN - connecting your on-premise to your AWS network
    - Client VPN - connecting a Client (a laptop) to your AWS network
  - **Storage Gateway**: A hybrid storage service that enables your on-premises applications to use AWS cloud storage. You can use this for backup and archiving, disaster recovery, cloud data processing, storage tiering, and migration.
  - **Active Directory**: The AWS Directory Service for Microsoft Active Directory also known as AWS Managed Microsoft AD - enables your directory-aware workloads and AWS resources to use managed Active Directory in the AWS Cloud.
- Logging Services
  - **CloudTrail** - logs all **API calls** (SDK, CLI) between **AWS services** (who can we blame)
    - Who created this bucket? -> detect developer misconfiguration
    - Who spun up that expensive EC2 instance? -> detect malicious actors
    - Who launched this SageMaker Notebook? -> automate responses
  - **CloudWatch** - is a collection of multiple services
    - CloudWatch **Logs**: Performance data about AWS services, e.g. CPU ultilization, memory, network in application logs, e.g. Rails, Nginx, Lambda logs
    - CloudWatch **Metrics**: Represents a time-ordered set of data points. A variable to monitor.
    - CloudWatch **Events**: trigger an event based on a condition e.g. ever hour take snapshot of server.
    - CloudWatch **Alarms** - triggers notifications based on metrics.
    - CloudWatch **Dashboard** - create visualization based on metrics.
- Know your initialisms
  - IAM, Identity and Access Management
  - S3, Simple Storage Service
  - SWF, Simple Workflow Service
  - SNS, Simple Notification Service
  - SQS, Simple Queue Service
  - SES, Simple Email Service
  - SSM, Simple Systems Manager
  - RDS, Relational Database Service
  - VPC, Virtual Private Cloud
  - VPN, Virtual Private Network
  - CFN, CloudFormation
  - WAF, Web Application Firewall
  - MQ, Amazon ActiveMQ
  - ASG, Auto Scaling Groups
  - TAM, Technical Account Manager
  - ELB, Elastic Load Balancer
  - ALB, Application Load Balancer
  - NLB, Network Load Balancer
  - EC2, Elastic Cloud Compute
  - ECS, Elastic Container Service
  - ECR, Elastic Container Repository
  - EBS, Elastic Block Storage
  - EFS, Elastic File Storage
  - EMR, Elastic MapReduce
  - EB, Elastic Beanstalk
  - ES, Elasticsearch
  - EKS, Elastic Kubernetes Service
  - MKS, Managed Kafka Service
  - IoT, Internet of Things
  - RI, Rserved Instances

## Security

- Shared Responsibility Model
  - Customers are responsible for Security **in** the Cloud
    - customer data
    - platforms, applications, identity and access management (IAM)
    - operating system, network and firewall configuration
    - client-side data encryption and data integrity authentication
    - server-side encryption (file system and/or data)
    - networking traffic protection (encryption, integrity, identity)
  - AWS is responsible for Security **of** the Cloud
    - software
      - operation of managed services
      - compute, storage, database, networking
    - hardware / global infrastructure
      - regions
      - AZs
      - edge locations
- AWS Compliance programs
  - a set of internal policies and procedures of a company to comply with laws, rules, and regulations or to uphold business reputation.
  - Health Insurance Portability and Accountability Act (HIIPAA)
  - The Payment Card Industry Data Security Standard (PCI DSS)
- AWS Artifact
  - How do we prove AWS meets a compliance?
    - No cost, self-service portal for on-demand access to AWS's compliance reports
    - On-demand **access to AWS's security and compliance reports** and select online agreements.
    - These checks are based on global compliance frameworks.
- Amazon Inspector
  - How do we prove an EC2 instance is harden?
    - hardening: the act of eliminating as many **security** risks as possible.
    - AWS Inspector runs a **security benchmark** against specific EC2 isntances.
    - both **network** and **host** assessments
      - install the AWS agent on your EC2 instances
      - run an assessment for your assessment target
      - review your findings and remediate security issues
    - a popular benchmark is made by Center for Internet Security, with 699 checks.
- AWS WAF (Web Application Firewall)
  - protects your web app from common web exploits
  - write your own rules to ALLOW or DENY traffic on the contents of an HTTP requests
  - use a ruleset from a trusted AWS Secruity Partner in the AWS WAF Rules Marketplace
  - WAF can be attached to either **CloudFront** or an **ALB**
  - Open Web Application Security Project (OWASP) Top 10 most dangerous attacks:
    - Injection
    - Broken authentication
    - Sensitive data exposure
    - XML External Entities (XXE)
    - Broken access control
    - Security misconfigurations
    - Cross site scripting (XSS)
    - Insecure deserialization
    - Using components with known vulnerabilities
    - Insufficient logging and monitoring
- AWS Shield
  - AWS Shield is a **managed** DDoS (Distributed Denial of Service) protection service that safeguards applications running on AWS
  - All AWS customers benefit from the automatic protections of AWS Shield Standard at no additional charge.
  - When you route your traffic through **Route53** or **CloudFront** you are using **AWS Shield Standard**.
  - protects you against **Layer 3, 4** and **7** attacks
    - 7 application
    - 4 transport
    - 3 network
  - That's for **Shield Standard**
  - **Shield Advanced**, 3000 USD/year
    - For additional protection against larger and more sophisticated attacks, visibility into attacks, and 24x7 access to DDoS experts for complex cases.
    - Available on
      - Route 53
      - CloudFront
      - ELB
      - Global Accelerator
      - Elastic IP (Amazon Elastic Compute Cloud and Network Load Balancer)
- Penetration Testing
  - what is PenTesting?
    - An authorized simulated cyberattack on a computer system, performed to evaluate the security of the system.
  - Can you do it on AWS? Yes.
  - Permitted services
    - EC2 instances, NAT Gateways, and ELB
    - RDS
    - CloudFront
    - Aurora
    - API Gateways
    - AWS Lambda and Lambda@Edge functions
    - Lightsail resources
    - Elastic Beanstalk environments
  - Prohibited activities
    - DNS zone walking via Amazon Route 53 Hosted Zones
    - DoS, DDoS, simulated DoS, simulated DDoS.
    - Port flooding
    - Protocol flooding
    - Request flooding (login request flooding, API request flooding)
- Guard Duty
  - what is **IDS/IPS**?
    - Intrusion Detection System and Intrusion Protection System
    - A device or software application that monitors a network or systems for malicious activity or policy violations.
    - **Guard Duty** is a threat detection service that continuously monitors for malicious, suspicious activity and unauthorized behavior. Uses machine learning to analyze the following AWS logs:
      - CloudTrail logs
      - VPC Flow logs
      - DNS logs
    - it will alert you of findings through automated CloudWatch events or with 3rd party services.
- Key Management Service
  - A managed service that makes it easy to create and control the encryption keys used to encrypt your data.
    - KMS is a multi-tenant HSM (hardware security module).
    - Many AWS services are integrated to use KMS to encrypt your data with a simple checkbox.
    - KMS uses Envelope Encryption.
      - **Envelope Encryption**: when encrypt your data, your data is protected, but you have to protect encryption key. when you encrypt your data key with a master key as an additional layer of security.
      - KMS Master key encrypts -> data key in the envelope encrypts -> data.
- Amazon Macie
  - **Macie** is a fully managed service that continuously monitors **S3 data access** activity for anomalies, and generates detailed alerts when it detects risk of unauthorized access or inadvertent data leaks.
  - uses **machine learning** to analyze your CloudTrail logs
  - a variety of alerts
    - anonymized access
    - config compliance
    - credential loss
    - data compliance
    - file hosting
    - identity enumeration
    - information loss
    - location anomaly
    - open permissions
    - privilege escalation
    - ransomware
    - service disruption
    - suspicious access
  - will identity the most at-risk users which could lead to a compromise
- Security Groups vs NACLs
  - **Security groups** act as a firewall at the **instance** level. Implicitly denies all traffic, create with your own **Allow** rules.
    - e.g. allow an EC2 instance access on port 22 for SSH
  - **NACLs (Network Access Control Lists)** act as a firewall at the **subnet** level, create with **Allow** and **Deny** rules.
    - e.g. block a specific IP address known for abuse
- AWS VPN
  - VPN (Virtual Private Network) lets you establish a secure and **private tunnel** from your network or device to the AWS global network.
    - **AWS site-to-site VPN** securely connect on-premises network or branch office site to VPC.
    - **AWS Client VPN** securely connect users to AWS or on-premises network.

## Variation Study

Similar names, completely different services.

- Cloud* Service
  - **CloudFormation**: infrastructure as code, set up services via templating script e.g. yml, json.
  - **CloudTrail**: logs all **api calls** between **AWS services** (who can we blame) e.g. AWS S3 API create-bucket --bucket my-bucket-ash-test-123
  - **CloudFront**: Content Distribution Network, creates a cached copy of your website and copies to servers located near people trying download website.
  - **CloudWatch**: is a collection of multiple services
    - CloudWatch Logs - custom log data, memory usage, rails logs, nginx logs
    - CloudWatch Metrics - metrics that are based on logs e.g. memory usage
    - CloudWatch Events - trigger an event based on a condition e.g. every hour take snapshot of server
    - CloudWatch Alarms - trigger notifications based on metrics
    - CloudWatch Dashboard - create viz basd on metrics
  - **CloudSearch**: search engine, you have an ecommerce website and you want to add a search bar.
- *Connect Service
  - **Direct Connect** - Dedicated Fiber Optics Connections from DataCenter to AWS.
    - A large enterprise has their own datacenter and they need an insanely fast connection directly to AWS. If extra security needed, apply a VPN connect on top of Direct Connect.
  - **Amazon Connect** - Call Center Service
    - A toll free number, accept inbound and outbound calls, setup automated phone systems.
  - **Media Connect** - New version of Elastic Transcoder, converts videos to different video types.
- Elastic Transcoder vs Media Convert
  - both transcode videos
  - Elastic Transcoder: the old way, transcodes videos to streaming formats.
  - **AWS Elemental MediaConvert**: the new way
    - transcodes videos to streaming formats
    - overlays images
    - insert video clips
    - extracts captions data
    - robust UI
- SNS vs SQS
  - both **connect apps** via messages
  - **Simple Notifications Service**: pass along messages e.g. PubSub
    - send notifications to **subscribers** of topics via multiple protocol, e.g. HTTP, Email, SQS, SMS
    - generally used for plain text emails, like billing alarms
    - can retry sending in case of failure for HTTPS
    - good for webhooks, simple internal emails, triggering lambda functions
  - **Simple Queue Service**: queue up messages, guaranteed delivery
    - places messages into a **queue**, applications pull queue using **AWS SDK**
    - can retain a message for up to 14 days
    - can send them in sequential order or in parallel
    - can ensure only one message is sent
    - can ensure messages are delivered at least once
    - good for delayed tasks, queuing up emails
- Inspector vs Trusted Advisor
  - both are **security tools**, both perform audits
  - **Amazon Inspector**
    - audits a single EC2 instance that you've selected
    - generates a report from a long list of security checks, i.e. 699 checks by CIS
  - **Trusted Advisor**
    - Trusted Advisor doesn't generate out a PDF report
    - gives you a holistic view of recommendations across multiple services and best practices
- ALB vs NLB vs CLB
  - all can attach Amazon Certification Manager (ACM) SSL Certificate
  - **Application Load Balancer**
    - Layer 7 Requests
    - **HTTP and HTTPS** traffic
    - Routing Rules, more usability from one load balancer
    - can attach WAF
  - **Network Load Balancer**
    - Layer 4 IP protocol data
    - **TCP and TLS traffic** where extreme performance is required.
    - capable of handling millions of requests per second while maintaining ultra-low latencies
    - optimized for **sudden and volatile traffic** patterns while using a single static IP address per AZ
  - **Classic Load Balancer (old)**
    - Layer 4 and Layer 7
    - Intended for applications that built within the EC2-Classic network
    - doesn't use Target Groups
- SNS vs SES
  - both send emails
  - **Simple Notifications Service**
    - pratical and internal
    - send notifications to subscribers of topics via multiple protocol, e.g. HTTP, email, SQS, SMS
    - SNS -> sending plain text emails triggered by AWS Services
    - Most exam questions are going to be talking about SNS because lots of services can trigger SNS for notifications.
    - Need to know what are **Topics** and **Subscriptions** regarding **SNS**.
  - **Simple Email Service**
    - professional, marketing, emails
    - a cloud based email service, like SendGrid
    - SES sends html emails, SNS cannot
    - SES can receives inbound emails
    - SES can create Email Templates
    - Custom domain name email
    - Monitor email reputation
- Artifact vs Inspector
  - both **compile out PDFs**
  - **AWS Artifact**
    - why should an enterprise trust AWS?
    - generates a security report that's based on global compliance frameworks such as:
      - Service Optimization Control (SOC)
      - Payment Card Industry (PCI)
  - **AWS Inspector**
    - how do we know this EC2 instance is secure? prove it?
    - runs a script that analyzes your EC2 instance, then generates a PDF report telling you which security checks passed
    - Audit tool for security of EC2 instances

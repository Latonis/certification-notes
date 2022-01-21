# AZ-900 Microsoft Azure Fundamentals

Let this page be my study notes for AZ-900 course notes.

## **Introduction**

Course will cover:

- Exams are more relevant to the roles and their requirements

### Portal Features:

- Personalize
- Access Control
- Cost Management
- One Stop Shop
- Constantly Updated
- Multi-Platform

### Azure Command Line Interface:

Coffee to VM analogy (Many ways to make the cup of coffee - Portal, CLI, etc.)

Advantages:

- Stable
- Structured very logically
- Cross Platform
- Automation for future use
- Keep track of what with logging and version control

### PowerShell:

- Comes pre-installed, text only
- Cmdlet
    - New-AzVm
- Azure Resource Manager
- Versatile

### Cloud Shell:

Interactive browser-accessible shell for managing Azure resources

Stand-Alone or In-Portal

Features:

Access

Shell

Tools

Storage

Integrated File Editor

### Azure Mobile Apps:

On Android and iOS

Do Azure things in the app

Shows quick information on the go

Health

Resources

Alerts

Uses Azure Resource Manager

Use Cloud Shell from phone

### ARM Templates:

[https://azure.microsoft.com/resources/templates/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl](https://azure.microsoft.com/resources/templates/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

Describe resource usage

Common Syntax

Idempotent

Run templates as many times as you like, outcome is the same

Written in JSON

Source Control

Keep track of all changes

Reuse

Use combination of multiple partial ARM templates to achieve success

Declarative

Specify what needs to be done, not exactly how it should be done

No Human Errors

- [x]  Create Free Azure Account

### Summary of Chapter 1:

Course Overview

Benefits

Structure of Course

Azure Portal

One-stop shop for managing all Azure resources

Azure CLI

text-only way of managing Azure resources

Azure PowerShell

uses cmdlets to manage Azure resources

Azure Cloud Shell

Works from anywhere a browser does

Azure Mobile Apps

Manage Azure on the Go

Arm Templates

Automate Azure infrastructure setup via ARM templates

### First two labs

```json
SSH key files '/home/cloud/.ssh/id_rsa' and '/home/cloud/.ssh/id_rsa.pub' have been generated under ~/.ssh to allow SSH access to the VM. If using machines without permanent storage, back up your keys to a safe location.
{
  "fqdns": "",
  "id": "/subscriptions/4cedc5dd-e3ad-468d-bf66-32e31bdb9148/resourceGroups/72-cb9e7b76-accessing-and-using-the-azure-cloud-sh/providers/Microsoft.Compute/virtualMachines/newVM",
  "location": "westus",
  "macAddress": "00-22-48-09-7D-32",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.78.108.17",
  "resourceGroup": "72-cb9e7b76-accessing-and-using-the-azure-cloud-sh",
  "zones": ""
}
```

```powershell
Remove-AzVM -name newVM -ResourceGroupName 72-cb9e7b76-accessing-and-using-the-azure-cloud-sh

Virtual machine removal operation
This cmdlet will remove the specified virtual machine. Do you want to continue?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y

OperationId : 93348fdc-73ec-4959-9165-347e46337047
Status      : Succeeded
StartTime   : 1/5/2021 9:06:02 PM
EndTime     : 1/5/2021 9:06:44 PM
Error       :
```

AZ-900 Microsoft Azure Fundamentals 2020 - Introduction Quiz: 100%

## Cloud Concepts

[What is cloud computing? - Learn](https://docs.microsoft.com/en-us/learn/modules/principles-cloud-computing/2-what-is-cloud-computing?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### The Language of Cloud Computing

**High Availability**

Core to the cloud

Traditional:

Owning the hardware

Physical access

cant just add servers

Cloud:

Don't down the hardware

add more severs with a click

if hardware fails, replace instantly

Use clusters to ensure high availability

**Fault Tolerance**

Resilience

Fault tolerance is part of the resilience of cloud computing

Zero Down-Time

Faults caused by Azure are also mitigated by Azure

**Disaster Recovery**

Catastrophic Disaster

Hurricane, flood, tornado, or cyber attacks are real threats

Plan to Recover

Complete plan to recover critical business systems

Specific Points

Designated Time to Recovery and Recovery Point

**Scalability**

Add more resources on an as-needed basis

Scaling out:

Add more resources to the application to mitigate

Scaling up:

Adding more computer power or resources to the current hardware

Scaling down:

Taking away computer power or resources from the current hardware

Auto-scaling occurs by rules set by the system-admins for when to scale up or back down

time

traffic

load

etc.

**Elasticity**

Ability to quickly expand or decrease computing resources, not just VMs.

Elasticity enables scaling

**Agility**

The ability to rapidly develop, test, and launch software applications that drive business growth

Review:

**High availability** means VMs can spin up fast to help process requests

**Fault tolerance** describes how Azure will ensure you have zero downtime for services provided by Azure

**Disaster recovery** uses time to recovery and recovery point metrics to recover from catastrophic failures

**Scalability** refers to scaling out or scaling up

**Elasticity** is the ability to quickly increase or decrease computer processing and resources

**Agility** means the ability to rapidly develop, test, and launch software applications

[Benefits of cloud computing - Learn](https://docs.microsoft.com/en-us/learn/modules/principles-cloud-computing/3-benefits-of-cloud-computing?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Economy of Cloud Computing

Capital Expenditure

money spent by a business or organization on acquiring or maintaining fixed assets, such as land, buildings, and equipment

Large upfront costs

Operational Expenditure

Ongoing cost for running a product, business, or system on a day to day basis, including annual costs

Pay as you go model

Hourly Pricing (VMs, App services)

Consumption (Pay for resources used)

pay per execution

pay per second

pay per combination of both

Low usage = low cost

Review:

Using the right budget in a company can enable huge change

Capital expenditure is buying hardware outright, paid upfront as a one time purchase

Operational expenditure is ongoing costs needed to run your business

Consumption-based pricing lets you pay only for what you use

[Capital expenditure (CapEx) versus operational expenditure (OpEx) - Learn](https://docs.microsoft.com/en-us/learn/modules/principles-cloud-computing/3c-capex-vs-opex)

### Cloud Service Models

3 Cloud Service Models

Infrastructure as a service (IaaS)

Infrastructure = actual servers

Scaling is fast

No ownership of hardware

Includes VMs and Servers, Networks, and Physical Buildings

Platform as a service (PaaS)

Superset of IaaS

Includes VMs and Servers, Networks, and Physical Buildings

AND Middleware

AND Tools

Built to support web application life style

Avoids the woes of software licensing and its accompanying annoyances

Software as a service (SaaS)

Implicitly includes features of IaaS and PaaS

Includes apps and uses for using software

Providing a managed service

Pay an access fee to use

No maintenance and latest features

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled.png)

Review:

Service is the core of Azure, and there are three main ways to go about it.

IaaS provides servers, storage, and networking as a service

PaaS is a superset of IaaS and also includes middleware, such as database management tools

SaaS is when a service is built on top of PaaS, life O365

Serverless means that *you* don't have any servers

Allows a single function to be hosted, deployed, run and managed on its own

[Types of cloud services - Learn](https://docs.microsoft.com/en-us/learn/modules/principles-cloud-computing/5-types-of-cloud-services?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Marketplace

Solutions and Services

Large selection from Microsoft and Partners

Apps, VMs, templates, services, and much more.

Azure App Store

Buy cloud services with a single click

Easy to integrate

Use from Portal, CLI, or PowerShell

Some are free, some are paid

Publish your Own

If you are a Microsoft partner, publish your own services in the Azure Marketplace

### Cloud Architecture Models

Private

Pros

Complete control of infrastructure

Benefits of public cloud

Better security and privacy

Cons

Maintenance

Staffing

Public

Azure, GCP, AWS, etc.

Pros

No purchase of hardware

Low monthly fees

Cons

No control over features and versions

Hybrid

Mix of private and public cloud

Pros

Avoid disruptions and outages

Adhere to regulation, governance, etc.

Span both public and private cloud

Alleviate capital expenditure investments

Cons

Complex infrastructure

Review:

Private cloud is Azure on your own hardware in a location of your choice

All the benefits of a public cloud, but one can lock it down. Lots of staff required for upkeep and maintenance

Public cloud is Azure, AWS, GCP, etc. No upfront costs, but monthly usage.

Little control over services and infrastructure

Hybrid cloud model is the nest of private and public, but could be complex

[Cloud deployment models - Learn](https://docs.microsoft.com/learn/modules/principles-cloud-computing/4-cloud-deployment-models?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Cloud Concepts Summary

Language of Cloud Computing

High availability, fault tolerance, disaster recovery, scalability, elasticity, and agility. 

Describes stable and dependable cloud computing, the ability to adapt to changes in resource demand, user base, and application usage

Language of Cloud Economics

CapEx and OpEx describes cost for computing

OpEx is cloud computing with a pay as you go model

Cloud Service Models

IaaS, PaaS, and SaaS are cloud service models that pretty much all Azure products and services fall under.

The shared responsibility model dictates whether you or Microsoft is responsible for a cloud service

Azure Marketplace

An extra layer of functionality for your cloud applications, by letting users use and integrate third party products and services

Cloud Architecture Models

Private, public, and hybrid approaches to using cloud computing for your business

AZ-900 Microsoft Azure Fundamentals 2020 - Cloud Concepts Quiz: 75%

AZ-900 Microsoft Azure Fundamentals 2020 - Cloud Concepts Quiz 2: 83%

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%201.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%201.png)

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%202.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%202.png)

## Azure Architecture

### Regions and Availability Zones

A region is a set of datacenters deployed within a latency defined perimeter and connected through  a dedicated regional low-latency network

Set of datacenters

Each region has more than one data center, which is a physical location

Latency defined perimeter

Latency is the time it takes data to travel

Assures that the data centers are not too far from each other

Regional low-latency network

Fiber connection between data centers in the region

How to Choose a Region

Location

Choose a region closets to the users to minimize latency

Features

Some features are not available in all regions

Price

Price of services vary from region to region

**Often have to choose which is the most important: location, feature, or price**

Paired Region

Each region is Paired

Paired with same geographic area, excluding Brazil South

Outage Failover

If the primary region has an outage, one can failover to the secondary region

Planned Updates

Only one region in a pair is updated at any one time

Replication

Some services use paired regions for replication

Availability Zones

Physical Location

Each availability zone is a physical location within a region

Independent

Each zone has its own power, cooling, and networking infrastructure

Zones

Each region has a minimum of three zones

Regions and Zones

Lego analogy

Summary:

Azure Region

A set of data centers that are close enough to each other that it does not matter which datacenter your data is in.

Latency is the time it takes for data to travel

Availability Zone

Within a region and each zone has its own separate power, cooling, and networking infrastructure.

Used for protecting from datacenter and data failures

### Resource Groups and Azure Resource Manager

Resource Groups

Everything inside azure is inside a resource group

A resource group is not a resource

Resource Group Facts

One resource

Each resource can only exist in a single resource group

Add/remove 

You can add or remove resources to any resource group at any time

Move resource

You can move a resource from one resource group to another

Multiple Regions

Resources from multiple regions can be in one resource group

Access Control

You can give users access to a resource group and everything in it

Interact

Resources can interact with other resources in different resource groups

Location

A resource group has a location, or region, as it stores meta data about the resources in it.

Azure Resource Manager (ARM)

ARMBenefits

Group Resource Handling

You can deploy, manage, and monitor resources as a group

Consistency

Deploying resources from various tools will always result in the same consistent state

Dependencies

Define dependencies between resources to make sure they do not conflict with each other over resources

Access Control

Built-in features in the ARM make it easy to assign access rights to users

Tagging

Tag resources to easily identify them for future scenarios

Tagging is a way to label individual resources

Billing

Use tagging to stay on top of billing for groups of resources

Summary

Resource Groups

All resources belong to a resource group

It is not a resource, but it helps structure the Azure architecture

Azure Resource Manager

All interaction with Azure resources go through the ARM.

It is the main Azure Architecture component for creating, updating, and manipulating resources

- [x]  Creating Resources Demo

[Principles of resource groups - Learn](https://docs.microsoft.com/en-us/learn/modules/control-and-organize-with-azure-resource-manager/2-principles-of-resource-groups?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Architecture Quiz: 100%

## Azure Compute

### Virtual Machines

Infrastructure as a Service

Managing everything except the hardware.

This includes the networking compnents

Tools

Use the Azure Portal to manage large numbers of VMs and even hybrid clouds

Compliance

Use Azure blueprints to make your VMs comply with company guidelines

Recommendations

Azure will recommend improvements to ensure better security, higher availability, and greater performance

Choice

Choose amount of RAM, number of CPUs, and operating system

Pricing

Calculated Hourly

More resources, higher cost per hour

Use Cases

Pros

Control

Use virtual machines when you need to control all aspects of an environment or machine

Application

Install specific applications on Windows or Linux machines

Existing Infrastructure

You can move existing resources and virtual machines to Azure from on-premises or another cloud provider

Cons

Not for Everything

If you can use another Azure service instead, it is often worth it

Maintenance

A lot of maintenance with VM

Operating system updates

Patches

Security concerns

Recap:

Virtual Machines are at the core of Azure compute and widely used

A virtual machine is ones machine exclusively

Users don't buy, own, or control any hardware

Virtual machines are an IaaS offering, user is responsible for entire machine

Azure virtual machines take advantage of Azure tools

Pricing goes up as resources go up, usage is by the hour

[Explore Azure Virtual Machines - Learn](https://docs.microsoft.com/learn/modules/intro-to-azure-compute/3-virtual-machines?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Scale Sets

A group of identical, load balances VMs

Water analogy

Schedule scaling if you know the patterns of usage

Benefits

Multiple VMs

Simple to manage multiple identical VMs using a load balancer

High Availability

If one VM fails or stops, the others in the scale set will keep working

Auto Scaling

Automatically match demand by adding or removing VMs from the scale set

Large Scale

Run up to one thousand VMs in a single scale set

No Extra Cost

No added cost for using scale sets

Use Case

Store and customer

Scale manually bad because tedious and not accurate

Scale set monitors all the time to adjust completely

Recap:

Scale sets are taking virtual machines to the next level and aiding in keeping sanity

Scale sets are identical VMs

Activated or deactivated as needed

A baseline VM for the scale set ensures application stability

Baseline VM is what you copy to make up the scale set of VMs

As resource usage increases, more VMs are activated to balance the load

User only pays for the VM, storage, and networking resources used, the use of scale sets as a system is not extra

### App Services

Full Managed Platform

Servers, network, and storage all managed by Azure

Allows user to focus on business value and logic

Web Apps

Website and online applications hosted on Azure's managed platform

Runs on both Windows and Linux Platforms

Supports a lot of languages, such as .NET, Java, Node.js, PHP, Python, and Ruby

Azure integration for easier deployment

Auto-scaling and load balancing

Web Apps for Containers

Deploy and run containerized applications in Azure

A container is completely self-contained

All dependencies are shipped inside the container

Deploy anywhere with a consistent experience

Reliable between environments

API Apps

Expose and connect your data backend

Application Programming Interface

No graphical component or user interface

Connect other applications programmatically

Use a range of programming languages

Recap:

App services is an easy way to host and manage a web application

App services are a PaaS offering on Azure

Web Apps are used to host web sites and web applications

Web Apps for Containers can host one's existing container images

API Apps can host data backend services

[Explore Azure App Service - Learn](https://docs.microsoft.com/learn/modules/intro-to-azure-compute/5-appservice?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Container Instances

Features

Manage Application Dependencies

All the dependencies for an application are included in the container image

One can manage the application and its dependencies with confidence

Less Overhead

Virtual machines require a lot more maintenance and updates

Containers do not have any components relating to the operating system that require maintenance

Increased Portability

Applications running in containers can be deployed easily to multiple different operating systems and hardware platforms

Efficiency

Development, deployment, and maintenance are all more efficient when using containers

Scaling and patching are much simpler

Consistency

Operations team can rely containers being the same every time, no matter which target they are being deployed to

Workflow

Software Development Cycle → Application placed in a container → Azure Container Instances

Azure Container Instances

User to run container workloads

Primary Azure service for running container workloads

Workload is the process or application being ran

On demand allows the user to save money

Use containerized applications to process data on demand, by only creating the container image when one needs it

Works with tool of choice

Use the Azure Portal, Azure CLI, or Powershell

[Explore Containers in Azure - Learn](https://docs.microsoft.com/learn/modules/intro-to-azure-compute/4-containers?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Kubernetes Service

Kubernetes (K8s) is Greek for *governor* or *captain*

Kubernetes is an open-source container orchestration system for automating application deployment, scaling, and management

Open Source

Public code base and community involvement in the product

Orchestration

Keeps track of lots of parts of a system

Makes sure containers are configured correctly to work together

Automatic Application Deployment

Kubernetes will deploy more images of containers as needed

Automatic Scaling

Automatic monitoring of application load to determine when to scale the numbers of containers used

Azure Kubernetes Service

Replicate Container Architectures

Reuse your container architecture my managing it in Kubernetes

This makes setup quicker and increases confidence in the stability of the sustem

Standard Azure Services Included

User does not have to worry about infrastructure and hardware.

IAM, elastic provisioning, and much more included

Azure Container Registry (ACR)

Keeps track of current valuid container images

Manages files and artifacts for containers

Feeds container images to ACI and AKS

Uses Azure identity and security features

Scenario

Order Processing in a container

Image created from ACR

Load balancing using pods

Cluster → Node → Pod

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%203.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%203.png)

### Windows Virtual Desktop

Use any VM one wants

Any device with web access can connect to the VM

Completely virtualized version of Windows, meaning it runs all in the cloud

Benefits

Reuse Windows 10 Licenses

Reduces cost and streamline license usage

Concurrency

Multiple users can use the same VM instance

Access Anywhere

Use Windows 10 from anywhere on any device with an internet browser

Secure Data

Use Azure Storage to secure the data

### Functions

What are Azure Functions

IaaS/PaaS vs Function

IaaS/PaaS

Install user's own applications

Access to the operating system

Resource visbility

An app service has no OS access, but it does have resource access

Function

Smallest compute service on Azure

Single function of compute

Called, or invoked, via a standard web address (URL)

**Runs once and stops**

Architecture

No maintenance

No processes

Nothing VM related

Serverless compute service

Allows focus to be solely on functionality

Benefits

Only runs when needed

Azure function only runs where there is data to process

No traffic means no resources are being used

Saves Money

No resources running means function is not being used

Resilience

If function fails, it does not affect other function instances

Demo:

App Service is Website

App Service Plan is Server

Compute Summary:

Virtual Machines

Virtualized hardware the user controls.

Spin up and down as needed

Take advantage of the Azure tools available

Priced per hour with many configs available

Scale Sets

Sets of identical VMs

Scale Sets automatically create and delete VMs for an appliaction

Provides high availability and protects against server failures

App Services

Managed platform to host the user's applications

Web App, Containers, and API

Supports many programming languages

Azure container instances

Hosts and runs a user's containers on Azure

Containers have less overhead than VMs and can be deployed consistently

Azure Kubernetes Service

Open-source tool for orchestrating and managing many container images and applications

Uses clusters and pods to scale and deploy functions

Windows Virtual Desktop

Completely virtualized Windows 10

Access with any device that has a browser and internet conneciton

Reuse licenses to save money

Functions

Serverless Azure offering

Function does one compute action each time the function is invoked

[Explore Serverless computing in Azure - Learn](https://docs.microsoft.com/learn/modules/intro-to-azure-compute/6-serverless-computing?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

[Essential Azure compute concepts - Learn](https://docs.microsoft.com/learn/modules/intro-to-azure-compute/2-essential-azure-compute-concepts?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

- [x]  Deploying Your First Azure Virtual Machine

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Compute Quiz: 100%

## Networking

### Virtual Network

Address Space

Range of IP addresses available

Subnets

Subnet network into portions to manage

Resource Grouping

Group resources onto the same subnet to make it easier to monitor

Address Allocation

More efficient to allocate addresses to resources on a smaller subnet

Subnet Security

Use network security groups to secure individual subnets

Subnet Regions and Subscriptions

Regions

A virtual network belongs to a single region

Every resource on the virtual network must be in the same region too

Subscriptions

A virtual network belongs to just one subscription

A subscription can have multiple virtual networks

Cloud Avantages

Scaling

Adding for virtual networks or more address to a network is simpolke

High Availability

Peering virtual networks, using a load balancer, or using a VPN gateway will all increase availability

Isolation

Manage and organize resources with subnets and network security groups

VNet Peering

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%204.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%204.png)

Peering Benefits

Low latency, high bandwidth

Resources in virtual networks are connected with a low latency, high bandwidth connection

Link Separate networks

Resources in separate virtual networks can communicate with each other

Data transfer

transfer data easily between subscriptions and deployment models in separate regions

Recap:

A virtual network is a fundamental part of Azure infrastructure

An address space is a range of IP addresses one can use for resources

Subnet is a smaller network, which is part of the VNet. 

Subnets are used for security and logical division of resources

A VNet is in a single region and single subscription

VNets in the cloud can scale, and they also have high availability and isolation

[Azure Virtual Network fundamentals - Learn](https://docs.microsoft.com/learn/modules/azure-networking-fundamentals/azure-virtual-network-fundamentals?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Load Balancer

A Load Balancer distributes new inbound flows that arrive on the Load Balancer's frontend to backend pool instances, according to rules and health probes

Inbound Flows

Traffic from the Internet or Local network

Frontend

Access point for the load balancer

All traffic goes here first

Backend

VM instances receiving the traffic

Rules and Health Proves

Checks to ensure backend instance can receive the data

Scenarios

Internet Traffic

Balance the load of incoming Internet traffic into a system or application

Internal Networks

A load balancer works well with internal applications

Port Forwarding

Traffic can be forwarded to a specific machine in the backend pool

Outbound Traffic

Allows for outbound connectivity for backend pool VMs

### VPN Gateway

Virtual Network Gateway

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%205.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%205.png)

Main Components

Azure VNet with VPN Gateway ↔ On Premises

Site-to-Site Connection

Recap:

VPN Gateways are instrumental in a hybrid cloud architecture

VPN gateway is a specific VNet Gateway

Consists of two or mole dedicated VMs

VNet Gateway + "VPN" becomes a VPN Gateway

Sends encrypted data between Azure and an on premises network

Azure Gateway Subnet, secure tunnel, and on-premises gateway makes up a VPN Gateway scenario

[Azure VPN Gateway fundamentals - Learn](https://docs.microsoft.com/learn/modules/azure-networking-fundamentals/azure-vpn-gateway-fundamentals?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Application Gateway

Compare to Load Balancer

Route traffic based on HTTP requests to the backend pool

URI Path or headers

Benefits

Scaling

Scale the application gateway up or down based on the amount of traffic received

Encryption

Comply with any security policies

Disable or enable traffic encryption to the backend

Zone Redundancy

Span multiple availability zones and improve fault resiliency

Multi-Site Hosting

Use the same application gateway for up to 100 websites

Recap:

An applicate gateway is a higher level load balancer

Works on HTTP request of traffic, instead of IP address and port

Traffic from a specific web addresses can go to a specific machine

Is a fit for most other Azure services

Supports auto-scaling, end-to-end encryption, zone redundancy, and multi-site hosting

### Content Delivery Network

CDN

Distributed network of servers that can deliver web content close to users

Use edge node that is closest to the user

Benefits

Better performance

Improve the user experience and the performance of the application

Scaling

Scale to suit any spikes in traffic, and it also protects the main backend server instance from high loads

Distribution

Edge servers will serve requests closest to the user

Less traffic is then sent to the server hosting the application

Terminology

Cache

Collection of temporary copies of original files

Primary purpose is to optimize speed for an application

When a copy expires, a new copy is needed

Origin Server

Original location of the files, such as a web application

Master copy of the application

[Create a Content Delivery Network for your Website with Azure CDN and Blob Services - Learn](https://docs.microsoft.com/learn/modules/create-cdn-static-resources-blob-storage/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### ExpressRoute

Super fast connection

Overview

Company needs

On-Premises and on Azure

Highly available

Periodically migrated

Network

Connection is over ExpressRoute

if you need a private, secure, high-bandwidth, low-latency connection, directly from your data center or infrastructure to Azure, go with ExpessRoute

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%206.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%206.png)

### Networking Summary

Virtual Network

A fundamental part of Azure

All services are connected to a VNet

Includes an IP address range and subnets

Belongs to a single region and a single subscription

Load Balancer

Distributes and balances the incoming traffic to an application or network

Uses IP address and port number to determine the receiving VM in the backend pool

VPN Gateway

Connects an Azure network with an on-premises network securely

Application Gateway

Distributes incoming traffic based on HTTP request properties, such as URL and host headers

Same session traffic can be handled by multiple servers

Express Route

Direct link between on-premises and Azure

Enables a private, secure, high-bandwidth, low-latency connection

Content Delivery Network

Stores a cached version of the application on an edge node

Provides better performance and less traffic to the main server

Content cache is updated as necessary

- [x]  Intro to Creating Azure Virtual Networks

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Networking Quiz: 100%

## Storage

Storage account must be a unique Azure Namespace

Every object in Azure has its own web address

[Benefits of using Azure to store data - Learn](https://docs.microsoft.com/learn/modules/intro-to-data-in-azure/2-benefits-of-using-azure-to-store-data?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Blob

Binary Large Object

pretty much anything

Storage Levels

Storage Account → Container → Blob

Scenarios

Images

Store various sizes and formats as a single image storage

All Types

Store any kind of files and have distributed access through the Azure cloud storage

Streaming

Stream audio and video directly from the blob storage

Log Files

Write to log files regardless of size and frequency

Data Store

Store any kind of data at scale, such as for archiving, backup, restore, and disaster recovery

Blob Types

Block

Store text and binary data up to 4.7TB

Made up of individually managed blocks of data

Append

Block blobs that are optimized for append operations

Works well for logging where data is constantly appended

Page

Store files up to 8TB

Any part of the file could be accessed at any time

Ex: virtual hard drive

Pricing Tiers

Hot

Frequently accessed files

Lower access times and higher access costs

Cool

Lower storage costs and higher access times

Data remains here for at least 30 days

Archive

Lowest cost and highest access times

[Store application data with Azure Blob storage - Learn](https://docs.microsoft.com/learn/modules/store-app-data-with-azure-blob-storage/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Disk

Managed Disk

Attach to VMs

Azure Manages

User does not have to owrry about backup and uptime

Size and Performance

Microsoft and Azure guarantees size and performance as per the agreement of use

Upgrade

Easy to upgrade disk size and type

Disk Types

HDD

Spinning hard drive

Low cost and suitable for backups

Standard SSD

Standard for production

Higher reliability, scalability, and lower latency than the HDD

Premium SSD

Super fast and high performance

very low latench

use for critical workloads

Ultra Disk

For the most demanding, data-intensive workloads

disk size up to 64TB

[Choose the right disk storage for your virtual machine workload - Learn](https://docs.microsoft.com/learn/modules/choose-the-right-disk-storage-for-vm-workload/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### File

On-Premises

Company → On-Premises Storage

Issues

Constraints

Contains limited amount of storage

Backups

time and resources spent on maintaining backups

Security

difficult to keep all data secure at all times

Specialist assistance is often needed

File Sharing

can be difficult to share files across teams and orgs

File Benefits

Sharing

Share access to the Azure file storage across machines and provide access to the on-prem infrastructure as well

Managed

user does not have to worry about hardware or operating system

Resilient

Network and power outages will  not affect the user's storage

Scenarios

Hybrid

Supplement or replace your existing on-premises file storage solution

Lift and Shift

Move your existing file storages and related services to Azure

### Archive

Overview

Requirement

Policies, legislation, and recovery can be requirements for archiving data

These can be very large amounts of data

Lowest Price

Archive tier is the lowest price for storage on Azure

Few dollars a month can get TBs of space

Features

Durable, encrypted, and stable

Perfectly suited for data that is accessed infrequently

Free up Premium Storage

Cheap archive storage allows for freeing up more premium storage on-prem

Secure

Fully secure to allow for any personal data such as financial records, medical data, and more

Blob

Archive storage is blob storage, so the same tools will work for both

### Summary

Blob

General storage for anything one would like

Block, append, and page

Blob is inside a container, which is inside a storage account

Hot, cool, or archive price and performance tiers

Disk

Disk is generally attached to a VM

Managed storage service by Azure

HDD, SSD, Premium SSD, or Ultra Disk

File

Mitigating on-prem file storage solutions

Use to have highly available and resilient storage that can be shared easily

Archive

Very cheap way to store massive amounts of data

blob storage type

- [x]  Create Azure Blob Storage and Upload a Blob

AZ-900 Microsoft Azure Fundamentals 2020 - Storage Quiz: 100%

## Database

book analogy in bag or in shelf and organized

[How Azure data storage can meet your business storage needs - Learn](https://docs.microsoft.com/learn/modules/intro-to-data-in-azure/3-how-azure-storage-meets-your-business-storage-needs?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Cosmos DB

Global from the Go

Synchronization

Easy with Cosmos

Traditional databases that aren't cloud enabled could be very difficult to set up across multiple regions

Azure takes care of these struggles with Cosmos DB

One Click to Add Regions

It is very easy to expand to more regions withCosmos DB and have the data stay in Sync

Continued Synchronization

Cosmos DB stays on top of all reads and writes to the data and makes sure the data is moved between regions to stay in Sync

Latency

Pretty fast no latench

Scalability

Automated

Cosmos DB automatically scales to meet resource demand

Infinite Resources

Any number of users of your application can be supported

Lowest Price

Even through the scaling is automatic, only pay for the resources that are used

Connectivity

Developer

Choose form various SDKs and APIs to interact

Languages

A language for most modern developers, including C Sharp, Java, and Node.JS

Platforms

Choose from numerous data platforms such as SQL, MongoDB, and Cassandra

Cosmos can run up quickly in cost

### Azure SQL

Managed Service - Database as a service

Migration

On-Prem → Azure SQL

Frictionless process

cost saving

lower total cost of ownership

Built-in Machine Learning

Optimization

Suggestions on how to optimize and imrpove performance of Azure SQL instances

Warnings

User will receive warnings of degrading instances, and if anything out of the ordinary is happening

Cloud Benefits

Scalability

Scale the Azure SQL instances and get high availability as well

Space

Manage huge databases up to 100TB

Security

Benefit from the build-in security features of the Azure cloud platform

[Introduction to Azure SQL - Learn](https://docs.microsoft.com/learn/modules/azure-sql-intro/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Database for MySQL

Context

MySQL is open source

Relational Database

It is mature and stable

Azure Advantages

Platform as a Service

Managed by Microsoft

Development Focus

Focus on developing business strengths instead of managing servers and networks

Choice of Language

Use the language and framework of choice

High Availability

Cloud can easily provide high availability and scalability.

Azure Security Features

Receive all high standard security features of Azure

Cloud Capabilities

All PaaS features such as database patching, automatic backups, and monitoring are included in the cost in Azure

MySQL Use Cases

Web Applications

E-Commerce

Mobile Apps

Digital Marketing

Finance Management

Gaming

[Deploy MySQL and MariaDB to Azure - Learn](https://docs.microsoft.com/learn/modules/deploy-mariadb-mysql-postgresql-azure/4-deploy-mysql-mariadb-azure?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Database for PostgreSQL

PostgreSQL

Open-source Database

Open-source relational database, similar to MySQL

Came after Ingres hence Postgres

Free and Stable

Since 1996

Features

Extensions

Use a large number of extensions, such as JSONB, geospatial functions, indexing, integration with tools and much more

Horizontal Scaling

Use very high performant access to distributed data sets

Performance Recommendations

Receive recommendations base don usage on how to make the DB perform better

Also receive notifications for disruptive events

Fully Managed

Azure gives automatic database patching, automatic backups, and build-in monitoring

PostgreSQL Use Cases

Financial Applications

Ideal for online transactions and integrates with mathematical software

Government

Governments use Postgres for Geometic (GIS) data. ie PostGIS

Manufacturing

Downtime is disastrous, and PostgreSQL provides automated failover and full redundancy

[Explain how to deploy PostgreSQL to Azure - Learn](https://docs.microsoft.com/learn/modules/deploy-mariadb-mysql-postgresql-azure/3-explain-how-deploy-postgresql-azure?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Database Migration Services

Database Migration

Single Tool

One step migration for Microsoft SQL to Azure SQL

Documentation

Comprehensive step-by-step guides and documentation for helping one migrate

Guide for non-MS

Very detailed guides for migrating from non-MS databases

[Exercise - Migrate a database with downtime by using Azure Database Migration Service - Learn](https://docs.microsoft.com/learn/modules/migrate-sql-server-relational-data/7-exercise-migrate-database-service?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Summary

Azure Databases

Cosmos DB

Globally distributed database

Super fast and easy to manage

Azure SQL

Fully managed and using stable Microsoft SQL Technology

Compatible with on-prem SQL servers

Azure Database for MySQL

Popular community driven open-source database that is used widely

Azure Database for PostgreSQL

Another popular choice for relational database

Azure offers a managed version

Provides enterprise features like horizontal scaling

Database Migration Services

Migration of almost any kind of database to Azure SQL or SQL server.

Guides, step-by-step instructions, and comprehensive documentation

AZ-900 Microsoft Azure Fundamentals 2020 - Databases Quiz: 60%

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%207.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%207.png)

AZ-900 Microsoft Azure Fundamentals 2020 - Databases Quiz: 100%

## Authentication and Authorization

[Identity and access - Learn](https://docs.microsoft.com/learn/modules/intro-to-security-in-azure/3-identity-and-access?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Identity Services

Authentication

Confirming you are you

Confirming Identity

First test for access

Authorization

Comes after authentication

Do you get access

Access Management

Authentication vs. Authorization

Know the difference to create effective access management

Keep out threat actors

Access management is critical to ensure only the right people and processes have access

### Azure Active Directory

Active Directory

Traditional Office Use

AD was designed for traditional office use with computers and printers

Was not built for cloud

Authentication

Active Directory authentication uses services that are not available on Azure

Disclaimer

AD is not Azure AD

Azure Active Directory (AAD) Service

Mandatory

Cannot have an Azure account with an AAD service

First User

Every Azure account needs a first user and this user is in the initial AAD instance

Tenant

Organization

A tenant represents the org

Dedicated AAD

A tenant is a dedicated instance of AAD that an org receives when signing up for Azure

Separate

Each tenant is distinct and completely separate from other AAD tenants

One User - One Tenant

Each user is Azure can only belong to a single tenant

Users can be guest of other tenants

Subscription

Billing Entity

All resources within a subscription are billed together

Cost Separation

Can have multiple subscriptions within a tenant to separate costs

Payment

If a subscription is not paid, all the resources and services associated with the sunscription stop

Hybrid Cloud Architecture

On-Prem → AAD → Azure

Recap:

Manage users and permissions with Azure Active Directory

Active Directory is *not* the same as Azure Active Directory

AD is not AAD

Every Azure account with have an Azure AD service

A tenant is a dedicated instance of Azure AD. 

Represents the org in Azure

A user belongs to a single tenant, but can be a guest in multiple

A subscription is a billing entity, all resources belong to a single subscription

Azure AD can be utilized in a hybrid cloud setup

### Multi-Factor Authentication

Approach

2 or more:

Something you know

Something you have

Something you are

Example:

Username and password - something you know

Code sent to phone - something you have

### Single Sign-On

Login to multiple services

Ex: Microsoft services for Outlook, Azure, etc

Azure SSO

Azure Active Directory Seamless Single Sign-On

Enable SSO in AAD

Seamlessly use all applications without logging in

Single username and Password

### Summary

AAD is Fundamental

Azure needs AAD

AAD is not the same as AD

AAD is First

First service of every new account is the Azure Active Directory Instance

Tenant

Tenant is a special instance of AAD. It is the first AAD instances that is created when a new Azure account is setup

A user belongs to a single (1) tenant

Subscription

Billing entity that controls the costs of resources and services associated with it

Hybrid Cloud

AAD Can help manage users in a hybrid cloud environment between on-prem and Azure

Multi-Factor Authentication

An extra layer of security using:

Something you know

Something you have

Something you are

Single Sign-On

Use a single username and password to log in to multiple applications using Azure Active Directory

AZ-900 Microsoft Azure Fundamentals 2020 - Authentication and Authorization Quiz: 100%

## Azure Solutions

### Internet of Things

A system of interrelated computing devices, mechanical and digital machines, objects, animals or people that are provided with unique identifiers and the ability to transfer data over a network without requiring human-to-human or human-to-computer interaction.

IoT Hub

Backend - Hub to receive data from IoT devices

Features

Managed and Secure

Ease of Deployment

Device authentication

PaaS

IoT Central

SaaS

Simplify and speed up the implementation of the IoT Solution

No coding Needed

One does not have to know how to write code to deploy an IoT project

Receive feeds from devices and focus on metrics and business value

Pre-made connectors

Use any of the hundreds of connectors that are ready to use in IoT central

Solutions

IoT Hub

PaaS solution that provides more control over the IoT data collection and processing

IoT Central

SaaS solution that provides premade IoT connections and dashboards to get set up quickly

Azure Sphere

An all-in-one solution for IoT devices on Azure

Specific Hardware

Only use hardware and chipsets certified by Microsoft for use on Azure

Security

Specialized security service that manages maintenance, updates, and general control

Operating System

Custom made for Azure Sphere devices.

Connects to the Sphere Security Service

[Introduction to Azure IoT Hub - Learn](https://docs.microsoft.com/learn/modules/introduction-to-iot-hub/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

[Introduction to Azure IoT - Learn](https://docs.microsoft.com/learn/paths/introduction-to-azure-iot/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Big Data

Data Collection

Big Data - Moving Definition

Business Value

Better service

Better products

More profit

Data Lake Analytics

Large amount of Data

Parallel Processing

Two or more processes or computers processing the same data at the same time

Ready to Go

Servers, processes and any other needed services are ready to go from the start

HDInsights

Similar to Azure Data Lake Analytics

Open source

Includes Apache Hadoop, Spark, and Kafka

Azure Databricks

Based on Apache Spark, a distributed cluster-computing framework

Run and process a dataset on many computers simultaneously

Databricks provides all the computing power

Integrates with other Azure Storage services

Azure Synapse Analytics

Azure's data warehouse offering

Used to be called Azure SQL Data Warehouse

Used for reporting and data analysis

Only limited by scope

Use Synapse SQL language to manipulate the data

Outcomes

Speed

Speed and efficiency of processing large amounts of data

Cost Reduction

Save large amounts of money on storage and processing by using a Big Data solution in the cloud

Better Decision Making

Immediate data processing and analysis in memory means one can make better decisions and make them faster

New Products and Services

Understand what customers want and provide them with much better products and services

[Introduction to Azure Data Lake storage - Learn](https://docs.microsoft.com/learn/modules/introduction-to-azure-data-lake-storage/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

[Implement a Data Warehouse with Azure Synapse Analytics - Learn](https://docs.microsoft.com/learn/paths/implement-sql-data-warehouse/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Machine Learning

Machine Learning

Models

Definition of what the machine learning application is learning.

Model is a set of rules of how to use the data provided

Model finds patterns based on the rules

Knowledge Mining

Use Azure search to find existing insights in the data

File relationships, geography connections, and more

Built-in Apps

Azure has a number of built-in apps that one can use for ML and AI right away

Includes cognitive services and bot services

Azure Bot Service

PaaS

Build bots for question and answer services, virtual assistants, and more

Code or Visual

Create a bot using the visual editor or programming

Language

Let users talk to the bot with natural language and speech integration

Integration

Integrate the bot with other services such as Facebook Messenger, Teams, etc.

Branding

Use a branding and own the data the bot uses and produces

Azure Cognitive Services

Vision

Use to recognize, identify, and caption videos and images

Decision

Apps can make decision based on content,

Detect potential offensive language, detect IoT anomalies and leverage data anlytics

Speech

Autunitic speech-to-text transcription

Speaker identification and verification

Azure Machine Learning Studio

Supports all Azure Machine Learning tools

Pre-made modules for a project

Use for real-world scenarios

Twitter sentiment analysis, photo grouping, and movie recommendations

Machine Learning Service

End-to-end Service

Service to use AI and machine learning almost anywhere on Azure

Tooling

Machine Learning Service is a collection of tools to help one build AI applications

Automation

Automatically recognizes trends in applications and creates models for user

[Predict rocket launch delays with machine learning - Learn](https://docs.microsoft.com/learn/paths/machine-learning-predict-launch-delay-nasa/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Serverless

Serverless means user is not managing the servers

Azure Functions

Golden Oldie

First "Serverless" service on Azure

Azure service most will start with when exploring serverless architecture

Single Task

only performs a single task when invoked

Runs once for each invocation

Basic Compute Unit

Fundamental compute action and can be run millions of times per second if needed

Logic Apps

Connect Systems

Connect systems both inside and outside of the Azure platform

Integrate not only apps, but also data flows, services, and entire systems

Automation

A lot of ways to schedule, automate, and orchestrate tasks and processes

Quick Start

No coding required to get started right away

Event Grid - big network of connections for any service that wants it

Routing Service

Event Grid is a routing service for sending and receiving events between applications

Serverless

No management of infrastructure components

Ease of Use

Event Grid makes complex cloud architecture simpler

Recap:

Serverless approaches work extremely well with cloud services

Yes there are servers (Just not the users)

Azure Functions are the most basic of compute tasks

Does one function then dies until next time it is called

Logic apps are a quick and simple way to integrate systems and applications inside and outside of Azure

Event Grid is a routing service for passing events between applications that need to know about the events

[Explore Serverless computing in Azure - Learn](https://docs.microsoft.com/learn/modules/intro-to-azure-compute/6-serverless-computing?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### DevOps

DevOps is the work between development and production

Azure DevOps

Azure Boards

Keep track of work tasks, timelines, issues, planning and much more

Azure Pipelines

Produce and test software automatically and continuously

Azure Repos

Store source code for the application securely in a managed way

Azure Test Plans

Design tests of application to implement automatically

Azure Artifacts

Share applications and code libraries with other teams inside and outside of the org

Azure DevTest Labs

Environment Management

Allow developers and engineers to create environments for test and development

Cost Management

User will not incur unexpected costs and will help minimize waste of resources on the account

Templates

Tailor the development and test environments and reuse them with templated deployments

GitHub and Github Actions

GitHub

Acquired by Microsoft

Code repository

GitHub Actions

Very similar to Azure Pipelines

Build code, test, and publish

Works with almost any platform

[Get started with Azure DevOps - Learn](https://docs.microsoft.com/learn/modules/get-started-with-devops/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Summary

Azure Solutions

Internet of Things

IoT is a network of millions of connected devices that function without human interaction

Iot Hub collates and manages data feeds as a PaaS product. 

IoT central is a SaaS offering with templates and dashboards for a quick start

Big Data

PRocessing and storage of very large data sets

Azure has Data Lake Analytics and HDInsight

Reduced cost, better decisions, and new products

Machine Learning

Use rules and models to train the AI implementation

Azure Machine Learning Studio has pre-made models and tools to help a user get started

Azure Machine Learning Service is a collection of tools

Serverless

Someone else's servers

Azure Function is a single unit of compute

Azure Logic Apps can connect data feeds and application

Azure Event Grid is a network to route events between applications

DevOps

Azure DevOps has 5 tools: 

Boards

Pipelines

Repos

Test plans

Artifacts

Azure DevTest Labs lets one create full development and test environments easily and cost effectively

GitHub and GitHub actions are tools similar to Azure DevOps

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Solutions Quiz: 67%

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%208.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%208.png)

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%209.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%209.png)

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Solutions Quiz: 100%

## Security

### Defense in Depth

On-Premises Defense

Physical hardware

Responsible for the security of the hardware, buildings, and staff

Layers of Defense

Several layers of defense, such as swipe cards, security guards, firewalls, and more

It is up to user

Responsible for adequate defense of hardware and data

Azure

Physical → Identity and Access → Perimeter → Network → Compute → Gateways and Firewalls → Data

[Defense in depth security in Azure](https://azure.microsoft.com/resources/videos/defense-in-depth-security-in-azure/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Securing Network Connectivity

Firewall

Rules

Firewall defines rules for what kind of traffic can and cannot access the device or service behind it

Variation

Firewalls comes as hardware and software versions

Critical Part

Any network that takes security serious will have a firewall

DDoS

Distributed Denial of Service

Web Server is flooded with requests to bring it down

DDoS Protection Service

Many Internet-Connected Devices

A lot of computers and other connected devices target a single website to make it stop

GitHub attack had 127 million requests per second

Protection

Protects the DDoS attack and deflects it

Various levels of protection depending on scenario

No Downtime

There is no interruption to the service at all

Azure will mitigate the attack globally

Network Security Group (NSG)

Resource Firewall

Personal Resource Firewall

Attach to virtual network, subnet, or network interface

Rules

A NSG determines who can access the resources attached to it, using rules for inbound and outbound traffic

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2010.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2010.png)

Application Security Groups

Protects Application Infrastructure

Focus the security on the application rather than the IP endpoint

Natural Extension

Group VMs and virtual networks into logical application groups and apply an application security groups

[Protect your network - Learn](https://docs.microsoft.com/learn/modules/intro-to-security-in-azure/5-network-security?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Security Center

Consistent and Manageable Cloud Security is Difficult

Functions

Threat Alerts

Ready for Hybrid architectures

Each VM has an agent installed that sends data

Azure Analyzes the data and alerts user

Highlights

Policy and compliance metrics

A "secure score" to entice great security hygiene

Integrate with other cloud providers

Alerts for resources that are not secure

Using Security Center

Define Policies

Set up policies for Azure to monitor resources from

A policy is a set of rules used to evaluate a resource

Use predefined policies or create custom ones

Protect Resources

Actively protect the resources through monitoring the policies and their outcomes

Response

Respond to any security alerts

Investigate all of them and then go back to step 1 to define new policies to account for the alert

[Get tips from Azure Security Center - Learn](https://docs.microsoft.com/learn/modules/intro-to-security-in-azure/2a-azure-security-center?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Key Vault

Attackers know where users keep their keys

Azure Key Vault

Secure Hardware

The key vault hardware is secure too

Not even MS can access the keys in it

Application Isolation

An application cannot pass secrets to other applications, nor can they access another application's secrets

Global Scaling

Scale globally like any other managed Azure service

[Configure and manage secrets in Azure Key Vault - Learn](https://docs.microsoft.com/learn/modules/configure-and-manage-azure-key-vault?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Information Protection

Secure documents, emails, and data outside of the company network

Classify Data

Classify data according to how sensitive it is either using policies or manually

Track Activities

Track what is happening with shared data and revoke access if needed

Share Data

Safely share data as you can control who edits, views, prints, and forwards it

Integration

Controls for document access is integrated with common applications and tools, such as Microsoft office

[Protect your shared documents - Learn](https://docs.microsoft.com/learn/modules/intro-to-security-in-azure/6-azure-information-protection?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Advanced Threat Protection

ATP

Monitor Users

Analyze user activity and information

This includes any permissions and membership of groups

Baseline Behavior

 Record what a user's normal behavior and routine is

Any activity outside this routine will be logged as suspicious

Suggest Changes

ATP will suggest changes to conform with security best practices to reduce risks

Cyber-Attack Kill-Chain

Reconnaissance

If a user is searching for information about other users, device IP addresses and more, ATP will raise alerts

Brute Force

Any attempts to guess user credentials will be identified and flagged

Increasing Privileges

Any attempt by a user to gain more privileges will be flagged

This could be through another user's login

[Azure Advanced Threat Protection - Learn](https://docs.microsoft.com/learn/modules/intro-to-security-in-azure/7-advanced-threat-protection?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Sentinel

Sentinel is a security information and event management tool

Data Collection → Aggregation and Normalization → Analysis and Threat Detection → Things Happen → Tale Action

Benefits and Features

Behavioral Analytics

Sentinel uses artificial intelligence to learn if any detected behavior is unusual

AWS Integration

Data from AWS services can be fed directly into Sentinel

Allows for one approach for threat detection across multi-cloud infrastructure

Cloud Scale

Sentinel can take advantage of Azure cloud scaling and deliver more accurate results quickly

### Azure Dedicated Hosts

Dedicated Hosts

Hardware Control

Full control of an entire physical server on Azure

Users and User's Alone

Physical layer isolation means user won't get any foreign VMs on dedicated host

Maintenance

Reduce impact on system by choosing when to install updates to the dedicated host

Cloud Benefits

Compliance

Take advantage of the stringent Azure compliance in combination with managing one's own hardware

Global Infrastructure

Availability zones, fault isolation, high availability, and scale sets come as standard

No optional extras

OS of one's chhoice

Choose Windows, Linux, or SQL server on a range of VM sizes

Even save money by using one's own licenses

### Summary

Security Summary

Defense in Depth

Need multiple layers of defense for infrastructure

Azure has physical, identity, perimeter, network, compute, gateways and firewalls, and data as protection layers

Securing Network Connectivity

A firewall controls the data coming in and out of a network based on rules

Azure protects against DDoS attacks with no downtime to you

A network security group protects a subnet or virtual machine

Azure Security Center

Monitor security hygiene for VMs

Define policies to protect one's resources better and respond to incidents

Azure Key Vault

A secure way to share access to applications and resources with third parties without every revealing any credentials

Azure Information Protection

Share files and data inside and outside of Azure and still maintain control over that data

Control who views, edits, prints and more

Azure Sentinel

Collect, aggregate, analyze and present security issues automatically for one to take action

Azure Dedicated Hosts

One's own dedicated Azure hardware to install Windows, Linux, or SQL Server VMs on

Gives control without losing cloud benefits like scaling, scale sets, fault isolation, and availability zones

Advanced Threat Protection

One secures and manages users of the org

Monitor users' behaviors, create a baseline of this behavior and report on any anomalies from it

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Security Quiz: 80%

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2011.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2011.png)

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Security Quiz: 80%

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Security Quiz: 100%

## Privacy, Compliance, and Trust

### Governance

Azure Policy

Create Policies in Azure

Governance validates that an organization can achieve its goals through effective and efficient use of IT

Role-Based Access Control (RBAC)

Define User Access

Define specific user access to individual resources

Minimum Access

RBAC can enable minimum access necessary to resources

Ensures only users with valid access can manage resources

Target Specific Use Cases

Be very explicit about uses and access

Allow an application access to certain resources or allow a user to manage resources in a resource group

Role Assignment

Security Principal

Object representing an entity such as a user or group which can access the resource

Role Definition

A collection of permissions such as read, write, and delete

Scope

The resources the access applies to

Specify which role can access a resource or resource group

Locks

Assigning

Assign a lock to a subscription, resource group, or resource

Types

A lock can be of two types

Delete - one cannot delete the locked object

Read-Only - one cannot make any changes to the locked object

Locked means locked

A lock needs to be removed before the locked actions can be performed again

Azure Blueprints

Templates for creating Azure resources

Resource templates

RBAC

Policies

Samples for common regulations

Cloud Adoption Framework

Collection of Documents

Lots of resources to guide user through the cloud adoption process

Guidance

Help to define strategies for adoption, planning the move, "being ready" for the cloud, adoption reasons, governance practices, and managing a living, breathing cloud architecture

Governance

Key to the cloud adoption process is governance of the process

Cloud Adoption Framework is a big step in that process

Azure Advisor for Security Assistance

Part of Azure Security Center

Recap:

Governance keeps one compliance and out of trouble

Azure Policy ensures that policies applied to resources are compliant

A policy is a set of rules to ensure compliant resources

Role Based Access Control (RBAC) ensures user compliance through assigning a role to the user

Role is a combination of security principal, role definition, and scope

Locks make sure that subscriptions, resource groups, or resources are either not modified or not deleted

Blueprints are templates for creating standard Azure environments

Azure Advisor for Security Assistance is part of the Security Center in Azure

[Define IT compliance with Azure Policy - Learn](https://docs.microsoft.com/learn/modules/intro-to-governance/2-azure-policy?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

[Define standard resources with Azure Blueprints - Learn](https://docs.microsoft.com/learn/modules/intro-to-governance/5-azure-blueprints?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

[Microsoft Cloud Adoption Framework for Azure - Cloud Adoption Framework](https://docs.microsoft.com/azure/cloud-adoption-framework/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Azure Monitor

Azure Monitor helps find resources that are not performing at 100%

Telemetry is the collection of measurements of other data at remote points

Azure Monitor

Constant feed

Most azure services feed telemetry data into Azure Monitor

Even on-prem can send telemetry to Azure monitor

Fully Managed

Azure Monitor is centralized and fully managed

Analyze all the data from one central place

Query Language

Full access to an interactive query language to learn about the telemetry data

Machine Learning

Predict and recognize problems faster with built-in machine learning

Outcomes

Maximize performance

Maximize Availability

identify issues

### Azure Service Health

Maintenance

Azure needs to be updated and maintained like all other computing infrastructure

Dashboard for Service Health

Notifies about any planned and unplanned incidents

Azure Service Health

Dasboard

Personalized dashboard to highlight service issues affecting your resources

Custom Alerts

Get notified of planned and non-planned outages

Alerts are simple to set up and customize

Real-Time Tracking

Track any alerts and issues in real-time and get full reports once resolved

Free Service

Azure Service Health service is completely free

### Compliance

Industry Regulation

General Data Protection Regulation

Main objective is to protect individuals and processing of their data

Gives control of personal data back to the individual, instead of the company owning it

Companies are required to implement a lot of tools for consumers to control their data

ISO Standard

Many different ISO categories, such as compliance with quality and customer satisfaction

Most common is ISO 9001:2008

Also includes food safety and environmental management

NIST

National Institute for Standards and Technology

Focuses purely on the tech industry

Developed Primarily for US Federal agenceies

Compliance with NIST means compliance with multiple Federal US regulations

Azure Compliance Manager

Azure knows about compliance and resources, and it can give you recommendations through the compliance manager

Recommendations

Get recommendations for ensuring compliance with GDPR, ISO, NIST, and others

Tasks

Assign compliance tasks to team members and track progress

Compliance Score

Chase a perfect score to be 100% compliant

Secure Storage

Upload documents to prove compliance and store them securely

Reports

Get reports of Compliance data to provide to managers and auditors

Azure Government Cloud

Dedicated Regions

If US govt body or contract for one, access is available

Government Cloud consists of dedicated separate datacenters

Exclusivity

Guaranteed only screen personnel from US federal, state, and local government have access

Compliance

Ensure compliance with required US government agencies, and level 5 DoD approval

Azure Benefits

Get standard Azure cloud benefits:

High availability, scalability, and managed resources

China Region

Located in China

Azure datacenter is physically within China and has no connection outside of China, including other Azure regions

Data is Kept in China

All customer data is kept inside Chinese borders

Certain global Azure services won't work fully

Compliant

Ensured compliance with Chinese regulations at all times

Recap:

Compliance is not negotiable

GDPR, ISO, and NIST are regulations and standards to ensure compliance with applicable legislation

Azure Compliance Manager provides recommendations, tasks to assign team members, a compliance score, secure document storage, and reports

Azure Government Cloud provides dedicated datacenters to US Government bodies.

Compliant with US federal, state, and local requirements

Azure China region contains all data and datacenters within China

Complies with all applicable Chinese regulations

[Compliance terms and requirements - Learn](https://docs.microsoft.com/learn/modules/principles-cloud-computing/3a-compliance?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Privacy

Azure Privacy

Azure Information Protection

Classify, label, and protect data based on data sensitivity 

Azure Policy

Define and enforce rules to ensure privacy and external regulations

Guides

Use guides to respond and comply with GDPR privacy requests

Compliance Manager

Make sure one is following privacy guidelines

Microsoft Privacy Statement

### Trust

Trust Center

Learn about Microsoft's effort on security, privacy, GDPR, data location, compliance and more

Service Trust Portal

Review all the independent reports and audits performed on Microsoft's products and services

Azure complies with more standards than any other cloud provider

[Explore your service compliance with Compliance Manager - Learn](https://docs.microsoft.com/learn/modules/intro-to-governance/6-azure-compliance?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Summary

Privacy, Compliance, and Trust

Governance

Azure Policy, Role-Based Access Control (RBAC), Locks and Azure blueprints

Azure Monitor

Collect telemetry data from resources, which one can analyze

Maximize performance and availability and identify issues

Azure Service Health

Notifies one about any planned and unplanned incidents on the Azure platform

Compliance

Comply with GDPR, adhere to ISO and NIST standards

Use Azure Compliance Manager to manage compliance

Government Cloud and China region

Privacy

Core part of Azure and its products

Azure Information Protection, Azure Poolicy, and the GDPR guide are all privacy tools

Trust

Trust Center is where one can find out what Microsoft does to keep user's trust

Service Trust Poral is where one can find audit reports and certificates awarded to Azure

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Privacy, Compliance, and Trust Quiz: 88%

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2012.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2012.png)

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Privacy, Compliance, and Trust Quiz: 100%

## Pricing

Pricing Structure

Azure

Don't own hardware - pay for access to it

Pay for number of hours using resource

Pay more for more resources

Service payment is tiered

Location can affect price

### Subscriptions

Billing and Pricing

All resources belong to a subscription

Subscriptions

Multiple Subscriptions

Any Azure account can have multiple subscriptions

Useful for organizing who pays for what

Billing Admin

One or more users can be a billing admin, which manages anything to do with billing and invoicing on Azure

Ensures separation of responsibility

Billing Cycle

A billing cycle on Azure is either 30 or 60 days

Offer Types

Offer type is the type of subscription

There are many different ones at any one time

Management Groups

Group Subscriptions

Take action across subscriptions in bulk

Very useful in large orgs with many subscriptions

Organize

Manage access, policies, and compliance in bulk

Ex: have a management group per country or department

Billing Logic

Maintain billing associated with the right budgets

Nest management groups to indicate hierarchy and relationship

[Understand Azure billing - Learn](https://docs.microsoft.com/learn/modules/create-an-azure-account/4-multiple-subscriptions?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Cost Management

Buying Azure Services

You can't use Azure without buying products and services

Free Accounts

Benefits

Many Free Services

VMs, databases, storage, and more

Always Free

Some services are always free for everyone, some totally free, some partially free up to a threshold

Azure Cost Management

Azure Portal

Access the Azure Cost Management tool from within the Azure Portal

Get a detailed view of current and projected costs

Free and included with all Azure subscriptions

Reports and Recommendations

Get detailed spending reports and recommendations on how to save on costs and analyze them

Optimization

Optimize current resources to save money and monitor any AWS charges too

Spot VMs

Spot VM Usage

Save up to 90% of the price

Evict at any time

Recap

Save money by using unused capacity

VM can be evicted at any time

Use for interruptible non-critical workloads

Use with Azure scale sets

Set a max price for the Spot VM

[Azure Free Account FAQ | Microsoft Azure](https://azure.microsoft.com/en-au/free/free-account-faq/)

[Azure Fundamentals part 6: Describe Azure cost management and service level agreements - Learn](https://docs.microsoft.com/learn/paths/az-900-describe-azure-cost-management-service-level-agreements/?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Pricing Factors

Influencing on Pricing

Resource Size

Different sizes of resources will have different pricing

More powerful VM costs more

Resource Type

Big difference in amount of hardware resources needed for various types of resources, as well as complexity

Location

Different Azure locations have different prices for services

Exchange rates, labor costs, and more have an influence

Bandwidth

Bandwidth one's services are using incurs cost as well

Zones and Bandwidth

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2013.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2013.png)

Pricing Calculator

Choose from all available Azure services

Select resource properties

Monthly cost estimate

Export estimate for further analysis and use

Total Cost of Ownership Calculator

Get an estimate of the total savings one could get for moving on-prem resources to Azure

Estimate Total savings over a period of time by using Azure

Comprehensive reports to share with stakeholders

### Best Practices

Spending Limits

Default Limit

Some azure accounts with monthly credits to use will have default spending limits

No Increase

When credits are used, either remote limit entirely or leave it in effect

No spending limit

Pay as you go accounts have no spending limit functionality

Quotas

Property Limit

A quota is a limit on a certain property of an Azure Service

Ensure Service Level

Quotas are necessary to ensure Azure can maintain their high service level

Quota Change

If one needs to increase quota for a particular service, ask Microsoft to increase

Tags

Non Functional labels

Attack to resource or resource group

Use as many tags as wanted/needed

Best Practices

Identify Roles

Protect sensitive data by defining which roles can access a resource

Related Resources

To make bulk processing and updating easier, define which resources are related

Filter

Filter resources per project, customer or for reporting purposes

Unambiguous

Create a list for tags used that includes:

Description, tag name, and potential values

Pay-as-you-Go

One of the most expensive options

Reserved Instances

Can save a lot

Reserve VM for a period

discount

Not all Azure services can be reserved

Advisor

Gives best practices and advice in general through recommendations

### Summary

Subscriptions

Every resource belongs to a subscription

Azure Account can have multiple subscriptions

Billing Admins control Costs

Management groups help keep track of many subscriptions

Cost Management

Use free accounts and Azure Cost Management to keep costs as low as possible and optimize resources

Pricing Factors

Resource size, resource type, location of the service and bandwidth used all affect the price of a service

Best Practices

Use spending limits, quotas for services, tags to order resources and reserved instances to manage costs and get the best price

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Pricing Quiz: 80%

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2014.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2014.png)

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Pricing Quiz: 100%

## Support

[Azure support options - Get help with your Azure subscription - Learn](https://docs.microsoft.com/learn/modules/create-an-azure-account/5-support-options?WT.mc_id=ACloudGuru_Learn_multiple-learn-wwl)

### Plans

Overview

5 different Levels: (Cost and Support increases as list goes)

Basic

Developer

Business Hour email support

Unlimited technical support cases

Guidance Troubleshooting

Response time < 8 hours

General Guidance for support

Standard

24/7 Email/Phone support

Unlimited technical support cases

Guidance Troubleshooting

Response time c < 8 hours

Response time b < 4 hours

Response time a < 1 hours

General Guidance for support

Professional Direct

24/7 Email/Phone support

Unlimited technical support cases

Guidance Troubleshooting

Response time c < 4 hours

Response time b < 2 hours

Response time a < 1 hours

Architecture Guidance for support

On boarding reviews

Webinar Training

Premier

24/7 Email/Phone support

Unlimited technical support cases

Guidance Troubleshooting

Response time c < 4 hours

Response time b < 2 hours

Response time a < 1 hours

Initial response time for premier package is < 15 minutes - Azure rapid response

Customer specific Guidance for support

Tech reviews, reporting, and a technical account manager

On-demand training

Inclusions - All Support Plans

24/7 Access

Around the clock access to billing and subscription support

Online Self-Help

Azure documentation and white papers

Forums

Connect with other Azure users to ask and answer questions

Azure Advisor

Best practice recommendations for multiple Azure services

Service Health

Access to current issues and future planned maintenance on the Azure platform

### Tickets

Definition

Ticket is a support enquiry

Unique ID

Single reference to request

Submit a ticket through the Azure Portal

Choose one of four support ticket types

Fill in details about issue

Request is processed according to support plan

### Channels

Support Channels

Azure Documentation

Collection of 1000+ product and service articles

Forums

Suits everyone from beginners to experts

Social Media

### Knowledge Center

FAQ for common questions

No New Questions

Cannot add new questions or add to an existing question

Search

Search by category, product, and free text

Complements other channels

### Service Level Agreements

Properties

Confidence

Critical top ensure confidence in the uptime and reliability of services

Contract

Contract between user and Azure stating MS's commitment for uptime and connectivity

Multiple SLAs

Many SLAs in Azure

Generally one SLA per product

Automatically use the SLA for the service one uses

Complex

SLAs can have various levels depending on the number and variety of services, which region is used, and much more

Mandatory

If one has an Azure account, the various SLAs apply.

There are no SLAs for free products and services

### Service Lifecycle

Gathering Custom Data

Customers can provide valuable feedback

Stages

Preview

Private

Only available to specific customers invited by he product team behind the service

Public

Available to all Azure customers

Enable preview features in the Azure Portal

General Availability

Available to all Azure customers as a normal service, including SLA

Services become generally available when they are ready

Can be gradual rollout to some regions first

Watch for previews, new features, and updates with the update feed by Azure

### Summary

Support

Plans

Basic, developer, standard, professional direct, and premier tiers

More pay more benefits and faster response

Tickets

Unique reference ID for support issue

Channels

Azure documentation, forums, and social media for help and support

Knowledge Center

Collection of most common questions

SLA

Contract between user and Azure documenting Microsoft's commitment for uptime and connectivity

Service Lifecycle

Azure services can be in private or public preview before they are generally available

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Support Quiz: 60%

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2015.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2015.png)

![AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2016.png](AZ-900%20Microsoft%20Azure%20Fundamentals%2010a7b9c852fa4f67965576b3c7def3ca/Untitled%2016.png)

AZ-900 Microsoft Azure Fundamentals 2020 - Azure Support Quiz: 100S%
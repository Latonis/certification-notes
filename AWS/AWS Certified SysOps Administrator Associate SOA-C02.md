# Cloud Guru
(https://learn.acloud.guru/course/aws-certified-sysops-admin-associate/dashboard)
=======
# Deployment, Provisioning, and Automation
## Bootstrap Script
```bash
#!/bin/bash  
yum update -y
yum install httpd -y
echo "<html><body><h1>Hello People of the Cloud!</h1></body></html>" >/var/www/html/index.html
systemctl start httpd
systemctl enable httpd
```
### Exam Tips
EC2 is like a VM, hosted in AWS instead of our own data center.
## Understanding EBS Volumes
### What is EBS?
Elastic Block Store
- Storage volumes that you can attach to your EC2 instances
- Use them the same way you would use any system disk
	- Create a file system
	- Run a database
	- Run an operating system
	- Store data
	- Install applications
### EBS Features
#### Mission Critical
1. Production workloads
	1. Designed for mission critical workloads
2. Highly Available
	1. Automatically replicated within a single availability zone to protect against hardware failures
3. Scalable
	1. Dynamically increase capacity and change the type volume with no downtime or performance impact to your live systems
### EBS Volume Types
#### General Purpose SSD (gp2)
- 3 IOPS per GiB, up to a maximum of 16,000 IOPS per volume
- gp2 volumes smaller than 1 TB can burst up to 3,000 IOPS
- Good for boot volumes or development and test applications that are not latency sensitive
#### Proivisoned IOPS SDD (io1)
- High performance, most expensive
- Up to 64,000 IOPs per volume
	- 50 IOPS per GiB
- Use if you need more than 16,000 IOPS
- Designed for I/O intensive appliactions, large databases, and altency-sensitive workloads
#### Provisioned IOPS SSD (io2)
- Latest generation
- Higher durability and more IOPS
- io2 is the same price as io1
- 500 IOPS per GiB
- Up to 64,000 IOPS
- 99.999% durability instead of up to 99.9%
- I/O intensive apps, large databases, and latency-sensitive workloads
- Applications that need high levels of durability
#### Throughput Optimized HDD (st1)
- Low-cost HDD volume
- Baseline throughput of 40 MB/s per TB
- Ability to burst up to 250 MB/s per TB
- Maximum throughput of 500 MB/s per volume
- Frequently accessed, throughput-intensive workloads
#### Cold HDD (SC1)
- Lowest cost option
- Baseline throguhput of 12 MB/s per TB
- Ability to burst up to 80 MB/s per TB
- Max throughput of 250 MB/s per volume
- A good choice for colder data requiring fewer scans per day
- Good for applications that need the lowest cost and performance is not a factor
- cannot be a boot volume
### Exam Tips
- EBS
	- Highly available and scalable storage volumes you can attach to an EC2 instance
	![[Pasted image 20211129195859.png]]
	![[Pasted image 20211129195935.png]]

## Bastion Hosts 
A public facing instance which enables you to SSH or RDP to your private instances from an untrusted network
- A bastion host has a public IP address and is connected to the internet/untrusted networks
- It is security hardened with any unnecessary services removed to reduce the attack surface.
![[Pasted image 20211129200215.png]]
### Exam Tips
1. Connect to Private instances
	1. A bastion host enables you to connect to private instances in your VPC from an untrusted network using SSH or RDP
2. Public Subnet
	1. A bastion is in a public subnet and is reachable from the internet
3. Security Groups
	1. You need to configure the security group associated with the private subnet to enable SSH/RDP access from the bastion.

## Elastic Load Balancer
A load balancer distributes network traffic across a group of servers.
- increase capacity when needed
### Application Load Balancer
- Used for balancing HTTP and HTTPs
- Operate at Layer 7 of the OSI model
	- ![[Pasted image 20211129200759.png]]
- They are application aware
	- Supports advanced request routing based on the HTTP Header
### Network Load Balancer
- TCP and high performance
- Used for load balancing TCP traffic when extreme performance is required
- Operates at Layer 4 of the OSI Model
- Capable of handling millions of requests per second, while maintaining ultra-low latencies
- As it is high performance, it is also the most expensive option.
### Classic Load Balancer (Legacy)
- HTTP/HTTPS and TCP
- Supports some Layer-7 Specific features
	- `X-Forwarded-For` headers
		- Idenity the originating IP address of a client connecting through a load balancer.
	- Sticky sessions
### Gateway Load Balancer
- Allows you to load balance workloads for third-party virtual applicances running in AWS, such as:
	- Virtual applicances purchased using the AWS marketplace
	- Virtual firewalls from companies like Fortinet, Palo Alto, Juniper, and Cisco
	- IDP/IPS systems from companies like CheckPoint, Trend Micro, etc.

### Exam Tips
![[Pasted image 20211129201232.png]]

## Elastic Load Balancer Error Messages


=======
# EC2
## EC2 Changing Instance Type
1. Must stop instance
2. Instance Settings
3. Change Instance Type
	1. EBS optimized instance is a choice, based on newer type of EC2 Instances
4. Instance is then restarted on new host

## Enchanced Networking
- EC2 Enhanced Networking (SR-IOV)
	- Higher bandwidth, higher PPS (packets per second), lower latency
		- Option 1: Elastic Network Adapter (ENA) up to 100 Gbps
		- Option 2: Intel 82599 VF up to 10 Gbps - LEGACY
		- Works for newer generation EC2 Instances
- Elastic Fabric Adapter (EFA)
	- Improved ENA for HPC, only works for Linux
	- Great for inter-node communications, tightly coupled workloads
	- Leverages Message Passing Interface (MPI) standard
	- Bypasses the underluing Linux OS to provide low-latency, reliable support
	- To get Driver info for network adapter
	```bash
	ethtool -i eth0
	```
## EC2 Placement Groups
- Sometimes you want control over the EC2 Instance placement strategy
- That strategy can be defined using placement groups
- When you create a placement group, you specify one of the following strategies for the group:
	- *Cluster*	
		![[Pasted image 20211025185652.png]]
		- Cluster instances into a low latency group in a single AZ
		- Pros: Great network (10 Gbps bandwidth between instances)
		- Cons: if the track fails, all instances fail at the same time
		- Use Case:
			- Big Data Job that needs to complete quickly
			- Application that needs extremely low latency and high network throughput
	- *Spread*
		 ![[Pasted image 20211025202414.png]]
		- Spreads instances across underlying hardware (max 7 instances per group per AZ)
		- Useful for critical applications (IE production)
		- Pros:
			- Can span across AZs
			- Reduced risk of simulatenous failure
			- EC2 instances are on different physical hardware
		- Cons:
			- Limited to 7 instances per AZ per placement group
		- Use Case:
			- Application that needs to maximize high availability
			- Critical Applications where each instance must be isolated from failure from each other
	- *Partition*
		 ![[Pasted image 20211025202549.png]]
		- Spreads instances across many different partitions (whcih rely on different sets of racks) within an AZ.
		- Scales to 100s of EC2 instances per group (Hadoop, Cassandra, Kafka)
		- Pros:
			- Up to 7 partitions per AZ
			- Can span across multiple AZs in the same region
			- Up to 100s of EC2 instances
			- The instances in a partition do not share racks with the instances in other partitions
			- A partition failure can effect many EC2 but won't affect other partitions
			- EC2 instances get access to the partition information from metadata
		- Use Case:
			- HDFS
			- HBase
			- Cassandra
			- Kafka
	## Shutdown Behavior
	- How should the instance react when shutdown is done using the OS?
		![[Pasted image 20211025202859.png]]
		- Stop (default)
		- Terminate
	- This is not applicable when shutting down from AWS console
	- CLI Attribute: `InstanceInitiatedShutdownBehavior`
	### Termination Protection
	- Enable termination protection:
		- To protect against accidental termination in AWS Console or CLI
	- **Exam Tip**:
		- We have an instance where shutdown behavior = terminate, and we enable terminate protection.
		- We then shutdown the instance from the OS, what will happen?
		- **Answer**:
			- Instance still be terminated, as it was from within the OS, not the CLI or console.
## EC2 Launch Troubleshooting
- `InstanceLimitExceeded`:
	- You have reached your limit of max number of vCPUs per region
	- On-demand instance limits are set on a per-region basis
	- Example:
		- If you run on-demand instance types, you will have 64 vCPUs by default
	- Resolution:
		- Either launch the instance in a different region or request AWS to increase your limit of the region.
	- Note:
		- vCPU based limits only apply to running On-Demand instances and Spot instances.
	- `InsufficientInstanceCapacity`:
		- AWS does not have enough On-Demand capacity in that particular AZ where the instance is launched.
		- Resolution:
			- Wait for a few minutes before requesting again.
			- If requesting more than 1 requests, break down the requests.
				- If you need 5 instances, rather than a single request of 5, request 1 by 1.
				- If urgent, submit a request for a different instance type now, which can be resized later.
				- Also, can request the EC2 instance in a different AZ.

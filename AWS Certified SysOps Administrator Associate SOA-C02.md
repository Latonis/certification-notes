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


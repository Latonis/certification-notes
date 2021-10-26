# AWS Databases
## Purpose-Built Databases
### Database Types
- Relational
	- Best with structured data
	- Atomic operations
	- Bad for semi-structured or sparse data
- Key-Value
	- Extremely Scalable
	- High throughput
	- Low latency
	- Flexible Schema
	- Should know access pattern
	- Not great for analytics
- Document
	- JSON-like documents
	- flexible schema
	- Aggregate across documents
	- High relational data shouldn't be stored here
- In-Memory
	- Microsend latency
	- Increidbly fast compared to disk
	- not great in environments where data needs persisted to disk
- Graph
	- Easily relate sets of data
	- Flexinle schema
	- Not great for high volume of transactions
- Time Series
	- Great for monitoring
	- Aggregate across documents
	- Great for time-ordered data
	- not great for data that is not time ordered
- Ledger
	- Immutable and transparent
	- highly scalable
	- not great for decentralized architectures
### OLTP and OLAP
#### OLTP ==Transactional==
- online transaction processing
- maintains record integrity in multi-access environments
- fast queries, higher volume
#### OLAP ==Analytical==
- Online analytical processing
- Complex queries that aggregate data
- Queries are generalyl slower
### What Does Relational Even Mean?
![[Pasted image 20211003181633.png]]
### What about Key-Value?
![[Pasted image 20211003181727.png]]
## Understanding RTO and RPO
![[Pasted image 20211003181921.png]]
### Recovery Point Objective
The maximum amount of time or data we can lose without impacting business operations
### Recovery Time Objective
The maximum amount of time the recovery process can take -- or, "How long can we be down for?"
### Considerations
#### Monitoring
How will we monitor our resources for failures, problems, or outages?
#### Backups
What abckup technologies can we leverage that meet our RPO and RTO needs?
#### Resiliency
How many regions or AZs will we leverage?
#### Availability
Measure of the percentage of time a workload is available for use.
![[Pasted image 20211003182207.png]]

### Reliability Design Principles
- Automatically Recover
	- Establish and leverage automated recovery processes when possible
- Scale Horizontally
	- Try to use fewer large monolithic designs, and instead use multiple smaller resources to reduce impact of failure events
- Identify Capacity Requirements
	- Monitor workload utilization to identify capacity requirements. Leverage automation to meet workload requirements
- Perform Changes through Automation
	- If possible, make changes to your infrastructure using automation, which also helps with change management and versioning.
### Test recovery procedures
Seriously, test your entire disaster recovery plan. Verify your RTO and RPO. Understand **how** your workload fails. Test Automation. Simulate failures.
## AWS Database Services Overview
### Shared Responsibility
![[Pasted image 20211003182602.png]]
### Relational Database Service (RDS)
#### Engine Support
- Oracle
- PostgreSQL
- SQL Server
- MariaDB
- MySQL
#### Notable Features
1. Supports Read Replicas
	- Easily offload read requests to read-only instances. 
	- Leverage replicas for DR.
2. Automated Backups
	- Using point-in-time restore (PITR), we can roll back to previous database states within our configured backup retention period. 
3. Scalable Storage and Compute
	- Easily modify database instances to scale the underlying EBS storage or instance type/size.
4. Multi-AZ
	- Create standby Multi-AZ instances that can be leveraged as a failover target in the event of an outage or planned maintenance.
	- Huge impact on availability and RPO/RTO.
### Aurora
#### Available Engines
- MySQL
- PostgreSQL
#### Notable Features
1. Scalable Reads
	1. Supports up to 15 read replicas to help offload read requests from primary instance, in addition to the ability to adjsut instance type/size of instances.
2. Automated Backups
	1. Using point-in-time restore (PITR), we can roll back to previous database states within our configured backup retention period. 
3. Auto Scaling Cluster Volume
	1. Leverages an Auto Scaling cluster volume, which scales in 10 GB increments
4. Supports Multi-Master
	1. Multi-master is a feature with a single primary write region and up to five read replica regions, where changes are propagated automatically.
### Redshift
#### Notable Features
Excels at OLAP.
1. Used as a data warehouse
	1. Designed for online analytical processing or business intelligence applications.
	2. Does well with complex queries on a large amount of data
2. Supports Clustering
	1. Clusters composed of scalable leader and compute nodes
3. Columnar Type
	1. In contrast to our row-based databases, Redshift stores data in columns, storing data as a single column for multiple rows on each block of data.
### Common Use Cases
- RDS
	- Web and mobile apps
	- Mobile or online games
	- E-commerce
- Aurora
	- Web and mobile apps
	- Mobile or online games
	- E-commerce
	- SaaS appliactions
- Redshift
	- Business intelligence
	- User engagement analysis
	- Analytical workloads
### DynamoDB
1. Key-Value and Document Database
	1. DynamoDB is a fully managed, highly scalable NoSQL Database
2. Common Uses
	1. Servless Web applications
	2. Microservices
	3. advertising
	4. gaming
	5. banking
3. Real-Time Data Processing
	1. Using DynamoDB streams, customers can track changes to items in a table, and then take action based on those changes.
#### Notable Features
1. Scalable Read/Writes
	1. Use Auto Scaling (the default capacity setting) or configure provisioned capacity.
	2. Underlying hardware is fully managed.
2. DAX
	1. Supports a fully managed in-memory cache through a feature called Amazon DynamoDB Accelerator (DAX)
3. Multi-Region Multi-Master
	1. Fully managed serverless architecture with multi-region and multi-master support using the global tables feature.
### Neptune
1. Graph Database
	1. Neptune is a graph database with support for Gremlin and SPARQL
2. Common Uses
	1. Fraud detection applications
	2. Social networking
	3. Knowledge graphs
	4. Network security
	5. Best for highly connected datasets
### DocumentDB
1. MongoDB Compatible
	1. Uses the open-source MongoDB 3.6 API.
	2. Customers can use their existing MongoDB drivers/tools.
2. Query JSON
	1. DocumentDB is a type of NoSQL database that allows customers to query or store data as JSON documents.
3. Use Cases
	1. Blogs/video platforms, cataloging
	2. Popular migration target for MongoDB users.
### Exam Tips
1. Understand Database Types
	1. Learn the use cases
	2. Cover the database types and how they're used.
# Relational Database Service
## Overview of Amazon RDS
### RDS Features
1. Multi-AZ
	1. standy database instance in another AZ
2. Read Replicas
	1. Scalable reads and can be leveraged as part of a disaster recovery plan
3. Automatic Backups
	1. Backups taken on a configurable schedule, with a configurable retention period
4. Configurable Storage
	1. Support for General Purpose, Provisioned IOPS, or even magnetic
5. IAM Authentication
	1. useful for temporary access
6. CloudWatch logs
	1. Ability to export metrics, including enhanced monitoring metrics, to CloudWatch Logs
## Understanding Read Replicas
![[Pasted image 20211004165059.png]]
- ==SQL Server doesn't currently support cross-region read replicas, all others do.==
- You cannot read-replica chain.
- Use for Disaster Recovery
- Migration
- Possible issue:
	- Monitor for replication lag
- Write requests might block read requests on primary regions
## Understanding Multi-AZ
![[Pasted image 20211004170041.png]]
**Failover Downtime**
- Single-AZ Setups: 3-5 Minutes
- Multi-AZ setups: ~60 seconds
- Downtime will vary, this does not account for transaction rollbacks
### Failover Conditions
1. Storage Failure
2. Network Interruptions
3. Loss of Availability
### Exam Tip
- When first enabled, Multi-AZ can result in a performance impact while the snapshot process completes in write-heavy environments. Think about hwo this can impact your considerations for your process to enable multi-az.
## Using Backup and Restore
### Things to know:
- Enabled by default
- Occur in a configurable 30 minute *backup window*
- Configurable backup retention period, up to 35 days
	- Default is 7 days
### Automated Backups
Automated backups take a storage volume snapshot and store it in S3 for the duration of our backup retention period.
![[Pasted image 20211004170844.png]]
### Manual Snapshots
1. Stored in S3
	1. Manual snapshots are stored in S3 until they are deleted
2. Storage Impact
	1. starting a snapshot on a single-az instance may result in I/O latencies
3. Restore times vary
	1. Snapshot is entire storage volume, including temp files. 
	2. More data = more time.
### Things to Know
#### Automated Backup
1. Autoamted backups as well as manual snapshots may result in brief storage I/O suspension in single-AZ setups
2. Automated backups do not include information about parameter or option groups, but can be specified during instance creation
3. When you delete an instance, by default, automatic backups are deleted, but they can be retained
4. To be shared, one must copy the automated snapshot to a new snapshot, then share it.
#### Manual Snapshot
1. Allows users to restore to a different storage type
2. Ability to specify desired parameter group during restore
3. Option group that is associated with the snapshot will be associated with the restored instance.
4. Manual snapshot can be shared as-is.
	1. Can't share snapshots with other accounts if encrypted with default-key
	2. KMS keys are region specific
	3. Must use custom KMS key and share that too.

![[Pasted image 20211004171323.png]]
### Point in Time Restore
- PITR provides the ability to restore to any specific time within our configured backup retention period.
- LRT (latest restorable time) is generally within ~5 minutes of your current time
	- Transaction logs are sent to s3 every 5 minutes.
	- ![[Pasted image 20211004171425.png]]
### Backups and Multi-AZ Impact
- For MySQL< MariaDB, Oracle, and Postgres configured for multi-AZ, automatic backups are taken from the standby instance.
- In contrast, SQL server may experience elevated I/O latencies.
### Copying Snapshots
- Shared snapshots across regions
- Copies are considered maual snapshots
1. Don't delete source
	1. If a copy snapshot operation begins, do not remoev the source snapshot before the copy operation completes.
2. Cross-Region copy limitations
	1. Snapshots cannot be copies to China (Beijing or Ningxia)
3. Encryption and Snapshots
	1. Can Copy KMS encrypted snapshots, but require access to the KMS key
	2. Copy of an encrypted snapshot must ALSO be encrypted.
## Monitoring in RDS
### Monitor All the THings
#### Events and Event Notifications
Events provide visibility into RDS activity, such as failovers, config changes, or maintenance. 
- Integrated with SNS to provide event notifications
![[Pasted image 20211004172105.png]]

#### Enhanced Monitoring
Access to real-time metrics from the underlying OS, access to Free Memory metrics.
- Adjustable granularity down to one-second monitoring interval.
![[Pasted image 20211004172214.png]]

#### Performance Insights
Provides insight into database load, wait events, top SQL, top hosts, and even top user.

**3 Important Dashboard Components**
1. Counter Metrics
	1. Used to monitor specific performance metrics; default metric displayed varies per engine
2. DB Load
	1. Compares database load to DB instance capacity.
	2. Generally want DB load to be less than Max vCPU.
3. Top Items
	1. Top waits, SQL, hosts, and users.
	2. If we slice DB Load Chart by waits, we can assess which queries result in the most waits and break down to which wait state the query is contributing.
### CloudWatch
**Powerful Monitoring and Alerting**
- Provides support for alarms, integration with CloudWatch Logs, and support for custom metrics
	- CloudWatch Events is being replaced by Event Bridge
	- Gives us the ability to take actions based on certain events, such as calling a Lambda function or sending an email notification
### Instance Statuses
1. *Failed*, *restore-error*, and *incompatible* type statuses can result in severe outages.
	1. Some statuses, such as *incompatible* statuses, are still billed.
	2. In contras t, a status like *failed* is not billed.
	3. ![[Pasted image 20211004172842.png]]
## Working with RDS Logs
![[Pasted image 20211004194344.png]]
MySQL
- Error
- General_log
- Slow_query
- Audit
MariaDB
- Error
- General_log
- Slow_query
- Audit
PosgreSQL
- PostgreSQL log file
Oracle
- Audit
- Alert
- Trace
- Listener
SQL Server
- Error
- Trace
- Agent
- Dump
All exportable to CloudWatch logs
### Additional Notes
#### MySQL and MariaDB
- Supports binary log (binlog)
	- Configurable retention using **rds_set_configuration** stored procedure
- Allows for Configurable **log_output**
	- FILE: general_log and slow_query_log are written to the file system; rotated hourly
	- TABLE: general_log written to general_Log table; slow_query_log written to slow_log table

#### PostgreSQL
- log_statement and log_min_duration
	- Used to log user activity, such as query events
	- log_statement defines which SQL statements are logged
	- log_min_duration defines the threshold for when a query is logged
- Configurable Log Retention
	- The log_retention_period parameter can be configured to retain logs for up to seven days
	- Measured in minutes

#### Oracle
- Supplemental Logging and Online Log Files
	- Can enable supplemental logging, *rdsadmin_util.alter_supplemental_logging*
	- Switch log files by using *rdsadmin_util.switch_logfile*
- Force Logging
	- Used to log all changes except those in temporary tablespaces
	- Enabled by stored procedure
#### SQL Server
- Error and Agent Logs
	- Accessed through console, CLI/API, or a stored procedure: *rds_read_error_log*
- Retention
	- Most logs are retained for seven days

### CloudWatch Logs Integration
![[Pasted image 20211004195453.png]]
- What does it provide?
	- Ability to store logs in a durable location
	- filter logs using filter expressions
	- create custom metrics and alarms
	- Ship log data to S3 for additional analysis
	- Supports Enhanced Monitoring logs
## Security in RDS
### Managing Access
#### Using Roles
- Roles can be used as a form of temporary IAM user permissions
	- AssumeRole
	- GetFederationToken
- Useful for providing cross-account access
- Can also be assumed and used by an application running in EC2
- ==User assuming cross-account role must be identified as a principal in the role's trust policy==
- ![[Pasted image 20211004200026.png]]
#### Service-Linked Roles
- RDS uses a service-linked role named AWSServiceRoleforRDS
	- Allows RDS to call other AWS Services
	- ==if you receive an error stating you cannot create the service-linked role, ensure the entity has the iam:CreateServiceLinkedRole permission== 
#### AWS Managed Policies
- AmazonRDSReadOnlyAccess
	- Read-only access to resources in the specified account
- AmazonRDSFullAccess
	- Full access to resources in the specified account
#### External Authentication
- Support for Kerberos and Microsoft Active Directory
- Supported for MySQL, SQL Server, Oracle, and PostgreSQL
- Users can use credentials from AWS Directory Service for Microsoft AD, or your on-prem AD
#### IAM Authentication
- Supported by RDS MySQL and RDS PostgreSQL
- Can be enabled during creation or through instance modification process (modify-db-instance)
- MySQL limited to 200 connections/second
- PostgreSQL requires SSL parameter set to 1
- Uses a generated authentication token
	- aws rds generate-db-auth-token
![[Pasted image 20211004200524.png]]

![[Pasted image 20211004200549.png]]
### Key Management Service
1. Enable at Creation
	1. You cannot enable or disable encryption for a preexisting database instance.
	2. You must enable encryption at time of creation
2. Encryption and Read Replicas
	1. Cannot have an encrypted read replica from an unencrypted source.
	2. Cannot have an unencrypted read replica from an encrypted source.
3. Copied Snapshots
	1. Copied snapshots of an encrypted DB instance will also be encrypted. 
	2. In same region, we can modify the encryption key (KMS key)
4. Cross-Region snapshot Copies
	1. KMS keys are region specific, meaning cross-region copies will require a valid KMS key in the target region to use for encryption
### RDS SSL/TLS Support
#### Things to know
- RDS CA-2019 is automatically enabled for new database instances
	- RDS CA-2015 bundle was just deprecated
	- RDS CA-2019 is the current bundle.
	- RDS CA-2019 contains old and new bundle.
- ==Setting rds.force_ssl to 1 requires SSL for all users==
	- if not using SSL to connect but it is required, this is the error:
	![[Pasted image 20211004201407.png]]
## Working with RDS in a VPC
### Subnet Groups
- Used to specify your VPC when creating via the CLI/API. Console lets you choose your VPC/subnet group.
- Subnet group must contain at least two different availability zones.
- Can contain either only public or private subnets, not a mix of both.
- Can change the VPC of a databa instance by modifying the subnet group.
## Managing RDS Resources
### Modifying Storage
- Storage-optimization
	- When the operation ebgins, the DB instance is placed in a storage-optimization status
	- After modification completes, no additional storage modifications for six hours
	- Increases to storage capacity must be a minimum of 10%
	- You can't reduce the amount of storage using this process.
	- ==This is considered an allocated storage change and doesn't result in an outage--thought it might result in a performance impact==
![[Pasted image 20211004202904.png]]

### Storage Modification Risks
- Storage Type Changes that cause an outage
	- General purpose (GP2) to Magnetic
	- Magnetic to General purpose (GP2)
	- Magnetic to Provisioned IOPS (IO1)
	- Provisioned IOPS (IO1) to magnetic
	- ==Provisioned IOPS (IO1) to General Purpose (GP2) and General Purpose (GP2) to Provisioned IOPS (IO1)==
		- Can result in an outage if DB Instance is Single-AZ and using a custom parameter group.
		- No outage for Multi-AZ.
### Instance Modifications
Single AZ:
![[Pasted image 20211004203310.png]]
Multi-AZ:
- With Multi-AZ enabled, the instance change is performed on the Multi-AZ standby instance first, drastically reducing downtime.
- After the modification to the standby group has completed, RDS performs a brief failover to promote the standby, then performs the change on the old primary.
- During the modification process, the RDS instance will show a status of Modifying
- Other statuses include backing-up, incompatible-parameters, maintenance, rebooting, and more.
- When the change is applied, whether or not there is an outage, and how Apply Immediately works will vary per setting.
### Parameter Groups
- Controls engine configuration values, such as read_only for MySQL or autovaccum_max_workers for PostgreSQL
- Static and dynamic parameters
	- Static Requires reboot
	- Dyanmic takes effect immediately
- Cannot modify default parameter group; must create custom parameter group and associate it with the instance
### Option Groups 
- Used to enable additional features, such as MARIADB_AUDIT_PLUGIN for MySQL or Oracle TDE
- Persistent and permanent options
- Links to VPC (or EC2 classic non-vpc) rather than the DB instance. Cannot be migrated between VPCs.
## Understanding RDS Maintenance
### Maintenance Status
#### Required
- Maintenance that must be applied; cannot defer required maintenance indefinitely
- With a status of REQUIRED, we should receive an email notification regarding the maintenance tasks (such as hardware maintenance)
- Multi-AZ reduces downtime to the duration of a Multi-AZ failover, generally less than a minute

#### Available
- There is a maintenance action available, but not being applied automatically
- We have the ability to manually apply this maintenance
- To apply available maintenance, we can adjust our preferred maintenance window to the current time and then apply the maintenance
#### Next Window
- An indication that upcoming maintenance will take place in the next window
#### In Progress
- Maintenance tasks are already being applied to that resource.
### Maintenance Windows
- 30 minute window in an 8 hour time block, variees per region.
- If left unspecified during creation, 30-minute window is selected at random
- Maintenance tasks can take longer than the 30-minute window
- Maintenance tasks will run until complete; no hard cutoff
- Can define preferred maintenance window from console, CLI, or API.![[Pasted image 20211004205207.png]]
### Types of Maintenance

#### Minimize Downtime

##### Hardware Maintenance
- Can't be deferred.
- Should receive email notifiaction from RDS
- Multi-AZ minimizes downtime

##### OS Maintenance
- can be degerred by using "defer upgrade"
- Applied to MAZ Secondary first.
- Multi-AZ minimizes downtime

##### DB Engine Maintenance
- Engine upgrades require downtime -- both instances undergo the change.
- Outage, regardless of multi-AZ

###  Engine Upgrades
#### Minor Version
- Can be done automatically, if automatic version upgrades are enabled.
- Minor version upgrades are backward-compatible
#### Major Version
- Manual upgrade process; not backward compatible
- Applied through instance modification process
## Troubleshooting RDS
### High-Level Troubleshooting Flow
#### The Issue
- This is where i'll highlight the issue we're trying to solve, such as replication or connection errors. It may provide the actual error as the issue.
#### The Symptom
- This section will provide some insight into what the syptoms of this issue would be.
- For replication errors, it could as simple as "a report fo stale data from one of our read replicas"
#### The Fix
- This is where we discuss the fix for the issue or error we're trying to solve, such as replication lag or connection errors.
### Parameter Changes Not Taking Effect
- After making several parameter value changes, the value are not being reflected in engine.
- After modifying the parameter group to a custom parameter group, the default parameter group is still assigned
Fix:
- Verify status of instance is pending-reboot.
- Perform a reboot on the resource (RebootDBInstance) from the CLI
- Verify parameter changes have taken effect, as in-sync
### Storage-full
Instance in Storage-full state
Fix:
- Perform a database instance modification (ModifyDBInstance) to increase storage allocation
- Configure CloudWatch Alarms to monitor FreeStorage metric
- Identify the cause (large data load, excessive logging or log retention related to replication)
### Replication is stopped
Receiving stale data
Fix (SQL):
- If the error doesn't impact data integrity: CALL mysql.rds_skip_repl_error;
- Ensure read_only oarameter is set to 1 on the read replica
- Avoid attempting to replicate MyISAM tables; ==replication only supports InnoDB Storage engine==
- If lag is significant, create a new read replica from the source
- Ensure source instance retains binary logs long enough for replicas to process changes
Fix (Postgres):
- Ensure wal_keep_segments paraeter is large enough to retain WAL files for all read replicas
- If leveraging multiple replicas, consider increasing max_wal_senders value TransactionLogsDiskUsage, Oldest Replication Slot Lag
### Insufficient Capacity Errors
- When attempting to modify or launch an instance, our dev team was returned an InsufficientDBInstanceCapacity error
- Unable to create new db at desired size
- Unable to perform instance modifications to desired size
Fix:
- select a different DB instance class
- Attempt to create the resource in another AZ (or don't identify one)
- Try the same request again at another time as a last resort
### Too Many Connections
Fix:
![[Pasted image 20211004211028.png]]
- Increase the max_connections parameter value - be cognizant of free memory
- Modify instance to alrger size.
- Implement connection pooling for your appliaction
- ==SQL Server configures max connections in server properties within SQL Server Management Studio (SMSS)==
## Pricing Models in RDS
### RDS Pricing
Cost is always an important topic
RDS pricing is broken down into several categories:
- Database Instance Pricing
- Database Instance Storage
- I/O (magnetic only)
- Backup Storage
- Data Transfer
### Pricing Models in RDS
- Instance Type and Size
	- Costs associated with the database instance type and size.
- On-Demand pricing
	- Supports on-demand purchasing options, where we pay per hour, calculated down to the second.
	- Great for when your database may only run intermittently.
	-Good fit for unpredictable workloads because we're not locked in.
- Reserved Instance Pricing
	- Supports Reserved Instances, providing much cheaper instance pricing than On-Demand.
	- Good fit for workloads where we known the amount of resource consumption
	- Supports one-to-three year terms
### Storage Pricing
- General Purpose
	- Bill based on capacity of the storage volume.
	- Can sustain 3k IOPS burst for 30 minutes.
- Provisioned IOPS
	- Billed for the capacity of the storage volume as well as the amount of IOPS allocated.
	- IOPS are billed per IOPS-month.
- Magnetic
	- Slow, deprecated, cheap.
	- Unavailable via the console; only available via CLI/API.
![[Pasted image 20211004211707.png]]
### Backup Storage
Billed based on automated database backups and any active database snapshots
- Backup storage is billed on a per GB-month basis.
- Increasing retention or taking additional snapshots increases this storage costs.
### Data Transfer Outbound
![[Pasted image 20211004211856.png]]
- Data Transfer costs are tiered based on the amount of data transfer
- Database snapshot copy accrues data transfer fees when copying between regions.
- Traffic in the same AZ is free.
- Traffic between RDS and RC2 in different AZ accrues EC2 regional data transfer fees.
- Traffic replicated across AZs for Multi-AZ is free.
###  Licensing
![[Pasted image 20211004212118.png]]
![[Pasted image 20211004212125.png]]
### Instance Scheduler
- If the resource ins't in use 24/7, consider stopping the resource to save money!
- CloudFormation for Instance Scheduler that can start and stop RDS resources as a cost-saving measure.
# Amazon DynamoDB
## DynamoDB Architecture
### Partitions and Data Distribution
DynamoDB stores data in partitions. A partition is an allocation of storage for a table, backed by SSDs and automatically replicated across multiple AZs within an AWS region.
To get the most out of DynamoDB throughput, create tables where the partition key has a large number of distinct values. Applications should request values fairly uniformly and randomly as possible.
![[Pasted image 20211006162024.png]]
### Architecture Terms:
- Table: collection of data.
	- DynamoDB tables must contain a name, primary key, and the requiread read and write throughput values.
	- Unlimited size.
- Partition key: a simple primary key, composed of one atrribute known as the partition key.
	- Also called the hash attribute.
- Partition and sort key: Also known as the composite primary key, this type of key comprises two attributes:
	- The first attribute is the partition key
	- second attribute is the sort key
		- This is also called the range attribute.

![[Pasted image 20211006162356.png]]

### DynamoDB Performance
- Ondemand Capacity
	- Database scales according to demand
	- Good option for:
		- New tables with unknown workloads
		- Applications with unpredictable traffic
		- Prefer to pay as you go
- Provisioned Capacity
	- Allows us to have consistent and predictable performance
	- Specify expected read and write throughput requirements
	- Read capacity units (RCUs)
	- Write capacity units (WCUs)
	- Price is determined by provisioned capacity
	- Cheaper per reuest than On-demand mode
	- Good option for:
		- Applications with predictable traffic
		- Applications whose traffic is consistent or ramps gradually
		- Capacity requirements can be forecasted, helping to control cost.

Both capacity modes have a limit of 40,000 RCUs and 40,000 WCUs.
You can switch between modes only once per 24 hours.
Table addressing is via **ARN**.
![[Pasted image 20211006162656.png]]
## DynamoDB Items
### DynamoDB Item Terms
![[Pasted image 20211006162835.png]]
- Item
	- A table may contain multiple items. An item is a unique group of attributes.
	- Items are similar to rows or records in a traditional relational database.
	- Items are limited to 400 KB.
- Attribute
	- Fundamental data element
	- Similar to fields or columns in an RDBMS.
### Data and Document Types
- Scalar
	- Exactly one value: number, string, binary, boolean, and null/
	- Applications must encode binary values in B64 format before sending them to DynamoDB.
- Document
	- Complex structure with nested attributes (e.g., JSON) - list and map.
- Document Types
	- List
		- Ordered collection of values
			- `FavoriteThings: ['Coffee', 12, 'Cookies']`
	- Map
		- Unordered collection of name-value pairs (siimilar to JSON)
		- ![[Pasted image 20211006163159.png]]
	- Set
		- Multiple scalar values of the same type - string set, number set, binary set
		- ![[Pasted image 20211006163222.png]]
## Management Console
- Table Names must be unique per AWS Account and region.
	- Between 3 and 255 characters long
	- UTF-8 encoded
	- Case sensitive
	- Contain a-z, A-Z, \_, ., and -.
- Primary key must consist of a partition key or a partition key and a sort key.
	- Only string, binary, and number data types are allowed for partition or sort keys
- Provisioned capacity mode is the default (free tier)
- Secondary Indexes creates a local secondary index.
	- Must be created at the time of table creation
	- Same partition key as the table, but a different sort key
- Provisioned Capacity is set at the table level.
	- Adjust at any time or enable auto scaling to modify them automatically
	- On-demand mode has default upper limit of 40,000 WCU and RCU.
		- Auto scaling can be capped manually.
## Console Metrics and CloudWatch
CloudWatch monitors your AWS resources in real time, providing visibility into resources utililzation, application performance, and operational health.
- Track metrics 
- Create dashboards
- Create alarms
- Create rules for events
- View logs
Helps Answer questions like:
-   How can I determine how much of my provisioned throughput is being used?
-   How can I determine which requests exceed the provisioned throughput limits of a table?
-   How can I determine if any system errors occurred?

**DynamoDB Metrics**
![[Pasted image 20211006164502.png]]

## Alerts and Alarms
Alarms can be created on metrics, taking an action if the alarm is triggered
Alarms have three states:
- Insufficient: not enough data to jump the state - alarms often start in this state
- Alarm: alarm treshrold has been triggered
- OK: Threshold has not been triggered
Alarms have a number of key components:
- Metric: data points over time being measure
- Threshold: Exceeding this is bad (static or anomaly)
- Period: How long the threshold should be triggered before an alarm is generated
- Action: What to do when an alarm triggers (SNS, EC2 autoscaling, etc.)

### Errors and Codes
Successful DynamoDB request return the HTTP status code for success (200 OK), along with the results of the request

If the request fails, DynamoDB returns an error with three components:
	- HTTP Status Code
	- Exception
	- Error message
	
Most AWS SDKs propagate these low-level errors for you. Handle using try-catch or if-then statements.

**Error retries and exponential backoff**
AWS SDKs all implement retry logic automatically.
Exponential backoff uses increasing wait times for consecutive error messages.
This algorithm helps mitigate request rate errors.

**Batch Operations**
- Batch operations tolerate the failure of individual requests
- The most common cause of errors is throttling
- Unprocessed items should be retried using exponential backoff.

![[Pasted image 20211006165546.png]]
## Paritions, Parition Keys, and Sort Keys
- The partition key or parition and sort key are used to uniquely write or read an item.
- Parition key is used for partition selection via the DynamoDB internal hash function.
- One partition holds 10 GB of data and supports up to 3,000 read capacity units (RCUs) or 1000 write capacity units (WCUs)
- Partition key is used to select the items to read/write
- Sort key is used to range select (eg *begins_with*) or to order results
- Sort keys may not be used on their own
![[Pasted image 20211006170124.png]]

## RCU and WCU
Provisioned Throughput
- Maximum amount of capacity an application can consume from a table or index
- Throttled Requests: `ProvisionedThroughputExceededException`

Eventually vs. Strongly Consistent Read
- Eventually consistent reads might include stale data
- Strongly consistent reads are awlays up to date but are subject to network delays

Read Capacity Units
- One RCU represents one strongly consistent read request per second, or two eventually consistent read requests, for an item up to 4kb in size.
- Transactional read requests require 2 RCUs for items up to 4kb.

For an 8 KB item size:
- 2 RCUs for one strongly consistent read
- 1 RCU for an eventually consistent read
- 4 RCUs for a transactional read

Write vs Transactional Write
- Writes are eventually consistent within one second or less.

Write Capacity Units (WCUs)
- One WCU represents one write per second for an item up to 1KB in size
- Transactional write requests require 2 WCUs for items up to 1KB

For a 3KB Item size:
- Standard: 3 WCUs
- Transactional: 6 WCUs

https://tutorialsdojo.com/calculating-the-required-read-and-write-capacity-unit-for-your-dynamodb-table/

## Consistency Model (Strongly vs Eventual)
![[Pasted image 20211006173209.png]]
![[Pasted image 20211006173242.png]]

### Eventual Consistency
- Request router randomly selects a storage node for the partition
- 1 in 3 change that you've selected stale data (worst case)
- Eventually consistent reads are 50% the "cost" of strongly consistent
- Strongly consistent reads require 2 of 3 matches across replicas

## Scans and Queries
### Scan
- Returns all items and attributes for a given table
- Filtering results do not reduce RCU consumption; they simply discard data
- Eventually consistent by default, but the `ConsistentRead` parameter can enable strongly consistent scans
- Limit the number of items returned
- A single query returns results that fit within 1 MB
- Pagination can be used to return more than 1 MB
- Parallel scans can be used to improve performance
- Prefer query over scan when possible
- If you are repeatedly using scans to filter on the same non-PK/SK attribute, consider creating a secondary index

### Query
- Find items based on primary key values
- Query limited to PK, PK+SK, or secondary indexes
- Requries PK attribute
- Returns all items with that PK value
- Optional SK attribute and comparison operation to refind results
- Filtering results do not reduce RCU consumption; they simply discard data
- Eventually consistent by default, but the `ConsistentRead` parameter can enable strongly consistent scans
- Limit the number of items returned
- A single query returns results that fit within 1 MB
- Pagination can be used to return more than 1 MB
## PutItem
- PutItem
	- Creates a new item
	- Replaces existing item with the same key
- UpdateItem
	- Creates a new item if the specified key does not exist; otherwise, it modifies an existing item's attributes
- DeleteItem
	- Deletes the item with the specified key
- Write Conflicts
	- ![[Pasted image 20211006173932.png]]
	- Default behavior: last write will be applied
## Batch Operations
`BatchGetItem`
- Returns attributes for multiple items from multiple tables
- Request using primary key
- Returns up to 16 MB of data, up to 100 items
- Get unprocessed items exceeding limits via `UnprocessedKeys`
- Eventually consistent by default
	- Can use `ConsistentRead`
- Retrieves items in parallel to minimize latency
 
`BatchWriteItem`
- Puts or deletes multiple items in multiple tables
- Writes up to 16 MB of data, up to 25 put or delete requests
- Get unprocessed items exeeding limits via `UnprocessedItems`
- Conditions are not supported for performance reasons
- Threading may be used to write items in parallel

## Provisioned vs. On-Demand Capacity Modes
### Provisioned Capacity
- minimum capacity required
- able to set a budget (max capacity)
- Subject to throttling
- auto scaling available
- risk of under-provisioning - monitor your metrics
- lower price per API call
	- ![[Pasted image 20211006174430.png]]
### On-Demand Capacity
- No min. capacity
	- Pay more per request than provisioned capacity
- Idle tables not charged for read/write, but only for storage and backups
- No capacity planning required - just make API calls
- Eliminates the tradeoffs of over or under provisioning
- Use on-demand for new product launches
- Switch to provisioned once a steady state is reached
	- ![[Pasted image 20211006174552.png]]

## Autoscaling
### Basics
- Auto scaling is best suited for predictable, gradually changing traffic patterns
- You may still manually change provisioned throughput settings
- Recommended to apply auto scaling uniformly to tables and global secondary indexes (GSIs)
![[Pasted image 20211006174846.png]]

## Indexes
### Secondary Indexes
- A secondary index
	- structure that contains a subset of attributes from a table, along with an alternate key to support query operations. You can retrieve data from the index using a query, just like with a table.
	- A table can have multiple secondary indexes
- Global Secondary Index
	- Index with a partition key and a sort key that can be different from those on the base table
	- The primary key of the GSI can be either simple (partition key) or composite (partition and sort key)
	- ==strong consistency is unsupported==
- Local Primary Index
	- Index that has the same partition key as the base table but a different sort key
	- The primary key of an LSI must be composite (partition and sort key)
	- ==Must be created at the time of table creation==

![[Pasted image 20211006175501.png]]

### Index Queries and Projection Expressions
A prooject is the set of attributes copied form a table into a secondary index. The partition key and sort key of the table are always projected into the index.
- ALL
	- All the table attributes are projected into the table
- KEYS_ONLY
	- Only the index and primary keys are projected into the index
- INCLUDE
	- Only the specified table attributes are projected into the index

Using GetItem, Query, or Scan operations return all attributes by default.
- Use projectione expresssion to get a subset of these attributes
- Example:
	- find all albums by `artist_id`, returning only title and price
### Sparse Indexes
DynamoDB writes a corresponding index item iff the index sort key value is present in the item.
- If the sory key doesn't appear in every table item, the index is said to be sparse
Globally secondary indexes are sparse by default.
- When you create a GSI, you specify a partition key and optionally a sort key.
- only items in the aprent table that contain those attributes apepar in the index.
By creating sparse indexes, you can provision GSIs with lower write throughput than that of the parent table.
- This can possibly save a lot of money that would otherwise be spent on storage (for no additional benefits)
## Importing Tables Using AWS Database Migration Service
![[Pasted image 20211006180646.png]]

**Steps to configure DMS**
1. Create replication instance
2. Create MYSQL source endpoint
3. Create service access role in IAM
4. Create DynamoDB target endpoint
5. Create database migration task

## On-Demand vs. Continuous (PITR) Backup
### On-Demand BAckup and Restore
Create full backups of your tables at any time in either the Console or API
- Backup and restore actions execute with zero impact on table performance or availability
- Backups are consistent withins econds and retained until deleted
- Backup and restore operates within the same region as the source table
### Point-in-time recovery (PITR)
Helps protect your DynamoDB tables from accidental writes or deltes. You can restore your data to any point in time in the last **35 days**.
- DynamoDB maintains **incremental** backups of your data
- Point-in-time recovery is not enabled by default
- The latest restorable timestamp is typically five minutes in the past

After restoring a table, you must manually set up the following on the restored table:
- Auto scaling policies
- AWS IAM policies
- CloudWatch metrics and alarms
- Tags
- Stream Settings
- TTL settings
- PITR recovery settings

## Offloading Large Attribute Values to S3
### Basics
![[Pasted image 20211006181616.png]]
- 400KB limit per item

## Transactions
Transactions enable developers to easily perform atomic writes and isolated reads across multiple items and tables.
`TransactWriteItems`
- Transact up to 25 items or 4MB
- Evaluate conditions
- iff all conditions are simultaneously true, perform write operations
`TransactGetItems`
- Transact up to 25 items or 4MB
- Return a consistent, isolated snapshot of items

DybamoDB performs **two underlying reads or writes** of every item in the transaction
- one to prepare the transaction
- one to commit the transaction

Apply transactions to items in:
- same partition key or across partition keys
- Same table or across table
- Same region only
- Same account only
- DynamoDB tables oly

Transactions scale like the rest of DynamoDB:
- Unlimited concurrent transactions
- Low latency, high availability
- Scales horizontally
- Up to you to design to avoid hot keys

Reasons for transaction failures:
- Precondition failure
- Insufficient capacity
- Transactional conflicts
- Transactions still in progress
- Service error
- malformed request
- permissions

## Time to Live (TTL)
### TTL Basics
Time to live (TTL) lets you define when table items expire so they can automatically be deleted from the database.
- No cost to use TTL
- Reduce storage costs by limiting storage usage to relevant items only
- Does nnot onsume provisioned throughput

Use Cases
- Session data
- Event logs
- Pattern searching and usage tracking
- Debugging and analytics
- Other temporary sensitive data for contractual or regulatory compliance

**How it works**
1. TTL Compares current time to the defined TTL attribute of an item
2. If current time > item's TTL value, item is marked for deletion
3. DynamoDB typically deletes expired items with 48 hours of expiration
4. Items are removed from LSIs and GSIs automatically using an eventually consistent delete operation.

![[Pasted image 20211007081734.png]]

Due to the potential delay between expiration and deletion time, use a filter expression to return only non-expired items via TTL field.
## DynamoDB Accelerator (DAX) Architecture
- Fully managed, highly available, in-memory cache for DynamoDB that delivers up to a 10x performane improvement
- Reduces request times from miliseconds to microseconds, even under load
- No need for develoeprs to manage caching logic
- Compatible with DynamoDB API Calls

![[Pasted image 20211007082031.png]]

### High Availability
- DAX is designed to run within a VPC. In the evevent of a primary node failure, DAX fails over to a read replica and promotes that node as the new primary.
- ![[Pasted image 20211007082350.png]]
### API Compatibility
- DAX is API compatible with DynamoDB
	- Read APIs
		- `GetItem`
		- `BatchGetItem`
		- `Query`
		- `Scan`
	- Modify APIs
		- `PutItem`
		- `UpdateItem`
		- `DeleteItem`
		- `BatchWriteItem`
	- Control plane APIs
		- not supported

## Global Tables
Global table are a fully managed, multi-master, multi-region replication solution
- Build high performance, globally distributed applicatiosn
- Low latency reads and writes to locally available tables
- Multi-region redundancy for DR or HA applications
- Easy to set up and no application rewrites required
- Replication latency typically under one second
- Must setup with an empty table
## Encryption
DynamoDB protects data stored at rest and in transit between on-premises clients and DynamoDB, and between DynamoDB and other AWS resources within the same AWS Region.
- Encryption in transit uses HTTPs.
- Encryption at rest uses AWS KMS to encrypt all table data.

When creating a new table, you may choose:
- AWS owned customer master key (CMK):
	- Default option
	- key owned by DynamoDB
	- no charges
- AWS Managed CMK
	- Key stored in AWS Account
	- Managed by AWS KMS
	- View the CMK and its key policy (policy can't be changed)
	- Audit encryption/decryption of your table using CloudTrail

**DynamoDB Encryption Client**
- Java and Python libraries that encrypt your data **prior** to sending to DynamoDB
- ![[Pasted image 20211007093714.png]]

## DynamoDB VPC Endpoints
Without VPC endpoint: 
![[Pasted image 20211007094103.png]]

With VPC endpoint: 
![[Pasted image 20211007094144.png]]

# Amazon Aurora
## Understanding Aurora Architecture
- Fully managed DB
- MySQL and PostgreSQL
- Cluster Architecture
![[Pasted image 20211007094522.png]]
- Excellent for online transaction processing use cases
- supports up to 15 read nodes
- solves several pain points for MariaDB, Oracle, MySQL, and PostgreSQL


### Storage Architecture
![[Pasted image 20211007094612.png]]
- data is replicated within the storage cluster
- Within the storage cluster, data is replicated six times

### Cluster Architecture
![[Pasted image 20211007094754.png]]
- Read nodes provide failover targets in the event of write node failure
- Failed nodes are automatically replaces
### Cluster Endpoints
![[Pasted image 20211007094818.png]]

### Why use Aurora instead of RDS?
- Auto scaling, self healing cluster volume storage
- Automatically grows in 10GB increments
- Scales to handle I/O requiresments of workload
- Great fit for OLTP workloads
- Easy to manage

## Getting Started with Amazon Aurora
### Engine Configurations
#### Aurora Serverless
- On-demand auto scaling
- Good for intermittent or unpredictable workloads
- Configurable capacity rated in ACUs (Aurora Capacity Units)
![[Pasted image 20211007095132.png]]

### Aurora Global Database
- Primary writer region and up to five secondary read-only regions
- Uses dedicated inafrastructure for replication
- Allows for low latency reads in other regions
![[Pasted image 20211007095227.png]]

## Working with Aurora Replicas
### Reader Notes
- Provide us with horizontal scalability
- Provid efault tolerance and availability
	- Used as failover targets
- Easy to create and manage

### RDS MySQL to Aurora MySQL
#### Create Aurora Replica from RDS Source
![[Pasted image 20211007160529.png]]
- Used as a near-zero downtime option to migrate data from RDS MySQL to Aurora
- Takes a snapshot of RDS source, restores to an Aurora cluster, and replicates changes through binlog replication
	- AuroraBinlogReplicaLag

![[Pasted image 20211007160757.png]]

#### High-Level Steps
![[Pasted image 20211007160735.png]]
1. Create Aurora replica from RDS MySQL or RDS PostgreSQL source.
2. Once replication lag reaches 0, halt write activity on RDS primary.
3. Complete cutover by promoting Aurora Replica to standalone.
4. Update endpount used in application

### Self-Hosted MySQL
![[Pasted image 20211007161413.png]]
1. Enable binary logging; ensure logs will be retained for duration of the migration
2. Export data form source instance (mysqldump, pg_dump); ensure to note binlog position.
3. Import the dump to Aurora cluster.
4. Configure replication between self-hosted source and Aurora target
5. When replication lag reaches 0, stop write activity to self-hosted database
6. Update endpoint in application for the cut over

### Replication between Clusters
![[Pasted image 20211007161507.png]]
- Using native replication, we can replicate between clusters in the same region or even configure cross-region replication
- Useful for mirgating data to another VPC or region with next to zero downtime.
![[Pasted image 20211007161518.png]]

### Replication Lag
![[Pasted image 20211007162025.png]]
- In highly concurrent or lock-heavy environments, may find replicaiton lag to be a concern.
- Impact on RDS to Aurora replication, as well as cross-region Aurora replication

### Recap
- Replicas are leveraged as failover targets in Aurora. They allow us to allocate instances across multiple AZs
- Conifgurable failover priority between tier 0 and tier 15
- Aurora MySQL uses binlog replication
- Aurora PostgreSQL uses replication slots
- On-prem to Aurora, RDS to Aurora and Aurora to Aurora all can encounter replication lag
- Replication in cluster is done at storage level only; only subject to `AuroraReplicaLag`
	- Generally less than 10ms

## Managing an Aurora Cluster
### Aurora Metrics
Cluster
- `VolumeBytesUsed`
- `VolumeWriteIOPS`
- `VolumeReadIOPS`
- All of these correlate to cluster volume

DB Instance
- Utilization metrics (CPU, freeable memory, etc.)
- AbortedClients
- AuroraReplicaLag
- Blocked transactions
- Commit latency
- Free local storage

### Storage
**Persistent**
- Data we're storing in our cluster volume is persistent

**Temporary**
- Tempo tables spilling to disk
- Temporary files
- log files, such as error logs
- Large ALTER operations

### Important Metrics
- DML and DDL latency provided in Aurora MySQL can be leveraged to perform initial investigation on a report of a slow query
- MaximumUsedTransacitonIDs is an important metric for PostgreSQL
- Metrics such as DB connections, IOPs, free storage, CPU, freeable memory, and buffer cache hit ratio are all important.
- While the default CloudWatch Metrics provide insight, there are more features available.

### Fault Injection Queries
![[Pasted image 20211007163841.png]]

### Stop, Start, Reboot
- Can't stop Multi-Master or Global Database clusters

### Deleting Resources
- After deleting all instances in the cluster via CLI or API, cluster volume remains
- When we need access again, we simply create instances in the cluster

## Common Backup and Restore Methods
### Service Backup
- Backups are created from the storage cluster
- Backup retention: 1 to 35 days
- Automatic backups can not be disabled
- Aurora creates incremental backups continuously

### PITR
![[Pasted image 20211007164211.png]]
- Creates a new cluster

### Backtrack
- rolls back database to a previous state
- Rewinds cluster storage in place
- Faster than PITR
- Use if accidentally removes a table
- Can move time backward and forward
- Limit of 72 hours

### Cluster Cloning
![[Pasted image 20211007164359.png]]
- Creates a new cluster
- Faster than PITR
- Connects to source storage cluster
- New writes to clone **go to** cloned cluster storage

### Aurora MySQL Tools
MySQL:
- MySQL native
- inefficient for more than 10GB
- Requires source database interruption

Percona, Xtrabackup:
- Use innobackupx to create backup
- Backup can be loaded directly from S3
- Intended for new cluster target

![[Pasted image 20211007164452.png]]

PostgreSQL:
- PostgreSQL Native
- Handles large datasets
- Requries source database interruption
![[Pasted image 20211007164528.png]]

## Working with Aurora in a VPC
### Read Replica VPC Migration
![[Pasted image 20211007165928.png]]
**Cluster Endpoint**
- Always resolves to write node

**Reader Endpoint**
- Always points to Read Node

**Custom Endpoint**
- Can point to custom parameter read node
![[Pasted image 20211007170030.png]]

### How to Use Aurora Global Database
### Aurora Global Database
- Primary writer region and up to 5 secondary read-only regions
- Uses dedicated infrastructure for replication
- Allows for low latency reads in other regions
- <1000ms replication log

### Advantages of Global Database
- Faster Replication
	- Not limited by native replication methods that are prone to replication lag and bottlenecks
- Offloads Replication
	- Replication costs are offlaoded to underlying storage, saving valuable resources
- RTO and RPO
	- Provides RPO of 1 second and RTO of ~1 minute, a huge perk for disaster recovery planning

![[Pasted image 20211007171003.png]]

### Global Database Pricing
![[Pasted image 20211007171116.png]]
- No regional database transfer fees

![[Pasted image 20211007171150.png]]
- Pay per replicated IOs

### Write Forwarding
Endpoints and Write Forwarding
![[Pasted image 20211007171311.png]]
- Statements are forwarded to primary cluster and executed on the primary instance
- The write forwarding is transparent to the application, it itneracts with the secondary region as normal

### Limitations of Global Databases
- No cloning
- No backtrack
- No parallel Query
- No Aurora Serverless
- No Stop/Start functionality

## Aurora Serverless
![[Pasted image 20211007171540.png]]
- No Scale-up cooldown
- Scale down 15 minutes from scale up
- Or 310 seconds from last scale down

Scaling Timed Out
- Safe Scaling Point
	- Yes: Increase maximum ACU
	- No: long-running query?
		- Wait and retry
		- Force Scaling 

### Zero Capacity Units
- Pause compute capacity after **consecutive minutes of inactivity**
	- Key Serverless feature
	- Only billed for data storage
	- Fantastic for infrequent/sporadic workloads

## Understanding Aurora Security
### Security Features
### IAM Authentication
![[Pasted image 20211007172434.png]]
![[Pasted image 20211007172445.png]]
- User in database with same username as user in IAM

![[Pasted image 20211007172459.png]]

Enabled IAM Auth -> Create IAM Policty enabling connection with IAM -> Create user in Aurora Cluster DB -> Token from IAM is passed to User -> Auth to DB
![[Pasted image 20211007172611.png]]
### SSL
![[Pasted image 20211007172707.png]]
SSL modes:
- Verify_identity
	- Verifies client server FQDN, and certificate authority
- Verify_ca
	- Verifies certificate authority
- Required
	- Requires SSL connection from client side
	- Can force SSL connections only
### KMS
- Encryption is enabled by default, with customer master key
- ![[Pasted image 20211007172750.png]]

Can't disable or enable encryption on existing instance
	- have to snapshot and recreate
- ==Keys are region specific==

![[Pasted image 20211007172856.png]]

## Using Aurora Cloning
### Reviewing the Basics
- Limit of 15 clones in total
- Clones can be in other VPCs
- ![[Pasted image 20211008133213.png]]
- Need to be in same region
- Can share across accounts

### Use Cases for Clones
- Schema Changes
	- Testing proposed schema changes without impacting production cluster
- Parameter Group Experimentation
	- Experiment with cluster-level parameter group changes safely
- Disruptive Workloads
	- Run long or potentially locking queries without impacting production funtionality
- Cross Account
	- Clusters can be cloned across accounts within the same region and AZ
- Outside Data Access
	- provide access to contractors or other outside parties using AWS Resource Access Manager (RAM)
- Faster than Snapshots
	- Utillize Aurora cloning to quickly move data between AWS Accounts

## Troubleshooting Aurora
### TCP Keepalive
Issue: Connections Remain Open
- application still shows a connection, but database has gone down
- During outage, aplpication continued waiting for a response from the db

Cause: No KeepAlives
- Without a TCP keepalive configured, application will continue waiting for a response for the query

Fix: 
- Configure TCP keepalive params on the application instance. Ensures application can close any inactive connections much faster
- Consider explicitly closing database connections
- In PostgreSQL and MySQL, memory allocations are made per connection, meaning a high amount of idle connections can waste resources
![[Pasted image 20211008134239.png]]

### DNS Caching and TTL
Issue: Application Write Failures
- Application continues connecting to old primary after a failover
- After scaling instance size, our application can't connect to the new instance
- Stale DNS records from cluster endpoints

Cause: DNS Cache or excessive TTL
- Somewhere throughout the networking layer, we are caching DNS, which results in stale records.
	- This can impact the time to complete failovers

Fix: 
- Ensure you're not caching DNS anywhere
- Leverage a Smart Driver such as the MariaDB Connector, which is a supported JDBC driver that has the ability to read a cluser topology from a metadata table
- Set Java DNS caching timeouts to much lower values
![[Pasted image 20211008134539.png]]

### Cluster Cache Management
Issue: Poor Performance after Failover
- Administrators raise concerns over a slow failover for Aurora PostgreSQL clusters.
- While the failover is fast, there is a significant performance degredation after the instance begins accepting connections.

Cause: Empty or Stale Buffer Cache
- Possible stale buffer cache on newly promoted primary.
- This cache must be rebuilt to reduce queries retrieving data from disk.

Fix:
- Set the value of the `apg_ccm_enabled` cluster parameter to 1.
- Configure promotion tier priority on the writer and a replica.
- Verify it's enabled
	- ![[Pasted image 20211008135030.png]]

### JDBC Connection String for Fast Failover
- We can optimize JDBC connections to withstand DB failures
- ![[Pasted image 20211008135214.png]]
- TCP Keepalive
- Secondary Endpoint
- Load-balanced Connection
-  ![[Pasted image 20211008135319.png]]

### MySQL Out-of-Memory Issues
Issue: Aurora OOM Crashes
- Dev team reports crashes when they attempt to import a `mysqldymp`, and sometimes during peak production hours

Crash:
- ![[Pasted image 20211008135616.png]]

Cause: Low memory
- Low amount of freeable memory
- Increase in the "swap" metric

Fix:
- Enabled `aurora_oom_response` parameter, and configure to the desired action
- `aurora_oom_response` is an instance-level parameter, uses a string with actions, and is separated by commas
- ![[Pasted image 20211008135726.png]]

### Use the Tools
1. CloudWatch Metrics
	1. Provides monitoring for useful Aurora-specifc metrics, as well as swap, database connections, and `FreeLocalStorage`
2. Enhanced Monitoring
	1. Extremely granular metrics, down to one-second monitoring interval. 
	2. Access to OS metrics and process lists
3. Performance Insights
	1. Quick Insight into database load and wait events
	2. Perfect for root cause investigations and optimizations
# Additional Database Services
## Overview of Neptune, DocumentDB, and QLDB
### Neptune
- Supports:
	- Apache - TinkerPop Gremlin
	- W3C - SPARQL Protocol
- Graph Database
	- Neptune is a graph database with support for Gremlin and SPARQL
- Scalable and Fault Tolerant
	- Supports Multi-AZ and up to 15 read replicas
	- Leverages a self-healing, fault-tolerant cluster volume

![[Pasted image 20211008140852.png]]
- Node or Vertex
	- Data inside Node
- Edges are information between nodes
#### What Do we Use Graphs for?
- Security
	- Pattern recongition is very powerful for detecting fraud, as well as other security-related use cases
- Social Media
	- Profile and social connection information
	- Interest graphs for potential conenctions and targeted advertising
- Science
	- Graph databases are used extensively in scientific modeling
### DocumentDB
- MongoDB Compatible
	- Uses the open-source MongoDB 3.6 API
	- Customers can use their exsting MongoDB drivers/tools.
- Query JSON	
	- DocumentDB is a type fo NoSQL database that allows customers to query or store data as JSON documents.
#### DocumentDB Features
- MongoDB compatible interface
- Like RDS, DocumentDB is fully managed
- Storaged automatically scales upward
- Able to index JSON data structures

#### Uses
- Great for content catalogs or content management systems
- user profile storage
- Can integrate with Lambda and other sources

### Quantum Ledger Database (QLDB)
- Serverless Immutable Database
- Immutable and Verifiable History
	- History of changes to underlying data is immutable and transparent
	- Change are permanently stored and can't be deleted or modified
- Amazon Ion
	- Uses a document data model, storing in tables of Amazon ION documents
	- Supports a SQL like query language called PartiQL

#### Uses
1. Finance
	1. Banking applications, where need to track a series of credits/debts
2. Insurance
	1. Insurance appliactions, where access to a history of claims is necesssary
3. Supply Chain
	1. Track movement of an item throughout the supply chain


## Understanding Redshift Architecture
Redshift is Amazon's analytics database, and is **designed to crunch large amounts of data as a data warehouse**.
### Cluster
![[Pasted image 20211008141913.png]]

### Node
![[Pasted image 20211008142042.png]]

### Slices
![[Pasted image 20211008142118.png]]
### Distribution Styles
- Even
	- Blocks are distributed evenly between cluster slices (default)
- Key
	- Identitical key values are stored on the same slice
- All
	- All slices store a copy of table data
## Loading and Unloading data with Redshift
### Loading Data from S3
![[Pasted image 20211008143258.png]]
- Copy command identifies target tables
- from directive identifies source files
- iam_role identifies role with S3 read permissions
- Redhift retrieves and processes file from S3
### Unloading Data to S3
![[Pasted image 20211008143346.png]]
- Unload command identifies data to unload
- To directive identifies target bucket
- iam_role identifies role with S3 write permissions
- FORMAT directive specifies the target file format
- Redshift puts generated file in S3 bucket
### Redhisft Spectrum
![[Pasted image 20211008143600.png]]
Read and write without loading or storing data locally

- create foreign tables from data stored in S3
- Uses EXTERNAL keyword for schema and table creation
- Supports SELECT and INSERT operations
- UPDATE and DELETE are not supported
# Migrating Data to AWS Databases
## Picking the Right Migration Tool
### Migration Methods
- Amazon RDS Snapshot Migration
- Percona XtraBackup
![[Pasted image 20211008143800.png]]
- Self Managed Export/Import
- AWS Database Migration Service
### Homogeneous Migration
Target is compatible with Source Service
- Amazon RDS Snapshot Migration
	- Managed point and click service available through the AWS management console
	- Best migration speed and ease of use
	- Can be used with binary log replication for near zero migration downtime
- Percona XtraBackup
	- Managed backup ingestion from Percona XtraBackup files stored in an Amazon S3 backup
	- High performance
	- Can be used with binary log replication for near zero migration downtime
- Self Managed Export/Import
	- Schema can be migrated as-is without conversion
	- Data migration can be performed manually using existing, well documented command line utilities
	- Can be used with binary log for near zero migration downtime
- AWS Database Migration Service
	- Supports heterogeneous and homogenous migrations
	- Managed point-and-click data migration service available through the AWS management console
	- Schemas must be migrated separately
	- Supports CDC replication for near-zero migration downtime
### Hterogeneous Migration
Two Phases
1. Schema Migration
	1. You must convert database objects such as tables, views, functions, and stored procedures to a compatible format before you can use them within the RDS database
	2. AWS Schema Conversion Tool can automatically convert the source database schema and a majority of the custom code, including views, stored procedures, and functions, to a compatible format
3. Data Migration
	1. After the database objects are successfully converted and migrated to Amazon Aurora, its time to migrate the data itself
	2. The task of moving data from a non-MySQL-compatible database to Amazon Aurora is best done using AWS DMS.
### Picking the Right Migration Tool
1. Review the available migration techniques and choose one that satisfies your requirements
2. Perpare a migration plan in the form of a step-by-step checklist
3. Prepare a "shadow" checklist with rollback procedures. ideally, you should be able to roll the migration back to a known, consistent state from any point in the migration checklist.
4. Use the checklist to perform a test migration, and take note of the time rquired to complete each step. If any missing steps are identified, add them to the checklist. If any issues are identified during the test migration, address them and rerun the test migration
5. Test all rollback procedures. if any rollback procedure has not been tested successfully, assume that it will not work
6. After you complete the test migration and become fully comfortable with the migration plan, execute the migration
## Introduction to Database Migration Service
### What is DMS?
- A cloud service that makes it easy to migrate relational databases, data warehouses, NoSQL ddatabases, and other types of data stores.
- You can use AWS DMS to migrate your data into the AWS Cloud, between on-premises instances (through an AWS Cloud Setup), or between combinations of cloud and on-premises setups.
- With DMS, you can perform one-time migrations, and also replicate ongoing changes to keep sources and targets in sync.
- For heterogeneous migrations, use the AWS Schema Conversion Tool to translate to the new platform.
### Tasks DMS Performs
- Automatically manages the deployment, management, and monitoring of all hardware and software needed for a migration
- Uses a pay-as-you-go model
- Provides automatic failover for the replication server.
- Ensures data is secure both at rest and in transit

### How DMS Works
#### What High-Level Steps are Taken?
- Create a replication server
- Create source and target endpoint that have connection information about your data stores
#### How Does a Migration Work?
- AWS DMS connects to the source data store
- Formats the data for consumption by the target data store
- Loads the data into the target data store
## DMS Data Migration Sources and Targets
### Components
![[Pasted image 20211009202126.png]]
- Replication Instances
- Endpoints
	- Source
	- Target
	- Engine Type
- Replication Tasks
	- Configure and move data
	- Source Endpoint
	- Type of endpoint
	- Full load  (migrate)
	- Full load + CDC (migrate and replicate changes)
	- CDC Only (replicate changes)
	- Table preparation Modes
		- Drop tables on target
		- Create tables
		- Truncate Mode

### Sources
- On-premises and EC2 Databases
- ![[Pasted image 20211009202438.png]]
- ![[Pasted image 20211009202455.png]]
### Target
- On-premises and Amazon EC2 Instance databases:
- ![[Pasted image 20211009202526.png]]
## Using the Schema Conversion Tool
Using Schema Conversion Tool, we can create table mapping rules and transform our data to facilitate a heterogenous migration, such as Oracle to Postgres.
### SCT
- You can use the AWS Schema Conversion Tool to convert your existing database schema from one database engine to another.
- You can convert relational OLTP schema or data warehouse schema
### Installing SCT
![[Pasted image 20211009202745.png]]
- The SCT is a standalone application that provides a project-based user interface.
- It's available on Fedora Linux, macOS, Windows, and Ubuntu 15.04.
1. Download the SCT installer
2. Extract the installer file for your OS
3. Run the installer
4. Install the JDBC drivers for the source and target database engines

### Converting Schemas
#### DB Migration Assessment Report
This report summarizes all the schema conversion tasks and details the action items for schema that can't be converted to the DB engine of your target DB instance.
#### Steps
1. Create mapping rules in the AWS SCT
2. Convert the schema using the AWS SCT.
3. Create migration assessment reports
4. Handle the manual conversion in the AWS SCT
5. Update and refresh the converted schema
6. Save and apply the converted schema
### Extraction and Replication
#### Using Data Extraction Agents
- In some migration scenarios, the source and target databases are very different from one another and require additional data transformation.
- AWS SCT is extensible, so you can address these scenarios using an *agent*
	- An agent is an external program that's inegrated with AWS SCT but performs data transformation elsewhere (such as on an Amazon EC2 instance)
#### Using AWS SCT Replication Agent
- For very large database migrations, you can use an AWS SCT replication agent (`aws-schema-conversion-tool-dms-agent`) to copy data from your on-prem database to S3 or a Snowball Edge device
- The replication agent works in conjunction with AWS DMS and can work in the background while AWS SCT is closed.
## Migrating using DMS with Data Validation
### Understanding Validation
#### DMS Data Validation
- AWS DMS provides support for data validation to ensure your data was migrated accurately from the source to the target
- If enabled, validation begins immediately after a full load is performed for a table
- Validation comapres the incremental changes for a CDC-enabled task as they occur.
### Task Settings and Statistics
#### Data Validation settings include the follow
- Data validation settings include the following:
	- ![[Pasted image 20211009203827.png]]
### Troubleshooting/Revalidation
#### Revalidating Tables during a Task
- While a task is running, you can request AWS DMS to perform validation.
	- Steps:
		1. Open DMS console
		2. Choose Tasks
		3. Choose the running task that has the table you want to revalidate
		4. Choose Table Statistics
		5. Choose the table you want to revalidate
		6. Choose Revalidate
#### Troubleshooting
- During validation, AWS DMS creates a new table at the target endpoint: `awsdms_validation_failures_v1`
- If any record enters the `ValidationSuspended` or `ValidationFailed` state, AWS DMS writes diagnostic information `awsdms_validation_failures_v1`. 
- You can query this table to help troubleshoot validation erros.
## Using AWS Glue
### What is Glue
![[Pasted image 20211009205130.png]]
- AWS Glue is a fully managed extract, transform, and load service that makes it easy to prepare and load your data for analytics
- How does it work? Select a data source and data target in AWS Glue. 
- AWS Glue will generate Apache Spark ETL code in Scala or Python to extract data from the source, transform the data to match the target schema, and load it into the target.
### AWS Glue Data Catalog
- The AWS Glue Data Catalog contains references to data that is used as sources and targets of your ETL jobs in AWS Glue.
- To create your data warehouse or data lake, you must catalog this data.
- The AWS Glue Data Catalog is an index to the location, schema, and runtime metrics of your data. You use the information in the Data Catalog to create and monitor your ETL jobs.
- Glue loads information regarding the source and target database into a structure called a tree. The structure includes the following:
	- Connections
	- Crawlers
	- Databases
	- Tables
	- ETL jobs
	- Triggers
### How much Does AWS GLue Cost?
- Your storage cost is still $0, as the storage for your first million tables is free.
- Your first million requests are also free.
- You will be billed for one million requests above the free tier, which is $1.
- Crawlers are billed at $0.44 per DPU-Hour, so you will pay for 2 DPUs \* 1/2 hour at $0.44 per DPU-Hour or $0.44.
### Migrating ETL
- You can migrate ETL processes. This includes the conversion of ETL-related business logic located inside the source data warehouses or in external scripts that are run separately.
- After migration, the ETL processes run in AWS Glue.
- You run ETL to Glue migration as a separate project from converting your DDL statements and data.
### AWS Glue Security
- AWS Glue supports data encryption at rest for authoring jobs in Glue and developing scripts using development endpoints. You can configure ETL jobs and development endpoints to use AWS KMS keys to write encrypted data at rest.
- AWS provides Secure Sockets Layer (SSL) ecnryption for data in motion. You can configure encryption settings for crawlers, ETL jobs, and development endpoints using security configurations in AWS Glue.
## Large Migrations using Snowball Edge
![[Pasted image 20211009210838.png]]
### What is Snowball Edge?
- AWS Snowball edge is a type of Snowball device with on-board storage and compute power for select AWS captabilities. Snowball Edge can do local processing and edge computing workloads in addition to transferring data between your local environment and the AWS Cloud.
### Migration Use Cases
- Bandwidth in network can become a limiting factor.
- What about tranfer of terabytes?
	- One hundred terabytes of data takes more than 100 days to transfer for a dedicated 100-Mbps connection.
- Another scenario that can delay a database migration is the lack of outside access to the database itself.
### Migration Processes
1. Use AWS SCT to extract the data locally and move it to an Edge device.
2. Ship the Edge device or devices back to AWS.
3. After AWS receives your shipment, the Edge device automatically loads its data into an Amazon S3 bucket.
4. AWS DMS takes the files and migrated the data to the target data store.
## Using DMS for Cross-Account Migration
###  Migration Considerations
- How do we migrate between accounts?
- We can set up a VPC peering connection between the accounts.
- Use a DB snapshot for one-time load.
- Use DMS for ongoing replication.
### VPC Peering
1. Owner of the **Requestor VPC** sends a request to the owner of the **acceptor VPC** to create the VPC peering connection.
2. The owner of the acceptor VPC accepts the VPC peering connectionr equest to activate the VPC peering connection.
3. The owner of each VPC in the VPC peering connection must manually add a route to one or more of their VPC route tables that point to the IP address range of the other VPC (the peer VPC).
4. Update the security group rules that are associated with your instance to ensure traffic to and from the peer VPC is not restricted. 
### Cross-Account Migration
![[Pasted image 20211009212625.png]]
- RDS Creates a storage volume snapshot of your DB instance. When you create a DB snapshot, you need to identify which DB instance you are going to back up, and then give your DB snapshot a name so you can restore from it later.
- When you create an encrypted DB instance, you can also supply the KMS key identifier for your encryption key. If you don't specify a KMS key identifier, Amazon RDS uses your default encryption key for your new DB instance.
- Use AWS DMS to replicate ongoing changes and to keep the source and target databases in sync.
## Investigating DMS Tasks
![[Pasted image 20211009212850.png]]
### Slow DMS Tasks
- Inadequate resources allocated to the DMS replication instance is a primary reason for slow DMS tasks.
- Check your replication instance's use of CPU, memory, swap files, and IOPS.
- IOPS solutions:
	- Increase IOPs for your replication instance
	- split tasks across multiple replication instances

- **How you can increase speed:**
	- for an RDS DB instance, disable Multi-AZ for the target DB instance.
	- Turn off any automatic backups
	- Turn off logging on the target database.
	- Use provisioned IOPS if available
	- Make sure that the task is optimized for LOB migration.


### DMS Network Issues
- What's the most common issue? Have you set up the proper egress on your security group for the DMS replication instance
	- Make sure to give egress to the source and target endpoints
- Does the security group used by the endpoints have ingress on the database port from the replication instance?
- What if you are using an Internet Gateway and the source endpoint is outside the VPC used by the replication instance? 
	- Edit the VPC security to include routing rules that send traffic to the IGW
- What if you are using an NAT Gateway used by the replication instance?
	- Configure the NAT Gateway using a single elastic IP address bound to a single elastic network interface
### Other DMS Issues
#### Load of a Schema Fails
- What if you get the error:
	- `Operation:getSchemaListDetails:errType=,status=0, errMessage=,errDetails=`.
- Make sure the user account used by AWS DMS to connect to the source endpoint has the necessary permissions.

#### Foreign Keys and Secondary Indexes are missing
- Important: DMS doesn't create secondary indexes, non-primary key constraints, or data defaults
- How to mitigate secondary objects?
	- Use the database's native tools if you migrating to the same database engine as your source database
	- Use the AWS Schema Conversion Tool (AWS SCT) if you are migrating to a different database engine
### CDC Stuck after Full Load
- AWS DMS settings can conflict with each other. This could cause slow or stuck replication changes
- Full table scans can affect performance. If you haven't created primary or unique keys on the target tables, full scans will occur.
# Monitoring and Optimization
## Improving Database Performance Using ElastiCache
### What is Elasticache?
- AWS ElastiCache is a web service used to deploy and run Memcached or Redis (both products exist outside AWS) server nodes
- Think of Elasticache as an AWS Managed wrapper for Memcached and Redis
- Improves performance by retreiving information from a fast, managed, in-memory system.
- Offloads the management, monitoring, and operation of in-memory environments.
### Elasticache Nodes, Shards, and Clusters
- A node is the smallest building block of an AWS ElastiCache deployment. It is RAM stored in a fixed size.
- Each node runs Memcached or Redis and has its own DNS name and port. Multiple types of nodes are supported, each with varying amounts of associated memory.
- A redis shard is a subset of the cluster's keyspace, that can include a primary node and zero or more read-replicas.
	- This concept is very similar to RDS read replicas
- The shards add up to form a cluster.
- ![[Pasted image 20211009214950.png]]

### Memcached
- ElastiCache for Memcached features:
	- automatica detection and recovery from cache node failures
	- Automatica discovery of nodes within a cluster
	- Flexible AZ placement of nodes and clusters
	- Integration with other AWS services such as EC2, CloudWatch, CloudTrail, and Amazon SNS.
	- Memcached is the simpler of the two options.

### Redis
- ElastiCache for Redis features:
	- Automatic recovery from cache node failures
	- Multi-AZ for a failed primary cluster to a read replica.
	- Redis (cluster mode enabled) supports partitioning your data across up to 90 shards.
	- Memcached = simple, Redis = complex
## Leveraging Performance Insights
### AWS RDS Performance Insights Overview
- How do you pinpoint performance bottlenecks?
	- Use Performance insights to quickly assess the load on your DB, and determine when and wehre to take action
- Use the performance insights dashboard to easily visualize database load and detect performance problems.
### Enabling Performance Insights
- To use performance insights, enable it on your DB instance.
- PI can be enabled and disabled without causing downtime, a reboot, or a failover
- The PI agent is lightweight and consumes limited CPU and memory on the DB host
- if DB load is high, the PI agent collects data less frequently
### PI Dashboard
- Contains database performance information to help you Analyze and troubleshoot performance issues using dashboard information
- On the main dashboard page, you can view the information about the database load
- You can also drill into details for a particular wait state, SQL query, host, or user.
### Performance Insights Metrics to CloudWatch
- Performance insights automatically publishes metrics to CloudWatch
- You can query data from PI, but having the PI metrics in CloudWatch enables incorporation of CloudWatch Alarms
- Metrics include, DBLoad, DBLoadCPU, DBLoadNonCPU.
### PI API
- Programatically retrieve PI data for RDS instance
- Use the API to offload data into a database, add PI data to existing monitoring dashboards, or build monitoring tools.
- Performance Insight Operations:
	- DescribeDimensionKeys
	- GetResourceMetrics
- AWS CLi command
	- aws pi describe-dimension-keys
		- Retrieves the top N dimension keys for a metric for a specific time period
	- aws pi get-resource-metrics
		- Retrieves PI metrics for a set of data sources, over a time period
## CloudWatch Logs
- Publish logs to CloudWatch for storage and further analysis
### IAM
- CloudWatch logs primary resources are: log groups, log streams, and destinations
- Resources that are created in an account are owned by that account.
- A permissions policy is used to describe who has access to which resources in the account
- When you grant. auser the `cloudwatch:PutInsightRule` and `cloudwatch:GetInsightRuleReport` permissions, that user can create a rule that evaluates any log group in CloudWatch logs and then see the results
### Log Filtering
- Prior to searching and filtering the log data using one or more metric filters, the CloudWatch logs agent must begin pubishing log data to CloudWatch.
- Metric filters define the terms and patterns to look for in log data as it is sent to CloudWatch logs. An example would be searching for a specific error cide.
- You can turn log data into numerical CloudWatch metrics that you can graph or set an alarm on.
## Trusted Advisor
### Cost Optimization
- Trusted Advisor tools provides real time guidance to help you provisio your resources following AWS best practices
- save money by using cost optimization to eliminate unused and idle resources or by making unnecessary commitments to reserved capacity
- What does Cost Optimization report on for databases?
	- ![[Pasted image 20211009221107.png]]

### RDS Backup
- One of the five categories in Trusted Advisor is fault tolerance
- Trusted Advisor Fault Tolerance can increase the availability and redundancy of your AWS application by taking advantage of auto scaling, health checks, multi AZ, and backup capabilities
- Fault Tolerance reports on the existence of backups. It also checks for automated backups of RDS DB instances. Backups are enabled with a retention period of 1 day by default. Backups reduce the risk of unexpected data loss and allow for PITR.
### Utilization
- Trusted Advisor can point out under utilized resources:
	- Inspects EBS volumec onfig for underused volumes. Create a snapshot of the udnerused volumes and delete them to reduce your costs.
	- Utilization can check Amazon Redshift for underused clusters. You can create a snapshot of the cluster and shut it down. You can also choose to downsize the cluster.
## CloudWatch Application Insights
## Advanced Audit Logging
## Deploying with CloudFormation
# Conclusion
## Review Checklist

> [!quote]
>"Everything fails, all the time." - Werner Vogels, CTO of AWS
>(There's some variation or reiteration of this quote everywhere)

Failure should not be thought of as an unlikely aberration. Instead it should be assumed that failures, both large and small, can, and will, occur. A failure can be categorized as 1 of 3 types:
- small scale event (a single server stopped responding)
- large scale event (multiple resources, possibly across a Region)
- colossal scale event (large number, widespread)
### Avoiding and Planning for Disaster
###### High availability
- Minimize how often your applications and data become unavailable.
- Provide redundancy and fault tolerance
###### Backup
- Make sure your data is safe in case of disaster.
- Can be a challenge to implement depending on which pace data is generated.
###### DR - Disaster Recovery
- Recover your data and get your applications back online after a disaster.
- Set of policies and procedures that enable the recovery or continuation of vital technology.
### AWS Well-Architected Framework Principles
##### [[Operational Excellence Pillar]]
States the importance of anticipating failure.
- **Anticipate failure**
- **Refine operational procedures frequently**
##### [[Reliability Pillar]]
Describes the important of designing your systems.
- **Test recovery procedures**
- **Automatically recover from failure.**
## Recovery
Organizations of all sizes, large and small, often have a *Business Continuity Plan* (BCP). A typical part of the BCP is to provide for IT Service Continuity, including IT disaster recovery planning.
##### #RPO: Recovery Point Objective
The maximum *acceptable amount of data loss*, measured in time.
- How often must your data be backed up?
To calculate RPO:
1. Determine how much data loss is acceptable, according to your BCP.
2. Figure out how quickly that data loss might occur, as a time measurement.

![[recovery-point.jpg|600]]
##### #RTO: Recovery Time Objective
The maximum *acceptable amount of time* after a disaster strikes that a business process can remain out of commission.
- How quickly must your applications and data be recovered?
![[recovery.jpg|600]]

##### Creating a DR Strategy with RTO and RPO
![[disaster-recovery.jpg]]
### Plan for Disaster Recovery
To properly scope your disaster recovery planning, you must look holistically at your use of AWS. If a disaster occurs, your RPO and RTO will guide your backup-and-restore plans and procedures across each of these service areas.
### #Resiliency
![[resiliency-math.jpg|500]]
Availability = Available for Use Time / Total Time = MTBF / MTBF + MTTR
- MTBF: Mean Time Between Failures
- MTTR: Mean Time to Recover
Easier formula when not using a time-based approach: Availability = Successful Responses / Valid Requests
### Active/Passive DR
![[active-passive.jpg|400]]
The workload operates from a single site and all requests are handled from this active Region.
### Active/Active DR.
![[active-active.jpg|400]]
Two or more Regions are actively accepting requests and data is replicated between them
## AWS #DataSync
![[icon_DataSync.png]]
Provides movement of large amounts of data online between on-premises storage and Amazon S3, EFS, or FSx. It supports scripted copy jobs and scheduled data transfers from on-premises NFS and Server Message Block (SMB) storage. It can also optionally use AWS Direct Connect links.
##### Protocols compatibility
- NFS: Network File System
- SMB: Server Message Block
- HDFS: Hadoop Distributed File Systems
- Object storage
##### Works with other cloud storage services
- Google Cloud Storage
- Microsoft Azure Blob and File Storage
- DigitalOcean Spaces
- Oracle Cloud Infrastructure Object Storage
- Cloudflare R2 Storage
- Backblaze B2 Cloud Storage
- (and more)
##### S3 Cross-Replication
For critical applications and scenarios, it's best to configure S3 cross-Region replication. To enable the replication, you add a replication configuration to your source bucket. The minimum configuration must indicate the destination bucket where you want Amazon S3 to replicate all objects, or a subset of objects. You must also include an IAM role that grants Amazon S3 permissions to copy the objects to the destination bucket.
Copied objects retain their metadata. The destination bucket can belong to another storage class.
##### EBS Volume Snapshots
You can back up the data that is on EBS volumes to Amazon S3 by taking point-in-time snapshots. Snapshots are incremental backups, which means that it saves only the blocks on the device that have changed since your most recent snapshot.
Each snapshot contains all the information that is needed to restore your data to a new EBS volume.
You can use the Amazon Data Lifecycle Manager to automate the creation, retention, and deletion of snapshots that back up your EBS volumes. Automating snapshot management helps to:
- Protect valuable data by enforcing a regular backup schedule.
- Retain backups as required by auditors or internal compliance.
- Reduce storage costs by deleting outdated backups.
Instance store volumes provide temporary block-level storage that works well for information that changes frequently, such as buffers, caches, and scratch data.
##### File System Replication
AWS DataSync makes data move faster between two EFS or Amazon FSx Windows File Server file systems, or between on-premises storage and AWS file storage.
### Compute Disaster Recovery
By launching instances in separate Availability Zones, you can protect your applications from the failure of a single location.
You can arrange for automatic recovery of an EC2 instance when a system status check of the underlying hardware fails. AMIs are preconfigured with OSes, and some preconfigured AMIs might also include application stacks. You can also configure your own custom AMIs. In the context of DR, AWS recommends that you configure and identify your own AMIs so that they launch as part of your recovery procedure.
##### Strategies for Compute Disaster Recovery
- Use the Amazon EC2 snapshot capability for backups.
	- Snapshots can be performed manually or scheduled.
- Use system or instance level system backups infrequently and as a last resort.
	- Drives up the cost of storage that is used quickly.
	- Prefer automated rebuild from configuration or code repositories instead.
- Cross-Region AMI copies.
- Cross-Region snapshot copies.
- Consider transient compute architectures.
	- Store essential data off the instance.
##### Networking: Design for resilience, recovery
- Amazon 53 provides load balancing and network routing capabilities that enable you to distribute network traffic. It also provides the ability to fail over between multiple endpoints and even to a static website that is hosted in Amazon S3.
- Elastic Load Balancing service automatically distributes incoming application traffic across multiple EC2 instances. It enables you to achieve fault tolerance in your applications by providing the load-balancing capacity that is needed in response to incoming application traffic. You can pre-allocate a load balancer so that its DNS name is already known.
- You can use Amazon VPC to extend an existing on-premises network topology to the cloud.
- AWS Direct Connect simplifies the setup of a dedicated network connection from an on-premises data center to AWS.
##### Databases: Features that support recovery
[[Amazon RDS]]
- Take snapshot data and save it in a separate Region.
- Combine read replicas with Multi-AZ deployments to build a resilient disaster recovery strategy.
- Retain automated backups.
- Consider using Amazon RDS in the DR preparation phase to store a copy of your critical data in a database that is already running. Then use RDS in the DR recovery phase to run your production database.
Amazon [[DynamoDB]]
- Back up entire tables in seconds
- Use point-in-time-recovery to continuously back up tables for up to 35 days.
- Initiate backups with a single click in the console or a single API call.
- Use Global Tables to build a multi-region, multi-master database that provides fast local performance for massively scaled globally distributed applications.
##### Automation services: Quickly replicate or redeploy environments
###### AWS CloudFormation
- Use templates to quickly deploy collections of resources as needed
- Duplicate production environments in new Region or VPC in minutes.
###### AWS Elastic Beanstalk
- Quickly redeploy your entire stack in only a few clicks
###### AWS OpsWorks
- Automatic host replacement
- Combine it with AWS CloudFormation in the recovery phase.
- Provision a new stack that supports the defined RTO.
# Common Disaster Recovery Patterns on AWS
- Backup and Restore
- Pilot Light
- Warm Standby
- Multi-site
![[disas-recov-strategies.jpg]]
### Backup and Restore Pattern
![[backup-restore.jpg]]
- Back up configuration and state data to S3.
- Implement lifecycle policy to save on cost.
- Restore when needed.
Checklist:
- Preparation phase:
	- create backups of current systems
	- store backups in Amazon S3
	- document procedure to restore from backups
- Know:
	- Which AMI to use, and build as needed
	- How to restore system from backups
	- How to route traffic to the new system
	- How to configure the deployment
- In case of disaster:
	- Retrieve backups from Amazon S3
	- Restore required infrastructure
	- Restore system from backup
	- Route traffic to new system
### Pilot Light Pattern
![[pilot-light.jpg]]
- Describes a disaster recovery pattern where a minimal backup version of your environment is always running. Analogous to a gas heater where a small flame is always on, even when the heater is off.
- Works like a backup and restore, but recovery time is typically faster, because the core pieces of the system are already running and up-to-date.
- Relatively inexpensive to implement.
In case of disaster:
- You quickly commission the compute resources to run the application or to orchestrate the failover to pilot light resources in AWS. The secondary database stores critical data.
- The primary environment can exist in an on-premises data center, or in another Region or AZ on AWS. You can use the pilot light pattern to meet your recovery time object (RTO).
Checklist:
- Preparation phase:
	- Configure EC2 instances to replicate or mirror servers.
	- Ensure that all supporting custom software packages are available on AWS
	- Create and maintain AMIs of key servers where fast recovery is needed.
	- Regularly run these servers, test them, and apply any software updates and configuration changes.
	- Consider automating the provisioning of AWS resources.
- In case of disaster:
	- Automatically bring up resources around the replicated core dataset.
	- Scale the system as needed to handle current production traffic.
	- Switch over to the new system.
### Warm Standby
![[warm-standby.jpg]]
- Like the pilot light pattern, but more resources are already running. The term warm standby describes a disaster recovery scenario where a scaled-down version of a fully functional environment is always running the cloud.
Preparation:
- All necessary components running 24/7, but not scaled for production traffic.
- Continuous testing.
In case of disaster:
- If the primary environment is unavailable, Amazon Route 53 switches over to the secondary system.
- The secondary system then scales up to handle production load.
### Multi-site pattern
![[multisite.jpg]]
With this pattern, you have a fully functional system that runs in a second Region of AWS. It runs at the same time as the on-premises systems or the systems that run in a different AWS Region.
- A multi-site solution runs in an active-active configuration. The data replication that you employ is determined from the recovery point that you choose.
Preparation:
- Similar to warm standby
- Configured for full scaling in or scaling out for production load
In case of disaster:
- Immediately fail over all production load.
###### AWS Services
All of the AWS services covered under backup and restore, pilot light, and warm standby also are used here for point-in-time data backup, data replication, active/active traffic routing, and deployment and scaling of infrastructure including EC2 instances.
For active/passive scenarios discussed earlier, both Amazon Route 53 and AWS Global Accelerator can be used for route network traffic to the active region.
For the active/active strategy here, both of these services also enable the definition of policies that determine which users go to which active regional endpoint.
###### [Amazon Aurora global database](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database.html)
Uses dedicated infrastructure that leaves your databases entirely available to serve your application, and can replicate to up to five secondary Region with typical latency of under a second. With active/passive strategies, writes occur only to the primary Region.
###### [AWS CloudFormation StackSets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/what-is-cfnstacksets.html)
Extends this functionality by enabling you to create, update, or delete CloudFormation stacks across multiple account and Regions with a single operation. AWS CloudFormation uses YAML or JSON to define IaC, AWS CDK (Cloud Development Kit) allows you to define infrastructure as Code using familiar programming languages.
## [AWS Elastic Disaster Recovery Service](https://aws.amazon.com/disaster-recovery/) (DRS)
![[icon_DRS.png]]
AWS Elastic DRS continuously replicates server-hosted applications and server-hosted database from any source into AWS using block-level replication of the underlying server. It can also be used for disaster recovery of AWS hosted workloads if they consist only of applications and databases hosted on EC2.
![[aws-drs.jpg]]
## AWS Storage Gateway
![[icon_storagegateway.png]]
AWS Storage Gateway is a hybrid storage service that enables your on-premises applications to use AWS Cloud storage. You can use the service for backup and archiving, disaster recovery, cloud data processing, storage tiering, and migration.
Your applications connect to the service through a virtual machine or hardware gateway appliance by using standard storage protocols. These protocols include NFS, SMB, Virtual Tape Library (VTL), and Internet Small Computer System Interface (iSCSI). The gateway connects to AWS storage services - such as Amazon S3, Amazon S3 Glacier, and Amazon EBS.
With a file gateway, you store and retrieve objects in Amazon S3.
![[storagegateway.jpg]]

##### Further Reading
- PDF: [Disaster Recovery Workloads Whitepaper](https://docs.aws.amazon.com/pdfs/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-workloads-on-aws.pdf#disaster-recovery-workloads-on-aws) 
- AWS Blog: [DR Architecture on AWS Part I](https://aws.amazon.com/blogs/architecture/disaster-recovery-dr-architecture-on-aws-part-i-strategies-for-recovery-in-the-cloud/)
- [Scheduling automated backups using Amazon EFS and AWS Backup](https://aws.amazon.com/blogs/storage/scheduling-automated-backups-using-amazon-efs-and-aws-backup/)
- Developer Guide: [What is AWS Backup?](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html)
- See also: PDF: [AWS Storage Gateway User Guide](https://docs.aws.amazon.com/pdfs/storagegateway/latest/vgw/storagegateway-vgw-ug.pdf#WhatIsStorageGateway)

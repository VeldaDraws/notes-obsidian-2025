## Storage Types
![[object-vs-block-storage.jpg|400]]
AWS storage services are grouped into 3 categories: file storage, block storage, and object storage.
- File storage: Data is stored as files in a hierarchy
	- Uses: Web serving, analytics, media, home directories.
- Block storage: data is stored in fixed-size blocks.
	- Uses: Transactional workloads, containers, VMs.
- Object storage: data is stored as objects in buckets.
	- Uses: Data archiving, backup and recovery, rich media files.

# Amazon S3
![[icon_s3.png|50]]
![[S3.jpg]]
Amazon S3 is an object storage service. Object storage stores data in a flat structure. An object is a file combined with metadata. You can store as many of these objects as willing.
- You store your objects in containers called **buckets**.
- When you store an object in a bucket, the combination of a bucket name, key, and version ID unique identifies the object.
- When you create the bucket, you specify at the minimum the *bucket name* and the *AWS Region*.
	- Each bucket name must be *unique across all AWS accounts in all Regions within a partition*.
	- A partition in this case is a grouping of Regions.
		- Standard Regions
		- China Regions
		- AWS GovCloud
- Bucket Naming Rules:
	- Between 3 and 63 characters long.
	- Only lowercase letters, numbers, dots, and hyphens.
	- Must begin and end with a letter or number.
	- *Cannot* be formatted as an IP address.
	- A bucket name cannot be used by another AWS account in the same partition until the bucket is deleted.
##### Object Key Names
![[bucket-key-name.jpg|400]]
The object key (key name) uniquely identifies the object in an Amazon S3 bucket. When you create an object, you specify the key name.
```
http://bucket_name.s3.amazonaws.com/prefix/object_key

http://testbucket123.s3.amazonaws.com/2022-01-01/adorable_cat_photo.jpg
```
🎯Amazon S3 supports buckets and objects, and there is no hierarchy. However, by using prefixes and delimiters in an object key name, the Amazon S3 console and the AWS SDKs are able to infer hierarchy and introduce the concept of folders.
### S3 Security
🎯***Everything in Amazon S3 is private by default.*** This means that all Amazon S3 resources, such as buckets and objects, can only be viewed by the user or AWS account that created that resource. Amazon S3 resources are all private and protected to begin with.
- Amazon S3 provides several security management features: IAM policies, S3 bucket policies, and encryption to develop and implement your own security policies.
- When IAM policies are attached to your resources (buckets and objects) or IAM users, groups, and roles, the policies define which actions they can perform
You should use IAM policies for private buckets in the following scenarios:
- You have many buckets with different permission requirements. Instead of defining many different S3 bucket policies, you can use IAM policies.
- You want all policies to be in a centralized location. By using IAM policies, you can manage all policy information in one location.
##### Amazon S3 Bucket Policies
Like IAM policies, S3 bucket policies are defined in a JSON format. The policy that is placed on the bucket applies to every object in that bucket.
S3 bucket policies specify what actions are allowed or denied on the bucket.
##### Amazon S3 Encryption
Reinforces encryption in transit and at rest.
Encryption in Transit:
- SSL/TLS
Server Side Encryption (SSE) - Encryption at rest:
- SSE-AES (AES-256)
- SSE-KMS (AWS KMS)
- SSE-C (customer provided key)
Client-Side Encryption
- You encrypt your own files before uploading them to S3.
##### Pre-signed URLs
You can generate a URL which provides you temporary access to an object to either upload or download object data. Commonly used to provide access to private objects. You can use AWS CLI or SDK to generate.
Example use: You have a web application which needs to allow users to download files from a password-protected part of your web-app. Your web-app generates a pre-signed URL which expires after 5 seconds.
### S3 Storage Classes
| **Storage Class**                                  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **S3 Standard**                                    | This is considered general-purpose storage for cloud applications, dynamic websites, content distribution, mobile and gaming applications, and big data analytics.                                                                                                                                                                                                                                                                                                                                                                           |
| **S3 Intelligent-Tiering**                         | This tier is useful if your data has unknown or changing access patterns. S3 Intelligent-Tiering stores objects in three tiers: a frequent access tier, an infrequent access tier, and an archive instance access tier. Amazon S3 monitors access patterns of your data and automatically moves your data to the most cost-effective storage tier based on frequency of access.                                                                                                                                                              |
| **S3 Standard-Infrequent Access (S3 Standard-IA)** | This tier is for data that is accessed less frequently but requires rapid access when needed. S3 Standard-IA offers the high durability, high throughput, and low latency of S3 Standard, with a low per-GB storage price and per-GB retrieval fee. This storage tier is ideal if you want to store long-term backups, disaster recovery files, and so on.                                                                                                                                                                                   |
| **S3 One Zone-Infrequent Access (S3 One Zone-IA)** | Unlike other S3 storage classes that store data in a minimum of three Availability Zones, S3 One Zone-IA stores data in a single Availability Zone, which makes it less expensive than S3 Standard-IA. S3 One Zone-IA is ideal for customers who want a lower-cost option for infrequently accessed data, but do not require the availability and resilience of S3 Standard or S3 Standard-IA. It's a good choice for storing secondary backup copies of on-premises data or easily recreatable data.                                        |
| **S3 Glacier Instant Retrieval**                   | Use S3 Glacier Instant Retrieval for archiving data that is *rarely* accessed and requires millisecond retrieval. Data stored in this storage class offers a cost savings of up to 68 percent compared to the S3 Standard-IA storage class, with the same latency and throughput performance.                                                                                                                                                                                                                                                |
| **S3 Glacier *Flexible Retrieval***                | S3 Glacier Flexible Retrieval offers low-cost storage for archived data that is **accessed 1 to 2 times per year**. With S3 Glacier Flexible Retrieval, your data can be accessed in as little as *1 to 5 minutes* using an expedited retrieval. You can also request free bulk retrievals in up to *5 to 12 hours*. It is an ideal solution for backup, disaster recovery, offsite data storage needs, and for when some data occasionally must be retrieved in minutes.                                                                    |
| **S3 Glacier Deep Archive**                        | S3 Glacier Deep Archive is the lowest-cost Amazon S3 storage class. It supports long-term retention and digital preservation for data that might be accessed once or twice a year. Data stored in the S3 Glacier Deep Archive storage class has a *default retrieval time of 12 hours*. It is designed for customers that retain data sets for *7 to 10 years or longer*, to meet regulatory compliance requirements. Examples include those in highly regulated industries, such as the financial services, healthcare, and public sectors. |
| **S3 on Outposts**                                 | Amazon S3 on Outposts delivers object storage to your on-premises AWS Outposts environment using S3 API's and features. For workloads that require satisfying local data residency requirements or need to keep data close to on premises applications for performance reasons, the S3 Outposts storage class is the ideal option.                                                                                                                                                                                                           |
### S3 Versioning
Versioning keeps multiple versions of a single object in the same bucket. This preserves old versions of an object without using different names, which helps with object recovery from accidental deletions, accidental overwrites, or application failures.
![[versioning.jpg|350]]
By using versioning-enabled buckets, you can recover objects from accidental deletion or overwrite.
Three categories of versioning:
- Unversioned (default)
- Versioning-enabled: Enabled for all objects in the bucket, can never returned to an unversioned state, only suspended versioning.
- Version-suspended: Versioning is suspended for new objects. All new objects in the bucket will not have a version. All existing objects will keep their object versions.
### Managing Storage Lifecycle
When you define a lifecycle config for an object or group of objects, you can choose to automate between two types of actions: transition and expiration.
- Transition actions: Define when objects should transition to another storage class.
- Expiration actions: Define when objects expire and should be permanently deleted.
Use cases:
- Periodic logs: May need for a week or a month.
- Data that changes in access frequency: May need to cold storage after a period of time.
# S3 CheatSheet
![[s3-cheatsheet.jpg]]
![[s3-cheatsheet-2.jpg]]
# [Amazon EBS](https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html)
![[inst-store-vs-ebs.jpg|450]]
Amazon Elastic Block Store (Amazon EBS) is block-level storage that you can attach to an Amazon EC2 instance. The attachable storage is referred to as an EBS volume.
##### Use Cases:
- OSs: The root device for an instance launched from AMI is typically an EBS volume and referred to as EBS-backed AMIs.
- Databases: As a storage layer for databases running on Amazon EC2 that will scale with your performance needs and provide consistent and low-latency performance.
- Enterprise applications: Provides high availability and high durability block storage to run business-critical applications.
- Big data analytics engines: Amazon EBS offers data persistence, dynamic performance adjustments, and the ability to detach and reattach volumes.
#### EBS Volume Types
###### SSDs
Used for transactional workloads and frequent read/write operations with small I/O size.

| General Purpose SSD Volumes                                                                | Provisioned IOPS SDD Volumes                                            |
| ------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| gp3. gp2                                                                                   | io2, io2 Block Express, io1                                             |
| Provides a balance of price and performance for a wide variety of transactional workloads. | Provides high-performance SSD designed for latency-sensitive workloads. |
| EBS Multi-Attach not supported.                                                            | EBS Multi-Attach supported.                                             |
| Size: 1GiB to 16 TiB                                                                       | io1: 4 GiB to 16 TiB                                                    |
|                                                                                            | io2 Block Express: 4 GiB to 64 GiB                                      |
###### HDDs
Used for large streaming workloads that need high throughput performance.

| Throughput Optimized HDD volumes                                      | Cold HDD volumes                                                     |
| --------------------------------------------------------------------- | -------------------------------------------------------------------- |
| st1                                                                   | sc1                                                                  |
| A low cost HDD for frequently access, throughput-intensive workloads. | The lowest cost HDD designed for less frequently accessed workloads. |
| Max IOPS per volume: 500                                              | 250                                                                  |

>[!info]
>AWS announced the Amazon EBS multi-attach feature that permits Provisioned IOPS SSD (io1 or io2) volumes to be attached to multiple EC2 instances at one time. This feature is not available for all instance types, and all instances must be in the same Availability Zone.

> [!note]
> All io2 volumes created after November 21, 2023 are io2 Block Express volumes. io2 volumes created before that date can be converted to io2 Block Express volumes by modifying the IOPS or size of the volume.

### EBS Snapshots
EBS snapshots are incremental backups that only save the blocks on the volume that have changed after your most recent snapshot. When you take a snapshot of your volume, the backups are stored in multiple AZs using Amazon S3. You manage them in the Amazon EBS console, which is part of the Amazon EC2 console.
# Amazon EFS
![[icon_EFS.jpg|50]]
Amazon Elastic File System (Amazon EFS) is a set-and-forget file system that automatically grows and shrinks as you add and remove files. There is no need for provisioning or managing storage capacity and performance. Amazon EFS can be used with AWS compute services and on-premises resources.

| Standard storage classes  | One zone storage classes |
| -- | -- |
|EFS Standard and EFS Standard-Infrequent Access (Standard-IA) offer Multi-AZ resilience and the highest levels of durability and availability.|EFS One Zone and EFS One Zone-Infrequent Access (EFS One Zone-IA) provide additional savings by saving your data in a single availability zone.|
## Amazon FSx
![[icon_FSx.jpg|50]]
Amazon FSx is a fully managed service that offers reliability, security, scalability, and a broad set of capabilities that make it convenient and cost effective to launch, run, and scale high-performance file systems in the cloud. With Amazon FSx, you can choose between four widely used file systems: Lustre, NetApp ONTAP, OpenZFS, and **Windows File Server**.

| **File System**                        | **Description**                                                                             |
| -------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Amazon FSx for NETAPP ONTAP**        | Fully managed shared storage built on the NetApp popular ONTAP file system                  |
| **Amazon FSx for OpenZFS**             | Fully managed shared storage built on the popular OpenZFS file system                       |
| **Amazon FSx for Windows File Server** | Fully managed shared storage built on Windows Server                                        |
| **Amazon FSx for Lustre**              | Fully managed shared storage built on the world's most popular high-performance file system |
# AWS Snowball
![[aws-snowball-overview.jpg]]
- Data transfers must be completed within 90 days of snowball being prepared.
- 50 TB or 80 TB
- 256-bit encryptions
- TPM
# AWS Snowball Edge
![[aws-snowball-edge-overview.jpg]]
- Can cluster in groups of 5 or 10 devices
- Three options
	- Storage Optimized (24 vCPUs)
	- Compute Optimized (54 vCPUs)
	- GPU optimized (54 vCPUs)
- 100 TB or 100TB Clustered (45TB per node)
# AWS Snowmobile
![[aws-snowmobile-overview.jpg]]
- Transfer up to 100PB
- GPS tracking, alarm monitoring, security surveillance with optional escort.
# Snowball Family Cheatsheet
![[snowball-cheatsheet.jpg]]
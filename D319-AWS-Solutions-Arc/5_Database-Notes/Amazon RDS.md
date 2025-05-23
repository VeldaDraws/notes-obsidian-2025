# [Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
![[AmazonRDS-Arch-example.jpg|400]]

Summary Page: [[Databases#RDS]]

Amazon RDS is a managed database service customers can use to create and manage relational databases in the cloud without the operational burden of traditional database management. You can offload some of the unrelated work of creating and managing a database and focus on the the tasks that differentiate your application.
##### Amazon RDS (RDBMS) DB Engines
Amazon RDS supports the following:
- IBM Db2
- MariaDB
- Microsoft SQL Server
- MySQL
- Oracle Database
- PostgreSQL
- [[Amazon Aurora]]
#### Amazon RDS Instance Types
Support for Amazon RDS features varies across AWS Regions and specific versions of each DB engine.
A DB instance class determines the computation and memory capacity of a DB instance. A DB instance class consists of both the DB instance class type and size.
- Standard classes: m classes
- Memory optimized classes: r and x classes
- Burstable classes: t classes
Underneath the DB instance is an EC2 instance, but it is managed through the Amazon RDS console instead of the EC2 console.
#### Storage on Amazon RDS
The storage portion of DB instances for Amazon RDS use Amazon EBS volumes for database and log storage, with the exception of Amazon Aurora, which is stored in cluster volumes.
- General Purpose SSD: gp2, gp3
- Provisioned IOPS: io1
- Magnetic: standard
#### VPC and Multi-Availability Zones
When you create a DB instance, you select the VPC your database will live in, and then can select the subnets that will be designated for your DB. This is called a DB subnet group, and has at least two Availability Zones in its Region.
In an Amazon RDS Multi-AZ deployment, Amazon RDS creates a redundant copy of your database in another Availability Zone. You end up with two copies of your database—a primary copy in a subnet in one Availability Zone and a standby copy in a subnet in a second Availability Zone.
![[RDS-Multi-AZ.jpg]]
Further Reading: [Configuring and managing a Multi-AZ deployment for Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)
### Amazon RDS Backup
You can use automated backups or manual snapshots to avoid losing your data.
##### Automated Backups
Turned on by default. Backs up your entire DB instance and transaction logs.
- Retaining backups: Between 0 and 35 days. (Note: 0 days setting stops automated backups from happening)
- Point-in-time recovery: Creates a new DB instance using data restored from a specific point in time.
##### Manual Snapshots
If you want to keep your automated backups longer than 35 days, use manual snapshots. Manual snapshots are similar to taking Amazon EBS snapshots, except you manage them in the Amazon RDS console.
### Amazon RDS Security
When it comes to security in Amazon RDS, you have control over managing access to your Amazon RDS resources, such as your databases on a DB instance.
If you want to restrict the actions and resources others can access, you can use AWS IAM policies.
You can also use security groups to control which IP addresses or EC2 instances can connect to your DB.
##### Further Reading:
- [Security in Amazon RDS](https://docs.aws.amazon.com//AmazonRDS/latest/UserGuide/UsingWithRDS.html)

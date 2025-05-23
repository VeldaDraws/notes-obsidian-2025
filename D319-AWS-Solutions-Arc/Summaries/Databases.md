# RDS
![[Amz-RDS-overview.png]]
- Relational Database Service (RDS) is the AWS solution for relational databases.
- Managed by AWS, (you cannot SSH into the VM running the database).
- There are 6 database options:
	- Aurora
	- MySQL
	- MariaDB
	- Postgres
	- Oracle
	- Microsoft SQL Server
- Multi-AZ is an option that you can turn on which makes an exact copy of your database into another AZ that is only on standby
	- Multi-AZ automatically synchronizes changes in the database over to the standby copy
	- Automatic Failover protection if one AZ goes down failover will occur and the standby slave will be promoted to master.
- Read-Replicas allow you to run multiple copies of your database, these copies only allow reads (no writes). Read-Replicas use Asynchronous replication
	- You must have automatic backups enabled to use Read Replicas. You can combine Read Replicas with Multi-AZ
	- Up to 5 read replicas.
	- Replicas can be promoted to their own database, but this breaks replication.
	- You can have Replicas of Read Replicas.
- RDS has 2 backup solutions: Automated Backups and Database Snapshots.
	- Automated Backups: You choose a retention period between 1 and 35 days. There is no additional cost for backup storage, you define your backup window.
	- Manual Snapshots: You manually create backups, if you delete your primary the manual snapshots will still exist and can be restored.
	- When you restore an instance it will create a new database. You just need to delete your old database and point traffic to new restored database.
- You can turn on encryption at-rest for RDS via KMS.
## Aurora
![[amz-aurora-overview.png]]
- Fully-managed Postgres or MySQL database that scales, automatic backups, high availability, and fault tolerance.
- Aurora MySQL is 5x faster than regular MySQL.
- Aurora Postgres is 3x faster over regular Postgres
- Aurora is 1/10 the cost over its competitors with similar performance and availability options.
- Aurora replicates **6 copies** for your database across **3 availability zones**.
- Aurora is allowed up to **15 Aurora Replicas**.
- An Aurora database can span multiple regions via Aurora Global Database.
- Aurora Serverless allows you to stop and start Aurora and scale automatically while keeping costs low.
- Aurora Serverless is ideal for new projects or projects with infrequent database usage.
## DynamoDB
- Fully managed NoSQL key/value and document database.
- Applications that contain large amounts of data but require predictable read and write performance while scaling is a good fit for DynamoDB
- DynamoDB scales with whatever read and write capacity you specify per second.
- DynamoDB can be set to have Eventually Consistent Reads (default) and Strongly Consistent Reads.
- Eventually Consistent Reads data is returned immediately but data can be inconsistent. Copies will be generally consistent in 1 second.
- Strongly Consistent Reads will wait until data is consistent. Data will never be inconsistent but latency will be higher. Copies of data will be consistent with a guarantee of 1 second.
- DynamoDB stores 3 copies of data on SSD drives across 3 regions.
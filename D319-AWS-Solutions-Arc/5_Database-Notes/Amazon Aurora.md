> [!info]
> Complete user guide as a PDF (4000+ pages long, sorry): https://docs.aws.amazon.com/pdfs/AmazonRDS/latest/AuroraUserGuide/aurora-ug.pdf#CHAP_AuroraOverview
> Docs: [How Aurora Serverless v2 works](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.how-it-works.html#aurora-serverless-v2.parameters)
> freeCodeCamp follow-along demo of creating an Aurora cluster: https://youtu.be/c3Cn4xYfxJY?si=WXVQe2wT2DeYDzAs&t=155303
> freeCodeCamp follow-along demo of Aurora Serverless v2: https://youtu.be/c3Cn4xYfxJY?si=J9YxLQxJm5VBW5Xo&t=156322
# Amazon Aurora
![[icon_AmAurora-wtr.png]] ![[icon_amAurora-solid.png|48]]
Summary Page: [[Databases#Aurora]]

Fully managed relational database engine compatible with MySQL and PostgreSQL.
- A cluster volume can grow to *a max size of 128 TiB*.
- Part of the managed database service [[Amazon RDS]].
When you build your first Aurora database, you start by opening the Amazon RDS console. Then you choose Aurora as the database engine and then select the instance type.
- Aurora automatically maintains six copies of your data across three Availability Zones and will automatically attempt to recover the database in a healthy Availability Zone with no data loss. **You can create up to 15 read replicas** that can serve read-only traffic as well as failover.
- Aurora management operations typically involve entire clusters of database servers that are synchronized through replication, instead of individual database instances.
An Amazon Aurora DB cluster consists of one or more DB instances and a cluster volume that manages the data for those DB instances. An Aurora cluster volume is a virtual database storage volume that spans multiple AZs, with each Availability Zone having a copy of the DB cluster data.
Two types of DB instances make up an Aurora DB cluster:
- **Primary** (writer) DB instance: supports read and write operations, and performs all of the data modifications to the cluster volume. Each Aurora DB cluster has one primary DB instance.
- Aurora **Replica** (reader) DB instance: Connects to the same storage volume as the primary DB instance but supports only read operations.
Amazon Aurora Global Database:
- A feature available that allows a single Aurora database to span multiple AWS Regions. Data is replicated with no impact on database performance.
#### Aurora endpoints
When you connect to a cluster, the host name and port that you specify point to an intermediate handler called an endpoint.
- Cluster endpoint: connect to the primary instance of your cluster to develop and test applications, and perform transformations like INSERT statements, and DDL, DML and ETL operations.
- Reader endpoint: Perform queries.
- Instance endpoint: You can find the instance endpoint location for each of your instances in the AWS Management Console only.
- Custom endpoint: connect to different subsets of DB instances on the DB cluster.
- Aurora Global Database writer endpoint.
#### Aurora Benefits
- Aurora MySQL is 5x better performance than traditional.
- Aurora Postgres is 3x better performance than traditional.
- 1/10 of the costs of other solutions offering similar performance and availability
### Aurora Scaling
![[aurora-scaling.jpg]]
Availability:
- Aurora deploys a minimum of **3 Availability Zones** that each contain **2 copies of your data** at all times.
	- ***6 copies total***
	- Lose up to 2 copies without affecting write availability
	- Lose up to 3 copies of your data without affecting read availability
Storage:
- A cluster starts with 10GB of storage and scales in 10GB increments, up to 64TB~128TB
- Storage is autoscaling
- Computing resources can scale up to 32 vCPUs and 244GB of memory
Security:
- TLS/SSL certificate can be applied to connections.
- Encrypted at rest by default (cannot be turned off). Can use KMS keys.
#### Aurora Serverless Provisioned
- Default compute configuration for Aurora
- The primary DB instance will not be created for you by default you have to create your instances after creating your cluster.
#### Aurora Reader and Writer Instances
![[aurora-read-write-instances.jpg]]
## [Aurora Serverless v2](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.how-it-works.html#aurora-serverless-v2.parameters)
- fully manages the autoscaling configuration for Amazon Aurora
- capacity is adjusted automatically based on application demand
- You're only charged for the resources that your clusters consume.
- suitable for most demanding, variable workloads
🎯**Aurora Serverless v2 ==does not scale to zero and must maintain at least 0.5 ACUs.==**
🎯**ACU: Aurora Capacity Unit**: Measurement used to determine cost vs capacity.
- 1 ACU is about 2GiB of memory, CPU and networking.
- Ranges between 0.5 ACUs and 128 ACUs
📢Amazon Aurora Serverless v1 fell out of support December 31, 2024.
⚙When you configure your cluster for Serverless v2 you set a minimum and maximum ACU capacity.
``` bash
aws rds create-db-cluster \
	--db-cluster-identifier my-serverless-v2-cluster \
	--region eu-central-1 \
	--engine aurora-mysql \
	--engine-version 8.0.mysql_aurora.3.04.1 \
	--serverless-v2-scaling-configuration MinCapacity=1,MaxCapacity=4 \
	--master-username myuser \
	--manage-master-user-password
```
⚙ When you create a Writer instance you need to specify the `db-instance-class` as being `db.serverless`
``` bash
aws rds create-db-instance \
	--db-cluster-identifier my-serverless-v2-cluster \
	--db-instance-identifier my-serverless-v2-instance \
	--db-instance-class db.serverless \
	--engine aurora-mysql
```

## Aurora Serverless v2 vs Provisioned
![[aurora-serverless-vs-provisioned.jpg]]
## Aurora Global Database
- An Aurora database spanning multiple regions for global low latency and high availability
- Has primary cluster in 1 region
	- has up to 5 secondary clusters in different regions
	- write operations occur on the primary cluster
	- data is replicated to secondary cluster
	- global database is only available in specific regions and specific database versions.
![[au_global-cluster.jpg]]

| Description           | Primary AWS Region | Secondary AWS Region                      |
| --------------------- | ------------------ | ----------------------------------------- |
| Aurora DB clusters    | 1                  | 5 max                                     |
| Writer instances      | 1                  | 0                                         |
| Read-only instances   | 15 max             | 16 total                                  |
| Read-only max allowed | 15 - s             | s = total number of secondary AWS Regions |
![[au_global_demo.jpg]]
##### Creating a global cluster in the CLI
``` bash
aws rds create-global-cluster --region primary_region \
	--global-cluster-identifier global_database_id \
	--engine aurora-mysql \
	--engine-version version # optional
```
Then create your primary cluster with global cluster identifier
``` bash
aws rds create-db-cluster \
	--region primary_region \
	--db-cluster-identifier primary_db_cluster_id \
	# ... shortened for brevity
	--global-cluster-identifier global_database_id
```
Then create your secondary cluster and use the global cluster identifier to place it within the global cluster.
``` bash
aws rds create-db-cluster \
	--region secondary_region \
	--db-cluster-identifier secondary_cluster_id \
	--global-cluster-identifier global_database_id \
	# ...
```

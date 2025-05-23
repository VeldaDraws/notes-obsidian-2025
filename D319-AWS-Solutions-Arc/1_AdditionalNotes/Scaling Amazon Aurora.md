Amazon Aurora extends the benefits of read replicas by employing an SSD-backed virtualized storage layer. Features a distributed, fault-tolerant, self-healing storage system that automatically scales up to 64 TB per database instance. It delivers high performance and availability, point-in-time recovery, continuous backup to Amazon Simple Storage Service (S3) and replication across three Availability Zones.
An Amazon Aurora DB cluster consists of one or more DB instances and the cluster volume that manages the data for those DB instances.
- Primary DB instance
	- Supports read and write operations and performs all data modifications to cluster volume.
	- Each Aurora DB cluster has one primary DB instance.
- Aurora Replica
	- Connects to the same storage volume as the primary DB instance and supports only read operations.
	- Each Aurora DB cluster can have up to 15 Aurora replicas in addition to the primary DB instance.
You can choose your DB instance class size and add Aurora replicas to increase read throughput.
##### [Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html) Serverless
In some environments, workloads can be intermittent and unpredictable. There can be periods of heavy workloads that might last only a few minutes or hours, and also long periods of light activity, or even no activity.
- [Aurora Serverless](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.html) is an on-demand, automatically scaling configuration for Amazon Aurora. Aurora Serverless enables your database to automatically start up, shut down, and scale capacity up or down based on your application's needs.
You can create a [database endpoint](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Endpoints.html) without specifying the DB instance class size. You specify Aurora ACUs.
- Each ACU (Aurora Capacity Unit) is a combination of processing and memory capacity.
- Database storage automatically scales from 10 GiB to 64 TiB, same as storage in a standard Aurora DB cluster.
- The database endpoint connects to a proxy fleet that route the workload to a fleet of resources.
( From: [[09_Elasticity_Availability_Monitoring]] )

An elastic infrastructure can expand and contract as capacity needs change. Elasticity means that the infrastructure can expand and contract when capacity needs change.
Examples:
- to increase the number of web servers when traffic spikes
- lower the write capacity on your database when traffic goes down
- handle the day-to-day fluctuation of demand throughout your architecture
## Scaling
A technique that is used to achieve elasticity.
Two main types:
- 📈 Horizontal Scaling
	- Add or remove resources, also referred to as *scaling out*. Terminating resources would be considered *scaling in*.
- 📊 Vertical Scaling
	- Increase or decrease the specifications of an individual resource. Vertical scaling can eventually reach a limit, and is not always as cost-efficient, but it is relatively easy to implement.
#### [[EC2 Auto Scaling]]
- Launches or terminates instances based on specified conditions
- Automatically registers new instances with load balancers when specified.
- Can launch across Availability Zones.
## Database Layer Scaling
#### [[Amazon RDS Scaling]]
- Scale DB instances vertically up or down.
- Scale instances horizontally.
- AWS Blog: [Scaling Your Amazon RDS Instance Vertically and Horizontally](https://aws.amazon.com/blogs/database/scaling-your-amazon-rds-instance-vertically-and-horizontally/)
#### [[Scaling Amazon Aurora]]
#### Database Sharding
![[db_sharding_example.jpg]]
Sharding, also known as horizontal partitioning, is a popular scale-out approach for relational databases that improves write performance. Sharding is a technique that splits data into smaller subsets and distributes them across a number of physically separated database servers.
- Each server is referred to as a database *shard*.
- A shard-ed database architecture offers scalability and fault tolerance.
	- if one database shard has a hardware issue or goes through failover, no other shards are impacted because the single point of failure or slowdown is physically isolated.
See Also: AWS Blog: [Sharding with Amazon Relational Database Service](https://aws.amazon.com/blogs/database/sharding-with-amazon-relational-database-service/)
#### [[Dynamo DB Auto Scaling]]

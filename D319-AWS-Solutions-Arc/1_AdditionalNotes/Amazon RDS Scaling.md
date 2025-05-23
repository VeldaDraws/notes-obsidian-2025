## Vertical Scaling: Push-button scaling
You can vertically scale your Amazon RDS DB by changing the instance class.
You can also use [Amazon RDS Storage Autoscaling](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.StorageTypes.html#USER_PIOPS.Autoscaling) to scale capacity in response to growing database workloads.
## Horizontal Scaling: Read replicas
Horizontally scale for read-heavy workloads, with up to five read replicas and up to 15 Aurora replicas. Replication is asynchronous.
Amazon RDS uses the MariaDB, MySQL, Oracle and PostgreSQL DB engines' built-in replication functionality to create a special type of DB instance called a read replica from a source DB instance.
See also: [Working with DB instance read replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html)

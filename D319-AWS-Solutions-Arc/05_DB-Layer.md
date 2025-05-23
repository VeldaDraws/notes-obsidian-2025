[[05_01-Databases-In-General]]
[[05_02-Database Layer - Overview]]
## Most Common AWS Database Options:
### Relational:
#### 🎯 **[[Amazon RDS]]**
- ![[icon_RDS.png]]
- Fully managed **relational** database service 
- Summary Page: [[Databases#RDS]]
#### Amazon Redshift
- ![[icon_redshift.png|50]]
- Enterprise-level, petabyte scale, fully managed data warehousing service.
- Massively parallel processing, columnar data storage, efficient, targeted data compression encoding schemes.
#### 🎯 [[Amazon Aurora]]
- ![[icon_amAurora-solid.png|48]]
- Part of Amazon RDS
- Aurora is MySQL and PostgreSQL compatible.
- Summary Page: [[Databases#Aurora]]
### Non-Relational:
#### 🎯 **Amazon [[DynamoDB]]**
- ![[icon_dynamodb.png|48]]
- NoSQL
- Key/Value Store
- Document Store
- Summary Page: [[Databases#DynamoDB]]
#### 🎯 [[Amazon ElastiCache]]
- ![[icon_ElastiCache.png|48]]
#### Amazon Neptune
- ![[icon_am-neptune.png|48]]
- Fully managed graph database service.
# Amazon DocumentDB (MongoDB)
![[icon_documentDB.jpg|50]]
Amazon #DocumentDB is a fully managed document, NoSQL database from AWS, that is full API compatible with MongoDB.
When you use Amazon DocumentDB, you begin by creating a cluster. A cluster consists of a cluster volume and instances: primary and replica.

| SQL         | Amazon Document DB |
| ----------- | ------------------ |
| Table       | Collection         |
| Row         | Document           |
| Column      | Field              |
| Primary Key | Object ID          |
##### Further Reading:
- [What is Amazon DocumentDB?](https://docs.aws.amazon.com/documentdb/latest/developerguide/what-is.html)
- [Amazon DocumentDB: How It Works](https://docs.aws.amazon.com/documentdb/latest/developerguide/how-it-works.html)
# DMS (Database Migration Service)
![[DMS.jpg]]
Migration Methods:
- **Homogenous data migration**
	- Migrate data with native database tools
- **Instance Replication**
	- Provision an instance with chosen instance type to perform the replications between databases
- **Serverless Replication**
	- a serverless offering where you pay as you go, with some limitations.
	- Does not have public IPs
	- Must user VPC endpoints to access specific AWS services.
	- Limited selection of possible sources and targets.
	- Doesn't support views with selection and transformation rules.
AWS DMS:
- Loads the tables with data without any foreign keys or constraints.
AWS Schema Conversion Tool (SCT):
- Identifies the issues, limitations and actions for the schema conversion.
- Generates the target schema scripts, including foreign keys and constraints.
- Converts code such as procedures and views from source to target and applies the code on the target.
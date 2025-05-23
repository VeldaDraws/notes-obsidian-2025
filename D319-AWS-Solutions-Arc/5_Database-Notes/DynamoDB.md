# Amazon DynamoDB
![[icon_dynamodb.png|62]]![[icon_dynamoDB.jpg|62]]
🎦 [AWS re:Invent 2023 - Data modeling core concepts for Amazon DynamoDB](https://www.youtube.com/watch?v=l-Urbf4BaWg): Roughly an hour, but well-explained.
#DynamoDB is a NoSQL (non-relational) key/value and document database for internet-scale applications. It has a flexible billing model, tight integration with IaC, and a hands-off operational model.
All data is stored on SSD storage and is spread across 3 different AZs.
![[dynamDB-better-example.jpg]]
#### Anatomy of DynamoDB
- Tables: rows and columns
	- ![[icon_dy_table.png]]
	- Similar to other database systems, a table is a collection of data.
- **Items**: *rows* of data
	- ![[icon_dy_item.png]]
	- Contains zero or more items. An item is a group of attributes that is uniquely identifiable among all the other items.
	- There is no limit to the number of items you can store in a table.
- **Attributes**: *columns* of data
	- ![[icon_dy_attrib.png]]
	- Each item is composed of one or more attributes. An attribute is a fundamental data element, something that does not need to be broken down any further.
- Keys: identifying names of your data
- Values: the actual data itself
Each key/value pair composes an attribute, and one or more attributes make up an item. At minimum, every item contains a primary key and a corresponding value.
##### DynamoDB Primary Keys
![[dynamoDB-creation.jpg]]
When you create a table, you have to define a Primary Key. The primary key determines *where and how* your data will be stored in partitions.
⚠ The primary key ***cannot*** be changed later.
- Partition Key (also known as a hash key) determines which partition data should be written to. (needed)
- Sort Key (also known as a range key) determines how data should be sorted on a partition. (optional)
🎯 Using only a partition key is called a *Simple Primary Key*.
- *Partition key has to be unique* when using a Simple Primary Key.
🎯 Using both a partition key and Sort is called a *Composite Primary Key*.
- *The combination of partition and sort key have to be unique* to be a Composite Primary Key.
🎯 DynamoDB's internal hash function (secret) decides which partition to write data.
DynamoDB distributes your items across partitions based on the primary key. When a lot of read or write activity occurs against items sorted in the same partition, the partition is said to be a *hot partition*. Hot partitions can negatively affect performance. To avoid hot partitions, try to have partition keys to be as specific as possible.
##### Data Types
- Scalar
	- Can only have one value
	- String, number, binary, boolean and null.
- Set
	- Unordered list of scalar values. The values must be unique within a set, and a set must contain at least one value.
- Document
	- Document data types are designed to hold different types of data that fall outside the constraints of scalar and set data types. You can nest document types together up to 32 levels deep.
##### Query and Scan
Can easily be done in the DynamoDB console with many sorting options.
🎯 #Query allows you to find items in a table based on primary key values.
- you can query any table or secondary index that has a composite primary key
- by default: reads as Eventually Consistent, sort ascending, and returns all attributes for items.
- you can return specific attributes by using `ProjectExpression`
🎯 #Scan will scan through all items and then return on or more items through filters. Note: less efficient than running a query. Lists all items in a table.
- by default, returns all attributes for items
- can be performed on tables and secondary indexes
- scan operations are sequential.
- you can return specific attributes by using `ProjectExpression`
##### Secondary Indexes
Secondary indexes solve two issues with querying data from DynamoDB:
- When you query for a particular item, specify a partition key exactly
- Lets you look up data by an attribute other than the table's primary key
When you create a secondary index, you can choose which attributes get copied from the base table into the index, called *projected attributes*.
You can create a #GSI (*global secondary index*) any time after creating a base table. In a GSI, the partition and hash keys can be different than the base table.
![[icon_dy_gsi.png]] (icon for GSI)
A #LSI (*local secondary index*) must be created at the same time as the base table.

| Parameter            | LSI                                                           | GSI                                                                        |
| -------------------- | ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Lifecycle            | same of that as the table                                     | independent of the table                                                   |
| Primary key schema   | partition key is same as the base table                       | partition key and the sort key can be different from the base table        |
| Querying capability  | Scoped to the partition as of the base table - local          | queries span the partitions on base table data                             |
| Provisioned capacity | LSI shares read/write throughput capacity with the base table | GSI has independent settings for read/write throughput from the base table |
| Read consistency     | Offers both strong and eventual read consistency              | Offers only eventual read consistency                                      |
##### Capacity Modes
When creating a table, you have the option of having DynamoDB operate in on-demand mode or provisioned mode. 
- In on-demand mode, DynamoDB automatically scales to accommodate your workload.
- In provisioned mode, you specify the number of reads and writes per second your application will require. (Provisioned Throughput)
	- Read Capacity Units - #RCUs and Write Capacity Units - #WCUs: 
		- DynamoDB reserves partitions based on the number of RCUs and WCUs you specify when creating a table.
- When you read an item from a table, that read may be strongly consistent or eventually consistent.
- Autoscaling: For varying workloads with undeterminable, fixed provisioned capacity.
📝You can switch between provisioned and on-demand mode only once every 24 hours.
##### DynamoDB Read Consistency
When data needs to be updated, it has to write updates to all copies. Data can be inconsistent when reading from a copy that has yet to be updated.
- Eventual Consistent Reads (default):
	- Reads are fast, no guarantee of consistency.
- Strongly Consistent Reads:
	- Guarantee of consistency but with a tradeoff of higher latency (slower reads).
##### DynamoDB Partitions
A partition is an allocation of storage for a table, backed by SSDs, and automatically replicated across multiple AZs within a AWS Region
Speeds up reads for very large table by logically grouping similar data together.
DynamoDB automatically creates partitions for you as your data grows, starting off with a single partition.
- For every ***10GB*** of data.
- When you exceed the RCUs or WCUs for a single partition.
( #RCUs  = read capacity units )
( #WCUs  - write capacity units )
✨Each partition has a max of 3000 RCUs and 1000 WCUs
✨DynamoDB *evenly* splits the RCUs and WCUs across partitions.
##### DynamoDB Benefits
- You are working with an OLTP workload
- Require misson-critical application that must be highly available at all times.
- A high level of data durability.
##### DynamoDB Security
- Data is redundantly stored on multiple devices across multiple facilities in a DynamoDB Region.
- 🔐All user data stored in DynamoDB is fully-encrypted at rest. DynamoDB encryption at rest provides enhanced security by encrypting all your data at rest using encryption keys stored in AWS KMS (Key Management Service).
- IAM administrators control who can be authenticated and authorized to use DynamoDB resources. You can use IAM roles to manage access permissions and implement security policies.
- As a managed service, DynamoDB is protected by the AWS global network security procedures.
⛅If you are using an AWS managed key for encryption at rest, usage of the key is recorded in AWS CloudTrail. CloudTrail can tell you who made the request, the services used, actions performed, parameters for the action, and response elements returned.
#### Considerations
- You can have a table without an index
- You can have more than one global secondary index on a table
- You can have more than one local secondary index on a table
### Further Reading:
- [DynamoDB Core Components](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html)
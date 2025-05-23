##### Database considerations: 
- Scalability
- Total storage requirements
- Object size and type
- Durability
##### Choosing between Unmanaged and Managed DB options
![[managed-vs-unmanaged.jpg|500]]
###### Unmanaged Databases
If you operate a relational database on premises, you are responsible for all aspects of operation. AWS is responsible for and has control over the hardware and underlying infrastructure.
###### Managed Databases
AWS takes care of the underlying infrastructure, but you are still responsible for the database tuning, query optimization, and ensuring that your customer data is secure. Provides the ultimate convenience but the least amount of control compared to the two previous options.
### Relational Databases vs Non-Relational
##### Relational Database Management System ( #RDMS ) Benefits
- Ease of use, data integrity, common SQL.
- Ideal for: Strict schema rules, ACID compliance, and data quality performance.
- Common Engines:
	- MySQL
	- PostgreSQL
	- Oracle
	- Microsoft SQL Server
	- Amazon Aurora
- Benefits:
	- SQL: including complex SQL uses like joining multiple tables to understand relationships between your data.
	- Reduced redundancy: You can store data in one table and reference it from other tables instead of saving the same data in different places.
	- Familiarity: Because relational databases have been popular choice since the 1970s, technical professionals often have familiarity and experience with them.
	- Accuracy: Relational databases ensure that your data has high integrity and adheres to the atomicity, consistency, isolation, and durability (ACID) principle.
- Use Cases:
	- Applications that have a fixed schema.
	- Applications that need persistent storage.
		- Enterprise resource planning (ERP) applications
		- Customer relationship management (CRM) applications
		- Commerce and financial applications.
##### Non-Relational Database Benefits
- Flexibility, scalability, high performance, highly functional APIs.
- Ideal for: Scaling horizontally, non-traditional schemas, read/write exceed what can be economically supported through traditional RDBMS.
- Key-Value Databases
	- Optimized to store and retrieve key-value pairs in large volumes and in milliseconds, without the performance overhead and scale limitations of relational databases.
- Document Databases
	- Designed to store data as documents. Data is typically represented as a readable document.
- In-memory databases
	- Used for read-heavy and compute-intensive applications that require low-latency access to data.
- Graph
	- Used for applications that need to enable users to query and navigate relationships between highly connected databases.

### Data - General
- Structured Data: Often organized to support transactional and analytical applications
- Semi-structured Data: Flexible and can be updated without the requirement to change the schema for every single record in a table.
- Unstructured: Not organized in any distinguishable or predefined manner. Common stores for unstructured data are non-relational key-value databases.
Tables should be indexed to allow a query to quickly find the data needed to produce a result.
- OLTP: Online Transactional Processing
	- Focus on recording Update, Insertion, and Deletion data transactions.
	- Simple and short queries
- OLAP: Online Analytical Processing
	- Stores historical data that has been input by OLTP
	- Allows users to view different summaries of multidimensional data.
#### Use Cases and Scenarios
Inventory control system that needs to be migrated to a *relational database* in the cloud
- [[Amazon RDS]]
*PostgreSQL* database consuming a substantial amount of *I/O resources* smaller than 4KB
- Amazon Aurora (Both MySQL and PostgreSQL compatible)
Data warehouse solution that provisions *infrastructure capacity* and automates ongoing administrative tasks.
- Amazon Redshift. Set up and deploy a new data warehouse in minutes, run queries across petabytes of data and extabytes from your data lake built on S3..
Gaming website that scaled quickly and loads slowly, needing a huge volume of uses.
- Amazon ElastiCache
Quickly gather shopping cart data from website and discard data on abandoned carts:
- Amazon [[DynamoDB]]. (10 trillion requests per day and support peaks of more than 20 million requests per second)
Fraud detection app that needs a database that supports near real-time detection of patterns
- Amazon Neptune (Main purpose to navigate relationships in data.)
Massive MongoDB database that needs to be migrated to the cloud.
- Amazon DocumentDB
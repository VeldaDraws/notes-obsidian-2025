# Caching - Overview
The speed at which you deliver content affects the success of your application.
In computing, a cache is a high-speed data storage layer. The primary purpose of a cache is to increase the performance of data retrieval by reducing the need to access the underlying, slower storage layer.
##### What should you cache:
- Data that requires a slow and expensive query to acquire.
- Relatively static and frequently accessed data - for example, a profile for your social media website.
- Information that can be stale for some time, such as a publicly traded stock price.
###### Speed and expense:
- Time-consuming database queries and frequently used, complex queries often create bottlenecks in applications. Generally, if the data requires a slow and expensive query to acquire, it's a candidate for caching.
###### Data and access patterns:
- Determining what to cache also involves understanding the data itself and its access patterns. For caching to provide meaningful benefits, the data should be relatively static and frequently accesses, such as a personal profile on a social media site.
###### Staleness
- Cached data is stale data. Even if it's not stale in certain circumstances, cached data should be considered and treated as stale.
##### Benefits of Caching
- Improve application speed.
- Reduce response latency.
- Reduces application processing and database access time for read-heavy workloads. (Write-heavy applications typically do not see as great of a benefit.)
Layers:
- CDNs
- DNS
- web applications
- databases
## Edge Caching - CDNs
A Content Delivery Network (CDN):
- Is a globally distributed system of caching servers.
- Caches copies of commonly requested files (static content).
- Delivers a local copy of the requested content from a nearby cache edge or Point of Presence.
- Improves application performance and scaling.
The CDN delivers a local copy of requested content from a cache edge or PoP (Point of Presence) that provides the fastest deliver to the requester.
## Amazon CloudFront
![[icon_CloudFront.jpg|50]]
- Amazon Global CDN
- Optimized for all delivery use cases, with a multi-tier cache by default and extensive flexibility.
- Provides an extra layer of security for your architectures.
- WebSockets and HTTP or HTTPS methods.
The CDN offers a multi-tier cache by default. Regional edge caches improve latency and lower the load on your origin servers when the object is not already cached at the edge.
CloudFront provides both network-level and application-level protection. Your traffic and applications benefit through various built-in protects, such as AWS Shield Standard, at no extra cost.
- Also use configurable features such as AWS Certificate Manage (ACM) at no extra cost.
- CloudFront supports SSL/TLS
- Supports HTTP methods: DELETE, GET, HEAD, OPTIONS, PATCH, POST, PUT
You can configure CloudFront to require that viewers use HTTPS to request your objects, so that connections are encrypted when CloudFront communicates with viewers.
Amazon CloudFront delivers your content to users through **edge locations**.
###### How caching works in Amazon CloudFront:
1. Request is routed to the most optimal edge location.
2. Non-cached content is retrieved from the origin server.
3. Origin server sends content to the edge location for caching.
4. Data is transferred to the user.
A objects become less popular, individual edge locations might remove those objects to make room for more popular content. For less popular content, CloudFront has regional edge caches.
Regional edge caches are CloudFront locations that are deployed globally and close to your viewers. They are located between your origin server and the global edge locations that serve content directly to viewers.
###### How to configure a CloudFront distribution
1. You specify an origin server.
	- S3 bucket, EC2 instance, etc.
2. You configure the distribution.
	- Access, security, geo-restrictions, etc.
3. CloudFront assigns a domain name.
4. CloudFront sends your distribution's configuration to edge locations.
###### How to expire content - 3 ways
See also: [Manage how long content stays in the cache (expiration)](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Expiration.html)
- TTL (Time-to-Live)
	- Controls how long your files stay in a cache before CloudFront forwards another request to your origin.
- Change object name
	- This method requires more effort, but replacement is more immediate. Although you can update existing objects in a CloudFront distribution and use the same object names, it is not recommended.
- Invalidate object
	- This method is a bad solution because the system must forcibly interact with all edge locations. Should be used sparingly.
###### Video on demand streaming:
Encoders:
- AWS Elemental MediaConvert
- Amazon Elastic Transcoder
The packing process creates segments, which are static files that contain your audio, video, and captions content. It also generates manifest files, which describe what segments to play and the specific order to play them in. Package formats include DASH/MPEG-DASH, HLS, and CMAF.
###### Use case: Map tiles
Cache places that people frequently view, and if the tile is already present in a particular CloudFront edge location, then it is served up directly.
###### Use case: DDoS Mitigation
![[diagram-ddos.jpg]]
See also: [AWS Best Practices for DDoS Resiliency](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/aws-best-practices-ddos-resiliency.html)
See also: [AWS WAF](https://aws.amazon.com/waf/)
## Caching Sessions - Elastic Load Balancing
![[D319-AWS-Solutions-Arc/2_Images/Caching-Images/icon_ELB.jpg|50]]
When a user or service interacts with a web application, it sends an HTTP request, and the application returns a response. A sequence of such transactions is called a session. Every request is independent of previous transactions.
To use sticky sessions, the client must support cookies.
- advantage: cost-effective
- disadvantage: limits scalability
### Persist Sessions
You can designate a layer in your architecture that can store sessions in a scalable and robust manner outside the instance.
###### Persist session data in a distributed cache
- Persist sessions in a distributed cache.
- Loss of sessions is a risk if sessions are stored locally on nodes.
###### Persist sessions inside a DynamoDB table
- Persist sessions in an Amazon DynamoDB database.
- Loss of sessions is a risk if sessions are stored locally on nodes.
## Caching Databases
Considerations:
- Concerned about response times for the customer.
- You have a high volume of requests that inundate your database.
- You would like to reduce costs.
A database cache supplements your primary database by removing unnecessary pressure on it, typically in the form of frequently accessed read data. The cache itself can be in a number of areas, including your database, application, or as a standalone layer.
## Amazon DynamoDB Accelerator (DAX)
![[icon_dy_dax.png]]
Fully managed, highly available, in-memory cache for DynamoDB.
Benefits:
- Extreme performance: single-digit millisecond latency.
- Highly scalable: add capacity as needed.
- Fully managed: Takes care of management tasks, including provisioning, setup and configuration, software patching, and replicating data over nodes during scaling operations.
- Integrated with DynamoDB: API-compatible with DynamoDB. Provision a DAX cluster, and use the DAX client SDK to point existing API calls at the DAX cluster.
- Flexible: You can provision one DAX cluster for multiple DynamoDB tables, multiple DAX clusters for a single DynamoDB table, or a combination of both.
- Secure: DAX fully integrates with AWS services to enhance security. You can use AWS IAM to assign unique security credentials to each user and control each user's access to services and resources. DAX supports Amazon VPC for secure and easy access from your existing applications.
##### Using DynamoDB with DAX to accelerate response time
The acceleration that you get by adding DAX to your architecture comes without needing to make any major changes in the game code. DAX handles cache invalidation and data population without your intervention.
##### Remote or side caches
- Cache hit: Data found in cache
- Cache miss: Data not found in cache
DAX is a transparent cache. Another way to implement a database cache deployment is to use a remote or side cache.
Side caches are typically used for read-heavy workloads
1. For a key-value pair, an application first tries to read the data from the cache. If the cache contains the data, the value is returned.
2. If the intended key-value pair is not found in the cache (called a cache miss), the application fetches the data from the underlying database.
3. It's important that the data is present when the application needs it again. To ensure that it is, the key-value pair that's obtained from the database is then written to the cache.
### Amazon ElastiCache
![[D319-AWS-Solutions-Arc/2_Images/Caching-Images/icon_ElastiCache.jpg|50]]
ElastiCache provides web applications with an in-memory data store in the cloud.
- Works an in-memory data store and cache
- Offers high performance
- Is fully managed
- Is scalable
- Supports Redis and Memcached

🎇Both ElastiCache for Memcached and for Redis have sub-millisecond response times.
##### ElastiCache for Memcached
- Scales up to 20 nodes per cluster.
- Ability to scale horizontally for writes and storage.
- Multi-threaded performance.
##### ElastiCache for Redis
- Scales up to 250 nodes for increased data access performance.
- Advanced data structures.
- Sorting/Ranking Datasets.
- Publish/Subscribe messaging.
- Multi-AZ Deployments with automatic failover.
- Persistence.
##### ElastiCache Components
A cache ***node*** is the smallest building block of an ElastiCache deployment. Each node has its own DNS name and port. It can exist isolated or in grouping with other nodes known as a ***cluster***.
##### ElastiCache Strategies:
- Lazy Loading
	- Loads data into the cache only when necessary. When your application requests the data, it first makes the request to ElastiCache cache. If data is existing and current, ElastiCache returns the data to your application. Otherwise it requests the data from the data store. Your application then writes the data to the cache so it can be retrieved quickly the next time it's requested.
	- Use lazy loading when you have data that will be read often, but written infrequently.
- Write-Through
	- It adds or updates data in the cache when the data is written to the database.
	- Use when you have data that must be updated in real time. It's a proactive approach.
- Adding a TTL
	- By adding a TTL value to each write, you enjoy the advantages of each strategy and avoid cluttering the cache with data. TTL is an integer value or key that specifies the number of seconds or milliseconds, depending on the in-memory engine, until the key expires. When an application attempts to read an expired key, it's treated as though the data isn't found in the cache.
##### Three-tier web hosting architecture
The database tier of your backend infrastructure might include Amazon RDS DB instances and an ElastiCache cluster that provides the in-memory layer.
In this web hosting architecture diagram:
- Amazon 53 enables you to map your zone apex DNS name to your load balancer DNS name
- Amazon CloudFront provides edge caching for high-volume content.
- A load balancer spreads traffic across web servers in Auto Scaling groups in the presentation layer.
- Another load balancer spreads traffic across backend application servers in the Auto Scaling groups that are in the application layer.
- Amazon ElastiCache provides an in-memory data cache for the application, which removes load from the database tier.
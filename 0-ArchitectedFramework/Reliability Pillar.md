https://docs.aws.amazon.com/pdfs/wellarchitected/latest/reliability-pillar/wellarchitected-reliability-pillar.pdf#welcome

The reliability pillar encompasses the ability of a workload to perform its intended function correctly and consistently when it's expected to.
### Shared Responsibility Model for Resiliency
##### AWS Responsibility
AWS is responsible for the infrastructure that compromises the hardware, software, networking, and facilities that run AWS Cloud services.
##### Customer Responsibility
Determined by the AWS Cloud services that you select.
![[reliability_sharedresponsibility.jpg|600]]
### Design Principles
- Automatically recover from failure
- Test recovery procedures
- Scale horizontally to increase aggregate workload availability
- Stop guessing capacity
- Manage change through automation
## Definitions
- [[#Foundations]]
- [[#Workload Architecture]]
- [[#Change Management]]
- Failure Management

### Resiliency and the components of reliability
- **Resiliency** is the ability of a workload to recover from infrastructure or service disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions, such as misconfigurations or transient network issues.
- **Availability** (aka service availability) is the percentage of time that a workload is available for use.
![[availability-formula.jpg]]
(Availability equals Available for Use Time divided by Total Time)

| Five Nine's | Max Unavailability per year | Application Categories                                 |
| ----------- | --------------------------- | ------------------------------------------------------ |
| 99%         | **3 days**, 15 hours        | Batch processing, data extraction, transfer, load jobs |
| 99.9%       | **8 hours**, 25 minutes     | Internal tools, knowledge management, project tracking |
| 99.99%      | **52 minutes**              | Video delivery, broadcast workloads                    |
| 99.999%     | **5 minutes**               | ATM transactions, telecommunication workloads          |
##### Measuring Availability based on requests
![[availability-formula-02.jpg]]
(Availability equals Successful Responses divided by Valid Requests)
##### Calculating dependency availability
![[availability-formula-03.jpg]]
(Estimated availability equals MTBF divided by MTBF plus MTTR)
- MTBF: Mean Time Between Failure
- MTTR: Mean Time to Recover
### Disaster Recovery (DR) objectives
##### Recovery Time Objective (RTO)
Defined by the organization. #RTO is the maximum acceptable delay between the interruption of service and restoration of service. This determines what is considered an *acceptable time window* when service is unavailable.
##### Recovery Point Objective (RPO) 
Defined by the organization. #RPO is the maximum acceptable amount of time since the last data recovery point. This determines what is considered an *acceptable loss of data* between the last recovery point and the interruption of service.

## Foundations
### Manage service quotas and constraints
- REL01-BP01 Aware of service quotas and constraints
	- Know which cloud resource constraints, such as disk or network, are potentially impactful
- REL01-BP02 Manage service quotas across accounts and regions 
	- If you are using multiple accounts or Regions, request the appropriate quotas in all environments in which your production workloads run.
- REL01-BP03 Accommodate fixed service quotas and constraints through architecture 
	- Design architectures for applications and services to prevent these limits from impacting reliability
- REL01-BP04 Monitor and manage quotas
	- Allow for planned growth in usage.
- REL01-BP05 Automate quota management
	- Implement tools to alert you when your workload approaches the limits and consider creating quota increase requests automatically.
		- [Quota Monitor](https://docs.aws.amazon.com/solutions/latest/quota-monitor-for-aws/solution-overview.html) for AWS
		- [AWS Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/what-is-control-tower.html)
		- [Trusted Advisor Organizational](https://docs.aws.amazon.com/organizations/latest/userguide/services-that-can-integrate-ta.html) (TAO) Dashboard
		- Consolidated Insights from Multiple Accounts (CIMA)
- REL01-BP06 Ensure that a sufficient gap exists between the current quotas and the maximum usage to accommodate failover
	- Maintain space between the resource quota and your usage.
### Plan your network topology
- REL02-BP01 Use highly available network connectivity for your workload public endpoints
	- Use highly available DNS, content delivery networks (CDNs), API gateways, load balancing, or reverse proxies.
	- You can also use health checks provided by Amazon Route 53. The health checks verify that your application is reachable, available, and functional, and they can be set up in a way that they mimic your user’s behavior, such as requesting a web page or a specific URL. In case of failure, Amazon Route 53 responds to DNS resolution requests and directs the traffic to only healthy endpoints.
- REL02-BP02 Provision redundant connectivity between private networks in the cloud and on-premises environments
	- Implement redundancy in your connections between private networks in the cloud and on-premises environments to achieve connectivity resilience.
- REL02-BP03 Ensure IP subnet allocation accounts for expansion and availability
- REL02-BP04 Prefer hub-and-spoke topologies over many-to-many mesh
	- When connecting multiple private networks, such as Virtual Private Clouds (VPCs) and on-premises networks, opt for a hub-and-spoke topology over a meshed one. Unlike meshed topologies, where each network connects directly to the others and increases the complexity and management overhead, the hub-and-spoke architecture centralizes connections through a single hub. This centralization simplifies the network structure and enhances its operability, scalability, and control.
	- ![[hubspoke-example.jpg]]
- REL02-BP05 Enforce non-overlapping private IP address ranges in all private address spaces where they are connected
	- An IP address management (IPAM) system can help with automating this.
	- [Amazon VPC IP Address Manager](https://docs.aws.amazon.com/vpc/latest/ipam/what-it-is-ipam.html)
## Workload Architecture
### Design your workload service architecture
Service-oriented architecture (SOA) is the practice of making software components reusable via service interfaces. Microservices architecture goes further to make components smaller and simpler.
- REL03-BP01 Choose how to segment your workload
	- Workloads should be supportable, scalable, and as loosely coupled as possible. Workloads that are capable of statelessness are more capable of being deployed as microservices.
	- Anti-Patterns to watch out for:
		- The [microservice Death Star](https://mrtortoise.github.io/architecture/lean/design/patterns/ddd/2018/03/18/deathstar-architecture.html) is a situation in which the atomic components become so highly interdependent that a failure of one results in a much larger failure, making the components as rigid and fragile as a monolith.
	- ![[mono-vs-micro.jpg]]
- REL03-BP02 Build services focused on specific business domains and functionality
	- [Bounded Context - Martin Fowler](https://martinfowler.com/bliki/BoundedContext.html)
	- Domain-driven design (DDD) is the foundational approach of designing and building software around business domains. It’s helpful to work with an existing framework when building services focused on business domains. 
		- ![[ddd.jpg|500]]
- REL03-BP03 Provide service contracts per API
	- Applications built with service-oriented or microservice architectures are able to operate independently while having integrated runtime dependency.
	- Incorporate AWS services including Amazon API Gateway, AWS AppSync, and Amazon EventBridge into your architecture to use API service contracts in your application. Amazon API Gateway helps you integrate with directly native AWS services and other web services.
### Design interactions in a distributed system to prevent failures
Components of the distributed system must operate in a way that does not negatively impact other components or the workload.
- REL04-BP01 Identify the kind of distributed systems you depend on
	- Distributed systems can be synchronous, asynchronous, or batch. Synchronous systems must process requests as quickly as possible and communicate with each other by making synchronous request and response calls using HTTP/S, REST, or remote procedure call (RPC) protocols.
	- Asynchronous systems communicate with each other by exchanging data asynchronously through an intermediary service without coupling individual systems.
	- Batch systems receive a large volume of input data, run automated data processes without human intervention, and generate output data.
- REL04-BP02 Implement loosely coupled dependencies
	- Dependencies such as queuing systems, streaming systems, workflows, and load balancers are loosely coupled. Loose coupling helps isolate behavior of a component from other components that depend on it, increasing resiliency and agility.
	- ![[tight-vs-loose.jpg]]
	- Amazon SQS queues and AWS Step Functions are just two ways to add an intermediate layer for loose coupling. Event-driven architectures can also be built in the AWS Cloud using Amazon EventBridge, which can abstract clients (event producers) from the services they rely on (event consumers). Amazon Simple Notification Service (Amazon SNS) is an effective solution when you need high-throughput, push-based, many-to-many messaging.
- REL04-BP04 Make mutating operations idempotent
	- An idempotent service promises that each request is processed exactly once, such that making multiple identical requests has the same effect as making a single request. This makes it easier for a client to implement retries without fear that a request is erroneously processed multiple times.
	- To do this, clients can issue API requests with an idempotency token, which is used whenever the request is repeated. An idempotent service API uses the token to return a response identical to the response that was returned the first time that the request was completed, even if the underlying state of the system has changed.
### Design interactions in a distributed system to mitigate or withstand failures
- REL05-BP01 Implement graceful degradation to transform applicable hard dependencies into soft dependencies
	- Application components should continue to perform their core function even if dependencies become unavailable.
- REL05-BP02 Throttle requests
	- Throttle requests to mitigate resource exhaustion due to unexpected increases in demand. Requests below throttling rates are processed while those over the defined limit are rejected with a return message indicating the request was throttled.
- REL05-BP03 Control and limit retry calls
	- Use exponential backoff to retry requests at progressively longer intervals between each retry. Introduce jitter between retries to randomize retry intervals. Limit the maximum number of retries.
- REL05-BP04 Fail fast and limit queues
	- When a service is unable to respond successfully to a request, fail fast. This allows resources associated with a request to be released, and permits a service to recover if it’s running out of resources.
- REL05-BP05 Set client timeouts
	- Set timeouts appropriately on connections and requests, verify them systematically, and do not rely on default values as they are not aware of workload specifics.
- REL05-BP06 Make systems stateless where possible
	- Systems should either not require state, or should offload state such that between different client requests, there is no dependence on locally stored data on disk and in memory. This allows servers to be replaced at will without causing an availability impact.
- REL05-BP07 Implement emergency levers
	- Emergency levers are rapid processes that can mitigate availability impact on your workload.
	- This may include mechanisms such as load shedding, throttling requests, or implementing graceful degradation.
	- [How Amazon.com Search Uses Chaos Engineering](https://community.aws/content/2dvVG1dk8rSnrDHekhjk09CjXVP/how-search-uses-chaos-engineering)

## Change Management
Monitor workload resources, design your workload to adapt to changes in demand, implement change.
Monitoring at AWS consists of four distinct phases:
1. Generation: monitor all components for the workload
2. Aggregation: define and calculate metrics
3. Real-time processing and alarming: send notifications and automate responses.
4. Storage and analytics.
### Monitor Workload Resources
- REL06-BP01 Monitor all components for the workload (Generation)
	- Collect and use critical metrics from all components of the workload to ensure workload reliability and optimal user experience. Detecting that a workload is not achieving business outcomes allows you to quickly declare a disaster and recover from an incident.
		1. Turn on logging where available - [AWS Services That Publish CloudWatch Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CW_Support_For_AWS.html)
		2. Review all default metrics and explore any data collection gaps
		3. Evaluate all the metrics to decide which ones to alert on for each AWS service in your workload
		4. Define alerts and the recovery process for your workload after the alert is invoked.
		5. Explore use of synthetic transactions to collect relevant data about workloads state.
- REL06-BP02 Define and calculate metrics (Aggregation)
	- Identify the sources of telemetry data that are relevant for your workloads and their components. Collect the metrics and logs using appropriate tools and processes.
- REL06-BP03 Send notifications (Real-time processing and alarming)
- REL06-BP04 Automate responses (Real-time processing and alarming)
- REL06-BP05 Analyze logs
- REL06-BP06 Regularly review monitoring scope and metrics
- REL06-BP07 Monitor end-to-end tracing of requests through your system

Design your workload to adapt to changes in demand p136
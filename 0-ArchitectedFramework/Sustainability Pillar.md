Full PDF [Whitepaper](https://docs.aws.amazon.com/pdfs/wellarchitected/latest/sustainability-pillar/wellarchitected-sustainability-pillar.pdf#sustainability-pillar)
# Cloud sustainability
📌The discipline of sustainability addresses the long-term environmental, economic, and societal impact of your business activities.
###### Emission Examples - Scope for AWS
- Scope 1
	- All direct emissions from the activities of an organization or under its control.
- Scope 2
	- Indirect emissions from electricity purchased and used to power data centers and other facilities.
- Scope 3
	- All other indirect emissions from the activities of an organization from sources it doesn't control.
###### The Shared Responsibility Model
![[sustain_shared.jpg]]
- AWS is responsible for optimizing the sustainability of the cloud – delivering efficient, shared infrastructure, water stewardship, and sourcing renewable power.
- Customers are responsible for sustainability in the cloud – optimizing workloads and resource utilization, and minimizing the total resources required to be deployed for your workloads.
###### Design principles for sustainability in the cloud
- Understand your impact
- Establish sustainability goals
- Maximize utilization
- Anticipate and adopt new, more efficient hardware and software offerings.
- Use managed services
- Reduce downstream impact of your cloud workloads.
#### Improvement Process
- To eliminate waste, low utilization, and idle or unused resources
- To maximize the value from resources you consume
1. Identify targets for improvement
2. Evaluate specific improvements
3. Prioritize and plan improvements
4. Test and validate improvements
5. Deploy changes to production
6. Measure results and replicate successes
#### Useful Resources:
- [AWS Architecture Blog: Optimizing your AWS Infrastructure for Sustainability, Part I: Compute](https://aws.amazon.com/blogs/architecture/optimizing-your-aws-infrastructure-for-sustainability-part-i-compute/)
	- [Part II: Storage](https://aws.amazon.com/blogs/architecture/optimizing-your-aws-infrastructure-for-sustainability-part-ii-storage/)
	- [Part III: Networking](https://aws.amazon.com/blogs/architecture/optimizing-your-aws-infrastructure-for-sustainability-part-iii-networking/)
#### Business metrics: Key Performance Indicators
![[sustain_kpi.jpg]]
Divide the provisioned resources by the business outcomes achieved to determine the provisioned resources per unit of work.
#### Sustainability as a non-functional requirement
Meeting sustainability targets might not require equivalent trade-offs in one or more other traditional metrics such as uptime, availability, or response time. You can achieve significant gains in sustainability with no measurable impact on service levels. Where minor trade-offs are required, the sustainability improvements gained by these trade-offs can outweigh the change in quality of service.
## Best Practices
- **Region Selection**
	- SUS01-BP01 Choose Region based on both business requirements and sustainability goals
		- AWS Blog: [What to Consider when Selecting a Region for your Workloads](https://aws.amazon.com/blogs/architecture/what-to-consider-when-selecting-a-region-for-your-workloads/)
- **Alignment to demand**
	- SUS02-BP01 Scale workload infrastructure dynamically
		- Use elasticity of the cloud and scale your infrastructure dynamically to match supply of cloud resources to demand and avoid overprovisioned capacity in your workload.
		- Docs: [Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
		- Docs: [Application Auto Scaling](https://docs.aws.amazon.com/autoscaling/application/userguide/what-is-application-auto-scaling.html)
		- Docs: [Kubernetes Cluster Autoscaler](https://aws.amazon.com/blogs/aws/introducing-karpenter-an-open-source-high-performance-kubernetes-cluster-autoscaler/)
	- SUS02-BP02 Align SLAs with sustainability goals
		- Review and optimize workload service-level agreements (SLA) based on your sustainability goals to minimize the resources required to support your workload while continuing to meet business needs.
		- AWS Blog: [Understand resiliency patterns and trade-offs to architect efficiently in the cloud](https://aws.amazon.com/blogs/architecture/understand-resiliency-patterns-and-trade-offs-to-architect-efficiently-in-the-cloud/)
		- AWS Blog: [Importance of Service Level Agreement for SaaS Providers](https://aws.amazon.com/blogs/apn/importance-of-service-level-agreement-for-saas-providers/)
	- SUS02-BP03 Stop the creation and maintenance of unused assets
		- Conduct an inventory
		- Analyze Usage
		- Remove unused assets
		- Communicate with third parties
		- Use lifecycle policies
		- Review and Optimize
	- SUS02-BP04 Optimize geographic placement of workloads based on their networking requirements
	- SUS02-BP05 Optimize team member resources for activities performed
	- SUS02-BP06 Implement buffering or throttling to flatten the demand curve
- **Software and Architecture**
	- SUS03-BP01 Optimize software and architecture for asynchronous and scheduled jobs
		- Use efficient software and architecture patterns such as queue-driven to maintain consistent high utilization of deployed resources.
		- Docs: [Understanding events and event-driven architectures](https://docs.aws.amazon.com/lambda/latest/dg/concepts-event-driven-architectures.html)
		- Workshop: [Event-driven architecture with AWS Graviton Processors and Amazon EC2 Spot Instances](https://catalog.workshops.aws/well-architected-sustainability/en-US/2-software-and-architecture/event-driven-architecture-with-graviton-spot)
	- SUS03-BP02 Remove or refactor workload components with low or no use
		- Remove components that are unused and no longer required, and refactor components with little utilization to minimize waste in your workload.
	- SUS03-BP03 Optimize areas of code that consume the most time or resources
		- Optimize your code that runs within different components of your architecture to minimize resource usage while maximizing performance.
	- SUS03-BP04 Optimize impact on devices and equipment
		- Understand the devices and equipment used in your architecture and use strategies to reduce their usage. This can minimize the overall environmental impact of your cloud workload.
	- SUS03-BP05 Use software patterns and architectures that best support data access and storage patterns
		- Understand how data is used within your workload, consumed by your users, transferred, and stored. Use software patterns and architectures that best support data access and storage to minimize the compute, networking, and storage resources required to support the workload.
- **Data Management**
	- SUS04-BP01 Implement a data classification policy
		- Classify data to understand its criticality to business outcomes and choose the right energy efficient storage tier to store the data.
		- AWS Startups: [Four simple steps to classify your data and secure your startup](https://aws.amazon.com/startups/learn/four-simple-steps-to-classify-your-data-and-secure-your-startup#overview)
	- SUS04-BP02 Use technologies that support data access and storage patterns
		- Use storage technologies that best support how your data is accessed and stored to minimize the resources provisioned while supporting your workload.
	- SUS04-BP03 Use policies to manage the lifecycle of your datasets
		- Manage the lifecycle of all of your data and automatically enforce deletion to minimize the total storage required for your workload.
		- Docs: [Evaluating Resources with AWS Config Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html)
		- Docs: [Amazon S3 analytics – Storage Class Analysis](https://docs.aws.amazon.com/AmazonS3/latest/userguide/analytics-storage-class.html)
	- SUS04-BP04 Use elasticity and automation to expand block storage or file system
		- Use elasticity and automation to expand block storage or file system as data grows to minimize the total provisioned storage.
	- SUS04-BP05 Remove unneeded or redundant data
		- Remove unneeded or redundant data to minimize the storage resources required to store your datasets
			- [Amazon DynamoDB TTL](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/TTL.html)
			- [Amazon S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)
			- [Amazon CloudWatch log retention](https://docs.aws.amazon.com/managedservices/latest/userguide/log-customize-retention.html)
			- [Working with backups on Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html)
	- SUS04-BP06 Use shared file systems or storage to access common data
		- Adopt shared file systems or storage to avoid data duplication and allow for more efficient infrastructure for your workload.
	- SUS04-BP07 Minimize data movement across networks
		- Use shared file systems or object storage to access common data and minimize the total networking resources required to support data movement for your workload.
	- SUS04-BP08 Back up data only when difficult to recreate
		- Avoid backing up data that has no business value to minimize storage resources requirements for your workload.
- **Hardware and services**
	- SUS05-BP01 Use the minimum amount of hardware to meet your needs
	- SUS05-BP02 Use instance types with the least impact
	- SUS05-BP03 Use managed services
	- SUS05-BP04 Optimize your use of hardware-based compute accelerators
- Process and culture
	- SUS06-BP01 Communicate and cascade your sustainability goals
	- SUS06-BP02 Adopt methods that can rapidly introduce sustainability improvements
	- SUS06-BP03 Keep your workload up-to-date
	- SUS06-BP04 Increase utilization of build environments
	- SUS06-BP05 Use managed device farms for testing
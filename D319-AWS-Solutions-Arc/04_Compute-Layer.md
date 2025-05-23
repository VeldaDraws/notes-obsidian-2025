# Compute Services
![[icon_compute.png|62]]

# Instances (Virtual Machines)
#### [AWS EC2](https://docs.aws.amazon.com/ec2/?nc2=h_ql_doc_ec2)
![[icon_ec2.png|62]]
Amazon Elastic Compute Cloud (Amazon EC2) provides on-demand, scalable computing capacity in the Amazon Web Services (AWS) Cloud.
![[EC2-Virtualization.jpg|250]]
#### Instance Store
Storage volumes for temporary, ephemeral data that is deleted when you stop, hibernate, or terminate your instance.
- Instance store volumes are SSDs that are physically attached to the server hosting your instance and are connected via a fast NVMe interface.
- The use of instance store volumes is included in the price of the instance itself.
- Instance store volumes work especially well for deployment models where instances are launched to fill short-term roles, import data from external sources, and effectively disposable.
#### Amazon EBS volumes
Persistent storage volumes for your data using Amazon Elastic Block Store.
- You can attach as many EBS volumes to your EC2 instance as you like, *but* one volume of EBS cannot be attach to more than a single instance.
- Types:
	- **EBS-Provisioned IOPS SSD** (for intensive I/O operations)
	- **EBS General Purpose SSD** (most regular servers)
	- **HDD Volumes** (where quick access isn't as important.)
- All EBS volumes can be copied by creating a snapshot. Existing snapshots can be used to generate other volumes that can be shared or attached to other instances or converted to images from which AMIs can be made.

### Instance Types
Configurations of CPU, memory, storage, etc. for your instances.
![[instance-naming2.png|550]]
##### Instance Families
- General Purpose
	- Provides a balance of compute, memory, and networking.
	- **Includes T3, T2, M5 and M4 types.**
	- t2.micro is part of the free tier and often good for experimenting, but can also be used for light-use websites.
	- T2s are burstable, which means you can accumulate CPU credits when your instance is underutilized that can be applied during high-demand periods in the form of higher CPU performance.
	- The **T4g, M4g instance types** use the AWS-designed ARM-based Graviton2 processor.
	- Mac instances are intended for developers working on applications aimed at devices in the macOS platform.
- Compute Optimized
	- Ideal for applications that benefit from high-performance processors.
	- **Includes C6i machines.**
- Memory Optimized
	- Designed to deliver fast performance for workloads that process large datasets in memory.
	- **R6i runs on 3rd-generation Intel Xeon** Scalable processors and emphasizes higher memory bandwidth and superior networking speeds.
	- The **X1e, X1, and R4** types are available with as much as 3.9TB of DRAM-based memory, and low-latency SSD storage volumes attached.
- Accelerated Computing
	- Uses hardware accelerators or co-processors to perform functions such as floating-point number calculations, graphics processing, or data pattern matching more efficiently than is possible in software running on CPUs.
	- You can achieve higher-performing general-purpose GPUs from the **P4, P3, G5, and F1 types** within the Accelerated Computing Group. (High-end NVIDIA GPUs).
- Storage Optimized
	- Designed for workloads that require high sequential read and write access to large datasets on local storage.
	- The **H1, I3, and D2 types** that currently make up the Storage Optimized family can deliver fast read/write and come with low-latency access to EBS instance storage volumes.
- HPC Optimized
	- Purpose built to offer the best price performance for running HPC workloads at scale on AWS.

| Instance type family  | Types                                                                                                                                                |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| General purpose       | Mac, T4g, T3, T2, M6g, M6i, M6a, M5, M5a, M5n, M5zn, M4, A1<br>![[general-purpose.png]]                                                              |
| Compute optimized     | C7g, C6g, C6i, C6a, Hpc6a, C5, C5a, C5n, C4<br>![[compute-optimized.png]]                                                                            |
| Memory optimized      | R6g, R6i, R5, R5a, R5b, R5n, R4, X2gd, X2idn, X2iedn, X2iezn, X1e, X1, High Memory, z1d<br>![[memory-optimized.png]]                                 |
| Accelerated computing | P4, P3, P2, DL1, Trn1, Inf1, G5, G5g, G4dn, G4ad, G3, F1, VT1                                                                                        |
| Storage optimized     | Im4gn, Is4gen, I4i, I3, I3en, D2, D3, D3en, H1                                                                                                       |
| See also:             | [[04_02-Instance-Types-Detailed]]<br>AWS Docs: [Amazon EC2 instance types](https://docs.aws.amazon.com/ec2/latest/instancetypes/instance-types.html) |
### AMIs (Amazon Machine Images)
![[ami-overview.jpg|300]]
Preconfigured templates for your instances that package the components you need for your server.
##### Finding AMIs
- Quick Start AMIs
- AWS Marketplace AMIs
- My AMIs
- Community AMIs
- Custom image (using EC2 Image Builder)
One of the advantages of using AMIs is that they are reusable. Your new instance could have the same configurations as your current instance if the configurations set in the AMI are the same.
Each AMI in the AWS Management Console has an AMI ID, which is prefixed by `ami-`, followed by a random hash of numbers and letters. The IDs are *unique* to each region.
An AMI includes the OS, storage mapping, architecture type, launch permissions, and any additional preinstalled software applications.
### Accessing Amazon EC2
- Amazon EC2 console
- AWS CLI
- AWS CloudFormation
- AWS SDKs
- AWS Tools for PowerShell
- Query API
### EC2 Pricing
- Free Tier
- On-Demand
	- Pay for instances by the second, min of 60 seconds. No long-term commitments or upfront payments required.
	- Use cases:
		- Users who prefer low cost and flexibility without upfront payment or long-term commitments
		- Applications with short-term, spiky, or unpredictable workloads that cannot be interrupted.
		- Applications being developed or tested on Amazon EC2 for the first time.
- Savings Plan
	- Flexible pricing model that offers low usage prices for 1-year or 3-year term commitment to a consistent amount of usage. Savings Plans apply to Amazon EC2, Amazon Lambda, and AWS Fargate usage and provide up to 72% savings on AWS compute usage.
	- Use cases:
		- Workloads with a consistent and steady-state usage
		- Customers who want to use different instance types and compute solutions across different locations.
		- Customers who can make monetary commitment to use Amazon EC2 over a 1-year or 3-year term.
- Reserved Instances
	- For applications with steady state usage that might require reserved capacity, Amazon EC2 offers the Reserved Instances option. 1-year or 3-year term.
		- Standard Reserve Instances
		- Convertible Reserved Instances
		- Scheduled Reserved Instances
- Spot Instances
	- Request unused EC2 instances
- Dedicated Hosts
	- Reduce costs by using a physical EC2 server that is fully dedicated for your use, either On-Demand or as part of a Savings Plan.
	- Can be purchased on demand (hourly).
	- Can be purchased as a Reservation for up to 70% off the On-Demand price.
### EC2 Instance Lifecycle
![[ec2-lifecycle.jpg]]
1. When you launch an instance, it enters the `pending` state. When an instance is pending, billing has not started. Prepares to enter the running state.
2. When your instance is `running`, it's ready to use, and the billing stage begins.
3. When you reboot an instance, it's different than performing a stop action and start action. `Rebooting` an instance is equivalent to rebooting an OS.
4. When you stop your instance, it enters the `stopping` then `stopped` state. You can stop and start an instance if it has an Amazon EBS volume as its root device.
5. When you `terminate` an instance, the instance stores are erased, and you lose both the public IP address and private IP address of the machine. Termination of an instance means that you can no longer access the machine. You stop incurring charges.
🎯 Difference between `stop` and `stop-hibernate`: When you stop an instance, it enters the stopping state until it reaches the stopped state. When you stop-hibernate an instance, Amazon EC2 signals the OS to perform hibernation (suspend-to-disk), which saves the contents from the instance RAM to the EBS root volume.
Further Reading: [Prerequisites for Amazon EC2 instance hibernation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/hibernating-prerequisites.html)
### EC2 Image Builder
![[icon_ec2-image-builder.png|62]]
![[EC2-Image-Builder.jpg]]
EC2 Image Builder simplifies the building, testing, deployment of VMs and container images for use on AWS or on-premises. Significantly reduces the effort of keeping images up-to-date and secure by providing a simple graphical interface, built-in automation, and AWS-provided security settings. Offered at no cost.

# Containers
![[container-icon.jpg|50]]
Container images contain the code and the environment necessary to run the code (libraries, settings, etc).
#### Considerations for Containers
Ideal for:
- Compute-intensive workloads
- Large monolithic applications.
- When you need to scale quickly.
- When you need to move your large application to the cloud without altering the code.
When *not* to use for:
- Applications that need persistent data storage (it can support persistent storage however it tends to be easier to containerize the applications that don't require persistent storage).
- Applications that have complex networking, routing, or security requirements - makes it more challenging for portability.
### Amazon EKS (Elastic Kubernetes Service)
![[eks-icon.jpg|50]]
Kubernetes is an open source container orchestrator originally built by Google. Plays a largely similar role as ECS, but isn't tied to any one platform. If you already use Kubernetes, you can use Amazon EKS to orchestrate the workloads in the AWS Cloud
💡 An EKS container is called a pod.
### Amazon ECS (Elastic Container Service)
![[icon_ecs.png|62]] 
Amazon ECS is an end-to-end container orchestration service that helps you spin up new containers. You can use ECS to define your application, selecting the container images, environment services and other elements your application will need. ECS will oversee the provisioning the necessary AWS instances, storage, and networking resources, and provide the tools to monitor and administer your deployment through its life cycle.
You have the option to run your tasks and services on a serverless infrastructure that's managed by another AWS service called AWS Fargate.
💡 An ECS container is called a task
![[ecs-core.jpg]]
A bit of history:
- Containers are often thought as recent, but the idea started in the 1970s with certain Linux kernels. Today, containers are used as a solution to problems of traditional compute.
- A container is a standardized unit that packages your code and its dependencies. This package is designed to run reliably on any platform.
- Docker is popular container runtime.
##### Differences between VMs and Containers:
![[vms-vs-containers.jpg]]
- A container is more lightweight, spins up quicker, ideal for applications that must scale quickly during I/O bursts.
- Containers provide speed, but VMs offer the full OS, and more resources, etc.

| Amazon EKS                                                                           | Amazon ECS                                                                                                                                                               |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| - The machine that runs the containers is called a worker node or a Kubernetes node. | - The machine that runs the containers is an EC2 instance that has an ECS agent installed and configured to run and manage your containers, called a container instance. |
| - An EKS container is called a pod.                                                  | - An ECS container is called a task.                                                                                                                                     |
| - Runs on Kubernetes.                                                                | - Runs on AWS native technology.                                                                                                                                         |
Further Reading:
- [Amazon EC2 container instances for Amazon ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/create-capacity.html)
- [What is Amazon EKS?](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html)
# Serverless
![[serverless-icon.jpg|50]]
A way for you to build and run applications and services without thinking about servers.
Running your code on servers that are built, managed, and maintained by AWS. Serverless computing always refers to the development of applications.
#### Advantages of Serverless:
- There are no servers to provision or manage.
- It scales with usage.
- You never pay for idle resources
- Availability and fault tolerance are built in.
#### Considerations for serverless applications
Questions to ask:
- Want to only focus on your code and not on infrastructure?
- Are your applications less compute intensive?
- Small, simple or modular?
- Need to be using multiple AWS services where one service might need to call another service?
- Applications that don't run longer than 15 minutes?
## [AWS Fargate](https://docs.aws.amazon.com/pdfs/AmazonECS/latest/developerguide/ecs-dg.pdf#AWS_Fargate)
![[icon-fargate.jpg|50]]
AWS Fargate is a purpose-built serverless compute engine for containers. It scales and manages the infrastructure. Fargate supports both Amazon ECS and Amazon EKS architecture and provides workload isolation and improved security by design.
AWS Fargate abstracts the EC2 instance so that you are not required to manage the underlying compute infrastructure.
##### Use Cases:
- Web apps, APIs, microservices...
- AI/ML applications
- Data processing
Also:
- You can create an empty ECS cluster, then launch Tasks as Fargate
- You no longer have to provision, configure, scale clusters of EC2 instances to run containers.
![[aws-fargate-vs-ecs.jpg|600]]
## AWS Lambda
![[icon-aws-lambda.jpg|50]]
Lambda handles everything required to run your code based on the incoming request or event and will scale automatically as needed. You upload your source code in one of the languages that Lambda supports, and Lambda takes care of everything required to run and scale your code with high availability.
You have the option of configuring your Lambda functions using the Lambda console, API, AWS CloudFormation, or AWS Serverless Application Model (AWS SAM).
AWS Lambda integrates with other AWS services to invoke Lambda functions. A Lambda function is custom code that you write in one of the languages that Lambda supports.
- An event source is the entity that publishes the event to Lambda
- Lambda functions are stateless, having no affinity to the underlying infrastructure.
When you create a Lambda function, you define the permissions for the function and specify which events trigger the function.
###### Function
A function is a resource that you can invoke to run your code in Lambda.
- You can:
	- Create the function from scratch
	- Use a blueprint that AWS provides
	- Select a container image to deploy for your function.
	- Browse the AWS Serverless Application Repository.
###### Trigger
Triggers describe when a Lambda function should run. A trigger integrates your Lambda function with other AWS services and event source mappings.
###### Event
An event is a JSON formatted document that contains data for a Lambda function to process. The runtime converts the event to an object and passes it to your function code.
###### Application Environment
An application environment provides a secure and isolated runtime environment for your Lambda function. An application environment manages the processes and resources that are required to run the function.
###### Deployment Package
You deploy your Lambda function code using a deployment package.
- .zip file archive: This contains your function code and its dependencies.
- container image: Compatible with the OCI (Open Container Image) specification.
###### Runtime
The runtime provides a language-specific environment that runs in an application environment. When you create your Lambda function, you specify the runtime that you want your code to run in. You can use built-in runtimes, such as Python, Node.js, Ruby, Go, Java, or .NET Core. Or you can implement your Lambda functions to run on a custom runtime.
###### Lambda function handler
The AWS Lambda function handler is the method in your function code that processes events. When your function is invoked, Lambda runs the handler method. When the handler exits ro returns a response, it becomes available to handle another event.
You can use the following general syntax when creating a function handler in Python:
```
def handler_name(event, context):
...
return some_value
```
- `handler()` - function to be run upon invocation
	- The handler always takes two objects: the `event` object and the `context` object.
- `event` object - data sent during Lambda function invocation
	- provides information about the event that triggered the Lambda function
- `context` object - methods available to interact with runtime information.
	- generated by AWS and provides metadata about the runtime environment.
		- `awsRequestId` property - used to track specific invocations of a Lambda function
		- `logStreamName` - CloudWatch log stream that your log statements will be sent to.
		- `getRemainingTimeInMillis()` - Method returns the number of milliseconds that remain before the running of your function times out.
###### Lambda function configurations: Memory and Timeout
Memory and timeout are configurations that determine how your Lambda function performs. They also affect your billing.
- Memory: You specify the amount of memory you want to allocate to your Lambda function.
- Timeout: You can control the maximum duration of your function by using the timeout configuration.
	- You can set the timeout value for a function to any value up to 15 minutes.
Follow these best practices
- Test the performance of your Lambda function to make sure that you choose the optimum memory size configuration.
- Load-test your Lambda function to analyze how long your function runs and determine the best timeout value.
###### Lambda Layers
- Enable functions to share code easily
- Promote separation of responsibilities
- Enables you to keep your deployment packages small.
- Limits:
	- Up to 5 layers
	- 250 MB
See also: [Managing Lambda dependencies with layers](https://docs.aws.amazon.com/lambda/latest/dg/chapter-layers.html)

###### Further Reading:
- [Configuring Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-functions.html)
- [Best practices for organizing larger serverless applications](https://aws.amazon.com/blogs/compute/best-practices-for-organizing-larger-serverless-applications/)
- [Resizing Images on the Fly with Amazon S3, AWS Lambda, and Amazon API Gateway](https://aws.amazon.com/blogs/compute/resize-images-on-the-fly-with-amazon-s3-aws-lambda-and-amazon-api-gateway/)
- [Cost Saving Example](https://aws.amazon.com/blogs/aws/new-for-aws-lambda-1ms-billing-granularity-adds-cost-savings/)
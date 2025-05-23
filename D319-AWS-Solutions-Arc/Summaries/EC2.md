### Elastic Compute Cloud
![[icon_ec2.png]]
##### Instance Types
- General Purpose: Balance of compute, memory, and networking resources
- Compute Optimized: Ideal for compute bound paplications that benefit from high performance processing.
- Memory Optimized: Fast performance for workloads that process large data sets in memory.
- Accelerated Optimized: Hardware accelerators, co-processors
- Storage Optimized: High sequential read and write access to very large data sets on local storage.

- Instance Sizes generally double in price and key attributes.
- Placement Groups let you choose the logical placement of your instances to optimize for communication, performance, or durability. 
	- Placement groups are free.
- **`UserData`**: A script that will automatically run when launching an EC2 instance.
- **`MetaData`**: Meta data about the current instance.
- **Instance Profiles**: A container for an IAM role that you can use to pass role information to an EC2 instance when the instance starts.
### Pricing Models
- On-Demand
	- No commitment, low cost initially, flexible. Pay by hour.
	- Use case: Short-term, spiky, unpredictable workloads, first time apps
	- Ideal when your workloads cannot be interrupted.
- Reserved Instances (RI)
	- Best long-term (75% off)
	- Use case: Steady or predictable usage.
	- Can resell unused reserved instances (Reserved Instance Marketplace)
	- Terms: 1 or 3 year
	- Payment Options: All Upfront, Partial Upfront, No Upfront.
	- Class Offerings:
		- Standard: Up to 75% reduced pricing compared to on-demand. Cannot change RI attributes.
		- Convertible: Up to 54% reduced pricing compared to on-demand. Allows to change RI attributesif greater or equal in value.
		- Scheduled: You reserve instances for specific time periods once a week for a few hours. Savings vary.
- Spot Pricing
	- 90% off. Request spare computing capacity. Flexible start/end times.
	- Use case: Can handle interruptions, non-critical background jobs.
	- Instances can be terminated by AWS at anytime.
	- If your instance is terminated by AWS, you don't get charged for a partial hour of usage.
	- If you terminate an instance you will still be charged for any hour that it ran.
- Dedicated Hosting
	- Most expensive.
	- Dedicated servers. Can be on-demand or reserved. Up to 70% off.
	- Use case: When you need a guarantee of isolate hardware (enterprise).
### AMI (Amazon Machine Image)
- Provides information required to launch an instance.
- AMIs are region specific, if you need to use an AMI in another region you can copy an AMI into the destination region via Copy AMI.
- You can create an AMI from an existing EC2 instance that's either running or stopped.
- Community AMIs are free AMIs maintained by the community.
- AWS Marketplace free or paid subscription AMIs maintained by vendors.
- AMIs have an AMI ID. The same AMI will vary in bother AMI ID and options.
##### AMI Components
- Template for the root volume for the instance.
- Launch permissions that control which AWS accounts can use the AMI to launch instances.
- A block device mapping that specifies the volumes to attach to the instance when it's launched.

### Auto-Scaling Groups (ASGs)
An ASG is a collection of EC2 instances grouped for scaling and management.
- Scaling Out = Add servers
- Scaling In = Remove servers
- Scaling Up: Increate the size of an instance.
Size of an ASG is based on a Min, Max, and Desired Capacity.
- Target Scaling policy: scales based on when a target value for a metric is breached. Average CPU Utilization exceed 75%.
- Simple Scaling policy triggers a scaling when an alarm is breached.
- Scaling Policy with Steps: new version of Simple Scaling Policy and allows you to create steps based on alarm values.
- Desired Capacity is how many EC2 instances you want to ideally run.
- An ASG will always launch instances to meet minimum capacity.
- Health checks determine the current state of an instance in the ASG
- Health checks can be run against either an ELB or the EC2 instances.
- When an Autoscaling launches a new instance it uses a Launch Configuration which holds the configuration values for that new instance AMI, Instance Type, Role.
- Launch Configurations cannot be edited and must be cloned or a new one created.
- Launch Configurations must be manually updated in by editing the Auto Scaling settings.
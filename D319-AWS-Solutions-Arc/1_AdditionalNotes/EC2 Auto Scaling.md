( From: [[Elasticity]] )

![[icon_EC2_autoscaling.jpg|50]]
Amazon EC2 Auto Scaling helps you maintain application availability and enables you to automatically add/remove EC2 instances according to policies that you define, schedules, and health checks.
- Integrates with Elastic Load Balancing
- Enables you to build highly available architectures that span multiple Availability Zones in a Region.
- If one Availability Zone becomes unhealthy or unavailable, Amazon EC2 Auto Scaling launches new instances in an unaffected Availability Zone.
#### Scheduled Scaling
Scaling actions are performed automatically as a function of date and time.
Example: Turning off your dev and test instances at night.
##### Dynamic or On-Demand Scaling
Enables you to define parameters that control the scaling process.
Example: Scaling based on CPU utilization
###### Dynamic scaling policy types:
- Simple scaling: single scaling adjustment
- Step scaling: Adjustment depends on size of alarm breach.
	- choose scaling metrics and threshold values for CloudWatch alarms that trigger the scaling process.
- Target tracking scaling: Target value for specific metric.
#### Predictive
Your capacity scales based on predicted demand. Uses machine learning based on data that is collected from your actual Amazon EC2 usage, and the data is further informed by billions of data points that are drawn from observations by AWS.
Use case: Handling an increase in workload for ecommerce website during a sale event.
### Auto-scaling Groups (ASGs)
![[ec2_auto_scaling-diagram.jpg]]
You can specify the minimum number of instances in each Auto Scaling Group and Amazon EC2 Auto-Scaling helps ensure that your group never goes below this size. You can also specify the maximum number of instances in each Auto Scaling group and Amazon EC2 Auto Scaling helps ensure that your group never goes above this size.
If you specify the desired capacity, either when you create the group or at any time after you create it, Amazon EC2 Auto Scaling helps ensure that your group has this many instances.

> [!note]
> Fargate does not use ASGs
##### Auto Scaling Purchasing Options
When you configure an Auto Scaling group, you can specify the EC2 instance type that it uses:
- On-Demand
- Reserved
- Spot
See Also: [Auto Scaling Groups with multiple instance types and purchase options.](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-mixed-instances-groups.html)
##### EC2 Auto Scaling Considerations
- Multiple types of automatic scaling. You might need to implement a combination of scheduled, dynamic, and predictive scaling.
- When to scale out or scale in. Try to scale out early and fast. Scale in slowly over time.
- Use of lifecycle hooks. Lifecycle hooks enable you to perform custom actions by pausing instances when an Auto Scaling group launches or terminates them. When an instance is paused, it remains in a wait state either until you complete the lifecycle action by using the complete-lifecycle-action command, or until the timeout period ends (1 hour by default.)
	- See also: [Amazon EC2 Auto Scaling Lifecycle Hooks](https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html)
##### Dynamic scaling policy types:
- Simple scaling: Increase or decrease the current capacity of the group based on a single scaling adjustment.
- Step scaling: policies increase or decrease the current capacity of the group based on a set of scaling adjustments, known as step adjustments, that vary based on the size of the alarm breach.
- Target Tracking Scaling
- Predictive Scaling
##### ASG Use Case
![[autoscaling-use.jpg]]
1. Burst of traffic from the internet hits domain.
2. Route53 points to Load Balancer
3. Load Balancer passes the traffic to its target group.
4. The target group is associated with our ASG and sends the traffic to instances registered with our ASG.
5. The ASG Scaling Policy checks if instances are near capacity.
6. The Scaling Policy determines if we need another instance, and it launches a new EC2 instance with the associated Launch Configuration to our ASG.
##### ASG Capacity Settings
- Min Size
	- `--min-size 2`
- Max Size
	- `--max-size 10`
- Desired Capacity
	- `--desired-capacity 2`
🎯ASG will always launch instances to meet minimum size capacity
##### Health Check Replacements
![[asg-healthcheck.jpg]]
Health Check Replacement is when an ASG replaces when the instance is considered unhealthy. There are two types of health checks ASG can perform:
- **EC2 Health Check**
	- If the EC2 instance fails either of its EC2 Status Checks
- **ELB Health Check**
	- ASG will perform a health check based on the ELB health check. ELB pings an HTTP endpoint at a specific path, port, and status code.
![[asg-health-cli.jpg]]

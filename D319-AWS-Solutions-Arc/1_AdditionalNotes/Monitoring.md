Monitoring can help you:
- Track how your resources are operating and performing.
- Track resource utilization and application performance to make sure that your infrastructure is meeting demand.
- Decide what permissions to set for your AWS resources to achieve the security goals that you want.
Monitoring can also help you understand and manage the cost of your AWS infrastructure.
- **AWS Cost Explorer**
	- Helps you to visualize, understand, and manage your AWS costs and usage with daily or monthly granularity.
- **AWS Budgets**
	- Enables you to set custom budgets that alert you when your costs or usage exceed your budgeted amount.
- **AWS Cost and Usage Report**
	- Contains the most comprehensive set of AWS cost and usage data available, including additional metadata about AWS services, pricing, and reservations.
- **The Cost Optimization Monitor**
	- A solution architecture that automatically processes detailed billing reports to provide granular metrics that you can search, analyze, and visualize in a dashboard that you can customize.
See also: [AWS Cost Management page](https://aws.amazon.com/aws-cost-management/)

## [CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
![[icon_CloudWatch.png|62]]
- Collects and tracks metrics for your resources and applications.
- Helps you correlate, visualize, and analyze metrics and logs.
- Enables you to create alarms and detect anomalous behavior.
- Can send notifications or make changes to resources that you are monitoring.
Amazon CloudWatch is a monitoring and observability service that is built for DevOps engineers, developers, site reliability engineers, and information technology managers.
##### How CloudWatch Responds
- [Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html)
	- Kept for 15 months.
- [Logs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)
	- Tracking log data can CloudWatch Logs Insights allows analyzation.
- [Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)
	- Can use to automatically initiate actions on your behalf. An alarm watches a single metric over a specified time period.
	- Invokes actions for sustained state changes only.
- [Events](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html) (Using EventBridge)
	- (Formerly known as Amazon CloudWatch Events)
	- Ingests a stream of real-time data from your own applications.
	- An event indicates a change in an environment, whether it's AWS, SaaS, or a service.
- [Rules](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-rules.html)
	- A rule matches incoming events and routes them to targets for processing. A rule can customized the JSON that is sent to the target by passing only certain parts, or by overwriting it with a constant.
- Targets
	- A target processes events. Targets can include EC2 instances, Lambda functions, Amazon Kinesis streams, Amazon ECS tasks, AWS Step Functions state machines, SNS topics, Amazon SQS queues, and built-in targets. A target receives events in JSON format.
##### Accessing CloudWatch
- Amazon CloudWatch Console
- AWS CLI
- CloudWatch API
- AWS SDKs
##### Related AWS Services
- Amazon SNS
- Amazon [[EC2 Auto Scaling]]
- AWS CloudTrail (module 8)
- IAM (module 8)
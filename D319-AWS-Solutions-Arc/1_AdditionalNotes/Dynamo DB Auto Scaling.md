
Amazon DynamoDB also has a feature called auto scaling that's enabled by default. Works with CloudWatch. Incurs no additional cost.
Further reading: [Managing throughput capacity automatically with DynamoDB auto scaling](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AutoScaling.html)
To Implement DynamoDB auto scaling:
1. Create a scaling policy for your DynamoDB table or GSI (global secondary index).
2. DynamoDB publishes consumed capacity metrics to Amazon CloudWatch.
3. If the table's consumed capacity exceeds your target utilization for a specific length of time, Amazon CloudWatch triggers an alarm. You can use Amazon SNS (Simple Notification Service) to view the alarm in the Amazon CloudWatch console.
4. The CloudWatch alarm invokes Application Auto Scaling.
5. Application Auto Scaling issues an `UpdateTable` request to DynamoDB.
6. DynamoDB processes the `UpdateTable` request and dynamically increases or decreases the table's provisioned throughput capacity so that it approaches your target utilization.
#### DynamoDB adaptive capacity
- Enables reading and writing to hot partitions without throttling
- Automatically increases the throughput capacity for partitions that receive more traffic.
- Is enabled automatically for every DynamoDB table.
- Adaptive capacity does not fix hot keys and hot partitions.
- See Also: [Designing partition keys to distribute your workload in DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-partition-key-uniform-load.html)

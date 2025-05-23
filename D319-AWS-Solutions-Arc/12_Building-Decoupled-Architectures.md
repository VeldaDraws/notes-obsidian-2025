Traditional infrastructures have chains of tightly integrated components. Each component has a specific purpose. When one component goes down, the disruption to the system can be fatal. In a tightly coupled system, scaling is also impeded.
##### Forms of System Coupling
A system can be coupled in many ways, and you should consider them when you build distributed applications in the cloud:
- Application-level coupling relates to managing incoming and outgoing dependencies.
- Platform coupling relates to the interoperability of heterogeneous systems components.
- Spatial coupling relates to managing components at a network-topology level or protocol level
- Temporal coupling refers to the ability of a system component to do meaningful work while it performs a synchronous, blocking operation.
##### Loosely Coupled Architectures
Use managed solutions as intermediaries between layers.
![[decoupling1.png]]
From: [Decoupling larger applications with Amazon EventBridge](https://aws.amazon.com/blogs/compute/decoupling-larger-applications-with-amazon-eventbridge/)
##### Message Queues for Decoupling Architectures
- A message is for communication between software components.
- Message queues provide communication and coordination for these distributed applications
- To send a message, a component that is called a producer adds a message to the queue. The message is stored in the queue until another component that is called a consumer retrieves and processes it.
# Amazon SQS (Simple Queue Service)
![[icon_SQS.jpg]]
- Fully managed message queueing service
- Uses a pull mechanism
- Messages are encrypted and stored until they are processed and deleted.
- Acts as a buffer between producers and consumers.
A queue is a temporary repository for messages that are waiting to be processed. Messages are stored until they are processed and deleted. Messages can contain up to 256 KB of text in any format. Amazon SQS works on a massive scale and processes billions of messages per day.
You can securely share Amazon SQS queues anonymously or with specific AWS accounts. Messages in SQS queues are encrypted with SSE by using keys that are managed in the AWS KMS.
##### Amazon SQS enables
- Asynchronous processing.
- Handle performance and service requirements.
- Easily recover from failed steps because messages will remain in the queue.
##### Amazon SQS General Use Cases
- Work Queues
- Buffering Batch Operations
- Request Offloading
- Trigger Amazon EC2 Auto Scaling
##### Queue Types
- Standard queues
	- At-least-once delivery: A message is delivered at least once, but occasionally more than one copy of a message is delivered.
	- Best-effort ordering: Might be delivered in a different order that is different from the order that they were sent in.
	- Unlimited Throughput
- FIFO queues (First in, first out)
	- Designed to guarantee that the messages are processed sequentially once.
	- Provides high throughput.
##### Dead-letter queue (DLQ) support
Amazon SQS features a dead-letter queue support. A DLQ is a queue of messages that could not be processed.
##### Visibility timeout
Period of time when Amazon SQS prevents other consumers from receiving and processing the same message.
##### Long polling
Queries all the servers for messages.
#### Amazon SQS Message Life Cycle
1. Create: Producer sends a message to queue, which gets distributed redundantly
2. Process: Message gets picked up for processing by a consumer, and the visibility timeout starts. During the timeout, other consumers cannot process the message.
3. Delete: Message gets deleted by the consumer after it is processed.
See also: Blog Post: [Use Case example](https://aws.amazon.com/blogs/compute/building-loosely-coupled-scalable-c-applications-with-amazon-sqs-and-amazon-sns/)

 Message queue use cases:
✔Service-to-service communication
✔Asynchronous work items
✔State change notifications
Not ideal for:
❌selecting specific messages
❌large messages
## Pub/sub messaging
Publish/subscribe messaging provides instant event notifications for distributed applications. Enables messages to broadcast to different parts of a system asynchronously.
## Amazon SNS
![[icon_SNS.jpg]]
- Highly available, durable, secure, and fully managed pub/sub messaging service
- Uses a push mechanism
- Supports encrypted topics using CMKs (customer master keys)
Amazon SNS is designed to meet the needs of the largest and most demanding applications, and it enables applications to publish an unlimited number of messages at any time.
When Amazon SNS receives your messages, they are encrypted by using a 256-bit AES-GCM. The encrypted messages are stored redundantly across multiple servers and data centers.
##### Supported Transport Protocols
- Email or Email-JSON
- HTTP or HTTPS
- SMS clients
- Amazon SQS queues
- AWS Lambda functions
##### Use cases for Amazon SNS
- Application and system alerts
- Push email and text messaging
- Mobile push notifications
##### Amazon SNS considerations
- Each notification message contains a single published message
- When a message is delivered successfully, there is no way to recall it.
- Amazon SNS will attempt to deliver messages from the publisher in the order that they were published into the topic.
##### Using Amazon S3 with Amazon SNS
You can use Amazon SNS to send messages in a single account or to resources in different accounts. AWS services can publish messages to your SNS topics to trigger event-driven computing and workflows.
##### Amazon SNS 4-phase retry policy
1. Retries with no delay in between attempts
2. Retries with minimum delay between attempts
3. Retries according to a back-off model
4. Retries with max delay between attempts. When the message delivery retry policy is exhausted, Amazon SNS can move the message to a DLQ.
### Amazon SNS vs Amazon SQS
- Amazon SNS uses a pub/sub messaging paradigm and enables applications to send time-critical messages to multiple subscribers through a push mechanism.
- Amazon SQS uses a send/receive messaging paradigm and exchanges messages through a polling model.
- Amazon SQS provides flexibility for distributed components of applications. They can send and receive messages without requiring that each component must be concurrently available.
## Amazon MQ
![[icon_AmazonMQ.jpg]]
Amazon MQ is a managed message broker service for Apache ActiveMQ that enables you to set up and operate message brokers in the cloud. Message brokers enable different software systems - which often use different programming languages on different platforms - to communicate and exchange information.
Amazon MQ reduces your operational load by managing your provisioning, setup, and maintenance of ActiveMQ, a popular open-source message broker.
With Amazon MQ, you can migrate messaging to the cloud while preserving the existing connections between your applications.
It's compatible with open-standard APIs and protocols:
- JMS, NMS, AMQP, STOMP, MQTT, WebSockets.
![[integrating-on-premises-and-cloud-environments.jpg]]
Amazon MQ enables organizations to send messages between applications in the cloud and applications that are on premises to enable hybrid environments and application modernization.

| Amazon MQ                                  | Amazon SQS and SNS                 |
| ------------------------------------------ | ---------------------------------- |
| For application migration                  | For born-in-the-cloud applications |
| JMS, NMS, AMQP, STOMP, MQTT and WebSockets | HTTPS                              |
| Pay per hour / GB                          | Pay per request                    |
| Can do pub/sub                             | Pub/sub in Amazon SNS              |
- If you use messaging with existing applications, and want to move your messaging to the cloud, AWS recommends using Amazon MQ.
- If you are building new applications in the cloud, AWS recommends using Amazon SQS and Amazon SNS.

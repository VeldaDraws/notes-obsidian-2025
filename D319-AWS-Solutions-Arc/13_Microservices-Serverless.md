**Microservices** Definition: Applications that are composed of independent services that communicate over well-defined APIs.
The microservices approach fosters innovation and ownership, and improves the maintainability and scalability of software applications
##### Monolithic vs [Microservice](https://aws.amazon.com/microservices/) applications
Monolithic applications run as a single service and are tightly coupled. If one process of the application experiences a spike in demand, the entire architecture must be scaled. Adding or improving features becomes more complex as the code base grows, which limits experimentation and makes it difficult to implement new ideas.
A microservice architecture provides much quicker iteration, automation, and overall agility. Start fast, fail fast, and recover fast. The services communicate by using lightweight API operations. Each service performs a single function that can support multiple applications. Because the services run independently, they can be updated, deployed, and scaled to meet the demand for specific functions of an application.
#### Characteristics of Microservices
- Decentralized
	- Distributed systems with decentralized data management. Doesn't rely on a unifying schema in a central database.
- Independent
	- Each component service can be changed, upgraded, or replaced independently without affecting the function of other services. Services do not need to share any of their code or implementation with other services.
- Specialized
	- Each componen service is designed for a set of capabilities and focuses on a specific domain.
- Polyglot
	- Microservices don't follow a single approach. Teams have freedom to choose the best tool for their specific problem.
- Black boxes
	- Individual component services are designed as black boxes, which mean that the details of their complexity are hidden from other components.
- DevOps
	- A key organizational principle for microservices, where the team responsible for building a service is also responsible for operating and maintaining it in production.
#### Containers in a Microservice Architecture
When you build a microservice architecture, you can use containers for the processing power.
Containers are a method of operating system virtualization that enables you to run an application and its dependencies in resource isolated processes. A container is a lightweight, standalone software package. It contains everything that a software application needs to run, such as the application code, runtime engine, system tools, system libraries, and configurations.
###### A problem that containers solve
Getting software to run reliably in different work environments.
- Developer's workstation
- Production environment
- Test environment
Containers can help ensure that applications deploy quickly, reliably, and consistently, regardless of deployment environment. A container is created from a read-only template that is called an image, typically built from a Dockerfile.
(To review: [[04_Compute-Layer#Containers]] )
After a cluster is up and running, you can define task definitions and services that specify which Docker container images to run across your clusters.
- A task definition is a text file in JSON format. Describes 1 up to 10 containers that form your application.
- Other parameters include which ports should be opened for your application and what data volumes should be used with the containers in task.
A service enables you to specify how many copies of your task definition to run and maintain in a cluster. You can optionally use an Elastic Load Balancing load balancer to distribute incoming traffic containers in your service.
See also: Case Study: [Coursera's transition from monolithic](https://aws.amazon.com/solutions/case-studies/coursera-ecs/)
#### AWS ECS launch types
###### [Fargate Launch Type](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/launch-type-fargate.html) (Part of the ECS Developer Guide Whitepaper)
![[fargate-launch-type.jpg]]
Host your cluster on a serverless infrastructure that Amazon ECS manages.
- pay-as-you-go
- allows focus on building applications without managing servers.
You have more control with Fargate than EC2 because you select the exact CPU and memory that your application needs.
See also: [AWS Fargate for Amazon ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html)
###### [EC2 Launch Type](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/launch-type-ec2.html) (Part of the ECS Developer Guide Whitepaper)
![[ec2-launch-type.jpg]]
A container instance is an EC2 instance that is running the Amazon ECS Container agent.
#### Amazon ECS cluster auto-scaling
You can create an Auto Scaling group for an Amazon ECS cluster. The Auto Scaling group contains container instances that you can scale out and in by using Amazon CloudWatch alarms. If you configure your Auto Scaling group to remove container instances, any tasks that are running on the removed container instances are stopped.
You can also take advantage of Amazon ECS cluster auto scaling, which gives you more control over how you scale tasks in a cluster.
#### Decomposing Monoliths:
1. Create container images, build and tag an image for each service. Then, register the images with Amazon Elastic Container Registry (ECR).
2. Choose launch type and create a new service for each piece of the original monolithic application. Amazon ECS deploys each service into its own container across an ECS cluster. Then create a target group for each service.
3. Connect load balancer to services. Create an Application Load Balancer and configure listener rules to connect to the services. The listener checks for incoming connection requests to your load balancer and uses the rules to route traffic appropriately.
### [AWS Cloud Map](https://aws.amazon.com/cloud-map/)
![[icon_awscloudmap.jpg|50]]
- Fully managed discovery service for cloud resources.
- Can be used to define custom names for application resources.
- Maintains updated location of dynamically changing resources, which increases application availability.
### [AWS App Mesh](https://aws.amazon.com/app-mesh/)
![[icon_awsappmesh.jpg|50]]
- Captures metrics, logs, and traces from all your microservices.
- Enables you to export this data to Amazon CloudWatch, AWS X-Ray, and compatible AWS Partner Network (APN) and community tools.
- Enables you to control traffic flows between microservices to help ensure that services are highly available.

## AWS Fargate
[[04_Compute-Layer#AWS Fargate]]
- Works with Amazon ECS and Amazon EKS
- Provisions, manages, and scales your container clusters

# Serverless
[[04_Compute-Layer#Serverless]]
![[icon_serverless.png]]
#### Tenets of Serverless Architecture
- No infrastructure to provision or manage
- Automatically scales by unit of consumption (rather than by server unit)
- Pay-for-value pricing model
- Built-in availability and fault tolerance
#### Benefits of Serverless
- Lower total cost of ownership
- Focus on your application, not configuration
- Build microservice applications
![[aws-serverless.jpg]]
(Coursework focuses on AWS Lambda, Amazon API Gateway, and AWS Step Functions)

## AWS Lambda and Lambda@Edge
( Review: [[04_Compute-Layer#AWS Lambda]] )
AWS Lambda is a fully managed compute service that runs your code in response to events and automatically manages the underlying compute resources for you. Lambda runs your code on a high-availability compute infrastructure.
Natively supports:
- Java
- Go
- PowerShell
- Node.js
- C#
- Python
- Ruby
### Lambda@Edge
A feature of Amazon CloudFront that enables you to run the code closer to users of your application, which improves the performance and reduces latency. Runs your code in response to events that are generated by Amazon CloudFront content delivery network (CDN).
## Amazon API Gateway
![[icon_APIgateway.jpg|50]]
Amazon API Gateway is a fully managed service that enables you to create, publish, maintain, monitor, and secure APIs at any scale. You can use it to create Representational State Transfer (RESTful) and WebSockets APIs that act as an entry point for applications so they can access backend resources. Applications can then access data, business logic, or functionality from your backend services.
- Handles up to 100s of thousands of concurrent API calls
- Can handle workloads that run on:
	- Amazon EC2
	- Lambda
	- Any web application
	- Real-time communication applications
- Can host and use multiple versions and stages of your APIs
#### Amazon API Gateway security
You can optionally set your API methods to require authorization.
- You can use AWS Signature Version 4 or Lambda authorizers
	- AWS Signature Version 4 is the process to add authentication information to AWS requests sent through HTTP.
	- A Lambda authorizer is a Lambda function that authorizes access to APIs by using a bearer token authentication strategy like OAuth.
- You can also apply a resource policy to a API to restrict access to a specific Amazon VPC or VPC endpoint.
Amazon API Gateway supports throttling settings for each method or route in your APIs. You can set a standard rate limit and burst rate limit per second for each method in your REST APIs and each route in WebSocket APIs.
You can use AWS WAF to secure your API Gateway APIs. AWS WAF is a web application firewall that helps protect your web applications from common web exploits that could affect availability, compromise security, or consume excessive resources.
## AWS Step Functions
![[icon_stepfunc.jpg|50]]
![[stepfunc.png|400]]
AWS Step Functions is a web service that enables you to coordinate components of distributed applications and microservices by using visual workflows.
See also:
- Example usage: [Taco Bell](https://www.youtube.com/watch?v=sezX7CSbXTg)
- Developer Guide: [What is Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
AWS Step Functions manages the logic of your application for you. It implements basic primitives, such as running tasks sequentially or in parallel, branching, and timeouts. This technique removes extra cofe that might be repeated in your microservices and functions. You can automatically retry failed or timed-out tasks.
AWS Step Functions enables you to create and automate your own state machines within the AWS environment by using the JSON-based Amazon States Language. This language contains a structure that is made of various states, tasks, choices, error handling and more.
A state machine is a collection of states that can do work.
- States are elements in your state machine. Individual states can make decisions based on their input, perform actions, and pass output to other states.
- A finite state machine can express an algorithm as a number of states, their relationships, and their input and output.
### State Types
| Task     | A single unit of work performed by a state machine.      |
| -------- | -------------------------------------------------------- |
| Choice   | Adds branching logic to a state machine                  |
| Fail     | Stops a running state machine and marks it as a failure  |
| Succeed  | Stops a running state machine successfully               |
| Pass     | Passes its input to its output, without performing work. |
| Wait     | Delays from continuing for a specific time.              |
| Parallel | Creates parallel branches to run in your state machine   |
| Map      | Dynamically iterates steps                               |
Example use: 
- VOD streaming using AWS Step Functions (to model workflow), Lambda, Elemental MediaConvert, AWS Batch, ECS:
	- [Docs Guide](https://docs.aws.amazon.com/wellarchitected/latest/streaming-media-lens/scenario-video-on-demand-streaming.html)
![[vod-streaming-architecture.png]]
### Workflow Studio for Step Functions Overview
![[wfs-panel-overview.png]]
### Amazon States Language
Amazon States Language is a JSON-based, structured language. AWS Step Functions then represents the JSON structure in a real-time graphical view. Sometimes referred to as ASL code.
From: [Developer Guide - Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)
``` JSON
{
  "Comment": "An example of the Amazon States Language using a choice state.",
  "QueryLanguage": "JSONata",
  "StartAt": "FirstState",
  "States": {
    "FirstState": {
      "Type": "Task",
      "Assign": {
        "foo" : "{% $states.input.foo_input %}" 
        },
      "Resource": "arn:aws:lambda:region:123456789012:function:FUNCTION_NAME",
      "Next": "ChoiceState"
    },
    "ChoiceState": {
      "Type": "Choice",
      "Default": "DefaultState",
      "Choices": [
        {
          "Next": "FirstMatchState",
          "Condition": "{% $foo = 1 %}"
        },
        {
          "Next": "SecondMatchState",
          "Condition": "{% $foo = 2 %}"
        }
      ]
    },
    "FirstMatchState": {
      "Type" : "Task",
      "Resource": "arn:aws:lambda:region:123456789012:function:OnFirstMatch",
      "Next": "NextState"
    },

    "SecondMatchState": {
      "Type" : "Task",
      "Resource": "arn:aws:lambda:region:123456789012:function:OnSecondMatch",
      "Next": "NextState"
    },

    "DefaultState": {
      "Type": "Fail",
      "Error": "DefaultStateError",
      "Cause": "No Matches!"
    },

    "NextState": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:region:123456789012:function:FUNCTION_NAME",
      "End": true
    }
  }
}
```
More detailed specifications: [States-Languages.net](https://states-language.net/)
### Further Reading
- Step-by-Step Guide: [Learn how to get started with Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/getting-started.html)

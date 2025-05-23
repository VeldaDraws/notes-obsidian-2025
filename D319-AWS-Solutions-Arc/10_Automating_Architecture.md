## Questions to ask:
- Where do you want to put your efforts?
- How would you ideally update production servers?
- How will you debug deployments?
- How will you manage dependencies on the various systems and subsystems in your organization?
- Is it realistic that you will be able to do all these tasks through manual configurations?
## Automation Overview:
Manually creating resources and adding new features and functionality to your environment doesn't scale. Having an audit trail is important for many compliance and security situations. It's dangerous to allow anyone in your organization to manually control and edit your environments.
One of the six design principles of operational excellence is to perform operations as code. Another design principle is to make frequent, small, reversible changes.
# AWS [CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
![[icon_CloudFormation.jpg]]
Provides a simplified way to model, create, and manage a collection of AWS resources.
- Collection of resources is called an AWS CloudFormation stack.
- No extra charge (pay only for resources you create)
- Can create, update, and delete stacks.
- Enables orderly and predictable provisioning and updating of resources.
- Enables version control of AWS resource deployments.
With AWS CloudFormation, you author a document that describes what your infrastructure should be, including all the AWS resources that should be a part of the deployment. You can think of this document as a model. You then use the model to create the reality because AWS CloudFormation can actually create the resources in your account.
When you use AWS CloudFormation to create resources, it is called an AWS CloudFormation stack. You create a stack, update a stack, or delete a stack. You can provision resources in an orderly and predictable way.
Using AWS CloudFormation enables you to treat your infrastructure as code - IaC. Author it with any code editor, check it into a version control system such as GitHub or AWS CodeCommit, and review files with team members before you deploy into the appropriate environments. If the AWS CloudFormation document that you create to model your deployment is checked in to a version control system, you could always delete a stack, check out an older version of the document, and create a stack from it.
1. Define your resources in a template or use a pre-built template.
2. Upload the template to AWS CloudFormation or point to a template stored in an S3 bucket.
3. Run a create stack action. Resources are created across multiple services in your AWS account as a running environment.
4. The stack retains control of the resources that are created. You can later update the stack, detect drift, or delete the stack.
See also: [List of AWS resources that CloudFormation supports](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)

> [!note]
> Cloud Formation *Designer* is now known as *Infrastructure Composer*
> ![[icon_infra-compose.png|48]]
> ![[cf_designer.jpg]]
> 
### IaC: Infrastructure as Code
For AWS, the built-in choice for IaC is AWS CloudFormation
- IaC is the process of provisioning and managing your cloud resources by writing a template file that is:
	- Human readable
	- Machine consumable
- It is infrastructure that you can replicate, re-deploy, re-purpose
- You can roll back to the last good state on failures.
##### Benefits
- Reduce multiple matching environments
- Rapid deployment of complex environments
- Provides configuration consistency
- Simple clean up when wanted.
- Easy to propagate a change to all stacks.
- Reusability, Repeatability, Maintainability
### Cloud Formation Template Syntax
- JSON or YAML
	- YAML: Less verbose, supports embedded comments. Optimized for readability.
	- JSON: More widely used by other systems.
- Treat templates as source code
- Store in a code repository.
- Templates can also be authored in the AWS CloudFormation Designer.
- **Parameters**:
	- Specify what values can be set at runtime when you create the stack
	- Example: region-specific settings, etc.
- **Resources** (Required):
	- Define what needs to be created in the AWS account.
- **Outputs**:
	- Specify values returned after the stack is created.
	- Example: Return the instanceid, public IP, etc.
- Conditions statement:
	- A single AWS template with defined conditions can deploy a different application infrastructure to different environments.
##### Brief Example: Creating an EC2 instance in a Specified Availability Zone:
JSON:
```
"Ec2Instance": {
    "Type": "AWS::EC2::Instance",
    "Properties": {
        "AvailabilityZone": "aa-example-1a",
        "ImageId": "ami-1234567890abcdef0"
    }
}
```
YAML:
```
Ec2Instance:
  Type: AWS::EC2::Instance
  Properties:
    AvailabilityZone: aa-example-1a
    ImageId: ami-1234567890abcdef0
```
### AWS CloudFormation Change Sets
Change sets enable you to preview changes before you implement them.
1. Create change set.
2. View change set.
3. Run change set.
- Use the `DeletionPolicy` attribute to preserve or backup a resource when its stack is deleted or updated.
### Drift Detection
Can be run on a stack by choosing Detect Drift from the Stack actions menu in the console. Performing drift detection on a stack shows you whether the stack has drifted from its expected template configuration.
### Scoping and Organizing Templates
As your org starts to use more templates, it will be important for you to have a strategy for templates.
The following is an example strategy:
- Frontend Services: Web interfaces, mobile access, analytics...
- Backend Services: Search, payments, reviews, recommendations...
- Shared Services: CRM databases, alarms, subnets, security groups...
- Network: VPCs, IGW, VPNs, NAT devices...
- Security: AWS IAM, users, groups, roles...
A good strategy is to group your resource definitions in templates similar to the way that you would organize the functionality of a large enterprise application into different parts.
### [AWS Quick Starts](https://aws.amazon.com/solutions/) (AWS Solutions)
- Gold-standard deployments.
- Based on best practices for security and high availability
- Can be used to create entire architectures with one click in less than an hour.
- Can be used for experimentation and as the basis for your own architectures.
Even if you do not use Quick Starts, you may find it helpful to look at a few of them to see the types of patterns and practices that the Quick Starts follow.
AMIs are another solution that people sometimes use, launched from the EC2 console.
# Elastic Beanstalk
![[icon_elasticbeanstalk.jpg|50]]
A painless way to get web applications up and running. It's a PaaS offering that allows you to remain in control of your code while AWS maintains the underlying infrastructure. It abstracts the provisioning of AWS compute and networking infrastructure.
- Supports a range of platforms: Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker.
- You can choose from two types of environments when you work with Elastic Beanstalk:
	- The single-instance environment enables you to launch a single EC2 instance and it does not include load balancing or automatic scaling.
	- The other type of environment, can launch multiple EC2 instances, and it includes load balancing and an automatic scaling configuration. A managed database layer is optional.
The AWS resources that are created by Elastic Beanstalk are visible in your AWS account. Your application code will run on these servers. Automatic scaling is configured, so if the load starts to stress the resources on these two instances, more application server instances will be launched automatically.
Elastic Beanstalk creates and manages scalable environments.
# AWS Systems Manager
![[icon_sysmanager.jpg|50]]
AWS Systems Manager is a management service that is designed to be highly focused on automation. It enables the configuration and management of systems that run on-premises or in AWS. AWS Systems Manager enables you to identify the instances that you want to manage, and then define the management tasks that you want to perform on those instances.
Example tasks that you can accomplish:
- Collecting software inventory
- Applying OS patches
- Creating system images
- Configuring OSs.
These capabilities can help you define and track system configurations, prevent drift, and maintain the software compliance of your Amazon EC2 and on-premises configurations.
You can install an AWS Systems Manager Agent (SSM Agent) on an EC2 instance, or even on an on-premises server, or a VM. Once the SSM Agent is installed, it will be possible for Systems Manager to update, manage, and configure the server on which it is installed.
SSM Agent is preinstalled, by default, on most AMIs, however, you must manually install the agent on EC2 instances that were created from other Linux AMIs.
See also: [Working with SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html)
AWS Systems Manager provides various tools:
- Run Bash, Powershell, Salt, or Ansible scripts.
- Maintenance Windows enables you to define a schedule for performing potentially disruptive actions on your instances.
- Parameter Store provides secure storage for configuration data and secrets management.
- Patch Manager automates the process of patching managed instances with both security-related updates and other types of updates.
- State Manager automates the process of keeping your Amazon EC2 and hybrid infrastructure in a state that you define.
- Automation enables you to built automation workflows to configure and manage instances and AWS resources.
- Session Manager enables you to manage your EC2 instances through an interactive, browser-based shell.
- Inventory provides visibility into your Amazon EC2 and on-premises computing environments.
- Documents define the actions that Systems Manager performs on your managed instances. You can use more than a dozen pre-configured documents by specifying parameters at runtime. You can also define your own documents in JSON or YAML, and specify steps and parameters.
##### AWS CloudFormation and Systems Manager
🎇AWS CloudFormation works well for defining AWS Cloud resources.
🎆Systems Manager works well for automating within guest operating systems.
You can use AWS CloudFormation at the AWS Cloud layer to define AWS resources. You can then use AWS Systems Manager to configure the OS of the instances that were created by the AWS CloudFormation stack.
See also: Blog Post: [Using AWS Systems Manager Automation and AWS CloudFormation together](https://aws.amazon.com/blogs/infrastructure-and-automation/using-aws-systems-manager-automation-and-aws-cloudformation-together/)
![[aws-cloudf-and-sysmang.png]]
# AWS OpsWorks (⚠[ended May 2024](https://docs.aws.amazon.com/opsworks/latest/userguide/stacks-eol-faqs.html))
![[icon_opsworks.jpg|50]]
See also: [Puppet's recommendations](https://www.puppet.com/blog/puppet-aws-opsworks)
⚠ (Some basic knowledge of AWS OpsWorks may show up on the SAA-C03 exam)
AWS OpsWorks is a **configuration management service**.
- Provides managed instances of Chef and Puppet
Comes in three different versions:
- **AWS OpsWorks for Chef Automate**
	- Provides a fully managed Chef Automate server that provides workflow automation for continuous deployment, and automated testing for compliance and security. The Chef Automate platform handles operational tasks, such as software and operating system configurations, continuous compliance, package installations, database setups, and more.
- **AWS OpsWorks for Puppet Enterprise**
	- Provides a managed Puppet Enterprise server and suite of automation tools that provide workflow automation for orchestration, automated provisioning, and visualization for traceability.
- **AWS OpsWorks Stacks**
	- A configuration management service that helps you configure and operate applications of all kinds and sizes by using Chef.
	- A fundamental unit of creation in an OpsWorks Stacks application is the stack.
	- After a stack is created, you can add multiple layers to that stack.
	- Layers depend on Chef recipes to handle tasks like installing packages on instances, deploying applications, running scripts, and so on.
	- One key OpsWorks Stacks feature is a set of lifecycle events: Setup, Configure, Deploy, Un-deploy, and Shutdown.


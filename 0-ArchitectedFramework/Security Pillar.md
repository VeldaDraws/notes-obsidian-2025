Docs: [Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html) (November 6, 2024 publication)
### Design Principles
- Implement a strong identity foundation.
- Maintain traceability.
- Apply security at all layers.
- Automate security best practices.
- Protect data in transit and at rest.
- Keep people away from data.
- Prepare for security events.
### Definition
- Security foundations
- IAM
- Detection
- Infrastructure protection
- Data protection
- Incident response
- Application security
## Shared Responsibility
![[Security_shared-responsibility-model.jpg]]
- AWS is responsible for protecting the infrastructure that runs all of the services offered in the AWS Cloud.
- Customer responsibility will be determined by the AWS Cloud services that a customer selects.
🎯Customers should carefully consider the services they choose as their responsibilities vary depending on the services used, the integration of those services into their IT environment, and applicable laws and regulations.
###### Examples of controls
- Inherited Controls
	- Controls that a customer fully inherit from AWS
	- Physical and Environmental controls
- Shared Controls
	- Controls that apply to both the infrastructure layer and customer layers, but in separate contexts or perspectives.
- Customer Specific
	- Controls that are solely the responsibility of the customer based on the application that they are deploying within AWS services.
## Governance
Meant to support business objectives by defining policies and control objectives to help manage risk. Achieve risk management by following a layered approach to security control objectives - each layer builds upon the previous one.
Governance is the way that decisions are guided consistently without depending solely on the good judgement of the people involved.
## AWS account management and separation
- Manage accounts centrally
	- AWS Organizations automates AWS account creation and management
		- Related notes: [[08_02-Other-AWS-Account-Practices#AWS Organizations]]
- Set controls centrally
	- Control what your AWS accounts can do by only allowing specific services, Regions, and service actions at the appropriate level.
		- Related notes: [[08_IAM]]
- Configure services and resources centrally.
### Best Practices
- SEC01-BP01 Separate workloads using accounts
- SEC01-BP02 Secure account root user and properties
	- See also: [[08_01-Root-User]]
## Operating your workloads securely
Operating workloads securely covers the whole lifecycle of a workload from design, to build, to run, and to ongoing improvement.
### Best Practices
- SEC01-BP03 Identify and validate control objectives
	- Based on your compliance requirements and risks identified from your threat model, derive and validate the control objectives and controls that you need to apply to your workload.
- SEC01-BP04 Stay up to date with security threats and recommendations
	- [MITRE ATT&CK knowledge base](https://attack.mitre.org/)
	- [CVE - Common Vulnerabilities and Exposures list](https://cve.org/)
	- [OWASP Top 10 project](https://owasp.org/www-project-top-ten/)
	- [AWS Security Bulletins](https://aws.amazon.com/security/security-bulletins/)
	- AWS services that automatically incorporate new threat intel over time:
		- [Amazon GuardDuty](https://aws.amazon.com/guardduty/): stays up to date with industry threat intelligence for detecting anomalous behaviors and threat signatures within your accounts.
		- [Amazon Inspector](https://aws.amazon.com/inspector/): automatically keeps a database of CVEs it uses for its continuous scanning features up to date.
		- Both [AWS WAF](https://aws.amazon.com/waf/) and [AWS Shield Advanced](https://docs.aws.amazon.com/waf/latest/developerguide/ddos-advanced-summary.html) provide managed rule groups that are updated automatically as new threats emerge.
- SEC01-BP05 Reduce security management scope
	- Determine if you can reduce your security scope by using AWS services that shift management of certain controls to AWS (managed services). These services can help reduce your security maintenance tasks, such as infrastructure provisioning, software setup, patching, or backups.
- SEC01-BP06 Automate deployment of standard security controls
	- (Related to SEC01-BP01)
	- Apply modern DevOps practices as you develop and deploy security controls that are standard across your AWS environments. Define standard security controls and configurations using Infrastructure as Code (IaC) templates, capture changes in a version control system, test changes as part of a CI/CD pipeline, and automate the deployment of changes to your AWS environments.
- SEC01-BP07 Identify threats and prioritize mitigations using a threat model
	- [OWASP Application Threat Modeling](https://owasp.org/www-community/Threat_Modeling)
- SEC01-BP08 Evaluate and implement new security services and features regularly
	- When you stay on top of new security services and features, you can make informed decisions about the implementation of controls in your cloud environments and workloads.
	- [AWS Security Blog](https://aws.amazon.com/blogs/security/)
	- [AWS Security Bulletins](https://aws.amazon.com/security/security-bulletins/)
	- [AWS re:Inforce](https://reinforce.awsevents.com/) (Annual security conference)
	- [AWS re:Invent](https://reinvent.awsevents.com/) (Annual general conference)
## Identity Management
- Human identities: workforce, third parties, users.
	- workforce: admin, developers, operators
	- users: consumers of your applications
	- third parties: contracts, vendors, partners
- Machine identities: These identities also include machines running within your AWS environment, like Amazon EC2 instances or AWS Lambda functions.
### Best Practices
- SEC02-BP01 Use strong sign-in mechanisms
	- [AWS Best Practice Guide](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec_securely_operate_aws_account.html)
- SEC02-BP02 Use temporary credentials
	- API and CLI requests to AWS services must, in nearly every case, be signed using [AWS access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
- SEC02-BP03 Store and use secrets securely
	- This is accomplished using secret access credentials, such as API access keys, passwords, and OAuth tokens.
	- [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)
- SEC02-BP04 Rely on a centralized identity provider
	- AWS IAM, Amazon Cognito, SAML, OIDC, etc.
- SEC02-BP05 Audit and rotate credentials periodically
- SEC02-BP06 Employ user groups and attributes
## Permissions Management
By setting permissions to specific human and machine identities, you grant them access to specific service actions on specific resources.
- Identity-based policies in AIM are *managed* or *inline*.
- Follow principle of least privilege
- etc.
### Best Practices
- SEC03-BP01 Define access requirements
- SEC03-BP02 Grant least privilege access
- SEC03-BP03 Establish emergency access process
	- [Break Glass Role](https://docs.aws.amazon.com/whitepapers/latest/organizing-your-aws-environment/break-glass-access.html) (Hardware-based MFA device recommended)
- SEC03-BP04 Reduce permissions continuously
	- Continually monitor and remove unused identities and permissions for both human and machine access.
	- Take advantage of [AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
- SEC03-BP05 Define permission guardrails for your organization
	- : You have clear isolation of environments using separate AWS accounts. Service control policies (SCPs) are used to define organization-wide permission guardrails.
- SEC03-BP06 Manage access based on lifecycle
- SEC03-BP07 Analyze public and cross-account access
- SEC03-BP08 Share resources securely within your organization
- SEC03-BP09 Share resources securely with a third party
	- You avoid using long-term AWS Identity and Access Management (IAM) credentials like access keys and secret keys, as they pose a security risk if misused. Instead, you use IAM roles and temporary credentials to improve your security posture and minimize the operational overhead of managing long-term credentials.

## Detection
(Page 99 of the PDF file)
- Detection consists of two parts: detection of unexpected or unwanted configuration changes, and the detection of unexpected behavior.
- Detection allows you to identify a potential security misconfiguration, threat, or unexpected behavior.
## Infrastructure Protection
(Page 115)
- Infrastructure protection encompasses control methodologies, such as defense in depth, that are necessary to meet best practices and organizational or regulatory obligations.
- Make sure you are familiar with Regions, Availability Zones, [AWS Local Zones](https://aws.amazon.com/about-aws/global-infrastructure/localzones/), and [AWS Outposts](https://aws.amazon.com/outposts/), which are components of the AWS secure global infrastructure.
### Protecting Networks
- When you follow the principle of applying security at all layers, you employ a [Zero Trust](https://aws.amazon.com/blogs/security/zero-trust-architectures-an-aws-perspective/) approach. Zero Trust security is a model where application components or microservices are considered discrete from each other and no component or microservice trusts any other.
- Because many resources in your workload operate in a VPC and inherit the security properties, it’s critical that the design is supported with inspection and protection mechanisms backed by automation.
##### Best Practices
- SEC05-BP01 Create network layers
	- Segment your network topology into different layers based on logical groupings of your workload components according to their data sensitivity and access requirements.
	- [Amazon VPC Lattice](https://aws.amazon.com/vpc/lattice/) can help make the interoperability of your components across network layers easier.
	- When using AWS Lambda, deploy in your subnets unless there's a specific reason not to.
	- Similar to modeling network layers based on the functional purpose of your workload's components, also consider the sensitivity of the data being processed.
- SEC05-BP02 Control traffic flow within your network layers
	- Focus on controlling traffic between the internet or other external systems to a workload and your environment (*north-south traffic*).
	- Afterwards, look at flows between different components and systems (*east-west traffic*).
- SEC05-BP03 Implement inspection-based protection
	- Traffic that traverses between your network layers are inspected and authorized. 
	- Allow and deny decisions are based on explicit rules, threat intelligence, and deviations from baseline behaviors. 
	- Protections become stricter as traffic moves closer to sensitive data.
- SEC05-BP04 Automate network protection
	- Automate the deployment of your network protections using DevOps practices, such as infrastructure as code (IaC) and CI/CD pipelines.
### Protecting Compute
Compute resources include EC2 instances, containers, AWS Lambda functions, database services, IoT devices, and more. Each of these compute resource types require different approaches to secure them.
##### Best Practices
- SEC06-BP01 Perform vulnerability management
- SEC06-BP02 Provision compute from hardened images
	- Provide fewer opportunities for unintended access to your runtime environments by deploying them from hardened images. 
	- Only acquire runtime dependencies, such as container images and application libraries, from trusted registries and verify their signatures. 
	- Create your own private registries to store trusted images and libraries for use in your build and deploy processes.
- SEC06-BP03 Reduce manual management and interactive access
- SEC06-BP04 Validate software integrity
	- Use cryptographic verification to validate the integrity of software artifacts (including images) your workload uses. 
	- Cryptographically sign your software as a safeguard against unauthorized changes run within your compute environments.
- SEC06-BP05 Automate compute protection
	- [Amazon Inspector](https://aws.amazon.com/inspector/) for continually scanning your runtime environments for known Common Vulnerabilities and Exposures (CVEs).
	- (page 140 for full implementation)
## Data Protection
(page 143)

### Protecting Data At Rest
(page 154)
- Data at rest represents any data that you persist in non-volatile storage for any duration in your workload.
- Tokenization is a process that allows you to define a token to represent an otherwise sensitive piece of information.
- Encryption is a way of transforming content in a manner that makes it unreadable without a secret key necessary to decrypt the content back into plaintext.
- Audit the use of encryption keys
##### Best Practices
- SEC08-BP01 Implement secure key management
	- AWS KMS, etc.
- SEC08-BP02 Enforce encryption at rest
	- Configure:
		- default encryption for new Amazon EBS volumes
		- encrypted AMIs
		- Amazon RDS
		- AWS KMS keys with policies that limit access to the appropriate principles for each classification of data.
		- encryption in other AWS services
- SEC08-BP03 Automate data at rest protection
- SEC08-BP04 Enforce access control
### Protecting Data In Transit

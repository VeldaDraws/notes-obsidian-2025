The ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value. Operational Excellence (OE) is a commitment to build software correctly while consistently delivering a great customer experience.
### Design Principles
- Organize teams around business outcomes.
- Implement observability for actionable insights.
- Safely automate where possible.
- Make frequent, small, reversible changes.
- Anticipate failure.
- Learn from all operational events and metrics.
- Use managed services where possible.
### Definition
Best practices:
- Organization
	- Your teams must have a shared understanding of your entire workload, their role in it, and shared business goals to set the priorities that will achieve business success.
	- How do you determine what your priorities are?
	- How do you structure your organization to support your business outcomes?
	- How does your organizational culture support your business outcomes?
- Prepare
	- You have to understand your workloads and their expected behaviors. You will then be able to design them to provide insight to their status and build the procedures to support them.
	- How do you implement observability in your workload?
	- How do you reduce defects, ease remediation, and improve flow into production?
	- How do you mitigate deployment risks?
	- How do you know that you are read to support a workload?
- Operate
	- Successful operation of a workload is measured by the achievement of business and customer outcomes. By concentrating on essential insights and eliminating unnecessary data, you maintain a straightforward approach to understanding workload performance.
	- How do you utilize workload observability in your organization?
	- How do you understand the health of your operations?
	- How do you manage workload and operations events?
- Evolve
	- Learn, share, and continuously improve to sustain operational excellence.
	- How do you evolve operations?

> [!info]
> You probably don't have to memorize all of this, especially the following, for the exam, but it doesn't hurt to skim through.
### Fully Separated Operating Model
#### Traditional Model
![[OE_traditional.jpg]]
In the traditional model, activities in each quadrant are performed by a separate team. Work is passed between teams through mechanisms such as work requests, queues, tickets, or by using an IT service management system (ITSM). The transition of tasks to or between teams increases complexity and may create bottlenecks and delays.
#### DevOps with Cloud-Managed Service Provider
![[OE_devops-w-cloudmanaged.jpg]]
The DevOps with cloud-managed service provider model follows a "you build it, you run it" methodology. However, your organization may not have the existing skills or team members to support a dedicated platform engineering and operations team, or may not be in a position to.
#### Cloud Operations and Platform Enablement (COPE)
![[OE_COPEmodel.jpg]]
The COPE model seeks to establish a "you build it, you run it" by supporting application teams to perform the engineering and operations activities for their workloads.
#### Distributed DevOps
![[OE_dist_DevOps.jpg]]
The distributed DevOps model separates (or distributes) the application engineering operations and infrastructure engineering operations responsibilities across the engineering teams, following the COPE methodology. Standards are distributed, provided, or shared to the application and platform teams.
#### Decentralized DevOps
![[OE_dec-DevOps.jpg]]
Your application engineers perform both the engineering and the operations of their workloads. Governance treated as decentralized. Standards are still distributed/provided/shared but the application teams are free to engineer and operate new platform capabilities of their workload.
### Evolving your operational model
![[OE_OpModelgraph.jpg]]
It's important to understand that this journal from a traditional to decentralized DevOps is likely to take time and require building maturity across a number of capabilities.
### Relationships and Ownership: Best Practices
- **OPS02-BP01 Resources have identified owners**
	- Resources for your workload must have identified owners for change control, troubleshooting, and other functions. Owners are assigned for workloads, accounts, infrastructure, platforms, and applications. Ownership is recorded using tools like a central register or metadata attached to resources.
- **OPS02-BP02 Processes and procedures have identified owners**
	- Understand who has ownership of the definition of individual processes and procedures, why those specific process and procedures are used, and why that ownership exists.
- **OPS02-BP03 Operations activities have identified owners responsible for their performance**
	- Understand who has responsibility to perform specific activities on defined workloads and why that responsibility exists.
- **OPS02-BP04 Mechanisms exist to manage responsibilities and ownership**
	- Understand the responsibilities of your role and how you contribute to business outcomes, as this understanding informs the prioritization of your tasks and why your role is important.
- **OPS02-BP05 Mechanisms exist to request additions, changes, and exceptions**
	- You can make requests to owners of processes, procedures, and resources.
- **OPS02-BP06 Responsibilities between teams are predefined or negotiated**
	- Inter-team communications channels are documented. Have defined or negotiated agreements between teams describing how they work with and support each other.
### Organizational Culture: Best Practices
- **OPS03-BP01 Provide executive sponsorship**
	- Organizations that endeavor to adopt, transform, and optimize their cloud operations establish clear lines of leadership and accountability for desired outcomes.
- **OPS03-BP02 Team members are empowered to take action when outcomes are at risk**
	- A cultural behavior of ownership instilled by leadership results in any employee feeling empowered to act on behalf of the entire company beyond their defined scope of role and accountability.
- **OPS03-BP03 Escalation is encouraged**
	- Team members are encouraged by leadership to escalate issues and concerns to higher-level decision makers and stakeholders if they believe desired outcomes are at risk and expected standards are not met.
- **OPS03-BP04 Communications are timely, clear, and actionable**
	- Leadership is responsible for the creation of strong and effective communications, especially when the organization adopts new strategies, technologies, or ways of working.
- **OPS03-BP05 Experimentation is encouraged**
	- Experimentation is a catalyst for turning new ideas into products and features.
- **OPS03-BP06 Team members are encouraged to maintain and grow their skill sets** 
	- Teams must grow their skill sets to adopt new technologies, and to support changes in demand and responsibilities in support of your workloads.
- **OPS03-BP07 Resource teams appropriately**
	- Provision the right amount of proficient team members, and provide tools and resources to support your workload needs. Overburdening team members increases the risk of human error.
### Implement Observability: Best Practices
Observability goes beyond simple monitoring.
- **OPS04-BP01 Identify key performance indicators.**
- **OPS04-BP02 Implement application telemetry.**
- **OPS04-BP03 Implement user experience telemetry.**
- **OPS04-BP04 Implement dependency telemetry.**
- **OPS04-BP05 Implement distributed tracing.**
### Design for Operations: Best Practices
Adopt approaches that improve the flow of changes into production and that help refactoring, fast feedback on quality, and bug fixing.
- **OPS05-BP01 Use version control**
	- Examples: source control systems such as Git, AWS CloudFormation templates, etc.
	- Your teams collaborate on code. When merged, the code is consistent and no changes are lost.
- **OPS05-BP02 Test and validate changes**
	- Your software changes are tested before they are delivered.
- **OPS05-BP03 Use configuration management systems**
	- You configure, validate, and deploy as part of your continuous integration, CI/CD pipeline. You monitor to validate configurations are correct. This minimizes any impact to end users and customers.
- **OPS05-BP04 Use build and deployment management systems**
	- These systems reduce errors caused by manual processes and reduce the level of effort to deploy changes.
	- ![[aws_codepipeline.jpg]]
- **OPS05-BP05 Perform patch management**
	- Perform patch management, to gain features, address issues, and remain compliant with governance.
	- Example: Amazon EC2 Image Builder provides pipelines to update machine images.
	- Patching should not be performed on production systems without first testing in a safe environment.
- **OPS05-BP06 Share design standards**
	- Using shared standards supports the adoption of best practices and maximizes the benefits of development efforts.
- **OPS05-BP07 Implement practices to improve code quality**
	- Examples include test-driven development, code reviews, standards adoption, and pair programming.
- **OPS05-BP08 Use multiple environments**
	- You test and promote code through environments on your path to production.
- **OPS05-BP09 Make frequent, small, reversible changes**
	- Frequent, small, and reversible changes reduce the scope and impact of a change. Development efforts are faster by deploying small changes frequently.
- **OPS05-BP10 Fully automate integration and deployment**
	- Automate build, deployment, and testing of the workload. This reduces errors caused by manual processes and reduces the effort to deploy changes.
	- Apply metadata using Resource Tags and AWS Resource Groups following a consistent tagging strategy to aid in identification of your resources.

### Further Reading
- (These notes were mostly taken from) PDF: [Operational Excellence Whitepaper](https://docs.aws.amazon.com/pdfs/wellarchitected/latest/operational-excellence-pillar/wellarchitected-operational-excellence-pillar.pdf#welcome)
Related Whitepapers:
- [AWS Tagging Best Practices](https://docs.aws.amazon.com/whitepapers/latest/tagging-best-practices/tagging-best-practices.html)
- [Introduction to DevOps on AWS](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/automation.html)
- [Organizing Your AWS Environment Using Multiple Accounts](https://docs.aws.amazon.com/whitepapers/latest/organizing-your-aws-environment/organizing-your-aws-environment.html)
- [AWS Cloud Adoption: Operations Perspective](https://docs.aws.amazon.com/whitepapers/latest/aws-caf-operations-perspective/aws-caf-operations-perspective.html)

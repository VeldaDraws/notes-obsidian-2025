## [[0_Preface]]

###### Extra notes
- [[CLI-Notes]]
- [[AWS Device Farm]]
### Section 2
###### Module 2: Cloud Architecting
- Notes: [[02_Well-Architected]]
- Quizlet: D319/[AWS Well-Architectured Framework](https://quizlet.com/1028064751/aws-well-architectured-framework-flash-cards/?i=1y0hnw&x=1jqt)
- Whitepaper (PDF) on [AWS Well-Architected Framework](https://docs.aws.amazon.com/pdfs/wellarchitected/latest/framework/wellarchitected-framework.pdf#welcome)
- White Papers, as Docs (⬇PDF button will show full whitepaper):
	- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html) 
	- [Operational Excellence Pillar](https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/welcome.html)
	- [Security Pillar](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html)
	- [Reliability Pillar](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html)
	- [Performance Efficiency Pillar](https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/welcome.html)
	- [Cost Optimization Pillar](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html)
	- [Sustainability Pillar](https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/sustainability-pillar.html)
###### Module 3: Adding a Storage Layer
- Notes: [[03_Storage-Layer]]
- Quizlet: D319/[AWS S3](https://quizlet.com/1027422520/aws-s3-flash-cards/?i=1y0hnw&x=1jqt)
- Further Reading:
	- [AWS CLI S3 Documentation](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/index.html#cli-aws-s3)
###### Module 4: Adding a Compute Layer
- Notes: [[04_Compute-Layer]]
- Quizlet: D319/[AWS EC2](https://quizlet.com/1027023317/aws-ec2-flash-cards/?i=1y0hnw&x=1jqt)
- Further Reading:
	- Whitepaper: [Compute](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/compute-services.html)
	- [What is Amazon EC2?](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
	- [EC2 FAQs](https://aws.amazon.com/ec2/faqs/)
	- [EC2 Builder Guide](https://docs.aws.amazon.com/imagebuilder/latest/userguide/what-is-image-builder.html)
	- [AWS Compute Optimizer Guide](https://docs.aws.amazon.com/compute-optimizer/latest/ug/what-is-compute-optimizer.html)
	- [AWS Pricing Whitepaper](https://docs.aws.amazon.com/whitepapers/latest/how-aws-pricing-works/abstract-and-introduction.html)
	- AWS: [Getting Started with Serverless Compute](https://aws.amazon.com/serverless/getting-started/?serverless.sort-by=item.additionalFields.createdDate&serverless.sort-order=desc)
###### Module 5: Adding a Database Layer
- Notes: [[05_DB-Layer]]
	- [[05_01-Databases-In-General]]
	- [[05_02-Database Layer - Overview]]
	- [[05_03-Choosing-a-service]]
	- 🎯 [[Amazon Aurora]]
	- 🎯 [[Amazon ElastiCache]]
	- 🎯 [[Amazon RDS]]
	- 🎯 [[DynamoDB]]
	- Tags: #RDMS , #DynamoDB , #Query , #Scan , #GSI , #LSI , #RCUs , #WCUs, #ElastiCache , #MemoryDB , #DocumentDB 
- Quizlet: D319/[AWS Database Layer](https://quizlet.com/1027502658/aws-database-layer-flash-cards/?i=1y0hnw&x=1jqt)
- Further Reading:
	- [Choosing an AWS database service](https://docs.aws.amazon.com/decision-guides/latest/databases-on-aws-how-to-choose/databases-on-aws-how-to-choose.html?icmpid=docs_homepage_databases)
		- Notes: [[05_03-Choosing-a-service]]
	- [Core Components of Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html)
	- [What is Amazon RDS?](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
	- [What is Amazon Aurora?](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)
		- Detailed (warning: large, but very detailed) PDF: [Aurora User Guide](https://docs.aws.amazon.com/pdfs/AmazonRDS/latest/AuroraUserGuide/aurora-ug.pdf#CHAP_AuroraOverview)
	- Docs: [How Aurora Serverless v2 works](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.how-it-works.html#aurora-serverless-v2.parameters)
### Section 3
###### Module 6: Network Layer
- IP Notation Review: [[06-01_IP-Notation-Refresh]]
- DNS Refresher: [[06_02_DNS-Refresher]]
- Notes: [[06_Network-Layer]]
- Quizlet: D319/[AWS Network Layer](https://quizlet.com/1027608577/aws-networking-layer-flash-cards/?i=1y0hnw&x=1jqt)
- Further Reading:
	- [How Amazon VPC Works](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html)
	- [One to Many: Evolving VPC Design](https://aws.amazon.com/blogs/architecture/one-to-many-evolving-vpc-design/)
	- Video: [AWS re:Invent 2018: Your Virtual Data Center](https://www.youtube.com/watch?v=jZAvKgqlrjY)
	- White Paper (PDF): [AWS VPC Connectivity Options](https://docs.aws.amazon.com/pdfs/whitepapers/latest/aws-vpc-connectivity-options/aws-vpc-connectivity-options.pdf#welcome)
###### Module 7: Connecting Networks
AWS Site-to-Site VPN, AWS Direct Connect, VPC Peering, Transit Gateway.
- Notes: [[07_Network-Connections]]
- Further Reading:
	- [Configure Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
	- [Example Routing Options](https://docs.aws.amazon.com/vpc/latest/userguide/route-table-options.html)
	- [Working With Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/WorkWithRouteTables.html)
	- [Control Traffic to Subnets Using Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html)
	- [Control Traffic to Resources Using Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- Whitepaper (PDF): Building a Scalable and Secure Multi-VPC AWS Network Infrastructure
	- [[building-a-scalable-and-secure-multi-vpc-aws-network-infrastructure.pdf]]
###### Module 8: Securing User and Application Access
- Crucial Notes on Root User: [[08_01-Root-User]]
- One or Multiple Accounts? [[08_02-Other-AWS-Account-Practices]]
- Notes: [[08_IAM]]
- Further Reading:
	- [Security Best Practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
	- [What is AWS Organizations?](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)
		- [(Full PDF Version)](https://docs.aws.amazon.com/pdfs/organizations/latest/userguide/organizations-userguide.pdf#orgs_introduction)
###### Module 9: Implementing Elasticity, High Availability, and Monitoring
- Notes: [[09_Elasticity_Availability_Monitoring]]
	- [[Elasticity]]
		- [[EC2 Auto Scaling]]
		- [[Amazon RDS Scaling]]
		- [[Scaling Amazon Aurora]]
		- [[Dynamo DB Auto Scaling]]
	- [[Availability]]
	- [[Monitoring]]
		- [[Monitoring#CloudWatch]]
###### Module 10: Automating Your Architecture
- Notes: [[10_Automating_Architecture]]
### Section 4
###### Module 11: Caching Content
- Notes: [[11_Caching-Content]]
###### Module 12: Building Decoupled Architectures
- Notes: [[12_Building-Decoupled-Architectures]]
###### Module 13: Building Microservices and Serverless Architecture
- Notes: [[13_Microservices-Serverless]]
- Review if needed:
	- [[04_Compute-Layer#Containers]] 
	- [[04_Compute-Layer#Serverless]]
	- [[04_Compute-Layer#AWS Lambda]]
###### Module 14: Planning for Disaster
- Notes: [[14_Disaster-Planning]]
	- Tags: #RPO , #RTO , #Resiliency , #DataSync 
###### Module 15: Bridging to Certification
- [[Domain 1]]: Design Resilient Architectures - 30%
- [[Domain 2]]: Design High-Performing Architectures - 28%
- [[Domain 3]]: Design Secure Applications and Architectures - 24%
- Domain 4: Design Cost-Optimized Architectures - 18%

## Summaries by Service
- [[S3]]
	- [[Snow-Family]]
- [[VPC]]
- [[Security Groups]]
- [[IAM]]
- [[Route53]]
- [[EC2]] - Pricing, AMIs, ASGs.
- [[Databases]] - RDS, Aurora, DynamoDB
- [[CloudFormation]]
- [[AWS WAF Manager]]

#### Other/Unorganized
[[Icon-Index]]
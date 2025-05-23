## Multi-Accounts
![[multi-vs-single-account.jpg|400]]
Advantages:
- Isolate units or departments
- Separate accounts for regulated workloads
- Easier to trigger costs alerts for each business unit's consumption.
Challenges:
- Security management (IAM policy replication)
- Creating new accounts
- Billing consolidation
- Centralized governance needed.
## AWS Organizations
![[icon_aws-organizations.jpg]]
AWS Organizations is a managed service for account management, An organization is an entity that you create to consolidate, centrally view, and manage all your AWS accounts. You determine the functionality of an organization through the feature set that you enable.
Organizations helps you manage policies for multiple AWS accounts. You can use the service to create groups of accounts. You can create groups of AWS accounts, and then apply different policies to each group.
The Organizations APIs can create new accounts programmatically and add them to a group.
Further Reading: AWS Organizations User Guide PDF: [[organizations-userguide.pdf]]

![[AWS-organizations-structure.jpg]]
##### In the AWS Organizations Primary Account:
1. Create a hierarchy of OUs (Organizational Units).
2. Assign accounts to OUs as member accounts.
3. Define SCPs (service control policies) that apply permissions restrictions to specific member accounts.
4. Attach the SPCs to root, OUs, or accounts.
##### SPC: Service Control Policies - Characteristics
- They enable you to control which services are accessible to IAM users in member accounts.
- SCPs cannot be override by the local administrator.
- IAM policies that are defined in individual accounts still apply.
##### Example uses of SCPs
- Create a policy that blocks service access or specific actions.
- Create a policy that allows full access to specific services.
- Create a policy that enforces the tagging of resources.
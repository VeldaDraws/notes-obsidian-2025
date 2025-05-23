### See also: [[08_01-Root-User]]
![[avoid-root.jpg|350]]
##### RBAC: Role-Based Access Control
Historically used on-premises and the cloud. You grant users explicit access to a set of permissions. However, the person who maintains the permissions in this model might find that they must constantly update the permissions files to add access to certain roles each time a resource is created.
##### ABAC: Attribute-Based Access Control
Enables you to use attributes to create general permissions rules that scale. Attributes are a key or key-value pair, such as a tag. IAM users have attributes that you create and apply, such as one or more tags.
# IAM: Identity and Access Management
![[icon_iam.jpg]]
- Securely control individual and group access to your AWS resources.
- Integrates with other AWS Services
- Federated Identity Management
	- Microsoft Active Directory
	- Standards-based Identity Providers
- Granular Permissions
- Support for multi-factor authentication
	- Can be hardware or virtual
### IAM Components
##### IAM Users
Person or application that is defined in an AWS account, that must make API calls to AWS Products.
- Each user must have a unique name within the AWS account.
- Must have a set of security credentials not shared with other users.
##### IAM Groups
A collection of IAM users.
You can use IAM groups to simplify how you specify and manage permissions for multiple users.
- All users in the group inherit the permission assigned to the group.
- 🔔 Groups cannot belong to other groups
- Groups can be granted permissions by using access control policies.
- Groups exist solely to make it easier to manage user permissions.
- Best practices:
	- Create groups that reflect job functions
	- Users can belong to more than one group but the most restrictive policy will apply.
##### IAM Policy
A document that defines permissions to determine what users can and cannot do in the AWS account.
##### IAM Role
Tool for granting *temporary* access to specific AWS resources in an AWS account.
- Not uniquely associated with one person
- Is assumable by a person, application, or service
- Often used to delegate access.
Use Cases:
- Provide AWS resources with access to AWS services.
- Provide access to externally authenticated users.
- Provide access to third parties
##### IAM Permissions
Permissions are specified in an IAM policy.
- Document formatted in JSON.
- Defines which resources and operations are allowed.
- Best practice: Follow the principle of least privilege.
- Two types of policies:
	- Identity-based: Attach to an IAM principal.
		- Attached to a user, group or role.
		- Types:
			- AWS Managed
			- Customer Managed
			- Inline
	- Resource-based: Attach to an AWS resource.
		- Attached to AWS Resources
		- Always an inline policy.
###### Identity-Based Policies
Permission policies that you can attach to a principal, or an identity, such as an IAM user, role or group. The policies control what actions that identity can perform, on which resources, and under what conditions.
###### Resource-Based Policies
JSON policy documents that you attach to a resource. These policies control which actions a specified principal can perform on that resource and under what conditions.
### Tagging
📑 A tag consists of a name and a value
- can be applied to resources across your AWS accounts
- tag keys and values are returned by many different API operations.
✨Tags can also be applied to IAM users or IAM roles.
🎯 Tags have many practical uses:
- technical tags to identify that a resource is a web server, environment, etc.
- business tags to identify the department or cost, etc.
- security tags such as an identifier for the specific data-confidentiality level that a resource supports.
### IAM Policy Document Structure
`Effect`
- Can be either `Allow` or `Deny`.
	- 👉 An explicit deny statement takes precedence over an allow statement.
`Action`
- Type of access that is allowed or denied.
`Resource`
- Resources that the action will act on.
- You must specify a list of resources to which the actions apply.
- 👉 If you create a resource-based policy, this element is optional
`Condition` (Optional)
- Conditions that must be met for the rule to apply.
Example skeleton:
```
{
	"Version": "2012-10-17",
	"Statment":[{
		"Effect": "effect",
		"Action": "action",
		"Resource": "arn",
		"Condition":{
			"condition":{
				"key": "value"
			}
		}
	}]
}
```
#### ARNs: Amazon Resource Names
Resources are identified by using Amazon Resource Name format.
You can use a wildcard `*` to give access to all actions for a specific use case.
```
"Action": "s3:*",
```
### IAM example Usage
![[bucket-use-case.jpg]]
Example bucket has two main directories: `home` and `share` where different teams can store content.
1. Add Zhang to IAM group for developers
2. Create the `home/zhang` directory in the bucket ( `bucket_name/home/zhang` )
3. Attach an IAM policy that grants access to the `bucket_name/home/zhang` directory. Zhang's access will include the rights that were granted from the group and also the rights that were directly attached to the IAM user principal.
### AWS STS: AWS Security Token Service
![[icon_STS.jpg]]
- Web service that enables you to request temporary, limited-privilege credentials.
- Credentials can be used by IAM users or for users that you authenticate.
### Identity Federation: Externally Authenticated Users
IAM supports identity federation for delegated access to the AWS Management Console or AWS APIs. With identity federation, external identities are granted secure access to resources in your AWS account without needing to create IAM users.
IdP: Identity Provider
- Examples: Microsoft Active Directory.
SAML: Security Markup Language
##### Identity Federation with an IdP/broker
1. User accesses an application, entering their ID/password.
2. Identity broker receives the authentication request.
3. If authentication request is successful, the broker makes a request to AWS STS.
4.  The user application receives the temporary AWS security credentials and redirects the user to the AWS Management Console.
##### Identity Federation using SAML
1. A user in your organization navigates to an internal port in your network.
2. The IdP authenticates the user's identity against the identity store.
3. The portal receives the authentication response as a SAML assertion from the IdP.
4. The client posts the SAML assertion to the AWS sign-in endpoint for SAML.
5. The client receives the temporary AWS security credentials.
#### Amazon Cognito
![[icon_cognito.jpg]]
Fully managed service. Provides authentication, authorization and user management for web and mobile applications.
- Amazon Cognito provides web identity federation. Can be used as the identity broker that supports IdPs that are compatible with OpenID Connect (OIDC).
- Federated Identities: Users sign in with social identity providers.
- User Pools: You can maintain a directory with user profiles authentication tokens.
- Identity Pools: Enable the creation of unique identities and permissions assignment for users.
## AWS CloudTrail
![[icon_cloudtrail.jpg]]
- Logs and monitors user activity.
- Provides event history.
- Security Analysis.
AWS CloudTrail is a service that enables governance, compliance, and auditing of your AWS account. You can monitor and retain account activity that is related to actions across your AWS infrastructure.
It provides an event history of account activity, including actions taken through the AWS Management Console, AWS SDKs, and command line tools.
You can discover and troubleshoot security and operational issues by capturing a comprehensive history of changes that occurred in your AWS account within a specified period of time.
#### Amazon EventBridge (formerly known as Amazon CloudWatch Events)
With Amazon EventBridge, you can define workflows that run when it detects events that can result in security vulnerabilities. You can create a workflow to add a specific policy to an S3 bucket when CloudTrail logs an API call that makes that bucket public.


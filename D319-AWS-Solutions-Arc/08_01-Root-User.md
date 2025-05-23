The AWS root user has two sets of credentials associated with it.
- email and password
- access keys (programmatic requests) in two parts:
	- access key ID
	- secret access key
🧨 Don't create an access key for the root account unless you absolutely need to (rare and/or unheard of).
### Best Practices
The root user has complete access to all AWS services and resources in your account. Therefore you should **not*** use the root user for everyday tasks.
- Choose a strong password for the root user.
- Enable MFA
	- something you know
	- something you have
	- something you are
- Never share your root user password or access keys with anyone.
- Disable or delete the access keys associated with the root user.
- Create IAM user for administrative tasks or everyday tasks.
### Resources:
- [Enabling a Hardware TOTP token in the Console](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_physical.html)
- [Enabling a FIDO Security Key in the Console](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_fido.html)
- [Enabling a Virtual MFA Device in the Console](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html)
- [Tasks That Require Root User Credentials](https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html)
	- Account-level settings
	- Restoring IAM user permissions
	- Closing your AWS account
	- Billing:
		- IAM access in the Billing and Cost Management console
		- [Managing an AWS account > AWS Billing User Guide](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-account-payment.html)
		- Tax invoices, VAT in AWS Europe, etc.
	- Signing up for AWS GovCloud
	- Register as a seller in EC2
	- Linking your AWS with MTurk Requester
	- MFA on a Bucket, policy config.
	- SQS policy config.

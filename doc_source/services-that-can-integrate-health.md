# AWS Health and AWS Organizations<a name="services-that-can-integrate-health"></a>

AWS Health provides ongoing visibility into your resource performance and the availability of your AWS services and accounts\. AWS Health delivers events when your AWS resources and services are impacted by an issue or will be affected by upcoming changes\. After you enable organizational view, a user in the organization’s management account can aggregate AWS Health events across all accounts in the organization\. Organizational view only shows AWS Health events delivered after the feature is enabled and retains them for 90 days\. 

For more information, see [Aggregating AWS Health events](https://docs.aws.amazon.com/health/latest/ug/aggregate-events.html) in the *AWS Health User Guide*\.

**Note**  
Currently, the organizational view feature is available only through the AWS Health API\. For more information, see the [AWS Health API Reference](https://docs.aws.amazon.com/health/latest/APIReference/Welcome.html)\.

Use the following information to help you to help you integrate AWS Health with AWS Organizations\.

**Topics**
+ [Service\-linked roles created when you enable integration](#integrate-enable-slr-health)
+ [Service principals used by the service\-linked roles](#integrate-enable-svcprin-health)
+ [Enabling trusted access with AWS Health](#integrate-enable-ta-health)
+ [Disabling trusted access with AWS Health](#integrate-disable-ta-health)

## Service\-linked roles created when you enable integration<a name="integrate-enable-slr-health"></a>

The following [service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html) are automatically created in your organization's accounts when you enable trusted access\. These roles allow AWS Health to perform supported operations within the accounts in your organization\.

You can delete or modify these roles only if you disable trusted access between AWS Health and Organizations or if the account is removed from the organization\.
+ `AWSServiceRoleForHealth_Organizations`

## Service principals used by the service\-linked roles<a name="integrate-enable-svcprin-health"></a>

The service\-linked roles in the previous section can be assumed only by the service principals authorized by the trust relationships defined for the role\. The service\-linked roles used by AWS Health grant access to the following service principals:
+ `health.amazonaws.com`

## Enabling trusted access with AWS Health<a name="integrate-enable-ta-health"></a>

For information about the permissions needed to enable trusted access, see [Permissions required to enable trusted access](orgs_integrate_services.md#orgs_trusted_access_perms)\.

You can enable trusted access using only the AWS Health commands in the AWS CLI or the equivalent API operations in any of the AWS SDKs\.

Call the [EnableHealthServiceAccessForOrganization](https://docs.aws.amazon.com/health/latest/APIReference/API_EnableHealthServiceAccessForOrganization.html) API operation\.

For more information, see [Enabling organizational view](https://docs.aws.amazon.com/health/latest/ug/aggregate-events.html#enable-organizational-view) in the *AWS Health User Guide*\.

## Disabling trusted access with AWS Health<a name="integrate-disable-ta-health"></a>

For information about the permissions needed to disable trusted access, see [Permissions required to disable trusted access](orgs_integrate_services.md#orgs_trusted_access_disable_perms)\.

After you disable this feature, AWS Health stops aggregating events for all other accounts in your organization\.

For more information, see [Disabling organizational view](https://docs.aws.amazon.com/health/latest/ug/aggregate-events.html#disabling-organizational-view) in the *AWS Health User Guide*\.

On the Organizations side, you can disable trusted access by using either the AWS Organizations console, by running a AWS CLI command, or by calling an API operation in one of the AWS SDKs\.

------
#### [ AWS Management Console ]

**To disable trusted service access using the Organizations console**

1. Sign in to the AWS Organizations console at [https://console\.aws\.amazon\.com/organizations/](https://console.aws.amazon.com/organizations/)\. You must sign in as an IAM user, assume an IAM role, or sign in as the root user \([not recommended](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#lock-away-credentials)\) in the organization's management account\. 

1. In the upper\-right corner, choose **Settings**\.

1. If you are the administrator of only AWS Organizations and not AWS Health, wait until the administrator of AWS Health tells you that they disabled integration with that service's console or tools, and that any resources have been cleaned up\.

1. In the **Trusted access for AWS services** section, find the entry for **AWS Health**, and then choose **Disable access**\.

------
#### [ AWS CLI, AWS API ]

**To disable trusted service access using an Organizations AWS CLI command or API**  
You can use the following AWS CLI commands or API operations to disable trusted service access:
+ AWS CLI: [aws organizations disable\-aws\-service\-access](https://docs.aws.amazon.com/cli/latest/reference/organizations/disable-aws-service-access.html)
+ AWS API: [DisableAWSServiceAccess](https://docs.aws.amazon.com/organizations/latest/APIReference/API_DisableAWSServiceAccess.html)

------
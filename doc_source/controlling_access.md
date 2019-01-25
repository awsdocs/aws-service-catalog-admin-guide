# Authentication and Access Control for AWS Service Catalog<a name="controlling_access"></a>

AWS Service Catalog integrates with AWS Identity and Access Management \(IAM\) to enable you to grant AWS Service Catalog administrators the permissions they need to create and manage products, and to grant end users the permissions they need to launch products and manage provisioned products\. These policies are either created and managed by AWS or individually by administrators and end users\. To control access, you attach these policies to the IAM users, groups, and roles that you use with AWS Service Catalog\.

**Topics**
+ [Predefined AWS Managed Policies](#permissions-managed-policies)
+ [Console Access for End Users](#permissions-end-users-console)
+ [Product Access for End Users](#permissions-end-users-product)
+ [Example Policies for Managing Provisioned Products](permissions-examples.md)

## Predefined AWS Managed Policies<a name="permissions-managed-policies"></a>

The managed policies created by AWS grant the required permissions for common use cases\. You can attach these policies to your IAM users and roles\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. 

The following are the AWS managed policies for AWS Service Catalog\.

**Administrators**  
+ **AWSServiceCatalogAdminFullAccess** — Grants full access to the administrator console view and permission to create and manage products and portfolios\.
+ **ServiceCatalogAdminReadOnlyAccess** — Grants full access to the administrator console view\. Does not grant access to create or manage products and portfolios\.

**End users**  
+ **AWSServiceCatalogEndUserFullAccess** — Grants full access to the end user console view\. Grants permission to launch products and manage provisioned products\.
+ **ServiceCatalogEndUserAccess** — Grants read\-only access to the end user console view\. Does not grant permission to launch products or manage provisioned products\.<a name="attach-managed-policy"></a>

**To attach a policy to an IAM user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Users**\.

1. Choose the name \(not the check box\) of the IAM user\.

1. On the **Permissions** tab, choose **Attach Policy**\.

1. On the **Attach Policy** page, select the check box next to the managed policy for AWS Service Catalog, and then choose **Attach Policy**\.

1. \(Optional\) You must grant administrators additional permissions for Amazon S3 if they need to use a private CloudFormation template\. For more information, see [User Policy Examples](https://docs.aws.amazon.com/AmazonS3/latest/dev/example-policies-s3.html) in the *Amazon Simple Storage Service Developer Guide*

### Deprecated Policies<a name="permissions-deprecated-policies"></a>

The following managed policies are deprecated:
+ **ServiceCatalogAdminFullAccess** — Use **AWSServiceCatalogAdminFullAccess** instead\.
+ **ServiceCatalogEndUserFullAccess** — Use **AWSServiceCatalogEndUserFullAccess** instead\.

Use the following procedure to ensure that your administrators and end users are granted permissions using the current policies\.<a name="migrate-deprecated"></a>

**To migrate from the deprecated policies to the current policies**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Policies**\.

1. In the search field, type **ServiceCatalog** to filter the policy list\. Choose the name \(not the check box\) for **ServiceCatalogAdminFullAccess**\.

1. For each attached entity \(user, group, or role\), do the following:

   1. Open the summary page for the entity\.

   1. Add one of the current policies, as described in the procedure [To attach a policy to an IAM user](#attach-managed-policy)\.

   1. On the **Permissions** tab, next to **ServiceCatalogAdminFullAccess**, choose **Detach Policy**\. When prompted for confirmation, choose **Detach**\.

1. Repeat the process for **ServiceCatalogEndUserFullAccess**\.

## Console Access for End Users<a name="permissions-end-users-console"></a>

Before end users can use a product to which you give access, you must provide them additional IAM permissions to allow them to use each of the underlying AWS resources in a product's AWS CloudFormation template\. For example, if a product template includes Amazon Relational Database Service \(Amazon RDS\), you must grant the users Amazon RDS permissions to launch the product\.

The **ServiceCatalogEndUserFullAccess** and **ServiceCatalogEndUserAccess** policies grant access to the AWS Service Catalog end user console view\. When a user who has either of these policies chooses **Service Catalog** in the AWS Management Console, the end user console view displays\. 

If you apply the **ServiceCatalogEndUserAccess** policy, your users have access to the end user console, but they won't have the permissions that they need to launch products and manage provisioned products\. You can grant these permissions directly to an end user using IAM, but if you want to limit the access that end users have to AWS resources, you should attach the policy to a launch role\. You then use AWS Service Catalog to apply the launch role to a launch constraint for the product\. For more information about applying a launch role, launch role limitations, and a sample launch role, see [AWS Service Catalog Launch Constraints](constraints-launch.md)\.

If you grant users the following IAM permissions, which are meant for AWS Service Catalog administrators, the administrator console view displays instead: 
+ `catalog-admin:ListPortfolios`
+ `catalog-admin:SearchListings`

Don't grant end users these permissions unless you want them to have access to the administrator console view\.

## Product Access for End Users<a name="permissions-end-users-product"></a>

Before end users can use a product to which you give access, you must provide them additional IAM permissions to allow them to use each of the underlying AWS resources in a product's AWS CloudFormation template\. For example, if a product template includes Amazon Relational Database Service \(Amazon RDS\), you must grant the users Amazon RDS permissions to launch the product\. 

If you apply the `ServiceCatalogEndUserAccess` policy, your users have access to the end user console view, but they won't have the permissions that they need to launch products and manage provisioned products\. You can grant these permissions directly to an end user in IAM, but if you want to limit the access that end users have to AWS resources, you should attach the policy to a launch role\. You then use AWS Service Catalog to apply the launch role to a launch constraint for the product\. For more information about applying a launch role, launch role limitations, and a sample launch role, see [AWS Service Catalog Launch Constraints](constraints-launch.md)\.
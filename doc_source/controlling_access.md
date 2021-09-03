# Identity and Access Management in AWS Service Catalog<a name="controlling_access"></a>

Access to AWS Service Catalog requires credentials\. Those credentials must have permission to access AWS resources, such as an AWS Service Catalog portfolio or product\. AWS Service Catalog integrates with AWS Identity and Access Management \(IAM\) to enable you to grant AWS Service Catalog administrators the permissions they need to create and manage products, and to grant AWS Service Catalog end users the permissions they need to launch products and manage provisioned products\. These policies are either created and managed by AWS or individually by administrators and end users\. To control access, you attach these policies to the IAM users, groups, and roles that you use with AWS Service Catalog\.

**Topics**
+ [Audience](#security-iam-audience)
+ [Predefined AWS Managed Policies](#permissions-managed-policies)
+ [Identity\-based policy examples for AWS Service Catalog](#security_iam_service-with-iam-id-based-policies-examples)
+ [Troubleshooting AWS Service Catalog identity and access](#security_iam_troubleshoot)
+ [Controlling Access](#access-control)
+ [Using Service\-Linked Roles for AWS Service Catalog AppRegistry](#slr-appregistry)

## Audience<a name="security-iam-audience"></a>

The permissions you have with AWS Identity and Access Management \(IAM\) may depend on the role you play in AWS Service Catalog\.

The permissions you have through AWS Identity and Access Management \(IAM\) may depend on the role you play in AWS Service Catalog\.

**Administrator** \- As an AWS Service Catalog administrator, you need full access to the administrator console and IAM permissions that allow you to perform tasks such as creating and managing portfolios and products, managing constraints, and granting access to end users\.

**End user** \- Before your end users can use your products, you need to grant them permissions that give them access to the AWS Service Catalog end user console\. They can also have permissions to launch products and manage provisioned products\.

**IAM administrator** \- If you're an IAM administrator, you might want to learn details about how you can write policies to manage access to AWS Service Catalog\. To view example AWS Service Catalog identity\-based policies that you can use in IAM, see [Predefined AWS Managed Policies](#permissions-managed-policies)\.

## Predefined AWS Managed Policies<a name="permissions-managed-policies"></a>

The managed policies created by AWS grant the required permissions for common use cases\. You can attach these policies to your IAM users and roles\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. 

The following are the AWS managed policies for AWS Service Catalog\.

**Administrators**  
+ **AWSServiceCatalogAdminFullAccess** — Grants full access to the administrator console view and permission to create and manage products and portfolios\.
+ **AWSServiceCatalogAdminReadOnlyAccess** — Grants full access to the administrator console view\. Does not grant access to create or manage products and portfolios\.

**End users**  
+ **AWSServiceCatalogEndUserFullAccess** — Grants full access to the end user console view\. Grants permission to launch products and manage provisioned products\.
+ **AWSServiceCatalogEndUserReadOnlyAccess** — Grants read\-only access to the end user console view\. Does not grant permission to launch products or manage provisioned products\.<a name="attach-managed-policy"></a>

**To attach a policy to an IAM user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Users**\.

1. Choose the name \(not the check box\) of the IAM user\.

1. On the **Permissions** tab, choose **Add permissions**\.

1. On the **Add permissions** page, choose **Attach existing policies directly**\.

1. Select the check box next to the managed policy for AWS Service Catalog, and then choose **Next: Review**\.

1.  On the **Permissions summary** page, choose **Add permissions**\. 

1. \(Optional\) You must grant administrators additional permissions for Amazon S3 if they need to use a private CloudFormation template\. For more information, see [User Policy Examples](https://docs.aws.amazon.com/AmazonS3/latest/dev/example-policies-s3.html) in the *Amazon Simple Storage Service Developer Guide\.*

### Deprecated policies<a name="permissions-deprecated-policies"></a>

The following managed policies are deprecated:
+ **ServiceCatalogAdminFullAccess** — Use **AWSServiceCatalogAdminFullAccess** instead\.
+ **ServiceCatalogAdminReadOnlyAccess** — Use **AWSServiceCatalogAdminReadOnlyAccess** instead\. 
+ **ServiceCatalogEndUserFullAccess** — Use **AWSServiceCatalogEndUserFullAccess** instead\.
+ **ServiceCatalogEndUserAccess** — Use **AWSServiceCatalogEndUserReadOnlyAccess** instead\.

Use the following procedure to ensure that your administrators and end users are granted permissions using the current policies\.<a name="migrate-deprecated"></a>

**To migrate from the deprecated policies to the current policies**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Policies**\.

1. In the search field, type **ServiceCatalog** to filter the policy list\. Choose the name \(not the check box\) for **ServiceCatalogAdminFullAccess**\.

1. For each attached entity \(user, group, or role\), do the following:

   1. Open the summary page for the entity\.

   1. Add one of the current policies described in the procedure linkend="attach\-managed\-policy" 

      Add one of the current policies described in th procedure:[To attach a policy to an IAM user](#attach-managed-policy)\.

      Add one of the current policies described in the procedure [To attach a policy to an IAM user](#attach-managed-policy)\.

   1. On the **Permissions** tab, next to **ServiceCatalogAdminFullAccess**, choose **Detach Policy**\. When prompted for confirmation, choose **Detach**\.

1. Repeat the process for **ServiceCatalogEndUserFullAccess**\.

## Identity\-based policy examples for AWS Service Catalog<a name="security_iam_service-with-iam-id-based-policies-examples"></a>

**Topics**
+ [Console access for end users](#permissions-end-users-console)
+ [Product access for end users](#permissions-end-users-product)
+ [Example policies for managing provisioned products](#example-policies)

### Console access for end users<a name="permissions-end-users-console"></a>

The ****AWSServiceCatalogEndUserFullAccess**** and ****AWSServiceCatalogEndUserReadOnlyAccess**** policies grant access to the AWS Service Catalog end user console view\. When a user who has either of these policies chooses AWS Service Catalog in the AWS Management Console, the end user console view displays the products they have permission to launch\.

Before end users can successfully launch a product from AWS Service Catalog to which you give access, you must provide them additional IAM permissions to allow them to use each of the underlying AWS resources in a product's AWS CloudFormation template\. For example, if a product template includes Amazon Relational Database Service \(Amazon RDS\), you must grant the users Amazon RDS permissions to launch the product\.

 To learn about how to enable end users to launch products while enforcing least\-access permissions to AWS resources, see [Using AWS Service Catalog Constraints](constraints.md)\. 

If you apply the **AWSServiceCatalogEndUserReadOnlyAccess** policy, your users have access to the end user console, but they won't have the permissions that they need to launch products and manage provisioned products\. You can grant these permissions directly to an end user using IAM, but if you want to limit the access that end users have to AWS resources, you should attach the policy to a launch role\. You then use AWS Service Catalog to apply the launch role to a launch constraint for the product\. For more information about applying a launch role, launch role limitations, and a sample launch role, see [AWS Service Catalog Launch Constraints](constraints-launch.md)\.

**Note**  
If you grant users IAM permissions for AWS Service Catalog administrators, the administrator console view displays instead\. Don't grant end users these permissions unless you want them to have access to the administrator console view\.

### Product access for end users<a name="permissions-end-users-product"></a>

Before end users can use a product to which you give access, you must provide them additional IAM permissions to allow them to use each of the underlying AWS resources in a product's AWS CloudFormation template\. For example, if a product template includes Amazon Relational Database Service \(Amazon RDS\), you must grant the users Amazon RDS permissions to launch the product\. 

If you apply the **ServiceCatalogEndUserAccess** policy, your users have access to the end user console view, but they won't have the permissions that they need to launch products and manage provisioned products\. You can grant these permissions directly to an end user in IAM, but if you want to limit the access that end users have to AWS resources, you should attach the policy to a launch role\. You then use AWS Service Catalog to apply the launch role to a launch constraint for the product\. For more information about applying a launch role, launch role limitations, and a sample launch role, see [AWS Service Catalog Launch Constraints](constraints-launch.md)\.

### Example policies for managing provisioned products<a name="example-policies"></a>

You can create custom policies to help meet the security requirements of your organization\. The following examples describe how to customize the access level for each action with support for user, role, and account levels\. You can grant users access to view, update, terminate, and manage provisioned products created only by that user or created by others also under their role or the account to which they are logged in\. This access is hierarchical — granting account level access also grants role level access and user level access, while adding role level access also grants user level access but not account level access\. You can specify these in the policy JSON using a `Condition` block as `accountLevel`, `roleLevel`, or `userLevel`\.

These examples also apply to access levels for AWS Service Catalog API write operations: `UpdateProvisionedProduct` and `TerminateProvisionedProduct`, and read operations: `DescribeRecord`, `ScanProvisionedProducts`, and `ListRecordHistory`\. The `ScanProvisionedProducts` and `ListRecordHistory` API operations use `AccessLevelFilterKey` as input, and that key's values correspond to the `Condition` block levels discussed here \(`accountLevel` is equivalent to an `AccessLevelFilterKey` value of "Account", `roleLevel` to "Role", and `userLevel` to "User"\)\. For more information, see the [AWS Service Catalog Developer Guide](https://docs.aws.amazon.com/servicecatalog/latest/dg/)\.

**Topics**
+ [Example: Full admin access to provisioned products](#full-admin)
+ [Example: End\-user access to provisioned products](#examples-end-user)
+ [Example: Partial admin access to provisioned products](#partial-admin)

#### Example: Full admin access to provisioned products<a name="full-admin"></a>

The following policy allows full read and write access to provisioned products and records within the catalog at the account level\. 

```
{  
   "Version":"2012-10-17",
   "Statement":[  
      {  
         "Effect":"Allow",
         "Action":[  
            "servicecatalog:*"
         ],
         "Resource":"*",
         "Condition": {
            "StringEquals": {
               "servicecatalog:accountLevel": "self"
            }
         }
      }
   ]
}
```

This policy is functionally equivalent to the following policy:

```
{  
   "Version":"2012-10-17",
   "Statement":[  
      {  
         "Effect":"Allow",
         "Action":[  
            "servicecatalog:*"
         ],
         "Resource":"*"
      }
   ]
}
```

In other words, not specifying a `Condition` block in any policy for AWS Service Catalog is treated as the same as specifying `"servicecatalog:accountLevel"` access\. Note that `accountLevel` access includes `roleLevel` and `userLevel` access\.

#### Example: End\-user access to provisioned products<a name="examples-end-user"></a>

The following policy restricts access to read and write operations to only the provisioned products or associated records that the current user created\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "servicecatalog:DescribeProduct",
                "servicecatalog:DescribeProductView",
                "servicecatalog:DescribeProvisioningParameters",
                "servicecatalog:DescribeRecord",
                "servicecatalog:ListLaunchPaths",
                "servicecatalog:ListRecordHistory",
                "servicecatalog:ProvisionProduct",
                "servicecatalog:ScanProvisionedProducts",
                "servicecatalog:SearchProducts",
                "servicecatalog:TerminateProvisionedProduct",
                "servicecatalog:UpdateProvisionedProduct"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "servicecatalog:userLevel": "self"
                }
            }
        }
    ]
 }
```

#### Example: Partial admin access to provisioned products<a name="partial-admin"></a>

The two policies below, if both applied to the same user, allow what might be called a type of "partial admin access" by providing full read\-only access and limited write access\. This means the user can see any provisioned product or associated record within the catalog's account but cannot perform any actions on any provisioned products or records that aren't owned by that user\. 

The first policy allows the user access to write operations on the provisioned products that the current user created, but no provisioned products created by others\. The second policy adds full access to read operations on provisioned products created by all \(user, role, or account\)\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "servicecatalog:DescribeProduct",
                "servicecatalog:DescribeProductView",
                "servicecatalog:DescribeProvisioningParameters",
                "servicecatalog:ListLaunchPaths",
                "servicecatalog:ProvisionProduct",
                "servicecatalog:SearchProducts",
                "servicecatalog:TerminateProvisionedProduct",
                "servicecatalog:UpdateProvisionedProduct"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "servicecatalog:userLevel": "self"
                }
            }
        }
    ]
 }
```

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "servicecatalog:DescribeRecord",
                "servicecatalog:ListRecordHistory",
                "servicecatalog:ScanProvisionedProducts"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "servicecatalog:accountLevel": "self"
                }
            }
        }
    ]
 }
```

## Troubleshooting AWS Service Catalog identity and access<a name="security_iam_troubleshoot"></a>

Use the following information to help you diagnose and fix common issues you might encounter when working with AWS Service Catalog and AWS Identity and Access Management\.

**Topics**
+ [I am not authorized to perform an action in AWS Service Catalog](#troubleshoot-one)
+ [I am not authorized to perform iam:PassRole](#troubleshoot-two)
+ [I want to view my access keys](#troubleshoot-three)
+ [I'm an administrator and want to allow others to access AWS Service Catalog](#troubleshoot-four)
+ [I want to allow people outside of my AWS account to access my AWS Service Catalog resources](#troubleshoot-five)

### I am not authorized to perform an action in AWS Service Catalog<a name="troubleshoot-one"></a>

If the AWS Management Console tells you that you're not authorized to perform an action, then you must contact your administrator for assistance\. Your administrator is the person that provided you with your user name and password\. The following example error occurs when the mateojackson IAM user tries to use the console to view details about a fictional my\-example\-widget resource but does not have the fictional awes:GetWidget permissions\. 

```
User: arn:aws:iam::123456789012:user/mateojackson is not authorized to perform: awes:GetWidget on resource: my-example-widget
```

In this case, Mateo asks his administrator to update his policies to allow him to access the my\-example\-widget resource using the awes:GetWidget action\.

### I am not authorized to perform iam:PassRole<a name="troubleshoot-two"></a>

If you receive an error that you're not authorized to perform the iam:PassRole action, then you must contact your administrator for assistance\. Your administrator is the person that provided you with your user name and password\. Ask that person to update your policies to allow you to pass a role to AWS Service Catalog\.

Some AWS services allow you to pass an existing role to that service, instead of creating a new service role or service\-linked role\. To do this, you must have permissions to pass the role to the service\.

The following example error occurs when an IAM user named marymajor tries to use the console to perform an action in AWS Service Catalog\. However, the action requires the service to have permissions granted by a service role\. Mary does not have permissions to pass the role to the service\.

```
User: arn:aws:iam::123456789012:user/marymajor is not authorized to perform: iam:PassRole        
```

In this case, Mary asks her administrator to update her policies to allow her to perform the iam:PassRole action\.

### I want to view my access keys<a name="troubleshoot-three"></a>

After you create your IAM user access keys, you can view your access key ID at any time\. However, you can't view your secret access key again\. If you lose your secret key, you must create a new access key pair\.

Access keys consist of two parts: an access key ID \(for example, AKIAIOSFODNN7EXAMPLE\) and a secret access key \(for example, wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY\)\.

Like a user name and password, you must use both the access key ID and secret access key together to authenticate your requests\. Manage your access keys as securely as you do your user name and password\.

Do not provide your access keys to a third party, even to help [find your canonical user ID ](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html#FindingCanonicalId) in the *AWS General Reference guide\.* By doing this, you might give someone permanent access to your account\.

When you create an access key pair, you are prompted to save the access key ID and secret access key in a secure location\. The secret access key is available only at the time you create it\. If you lose your secret access key, you must add new access keys to your IAM user\. You can have a maximum of two access keys\. If you already have two, you must delete one key pair before creating a new one\. To view instructions, see [Managing access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey) in the *IAM User Guide*\.

### I'm an administrator and want to allow others to access AWS Service Catalog<a name="troubleshoot-four"></a>

To allow others to access AWS Service Catalog, you must create an IAM entity \(user or role\) for the person or application that needs access\. They will use the credentials for that entity to access AWS\. You must then attach a policy to the entity that grants them the correct permissions in AWS Service Catalog\.

To get started right away, see [Creating your first IAM delegated user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-delegated-user.html) in the *IAM User Guide*\.

### I want to allow people outside of my AWS account to access my AWS Service Catalog resources<a name="troubleshoot-five"></a>

You can create a role that users in other accounts or people outside of your organization can use to access your resources\. You can specify who is trusted to assume the role\. For services that support resource\-based policies or access control lists \(ACLs\), you can use those policies to grant people access to your resources\.

To learn more, consult the following:
+ To learn whether AWS Service Catalog supports these features, see [Identity and Access Management in AWS Service Catalog](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/controlling_access.html) in the *AWS Service Catalog Administrator Guide*\.
+ To learn how to provide access to your resources across AWS accounts that you own, see [Providing access to an IAM user in another AWS account that you own ](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_aws-accounts.html) in the *IAM User Guide*\.
+ To learn how to provide access to your resources to third\-party AWS accounts, see [Providing access to AWS accounts owned by third parties](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html) in the *IAM User Guide*\.
+ To learn how to provide access through identity federation, see [Providing access to externally authenticated users \(identity federation\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_federated-users.html) in the *IAM User Guide*\.
+ To learn the difference between using roles and resource\-based policies for cross\-account access, see [How IAM roles differ from resource\-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_compare-resource-policies.html) in the *IAM User Guide*\.

## Controlling Access<a name="access-control"></a>

 An AWS Service Catalog portfolio gives your administrators a level of access control for your groups of end users\. When you add users to a portfolio, they can browse and launch any of the products in the portfolio\. For more information, see [Managing Portfolios](catalogs_portfolios.md)\. 

### Constraints<a name="constraints-access-control"></a>

Constraints control which rules are applied to your end users when launching a product from a specific portfolio\. You use them to apply limits to products for governance or cost control\. For more information about constraints, see [Using AWS Service Catalog Constraints](constraints.md)\.

 AWS Service Catalog launch constraints give you more control over permissions needed by an end user\. When your administrator creates a launch constraint for a product in a portfolio, the launch constraint associates a role ARN that is used when your end users launch the product from that portfolio\. Using this pattern, you can control access to AWS resource creation\. For more information, see [AWS Service Catalog Launch Constraints](constraints-launch.md)\.

## Using Service\-Linked Roles for AWS Service Catalog AppRegistry<a name="slr-appregistry"></a>

This section describes how AWS Service Catalog AppRegistry uses the service\-linked role,** AWSServiceCatalogAppRegistryServiceRolePolicy**, to create, update, and delete AWS Resource Groups in your accounts\. AWS Resource Groups provide customers with visibility and operation of all resources in an application across CloudFormation stacks\.

AppRegistry uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that links directly to AppRegistry\. AppRegistry predefines service\-linked roles and includes all the permissions that the service requires to call other AWS services on your behalf\.

A service\-linked role makes setting up AppRegistry easier because you don’t have to manually add the necessary permissions\. AppRegistry defines the permissions of its service\-linked roles, and unless defined otherwise, only AppRegistry can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

You can delete a service\-linked role only after first deleting their related resources\. This action protects your AppRegistry resources because you can't inadvertently remove permission to access the resources\.

**Note**  
AppRegistry creates a new tag on the resource groups: `EnableAWSServiceCatalogAppRegistry`, `true`  
You should not modify this tag\. Modifying this tag results in AppRegsitry losing permissions to manage Service linked resource groups created for applications and associated stacks\. 

### Service\-Linked Role Permissions for AWS Service Catalog AppRegistry<a name="permissions-slr"></a>

AppRegistry uses the service\-linked role named **AWSServiceRoleForAWSServiceCatalogAppRegistry** to enable AppRegistry to call AWS APIs on your behalf\.

The **AWSServiceRoleForServiceCatalogAppRegistry** service\-linked role trusts the servicecatalog\-appregistry\.amazonaws\.com service principal to assume the role\.

The role permissions policy allows AppRegistry to complete the following actions on the specified resources:

```
             {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "cloudformation:DescribeStacks",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "resource-groups:CreateGroup",
                "resource-groups:Tag"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:RequestTag/EnableAWSServiceCatalogAppRegistry": "true"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "resource-groups:DeleteGroup",
                "resource-groups:UpdateGroup",
                "resource-groups:GetGroup",
                "resource-groups:GetTags",
                "resource-groups:Tag",
                "resource-groups:Untag"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/EnableAWSServiceCatalogAppRegistry": "true"
                }
            }
        }
    ]
}
```

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide\.*

To allow an IAM entity to create the **AWSServiceRoleForServiceCatalogAppRegistry **service\-linked role, add this statement to the permissions policy for the IAM entity that needs to create the service\-linked role\.

```
             {
    "Effect": "Allow",
    "Action": [
        "iam:CreateServiceLinkedRole"
    ],
    "Resource": "arn:aws:iam::*:role/aws-service-role/servicecatalog-appregistry.amazonaws.com/AWSServiceRoleForServiceCatalogAppRegistry*",
    "Condition": {"StringLike": {"iam:AWSServiceName": "servicecatalog-appregistry.amazonaws.com"}}
}
```

### Creating a service\-linked role for AWS Service Catalog AppRegistry<a name="create-role"></a>

When the customer requests a specific operation, our service automatically creates the role\. When you create an application or update and existing application in the AWS Management Console, the AWS CLI, or the AWS API, AppRegistry creates the service\-linked role for you\.

**Important**  
This service\-linked role can appear in your account if you completed an action in another service that uses the features supported by this role\.

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you create and application or update an existing application, AppRegistry creates the service\-linked role for you again\. For more information, see [Deleting a Service\-Linked Role for AWS Service Catalog AppRegistry](#delete-slr)\.

You can also use the IAM console to create a service\-linked role with the** AWSServiceRoleForAWSServiceCatalogAppRegistry** use case\. In the AWS CLI or the AWS API, create a service\-linked role with the servicecatalog\-appregistry\.amazonaws\.com service name\. For more information, see [Creating a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide\.* If you delete this service\-linked role, you can use this same process to create the role again\.

### Editing a Service\-Linked Role for AWS Service Catalog AppRegistry<a name="edit-slr"></a>

After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. But you can use the IAM console, CLI, or API to edit the service\-linked role’s description\.

For more information, see [Editing a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide\.*

### Deleting a Service\-Linked Role for AWS Service Catalog AppRegistry<a name="delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don’t have an unused entity that is not actively monitored or maintained\. However, you must clean the resources for your service\-linked role before you can manually delete it\.

You can use AppRegistry to clean resources and then use the IAM console, CLI, or API to perform the deletion\.

To clean your service\-linked role’s resources before manual deletion, you must first disassociate all resources from applications\. Next disassociate all attribute groups form applications\. Then you can delete the applications\.

### Supported Regions for AWS Service Catalog AppRegistry Service\-Linked Roles<a name="regions-slr"></a>

AppRegistry supports using service\-linked roles in all of the regions where the service is available\. For more information, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html) in the *AWS General Reference guide\.*
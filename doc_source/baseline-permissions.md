# Baseline permissions<a name="baseline-permissions"></a>

This section provides instructions on how to set up baseline AWS users and permissions for the AWS Service Management Connector for ServiceNow\.

## Available template for baseline permissions<a name="baseline-permissions-template"></a>

To use an AWS CloudFormation template to set up the AWS configurations of the Connector for ServiceNow, see the AWS configurations for Connector for ServiceNow 3\.7\.1 \- [AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForServiceNowv-AWS_Configurations_Commercialv3.7.1.json) and [AWS GovCloud Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForServiceNowv-AWS_Configurations_GovCloudv3.7.1.json)\.

**Note**  
If you use the Connector for ServiceNow v3\.7\.1\_AWS Configuration template, skip to [Configuring AWS Service Catalog](configure-sc.md)\. 

 For each AWS account, the Connector for ServiceNow requires two IAM users:
+ **AWS Sync User**: An IAM user to sync AWS resources \(such as portfolios, products, automation documents \(runbook\), configuration items, and security findings\) to ServiceNow\.
+ **AWS End User role**: An IAM user who can provision products as an end user, execute requests, and view resources that ServiceNow exposes\. This role includes any required roles to provision and execute\. 

## Creating AWS Service Management Connector Sync user<a name="scsyncuser"></a>

The following section describes how to create the AWS Sync user and associate the appropriate IAM permission\. To perform this task, you need IAM permissions to create new users\.

**To create AWS Service Management Connector sync user**

1. Follow the instructions in [Creating an IAM user in your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) to create a sync user \(SMSyncUser\)\. The user needs programmatic and AWS Management Console access to follow the Connector for ServiceNow installation instructions\. 

1. Set permissions for your sync user \(SMSyncUser\)\. Choose **Attach existing policies directly** and select:
   + **AWSServiceCatalogAdminReadOnlyAccess** \(AWS managed policy\)
   + **AmazonSSMReadOnlyAccess** \(AWS managed policy\)
   + **AWSConfigUserAccess** \(AWS managed policy\)

1. Create this policy: `ConfigBidirectionalSecurityHubSQSBaseline`\. Then follow the instructions in [Creating IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html), and add this code in the JSON editor: 

   ```
   {
   
       "Version": "2012-10-17",
   
       "Statement": [
   
           {
   
               "Sid": "VisualEditor0",
   
               "Effect": "Allow",
   
               "Action": [
   
                   "cloudformation:RegisterType",
   
                   "cloudformation:DescribeTypeRegistration",
   
                   "cloudformation:DeregisterType",
   
   		        "sqs:ReceiveMessage",
   
   		         "sqs:DeleteMessage",
   
                             "sqs:DeleteMessageBatch",
   
   		          "config:PutResourceConfig",
   
   		          "securityhub:BatchUpdateFindings"
   
               ],
   
               "Resource": "*"
   
           }
   
       ]
   
   }
   ```

   The provided AWS Configuration template consists of two policies: `ConfigBiDirectionalPolicy` and `SecurityHubPolicy`\.

1. Create this policy: `OpsCenterExecutionPolicy` Then follow the instructions in [Creating IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html), and add this code in the JSON editor:

   ```
     {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "ssm:GetOpsItem",
                   "ssm:UpdateOpsItem",
                   "ssm:DescribeOpsItems"
                ],
               "Resource": "*"
           }
       ]
   }
   ```

1. Add a policy that allows `budgets:ViewBudget` on all resources \(\*\)\. 

1. Review and choose **Create User**\. 

1. Note the access and secret access information\. Download the \.csv file that contains the user credential information\.

## Creating AWS Service Catalog end user<a name="scenduser"></a>

 This section describes how to create the AWS Service Management Connector end user and associates the appropriate IAM permission\. To perform this task, you need IAM permissions to create new users\. 

**To create AWS Service Management Connector end user**

1.  Follow the instructions in [Creating an IAM user in your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) to create a user \(SMEndUser\)\. The user needs programmatic and AWS Management Console access to follow the Connector for ServiceNow installation instructions\.

    For products using AWS CloudFormation StackSets, you need to create a StackSet inline policy\. With AWS CloudFormation StackSets, you are able to create products across multiple accounts and Regions\. 

   Using an administrator account, you define and manage an AWS Service Catalog product\. You also use it to provision stacks into selected target accounts across specified Regions\. You need to have the necessary permissions defined in your AWS accounts\. 

    To set up the necessary permissions, see [Granting Permissions for Stack Set Operations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs.html)\. Follow the instructions to create an **AWSCloudFormationStackSetAdministrationRole** and an **AWSCloudFormationStackSetExecutionRole**\. 

    Create the StackSet inline policy to enable provisioning a product across multiple Regions within one account\. 

   ```
       {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Action": [
                       "sts:AssumeRole"
                   ],
                   "Resource": [
                   "arn:aws:iam::123456789123:role/AWSCloudFormationStackSetExecutionRole"
                   ],
                   "Effect": "Allow"
               },
               {
                   "Effect": "Allow",
                   "Action": [
                       "iam:GetRole",
                       "iam:PassRole"
                   ],
       "Resource":       "arn:aws:iam::123456789123:role/AWSCloudFormationStackSetAdministrationRole"
               }
           ]
       }
   ```
**Note**  
Replace **123456789123** with your account information\. The [Connector for ServiceNow v3\.7\.1 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForServiceNowv-AWS_Configurations_Commercialv3.7.1.json) and [Connector for ServiceNow v3\.7\.1 \- AWS GovCloud Regions]( https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForServiceNowv-AWS_Configurations_GovCloudv3.7.1.json) files include the stack set permissions\.

1. Add the following permissions \(policies\) to the user:
   + **AWSServiceCatalogEndUserFullAccess** \(AWS managed policy\)
   + **StackSet \(inline policy\)** \- For AWS Service Catalog products with stack sets, you need to modify the SMEndUser to include the Read Only permissions for the services you want to provision\. For example, to provision an Amazon S3 bucket, include the **AmazonS3ReadOnlyAccess** policy to the SMEndUser\.
   + **OpsCenterExecutionPolicy**
   + **AmazonEC2ReadOnlyAccess** \(AWS managed policy\)
   + **AmazonS3ReadOnlyAccess** \(AWS managed policy\)

## Creating SCConnectLaunch role<a name="scconnectlaunchrole"></a>

The SCConnect Launch role is an IAM role that places baseline AWS service permissions into the AWS Service Catalog launch constraints\. Configuring this role enables segregation of duty through provisioning product resources for ServiceNow end users\. 

The SCConnectLaunch role baseline contains permissions to Amazon EC2 and Amazon S3 services\. If your products contain more AWS services, you must either include those services in the SCConnectLaunch role or create new launch roles\.

This section describes how to create the **SCConnectLaunch** role\. This role places baseline AWS service permissions in the AWS Service Catalog launch constraints\. For more information, see [AWS Service Catalog Launch Constraints](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/constraints-launch.html)\.

**To create SCConnectLaunch role**

1. Create this policy: `AWSCloudFormationFullAccess` policy\. Choose **create policy** and add this code in the JSON editor:

   ```
                                {
               "Version": "2012-10-17",
               "Statement": [
                   {
                       "Effect": "Allow",
                       "Action": [
                       "cloudformation:DescribeStackResource",
                       "cloudformation:DescribeStackResources",
                       "cloudformation:GetTemplate",
                       "cloudformation:List*",
                       "cloudformation:DescribeStackEvents",
                       "cloudformation:DescribeStacks",
                       "cloudformation:CreateStack",
                       "cloudformation:DeleteStack",
                       "cloudformation:DescribeStackEvents",
                       "cloudformation:DescribeStacks",
                       "cloudformation:GetTemplateSummary",
                       "cloudformation:SetStackPolicy",
                       "cloudformation:ValidateTemplate",
                       "cloudformation:UpdateStack",
                       "cloudformation:CreateChangeSet",
                       "cloudformation:DescribeChangeSet",
                       "cloudformation:ExecuteChangeSet",
                       "cloudformation:DeleteChangeSet",
                       "s3:GetObject"
                       ],
                       "Resource": "*"
                   }
               ]
           }
   ```
**Note**  
**AWSCloudFormationFullAccess** includes additional permissions for ChangeSets\.

1.  Create this policy: `ServicecodeCatalogSSMActionsBaseline`\. Follow the instructions in [Creating IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html), add this code in the JSON editor: 

   ```
                               {
               "Version": "2012-10-17",
               "Statement": [
                   {
                       "Sid": "Stmt1536341175150",
                       "Action": [
                           "servicecatalog:ListServiceActionsForProvisioningArtifact",
                           "servicecatalog:ExecuteprovisionedProductServiceAction",
                           "ssm:DescribeDocument",
                           "ssm:GetAutomationExecution",
                           "ssm:StartAutomationExecution",
                           "ssm:StopAutomationExecution",
                           "cloudformation:ListStackResources",
                           "ec2:DescribeInstanceStatus",
                           "ec2:StartInstances",
                           "ec2:StopInstances"
                       ],
                       "Effect": "Allow",
                       "Resource": "*"
                   }
               ]
           }
   ```

1. Create the **SCConnectLaunch** role\. Then assign the trust relationship to AWS Service Catalog\.

   ```
                               {
             "Version": "2012-10-17",
             "Statement": [
               {
                 "Sid": "",
                 "Effect": "Allow",
                 "Principal": {
                   "Service": "servicecatalog.amazonaws.com"
                 },
                 "Action": "sts:AssumeRole"
               }
             ]
           }
   ```

1. Attach the relevant policies to the **SCConnectLaunch** role\. 

   Attach these baseline IAM policies:
   + **AmazonEC2FullAccess** \(AWS managed policy\)
   + **AmazonS3FullAccess** \(AWS managed policy\)
   + **AWSCloudFormationFullAccess** \(custom managed policy\)
   + **ServiceCatalogSSMActionsBaseline** \(custom managed policy\)
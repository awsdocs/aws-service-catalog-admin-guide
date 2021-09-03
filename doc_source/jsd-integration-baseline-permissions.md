# Baseline Permissions<a name="jsd-integration-baseline-permissions"></a>

 This section provides instructions on how to set up the baseline AWS users and permissions for the AWS Service Management Connector for Jira Service Management\.

## Available template for baseline permissions<a name="template-baseline"></a>

To use an AWS CloudFormation template to set up the AWS configurations of the Connector for Jira Service Management, see the AWS configurations for [Connector for Jira Service Management v1\.8\.2 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.2-AWS_Configurations_Commercial.json ) and [Connector for Jira Service Management v1\.8\.2 \- AWS GovCloud West Region](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.2-AWS_Configurations_GovCloud.json)\.

**Note**  
If you use the Connector for Jira Service Management v1\.8\.2\_AWS Configuration template, skip to [Configuring AWS Service Catalog](jsd-integration-configure-sc.md)\.

For each AWS account, the Connector for Jira Service Management requires two sets of an access key identifier and a secret key for API access\. These correspond to users in AWS Identity and Access Management \(IAM\)\. Specifically, you should set up:
+ An IAM user to sync AWS resources to Jira Service Management\.
+ An IAM user able to perform end user functionality to provision and execute requests exposed through Jira Service Management, including any roles required to perform the provisioning and execution\. We recommend launch roles for AWS Service Catalog\.

 These can be the same user and can be an existing user\. We recommend you assign two new users for Connector\. 

**Note**  
 To use an AWS CloudFormation template to set up the AWS configurations of the Connector for Jira Service Management, see the two JSON AWS Configurations for [Connector for Jira Service Management v1\.8\.2 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.2-AWS_Configurations_Commercial.json) and [Connector for Jira Service Management v1\.8\.2 \- AWS GovCloud West Region](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.2-AWS_Configurations_GovCloud.json)\.

## Creating AWS Service Management Connector Sync User<a name="jsd-creating-sc-sync-user"></a>

 The following section describes how to create the AWS Connector sync user and associate the appropriate IAM permissions\. To perform this task, you need IAM permissions to create new users\. 

**To create AWS Service Management Connector sync user**

1. Follow the instructions in **[Creating IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html)** to create the policy, **SSMOpsItemActionPolicy**\. This policy enables Jira administrators to create and manage AWS Systems Manager OpsItems\. 

   Copy this policy and paste it into **Policy Document**:

   ```
   {
   
       "Version": "2012-10-17",
   
       "Statement": [
   
           {
   
               "Effect": "Allow",
   
               "Action": [
   
                   "ssm:CreateOpsItem",
   
                   "ssm:GetOpsItem",
   
                   "ssm:UpdateOpsItem",
   
                   "ssm:DescribeOpsItems",
   
                   "ssm:CreateOpsItem"
   
               ],
   
               "Resource": "*"
   
           }
   
       ]
   
   }
   ```

1. Follow the instructions in [Creating IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html) and create the policy, **ConfigBidirectionalSecurityHubSQSBaseline**\. 

   Copy this policy and paste it in the JSON editor\.

   ```
                       {
      "Version":"2012-10-17",
      "Statement":[
         {
            "Sid":"VisualEditor0",
            "Effect":"Allow",
            "Action":[
               "cloudformation:RegisterType",
               "cloudformation:DescribeTypeRegistration",
               "cloudformation:DeregisterType",
               "sqs:ReceiveMessage",
               "sqs:DeleteMessage",
               "sqs:DeleteMessageBatch",
               "config:PutResourceConfig",
               "securityhub:BatchUpdateFindings"
            ],
            "Resource":"*"
         }
      ]
   ```

1. Follow the instructions in **[Creating an IAM User in Your AWS Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)** to create a sync user \(SCSyncUser\)\. The user needs programmatic and AWS Management Console access to follow the Connector for Jira Service Management installation instructions\.

   Set permissions for your sync user \(SCSyncUser\)\. Choose **Attach the following policies directly** and select **AWSServiceCatalogAdminReadOnlyAccess**,** AmazonSSMReadOnlyAccess**,**SSMOpsItemActionPolicy, **and** ConfigBidirectionalSecurityHubSQSBaseline\.**

1.  Also add a policy allowing **budgets:ViewBudget** on all resources \(\*\)\. 

1.  Review and choose **Create User**\. 

1. Note the access and secret access information\. Download the \.csv file that contains the user credential information\.

## Creating AWS Service Management Connector End User<a name="jsd-creating-sc-end-user"></a>

 The following section describes how to create the AWS Service Management Connector end user and associate the appropriate IAM permissions\. To perform this task, you need IAM permissions to create new users\. 

**To create AWS Service Management Connector end user**

1. Follow the instructions in [Creating an IAM User in Your AWS Account](https://https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) to create a user \(such as SCEndUser\)\. The user needs programmatic and AWS Management Console access to follow the Connector for Jira Service Management installation instructions\.

1.  For products with AWS CloudFormation StackSets, you need to create a stack set inline policy\. With AWS CloudFormation StackSets, you can create products to deploy across multiple accounts and Regions\. 

   Using an administrator account, you define and manage an AWS Service Catalog product and use it as the basis for provisioning stacks into selected target accounts across specified Regions\. You need to have the necessary permissions defined in your AWS accounts\. 

    To set up the necessary permissions, follow the instructions in [Granting Permissions for Stack Set Operations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs.html) to create an **AWSCloudFormationStackSetAdministrationRole** and an **AWSCloudFormationStackSetExecutionRole**\. 

1.  Create the stack set inline policy to enable the provisioning of a product across multiple Regions in one account, replacing the `arn` number string with your account number\. 

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
 The [Connector for Jira Service Management v1\.8\.2 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.2-AWS_Configurations_Commercial.json) and [Connector for Jira Service Management v1\.8\.2 \- AWS GovCloud West Region](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.2-AWS_Configurations_GovCloud.json) templates include the AWS CloudFormation StackSet permissions\. 

1.  Add the following permissions \(policies\) to the user **SCEndUser**: 
   + **AWSServiceCatalogEndUserFullAccess** \- \(AWS managed policy\)
   + **StackSet** \- \(inline policy\)
   + **AmazonS3ReadOnlyAccess** \- \(AWS managed policy\)
   + **AmazonEC2ReadOnlyAccess** \- \(AWS managed policy\)
   + **AWSConfigUserAccess** \- \(AWS managed policy\)
   + **SSMOpsItemActionPolicy** \- \(inline policy\)
   + **ConfigBidirectionalSecurityHubSQSBaseline** \- \(inline policy\)
**Note**  
 For AWS Service Catalog products with AWS CloudFormation StackSets, you need to include the read only permissions for the services you want to provision\. For example, to provision an Amazon S3 bucket, include the **AmazonS3ReadOnlyAccess** policy to the **SCEndUser** role\. 

1. Also add a policy that allows the following on all resources \(\*\): **ssm:DescribeAutomationExecutions**, **ssm:DescribeDocument**, and ssm:**StartAutomationExecution**\. 

1. Review and choose **Create User**\. 

1. Note the access and secret access information\. Download the \.csv file that contains the user credential information\.

## Creating SCConnectLaunch Role<a name="jsd-creating-scconnectlaunch-role"></a>

 The following section describes how to create the **SCConnectLaunch** role\. This role places baseline AWS service permissions into the AWS Service Catalog launch constraints\. For more information, see [AWS Service Catalog Launch Constraints](constraints-launch.md)\. 

**To create SCConnectLaunch role**

1. Create the **AWSCloudFormationFullAccess** policy\. Choose **create policy** and then paste the following in the JSON editor\.

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

1. Create a policy called **ServiceCatalogSSMActionsBaseline**\. Follow the instructions in [Creating IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html), and paste the following into the JSON editor\. 

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

1. Create the **SCConnectLaunch** role\. Assign the trust relationship to AWS Service Catalog\.

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

1. Attach the relevant policies to the **SCConnectLaunch** role\. Attach the following baseline IAM policies:
   + **AmazonEC2FullAccess** \(AWS managed policy\)
   + **AmazonS3FullAccess ** \(AWS managed policy\)
   + **AWSCloudFormationFullAccess** \(custom managed policy\)
   + **ServiceCatalogSSMActionsBaseline** \(custom managed policy\)

**Note**  
 To use an AWS CloudFormation template to set up the AWS configurations of the Connector for Jira Service Management, see the two JSON AWS Configurations for [Connector for Jira Service Management v1\.8\.2 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.2-AWS_Configurations_Commercial.json) and [Connector for Jira Service Management v1\.8\.2 \- AWS GovCloud West Region](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.2-AWS_Configurations_GovCloud.json  )\.
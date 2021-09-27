# Configuring AWS Service Catalog<a name="configure-sc"></a>

After you create two IAM users with baseline permissions in each account, the next step is to configure AWS Service Catalog\. This section describes how to configure AWS Service Catalog to have a portfolio with an Amazon S3 bucket product\. Use the Amazon S3 template in [Creating an Amazon S3 Bucket for Website Hosting for your preliminary product](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/quickref-s3.html#scenario-s3-bucket-website)\. Copy and save the Amazon S3 template to your device\.

**To configure AWS Service Catalog**

1. Follow the steps in [Create an AWS Service Catalog Portfolio](getstarted-portfolio.md) to create a portfolio\.

1.  To add the Amazon S3 bucket product to the portfolio you created in Step 1, go to the AWS Service Catalog console\. In the **Upload new product** page, enter the product details\. 

1.  For Select template, choose the Amazon S3 bucket AWS CloudFormation template you saved to your device\. 

1. Set **Constraint type** to **Launch** for the product that you created now with the SCConnectLaunch role in the baseline permissions\. For additional launch constraint instructions, see [AWS Service Catalog Launch Constraints](constraints-launch.md)\. 
**Note**  
The AWS configuration design requires each AWS Service Catalog product to have a launch constraint\. Failure to follow this step could result in an “Unable to Retrieve Parameter” message in the ServiceNow Service Catalog\. 

1. Add the SnowEndUser IAM user to the AWS Service Catalog portfolio\. For additional user access instructions, see [Granting Access to Users](catalogs_portfolios_users.md)\. 

**Note**  
 The AWS configuration design requires each AWS Service Catalog product to have either a launch constraint or a stack set constraint\. Failure to follow this step could result in an “Unable to Retrieve Parameter” error in the ServiceNow Service Catalog\. 

## Creating Stack Set constraints<a name="stackset-constraints"></a>

AWS CloudFormation StackSets enable users to create and deploy products across multiple accounts and Regions\. 

**To apply a stack set constraint to an AWS Service Catalog product**

1. Go to AWS Service Catalog as a catalog admin\.

1. Choose the portfolio that contains the product\.

1. Expand **Contraints** and choose **Add constraints**\.

1. Choose the product from **Product** and set **Constraint type** to **Stack Set**\. Choose **Continue**\.

1. On the Stack Set constraint page, enter a description\.

1. Choose the account\(s\) in which you want to create products\.

1. Choose the Region\(s\) in which you want to deploy products\. Products deploy in these Regions in the order you specify\.

1. Choose **AWSCloudFormationStackSetAdministrationRole** to manage your target accounts\.

1. Choose **AWSCloudFormationStackSetExecutionRole** for the role the Administrator will assume\.

1. Choose **Submit**\.

Note that the [Connector for ServiceNow v3\.7\.1 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForServiceNowv-AWS_Configurations_Commercialv3.7.1.json) and [Connector for ServiceNow v3\.7\.1 \- AWS GovCloud Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForServiceNowv-AWS_Configurations_GovCloudv3.7.1.json) templates create the permissions as well as outputs for stack set constraints\. 

Example stack set outputs: 

```
             SCStackSetAdministratorRoleARN 
             arn:aws:iam::123456789123:role/AWSCloudFormationStackSetAdministrationRole SCIAMStackSetExecutionRoleName 
             AWSCloudFormationStackSetExecutionRole  
             SCIAMAdminRoleARN 
             arn:aws:iam::123456789123:role/AWSCloudFormationStackSetAdministrationRole
```

**Note**  
Replace the **123456789123** with your account information\.

## Relating budgets to products and portfolios<a name="servicenow-budgets"></a>

 The Connector for ServiceNow enables ServiceNow administrators to view budgets related to AWS Service Catalog products and portfolios\. AWS Service Catalog administrators can create or associate existing budgets to products and portfolios\. 

 For more information on creating and associating budgets, see [Managing Budgets](catalogs_budgets.md)\. 

# Connector for ServiceNow<a name="integrations-servicenow"></a>

To help customers integrate provisioning secure, compliant, and pre\-approved AWS products into their ServiceNow portal, AWS created the AWS Service Catalog Connector for ServiceNow\.

AWS Service Catalog Connector for ServiceNow synchronizes AWS Service Catalog portfolios and products with the ServiceNow Service Catalog to enable ServiceNow users to request approved AWS products via ServiceNow\.

**Topics**
+ [Background](#background)
+ [Getting Started](#getting-started)
+ [Release Notes](#release-notes)
+ [Baseline Permissions](baseline-permissions.md)
+ [Configure AWS Service Catalog](configure-sc.md)
+ [Creating StackSet Constraints](stackset-constraints.md)
+ [Configure ServiceNow](configure-snow.md)
+ [Validate Configurations](validate-configurations.md)
+ [ServiceNow Additional Administrator Features](additional-configurations.md)
+ [Upgrade Instructions](upgrade-instructions.md)

## Background<a name="background"></a>

AWS Service Catalog allows you to centrally manage commonly deployed AWS services and provisioned software products\. It helps your organization achieve consistent governance and compliance requirements, while enabling users to quickly deploy only the approved AWS services they need\.

[ServiceNow](https://www.servicenow.com/) is an enterprise service management platform that places a service‑oriented lens on the activities, tasks, and processes that make up day‑to‑day work life to enable a modern work environment\. [ServiceNow Service Catalog](https://www.servicenow.com/products/it-service-automation-applications/service-catalog.html) is a self\-service application that end users can use to order IT services based on request fulfillment approvals and workflows\.

## Getting Started<a name="getting-started"></a>

Before installing the AWS Service Catalog Connector for ServiceNow, verify that you have the necessary permissions in your AWS account and ServiceNow instance\.

### AWS prerequisites<a name="aws-prereqs"></a>

To get started you need an AWS account to configure your AWS portfolios and products\. For details, see [Setting Up for AWS Service Catalog](setup.md)\.

For each AWS account, the Connector for ServiceNow also requires two AWS Identity and Access Management \(IAM\) users and two IAM roles:
+ An IAM user to sync AWS Service Catalog portfolios and products to ServiceNow Service Catalog items\.
+ An IAM role configured as an AWS Service Catalog end user and assigned to each portfolio\.
+ An IAM end user to assume the previous end user role\. This end user has a baseline of permissions to provision AWS services in the ServiceNow Service Catalog\. This ServiceNow end user is linked to the end user role in IAM\.
+ An IAM launch role used to place baseline AWS service permissions into the AWS Service Catalog launch constraints\. Configuring this role enables segregation of duty by provisioning product resources on behalf of the ServiceNow end user\.

Baseline permissions enable an end user to provision the following AWS services: Amazon Simple Storage Service and Amazon Elastic Compute Cloud\. To allow end users to provision AWS services beyond the baseline permissions, you must include the additional AWS service permissions to the launch role\. For information about initial permissions setup actions, see [Baseline Permissions](baseline-permissions.md)\.

**Note**  
 To use an AWS CloudFormation template to set up the AWS configurations of the Connector for ServiceNow, see [Connector for ServiceNow\-AWS Configuration](https://s3.amazonaws.com/servicecatalogconnector/SC_ConnectorForServiceNowv2.0.2-AWS_Configurations.yml)\. 

### ServiceNow Prerequisites<a name="servicenow-prereqs"></a>

In addition to the AWS account, you need a ServiceNow instance to install the ServiceNow Connector scoped application\. The initial installation should occur in either an enterprise sandbox or a [ServiceNow Personal Developer Instance](https://developer.servicenow.com/app.do#!/training/article/app_store_learnv2_buildmyfirstapp_kingston_servicenow_basics/app_store_learnv2_buildmyfirstapp_kingston_personal_developer_instances?v=kingston) \(PDI\), depending on your organization’s technology governance requirements\. The ServiceNow administrator needs the admin role to install the Connector for ServiceNow scoped application\.

## Release Notes<a name="release-notes"></a>

**Version 2\.0\.2** of the AWS Service Catalog Connector for ServiceNow includes:
+ Support for AWS CloudFormation StackSets, enabling launch of AWS Service Catalog products across multiple regions and accounts\.
+ Support for AWS CloudFormation Change Sets, enabling a preview of resource changes from a launch or update\.
+ Display of AWS Service Catalog portfolios \(including correlated products\) as sub\-categories in the ServiceNow Service Catalog\.

This version also includes prior AWS Service Catalog Connector for ServiceNow features such as:
+ Support AWS Service Catalog self\-service actions\.
+ Enable ServiceNow administrators to delete AWS Service Catalog products in ServiceNow that do not have self\-service actions associated\.
+ Render AWS Service Catalog products in the ServiceNow Portal page\.
+ Enable multi\-account support\.
+ Request update against an existing AWS Service Catalog product provisioned in ServiceNow\.
+ Validate AWS Regions and identities associated with syncing AWS and ServiceNow\.
+ Sync product details in the My Asset/CMDB view\.
# AWS Service Catalog Connector for Jira Service Desk<a name="integrations-jiraservicedesk"></a>

 To help customers integrate provisioning secure, compliant, and pre\-approved AWS products into their Jira Service Desk portal, AWS created the AWS Service Catalog Connector for Jira Service Desk \(Server and Data Center\)\. 

 The AWS Service Catalog Connector for Jira Service Desk synchronizes AWS Service Catalog portfolios and products with the Jira Service Desk request type to enable Jira Service Desk users to request permitted AWS products via Jira Service Desk\. 

**Topics**
+ [Background](#jsd-integration-background)
+ [Jira Service Desk Supported Versions and Releases](#jsd-supported-versions)
+ [Getting Started](#jsd-integration-getting-started)
+ [Release Notes](#jsd-integration-release-notes)
+ [Baseline Permissions](jsd-integration-baseline-permissions.md)
+ [Configuring AWS Service Catalog](jsd-integration-configure-sc.md)
+ [Configuring Jira Service Desk](jsd-integration-configure-jsd.md)

## Background<a name="jsd-integration-background"></a>

 AWS Service Catalog allows you to centrally manage commonly deployed AWS services and provisioned software products\. It helps your organization meet consistent governance and compliance requirements, while enabling users to quickly deploy only the approved AWS services they need\. 

[Atlassian Jira Service Desk](https://www.atlassian.com/software/jira/service-desk/) is service desk software for modern IT teams\. Jira Service Desk request types enable self\-service for developers and end users to order IT services based on request fulfillment approvals and workflows\.

## Jira Service Desk Supported Versions and Releases<a name="jsd-supported-versions"></a>

 The AWS Service Catalog Connector for Jira Service Desk supports Jira Service Desk Server and Data Center versions\. Jira software \(Jira Service Desk\) releases are supported from Jira 7\.11\.2 \(JSD 3\.14\.2\) to Jira 8\.5\.1 \(JSD 4\.5\.1\)\.

## Getting Started<a name="jsd-integration-getting-started"></a>

 Before installing the AWS Service Catalog Connector for Jira Service Desk, you need an AWS account and an Atlassian instance with [Jira Service Desk pre\-installed](https://confluence.atlassian.com/servicedeskserver043/installing-jira-service-desk-974367443.html)\. Verify that you have the necessary permissions in your AWS account and Jira Service Desk software\. 

**Note**  
 The [Jira Products on AWS Reference Deployment Quick Start](https://aws.amazon.com/quickstart/architecture/jira/) is available to use AWS resources for infrastructure required to install Jira Service Desk data center version\.

### AWS prerequisites<a name="jsd-integration-aws-prereqs"></a>

 To get started, you need an AWS account to configure your AWS portfolios and products\. For details, see [Setting Up for AWS Service Catalog](setup.md)\. 

 For each AWS account, the Connector for Jira Service Desk also requires two AWS Identity and Access Management \(IAM\) users and one IAM role: 
+ An IAM user to sync AWS Service Catalog portfolios and products to Jira Service Desk AWS Service Catalog items\.
+ An IAM role configured as an AWS Service Catalog end user and assigned to each portfolio\.
+ An IAM launch role used to place baseline AWS service permissions into the AWS Service Catalog launch constraints\. Configuring this role enables segregation of duty by provisioning product resources on behalf of the Jira Service Desk end user\.

 Baseline permissions enable an end user to provision the following AWS services: Amazon Simple Storage Service and Amazon Elastic Compute Cloud\. To allow end users to provision AWS services beyond the baseline permissions, you must include the additional AWS service permissions to the appropriate roles\. For information about initial permissions setup actions, see [Baseline Permissions](jsd-integration-baseline-permissions.md)\. 

**Note**  
 To use an AWS CloudFormation template to set up the AWS configurations of the Connector for Jira Service Desk, see the two JSON AWS Configurations for [Connector for Jira Service Desk v1\.0\.4 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SC_ConnectorForJSD1.0.4-AWS_Configurations_final.json) and [Connector for Jira Service Desk v1\.0\.4 \- AWS GovCloud West Region](https://servicecatalogconnector.s3.amazonaws.com/SC_ConnectorForJSDv1.0.4+-AWS_Configurations_GovCloudv_final.json)\.

### Jira Service Desk prerequisites<a name="jsd-prereqs"></a>

 In addition to your AWS account, you need the Jira Service Desk software installed on your Atlassian instance before you can install the AWS Service Catalog Connector add\-on\. The Jira Service Desk administrator needs the admin role in order to install the AWS Service Catalog Connector add\-on\. 

 Before configuring your AWS connector, ensure that you follow Atlassian recommendations for securing your Jira Service Desk instances\. For more information, see [Preventing Security Attacks](https://confluence.atlassian.com/adminjiraserver0713/preventing-security-attacks-964984188.html)\. 

 The Connector for Jira Service Desk add\-on is available to download in the [Atlassian Marketplace](https://marketplace.atlassian.com/apps/1221283/aws-service-catalog-connector-for-jsd)\. 

## Release Notes<a name="jsd-integration-release-notes"></a>

 **Version 1\.0\.4** of the AWS Service Catalog Connector for Jira Service Desk includes: 
+ Rendering AWS Service Catalog portfolios and products in the Jira Service Desk Customer Portal and Jira Agent views\.
+ The ability for Jira Service Desk administrators to associate Jira Service Desk approval groups to AWS Service Catalog portfolios to require approvals for Jira Service Desk user product requests\.
+ The ability for Jira Service Desk users to request AWS Service Catalog products through Jira Service Desk\.
+ Support for AWS Service Catalog self\-service actions for Jira Service Desk users to update and terminate products\.
+ Support for AWS CloudFormation StackSets, enabling launch of AWS Service Catalog products across multiple regions and accounts\.
+ Support for CloudFormation Change Sets, enabling a preview of resource changes prior to a launch or update\.
+ Support for multiple AWS accounts\.
+ Support for FIPS endpoints and usage in the AWS GovCloud West region\.
+ Support for the latest releases of Jira Service Desk Server and Data Center versions\.

# AWS Service Management Connector for Jira Service Management<a name="integrations-jiraservicedesk"></a>

The AWS Service Management Connector for Jira Service Management \(formerly the AWS Service Catalog Connector\) enables Jira Service Management end users to provision, manage, and operate AWS resources natively through Atlassian's Jira Service Management\.

 It enables Jira Service Management administrators to:
+ Provide pre\-approved, secured, and governed AWS resources to end\-users through AWS Service Catalog\.
+ Create and manage operational items through AWS Systems Manager OpsCenter\.
+ Execute automation playbooks through AWS Systems Manager Automation\. 
+ Track resources in a configuration item view powered by AWS Config\. 
+ View, update, and resolve issues through AWS Security Hub findings seamlessly on the Jira Service Management with the AWS Service Management Connector\. 

This workflow simplifies AWS product request actions for Jira Service Management users and provides Jira Service Management governance and oversight over AWS products\. 

The AWS\-supplied connector is available at no charge in the Atlassian Marketplace\. This new feature is generally available in all AWS Regions where AWS Service Catalog, AWS Config, and AWS Systems Manager services are available\. 

**Topics**
+ [Background](#jsd-integration-background)
+ [Jira Service Management Supported Versions and Releases](#jsd-supported-versions)
+ [Getting Started](#jsd-integration-getting-started)
+ [Release Notes](#jsd-integration-release-notes)
+ [Baseline Permissions](jsd-integration-baseline-permissions.md)
+ [Configuring AWS Service Catalog](jsd-integration-configure-sc.md)
+ [Configuring AWS Security Hub](config-security-hub.md)
+ [Configuring Jira Service Management](jsd-integration-configure-jsd.md)
+ [IT Lifecycle Management Setup and Use Case](jsd-it-lifecycle.md)
+ [Validating Configurations](jsd-validate-configurations.md)
+ [Managing AWS Security Hub settings in JSM Integration](security-hub.md)
+ [Jira Additional Administrator Features](jsd-admin-features.md)

## Background<a name="jsd-integration-background"></a>

 [AWS Service Catalog](https://aws.amazon.com/servicecatalog) allows you to centrally manage commonly deployed AWS services and provisioned software products\. It helps your organization meet consistent governance and compliance requirements, while enabling users to quickly deploy only the approved AWS services they need\. 

 [AWS Config](https://aws.amazon.com/config) enables you to assess, audit, and evaluate the configurations of your AWS resources\. AWS Config continuously monitors and records all your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations\. 

 [AWS Systems Manager](https://aws.amazon.com/systems-manager) gives you visibility and control of your infrastructure on AWS\. Systems Manager provides a unified user interface so you can view operational data from multiple AWS services, investigate and resolve operational issues through OpsCenter, and allows you to automate operational tasks across your AWS resources\. 

[AWS Security Hub](https://aws.amazon.com/security-hub/) gives you a comprehensive view of your security alerts and security posture across your AWS accounts\. With Security Hub, there is a single place that aggregates, organizes, and prioritizes your security alerts, or findings\. 

[Atlassian Jira Service Management](https://www.atlassian.com/software/jira/service-desk/) is service desk software for modern IT teams\. Jira Service Management request types enable self\-service for developers and end users to order IT services based on request fulfillment approvals and workflows\.

## Jira Service Management Supported Versions and Releases<a name="jsd-supported-versions"></a>

The AWS Service Management Connector for Jira Service Management supports Jira Service Management Server and Data Center versions\. We support Jira software \(Jira Service Management\) releases for the current and one previous version in each of the major, minor, and point release streams for:
+ Jira Server 7\.13\.17 to 8\.17\.0
+  Jira Data Center 7\.13\.17 to 8\.17\.0

A Jira Service Management Cloud Connector is also available in the Atlassian Marketplace\. For more information, see [AWS Service Catalog for Jira Service Management Cloud](https://marketplace.atlassian.com/apps/1221551/aws-service-catalog-for-jsd-cloud?hosting=cloud)\.

## Getting Started<a name="jsd-integration-getting-started"></a>

 Before installing the AWS Service Management Connector for Jira Service Management, you need an AWS account and an Atlassian instance with [Jira Service Management pre\-installed](https://confluence.atlassian.com/servicedeskserver043/installing-jira-service-desk-974367443.html)\. Verify that you have the necessary permissions in your AWS account and Jira Service Management software\. 

For a zip file containing Connector add\-on code as well as AWS Configuration files, download and extract the [AWS Service Management Connector for JSM\-Configuration Files](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSD.zip)\.

**Note**  
 The [Jira Products on AWS Reference Deployment Quick Start](https://aws.amazon.com/quickstart/architecture/jira/) is available to use AWS resources for infrastructure required to install Jira Service Management data center version\.

### AWS prerequisites<a name="jsd-integration-aws-prereqs"></a>
+ To use AWS Service Catalog with the Connector, you need an AWS account to configure your AWS portfolios and products\. For more information, see [Setting Up AWS Service Catalog](setup.md)\.
+ To see AWS Config details, configure the service settings to record data for the resource types of interest\. We recommend including provisioned products and AWS CloudFormation stacks, in addition to the major resource types your team uses\. For more information, see [Setting Up AWS Config with the Console](https://docs.aws.amazon.com/config/latest/developerguide/gs-console.html)\.
+ To use AWS Systems Manager Automation with the Connector, you don't need AWS\-side setup\. A number of automation documents are available from AWS as standard\. If you want to use additional automation documents, they are available in the Connector\. For more information, see [Working with Automation Documents \(Playbooks\)](https://docs.aws.amazon.com/systems-manager/latest/userguide/automation-documents.html)\.
+ To use AWS Systems Manager OpsCenter with the Connector, enable OpsCenter in the AWS Systems Manager console\. For more information, see [Getting Started with OpsCenter\.](https://docs.aws.amazon.com/systems-manager/latest/userguide/OpsCenter-getting-started.html) The Connector also enables viewing resources and automation documents \(runbooks\) associated to OpsItem\. For more information to associate resources to OpsItems in AWS OpsCenter, see [Working with Related Resources](https://docs.aws.amazon.com/systems-manager/latest/userguide/OpsCenter-working-with-OpsItems.html#OpsCenter-working-with-OpsItems-related-resources) \. For more information to associate automation documents to OpsItems in AWS OpsCenter, see [Remediating OpsItem issues using Systems Manager automation](https://docs.aws.amazon.com/systems-manager/latest/userguide/OpsCenter-remediating.html)\.
+ To use AWS Security Hub with the Connector, you must enable the service in all Regions and accounts where you want to sync Findings\. For more information, see [Setting up Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html)\. We recommend you connect ServiceNow with the primary \(master\) AWS account for AWS Security Hub\. For more information, see [Managing master and member accounts\.](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-accounts.html) 

 For each AWS account, the Connector for Jira Service Management also requires API access with [Baseline permissions](baseline-permissions.md)\.

### Jira Service Management prerequisites<a name="jsd-prereqs"></a>

 In addition to your AWS account, you need the Jira Service Management software installed on your Atlassian instance before you can install the AWS Service Management Connector add\-on\. The Jira Service Management administrator needs the *admin* role to install the AWS Service Management Connector add\-on\. 

 Before configuring your AWS connector, ensure you follow Atlassian recommendations for securing your Jira Service Management instances\. For more information, see [Preventing Security Attacks](https://confluence.atlassian.com/adminjiraserver/preventing-security-attacks-938847893.html)\. 

 The Connector for Jira Service Management add\-on is available to download in the [Atlassian Marketplace](https://marketplace.atlassian.com/apps/1221283/aws-service-catalog-connector-for-jsd)\. 

## Release Notes<a name="jsd-integration-release-notes"></a>

Version 1\.8\.2 of the AWS Service Management Connector for Jira Service Management introduces an integration with AWS Security Hub\.

**AWS Security Hub integration ** 
+ Configure synchronization of AWS Security Hub Findings within Jira Service\. 
+ View, investigate and resolve AWS Security Hub Findings as Jira issues\. 
+ View updates from synced Security Findings Jira issues in AWS Security Hub\. 

 This version also includes prior AWS Service Management Connector for Jira Service Management features\. 

**AWS Service Catalog**
+ Render AWS Service Catalog portfolios and products in the Jira Service Management Customer Portal and Jira Agent views\.
+ Associate Jira Service Management approval groups to AWS Service Catalog portfolios to require approvals for Jira Service Management user product requests\. 
+ Assign the default Jira user that the Jira workflow engine uses\.
+  Configure AWS product request form components available for end users to view\. 
+ Create AWS Tags across provisioned products\.
+  View AWS specific parameters on EC2 resources, such as Availability Zones, Image ID, Instance Id, KeyPair, Security Group, and VPC\. 

**AWS Config**
+ Render AWS Config configuration item details on provisioned AWS products through Jira Service Management request\.
+ View the configuration item relationships in a tree structure\.
+ Associate AWS Config items details to Jira issues\.

**AWS Systems Manager Automation**
+ Render AWS Systems Manager automation documents in the Jira Service Management Customer Portal and Jira Agent views\.
+ Request and execute AWS Systems Manager automation documents through Jira Service Management\.
+ Create Jira issues \(incidents\) that provide actionable remediation suggestions through a Connector specific AWS Systems Manager automation document\.

**AWS Systems Manager OpsCenter**
+ Create and update a Jira Issue when you create and update an operational item \(OpsItem\) in AWS Systems Manager OpsCenter\.
+ Update OpsItems in AWS Systems Manager OpsCenter when you update the Jira issue in Jira Service Management\.
+ View and execute automation runbooks to resolve OpsItems and view execution results from the Jira Issue\.
+ Support multiple AWS accounts\.
+ Support FIPS endpoints and usage in the AWS GovCloud East and GovCloud West Regions\.
+ Support the latest releases of Jira Service Management Server and Data Center versions\.
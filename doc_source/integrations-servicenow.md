# AWS Service Management Connector for ServiceNow<a name="integrations-servicenow"></a>

The AWS Service Management Connector for ServiceNow \(formerly the AWS Service Catalog Connector\) enables ServiceNow end users to provision, manage, and operate AWS resources natively through ServiceNow\. 

ServiceNow administrators can:
+ Provide pre\-approved, secured, and governed AWS resources to end users through AWS Service Catalog\.
+ Execute automation playbooks through AWS Systems Manager\. 
+ View and manage operational items as incidents through AWS Systems Manager OpsCenter
+ Track resources in the CMDB, powered by AWS Config, seamlessly on ServiceNow with the AWS Service Management Connector\.
+ Define new resource types based on ServiceNow CMDB tables and synchronize these with AWS Config custom resources\.
+ Configure syncing AWS Security Hub findings to ServiceNow incidents or problems\.

 ServiceNow end users can: 
+ Browse, request, and provision pre\-secured AWS solutions\.
+ View AppRegistry applications, attribute groups, and related resource details with AWS Service Catalog \- AppRegistry
+ View, update and resolve incidents from AWS Systems Manager OpsItems
+ View configuration item details\.
+ Execute workflows in ServiceNow on AWS resources\. 
+ View, update, and resolve ServiceNow incidents or problems through AWS Security Hub findings\.

These features simplify AWS product request actions for ServiceNow users, and provide ServiceNow governance and oversight over AWS products\. 

The AWS\-supplied connector is available at no charge in the ServiceNow store\. It supports ServiceNow platform releases Rome \(R\), Quebec \(Q \- Patch 5 going forward\), Paris \(P\) and Orlando \(O\)\. These new features are generally available in all AWS Regions where AWS Service Catalog, AWS Conﬁg, and AWS Systems Manager services are available\.

**Topics**
+ [Background](#background)
+ [Getting started](#getting-started)
+ [Release notes](#release-notes)
+ [Baseline permissions](baseline-permissions.md)
+ [Configuring AWS Service Catalog](configure-sc.md)
+ [Configuring AWS Config](servicenow-aws-config.md)
+ [Configuring AWS Security Hub](servicenow-security-hub.md)
+ [Configuring AWS Systems Manager OpsCenter](configure-ops.md)
+ [Configuring ServiceNow](config-servnow.md)
+ [Configuring AWS Config integration in ServiceNow](configure-integ.md)
+ [Configuring AWS Systems Manager OpsCenter integration in ServiceNow](integrate-opscenter.md)
+ [Validating configurations](validate-configurations.md)
+ [ServiceNow additional features](additional-configurations.md)
+ [Version 2\.3\.4 release transition instructions](transition-instructions.md)

## Background<a name="background"></a>

[AWS Service Catalog](http://aws.amazon.com/servicecatalog) allows you to centrally manage commonly deployed AWS services and provisioned software products\. It helps your organization achieve consistent governance and compliance requirements, while enabling users to quickly deploy only the approved AWS services they need\. It also offers AWS Service Catalog\-AppRegistry so you can create a repository of your applications and associated resources\.

[AWS Config](http://aws.amazon.com/config) enables you to assess, audit, and evaluate the configurations of your AWS resources\. AWS Config continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations\.

[AWS Systems Manager](http://aws.amazon.com/systems-manager) gives you visibility and control of your infrastructure on AWS\. Systems Manager provides a unified user interface so you can view operational data from multiple AWS services, investigate and resolve operational issues through the OpsCenter, and automate operational tasks across your AWS resources\.

[AWS Security Hub](https://aws.amazon.com/security-hub/?aws-security-hub-blogs.sort-by=item.additionalFields.createdDate&aws-security-hub-blogs.sort-order=desc) gives you a comprehensive view of your security alerts and security posture across your AWS accounts\. With Security Hub, there is a single place that aggregates, organizes, and prioritizes your security alerts, or findings\. 

[ServiceNow](https://www.servicenow.com/) is an enterprise service management platform that places a service\-oriented lens on the activities, tasks, and processes that enables day\-to\-day work life and a modern work environment\. [ServiceNow Service Catalog](https://www.servicenow.com/products/it-service-automation-applications/service-catalog.html) is a self\-service application that end users can use to order IT services based on request fulfillment approvals and workflows\. The [ServiceNow CMDB](https://docs.servicenow.com/bundle/orlando-servicenow-platform/page/product/configuration-management/concept/c_ITILConfigurationManagement.html) provides resource transparency and relationships for the logical components of a service\. 

## Getting started<a name="getting-started"></a>

Before installing the AWS Service Management Connector for ServiceNow, verify that you have the necessary permissions in your AWS account and ServiceNow instance\.

### AWS prerequisites<a name="aws-prereqs"></a>

To start, use the following services:
+  AWS Service Catalog with the Connector 

  You need an AWS account to configure your AWS portfolios and products\. For details, see [Setting up for AWS Service Catalog](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/setup.html) and [Using AWS Service Catalog\-AppRegistry\.](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/appregistry.html)
+  AWS Config details

  Configure the service settings to record data for the resource types of interest\. We recommend you include provisioned products and AWS CloudFormation stacks, in addition to the major resource types that your team uses\. For more information, see [Setting up AWS Config with the console](https://docs.aws.amazon.com/config/latest/developerguide/gs-console.html)\. This version of the Connector enables the import of aggregated Config data in a single AWS account from more than one AWS Region or account\. To use this feature, you must configure an aggregator in AWS\. For more information, see [Setting up an Aggregator using the console](https://docs.aws.amazon.com/config/latest/developerguide/setup-aggregator-console.html)\. 
+  AWS Systems Manager Automation with the Connector

  This feature requires no AWS\-side set up\. As standard, AWS provides a number of automation documents \(runbooks\)\. If you want additional automation documents \(runbook\), retrieve them in the Connector\. For more information, see [Working with Automation Runbooks](https://docs.aws.amazon.com/systems-manager/latest/userguide/automation-documents.html)\. 
+  AWS Systems Manager OpsCenter with the Connector

  You must enable the service in all Regions and accounts where you want to sync OpsItems\. For more information, see [ Getting started with OpsCenter](https://docs.aws.amazon.com/systems-manager/latest/userguide/OpsCenter-getting-started.html) 
+ AWS Security Hub with the Connector

  You must enable the service in all Regions and accounts where you want to sync Findings\. For details see [Setting up Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html)\. We recommend you connect ServiceNow with the primary \(master\) AWS account for AWS Security Hub\. For more information, see [Managing master and member accounts](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-accounts.html)\.

### ServiceNow prerequisites<a name="servicenow-prereqs"></a>

In addition to the AWS account, you need a ServiceNow instance to install the ServiceNow Connector scoped application\. The initial installation should occur in either an enterprise sandbox or a [ServiceNow Personal Developer Instance](https://developer.servicenow.com/app.do#!/document/content/app_store_doc_getting_started_newyork_topic_lyf_bf2_3r?v=newyork) \(PDI\), depending on your organization’s technology governance requirements\. 

The ServiceNow administrator needs the admin role to install the Connector for ServiceNow scoped application\.

## Release notes<a name="release-notes"></a>

Version 3\.7\.1 of the AWS Service Management Connector for ServiceNow \(formerly the AWS Service Catalog Connector\) includes:

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/servicecatalog/latest/adminguide/integrations-servicenow.html)

This version also includes prior AWS Service Management Connector for ServiceNow feature integrations to AWS services, such as AWS Security Hub, AWS Config, and AWS Systems Manager Automation\.
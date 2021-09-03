# Validating configurations<a name="validate-configurations"></a>

 You can validate the AWS Service Management Connector for ServiceNow installation procedures\. 

## AWS Service Catalog integration features<a name="sc-integration-features"></a>

**To order an AWS Service Catalog product**

1. Log in to your ServiceNow instance as the end user \(for this example, Abel Tuter\)\. 

1. Enter **Service Catalog** in the navigation filter and choose **Service Catalog**\. 

1. Select the **AWS Service Catalog S3 Storage** product to provision\. 

1. Enter the product request details, including product name, parameters, and tags\. 

1.  Choose **Order Now** to submit the ServiceNow request and provision the AWS Service Catalog product\. 

1. After approximately one minute, you receive an order status acknowleging the submission\.

**To view provisioned products**

End users can view products in two places on the ServiceNow portal: request items \(Requests\) or My AWS Products widgets\. 

**To view products in Service Portal Requests**

1. Choose **Requests** in the home page navigation bar\.

1. Select the request item, which contains the AWS Service Catalog product and request item number\.
**Note**  
AWS product events and outputs update the request item\. When you terminate the AWS product, the ServiceNow request item enters a state of **Closed Complete**\. 

**To view products in the My AWS Products widget Service Portal Requests**

1. In the My AWS Products widget and choose the AWS Select Product name that you entered into the request form\.

1. View the **Status and Product Events**\.

1. If you want to perform post\-provisioned operational actions, choose **Request Update**, **Request Self\-Service Action**, or **Terminate**\.

## AWS Config integration features<a name="config-integration"></a>

To see AWS Config details, configure the service settings to record data for the resource types of interest\. For more information, see [Setting Up AWS Config with the Console](https://docs.aws.amazon.com/config/latest/developerguide/gs-console.html)\.

**To view configuration item details from AWS Config in the ServiceNow CMDB**

1.  Log in to your ServiceNow instance as a user \(for example, System Administrator\) in the fulfiller view \(Standard user interface view\)\. 

1.  In the navigator, enter **AWS Service Management**\. 

1.  Choose **AWS Config**\. 

Select and view relationships for available AWS resources\. This table illustrates the available AWS resources, ServiceNow CMDB label, and table name\.


| AWS resources \(AWS Config\) | ServiceNow CMDB/Scoped App Table Label | ServiceNow CMDB/Scoped App Table Name | 
| --- | --- | --- | 
| Accounts | CMDB CI Cloud Service Accounts | mdb\_ci\_cloud\_service\_account | 
| VPCs | Cloud Networks  | cmdb\_ci\_network | 
| Availability Zones | Availability Zone | cmdb\_ci\_availability\_zone | 
| EC2 Instances | Virtual Machine Instance | cmdb\_ci\_vm\_instance | 
| EBS Volumes | Storage Volume | cmdb\_ci\_storage\_volume | 
| Security Groups | Compute Security Group | cmdb\_ci\_compute\_security\_group | 
| Auto Scaling Group | Auto Scaling Groups | x\_126749\_aws\_sc\_cmdb\_ci\_autoscaling\_group | 
| Network Interfaces | Cloud Mgmt Network Interface | cmdb\_ci\_nic | 
| RDS Instances | Cloud DataBase | cmdb\_ci\_cloud\_database | 
| Subnets | Cloud Subnet | cmdb\_ci\_cloud\_subnet | 
| Load Balancers \(V2\) | Load Balancer Service | cmdb\_ci\_lb\_service | 
| S3 Buckets | Cloud Object Storages | cmdb\_ci\_cloud\_object\_storage | 
| CloudFormation Stacks | CloudFormation Stack | x\_126749\_aws\_sc\_cmdb\_ci\_cloudformation\_stack | 
| CloudFormation Provisioned Products | CloudFormation Provisioned Product | x\_126749\_aws\_sc\_cmdb\_ci\_config\_pp | 
| Tags | Key Value | cmdb\_key\_value | 
| Lambdas | Cloud Function | cmdb\_ci\_cloud\_function | 
| Dynamo DB | DynamoDB Table | cmdb\_ci\_dynamodb\_table | 
| OS images | Images | cmdb\_ci\_os\_template | 

**Note**  
AWS resources, in scope for this release, determine configuration items and relationships\. Configuration item relationships display AWS Regions\. If you have questions or feedback, email aws\-servicemanagement\-connector@amazon\.com\. 

## AWS Systems Manager Automation Integration features<a name="sys-integration"></a>

**To request an AWS Systems Manager automation document \(runbook\) execution**

1.  Log in to your ServiceNow instance as the end user \(for this example, Abel Tuter\)\. 

1.  In the navigation filter, enter **AWS Systems Manager**, then choose **Systems Manager**\. 

1.  Select an AWS Systems Manager document to execute\. 

1.  Enter the request details, including parameters and tags\. 

1.  Choose **Order Now** to submit the ServiceNow request and execute the AWS Systems Manager document\. 

1.  You receive an order status acknowledging your request submission\. 

**To view AWS Systems Manager document executions**

1.  Log in to your ServiceNow instance as the end user \(for example, Abel Tuter\)\. 

1.  In the navigation filter, enter **AWS Systems Manager**, then choose **Automation Executions**\. 

1.  The user interface view displays the latest executions and provides the status\. 

## AWS Systems Manager \- OpsCenter Integration features<a name="integration-features"></a>

**To view OpsItems from AWS Systems Manager \- OpsCenter**

1. To view AWS OpsItem, you must have the role `x_126749_aws_sc.opscenter_manager` with the Connector scope app\. 

1. Log in to your ServiceNow instance as a user \(for example, System Administrator\) in the fulfiller view \(Standard user interface view\)\. 

1. In the navigator, enter **AWS Service Management**\. 

1. Choose **AWS Systems Manager \- OpsCenter**\. 

1. Choose **OpsItems** to show a list of all synced Findings\. 

1. Choose an OpsItems to open the record\. 

   The Incident and Problem fields show the Incident for the OpsItems, if these exist\. 

1. Choose the ⓘ icon to the right of the field to preview the Incident\. 

1. Choose **Open Record** on the preview form to open the Incident\. 

   If the Connector configuration does not to automatically create a ServiceNow Incident when a new Finding syncs, you can create one manually\. To do so, choose the link at the bottom of the form\. 

**To execute an AWS Systems Manager – Automation Document from an AWS OpsItems associated to a ServiceNow Incident**

One of the following conditions must be true to view or execute automation documents \(runbooks\): 
+ The user has the role Account Manager or Automation Manager\. 
+ The user is assigned to a linked incident\.
+ The system parameter *Assignment Group \(SYS\_ID\) for created incidents* is set to a valid group, a linked incident whose Assignment group is set to that group, and the user is a member of that group\. 
**Note**  
To enable this feature, you must activate AWS Systems Manager Automation in the AWS Account and opt in to the Connector

1. Log in to your ServiceNow instance as a user \(for example, System Administrator\) in the fulfiller view \(standard user interface view\)\. 

1. In the navigator, enter **AWS Service Management**\. Then choose **AWS Systems Manager \- OpsCenter**\. 

1. Choose OpsItems to show a list of all synced Findings\. Then choose **Execute Automation Document**\.

1. Choose your Automation Document\.
**Note**  
You can configure an OpsItem with Automation Documents and mark it as *Associated*\. 

1. Choose **Order Execution** next to the Automation Document you want to execute\. You’ll see the ServiceNow catalog item associated with the Automation Document\. 

1. Enter the necessary AWS parameters and choose **Order Now**\. 

1. In OpsItems in the scoped app\. Choose the OpsItem in the Automation Document where you executed it\. 

1. In OpsItem Automation Executions, review the success or failure status\.

1. Follow your organization's incident management procedures to determine related incident resolution actions\.

**Fields mapped from OpsCenter OpsItem records to ServiceNow Incident records **

This table shows how AWS OpsItems map to ServiceNow incidents\.


| AWS Ops Center | ServiceNow Incident | 
| --- | --- | 
| Title  | short\_description  | 
| Description | description  | 
| CreatedTime  | opened\_at  | 
| Status | incident\_state  | 
| Severity  | impact/urgency  | 
| Priority | priority | 
| CreatedBy  | Not synced  | 
| LastModifiedTime | Not synced  | 
| LastModifiedBy | Not synced  | 
| Source | Not synced  | 
| OpsItemId  | Not synced  | 
| OperationalData | Not synced  | 
| Category  | Software | 

**Incident Status** is an integer in ServiceNow\. We map OpsItem status values to values\.


| ServiceNow Incident Status  | OpsCenter Status  | 
| --- | --- | 
| New \(primary\) | Open | 
| On Hold | Open | 
| In Progress | In Progress | 
| Resolved \(primary\) | Resolved | 
| Closed | Resolved | 
| Cancelled | Resolved | 

In this type of subjective mapping, we only change the target value if it is incompatible\. An example of subjective mapping would be if *New* and *On Hold* in ServiceNow both map to *Open* in AWS\. An example of an incompatible target would be if the incident is *On Hold*, while we're synchronizing from AWS an OpsItem that is *Open*, and we don't change *On Hold*\.

**Priority**: In Incident, you can’t set the Priority field directly\. The values of the **Impact** and **Urgency** fields calculate the **Priority** field\. When synchronizing from AWS, we set by default the fields shown in the table below: 


| OpsItem Priority  | ServiceNow Incident | 
| --- | --- | 
|  | Impact | Urgency | Priority \(Calculated\) | 
| 1 | High | High |  Critical \(1\) | 
| 2 | Medium |  High | High \(2\) | 
| 3 | Medium | Medium | Moderate \(3\) | 
| 4 | Low  | Medium | Low \(4\) | 
| 5 | Low  | Low  | Planning \(5\) | 

You can find these mappings in a ServiceNow table *Priority Data Lookup*\. While we can use this table to find the required values of **Impact** and **Urgency**, note that you can customize the mappings and also define new priority values\. Additionally, you might want a specific priority in AWS to map to an entirely different priority in an Incident or Problem\. 



## AWS Security Hub Integration Features<a name="hub-integration"></a>

**To view Findings from AWS SecurityHub**

1.  To view AWS Security Hub Findings, you must have the role** x\_126749\_aws\_sc\.finding\_manager** from the Connector scope app\. 

1. Log in to your ServiceNow instance as a user \(for example, System Administrator\) in the fulfiller view \(standard user interface view\)\.

1.  In the navigator, enter **AWS Service Management**\.

1.  Choose **AWS Security Hub**\.

1. Choose **Findings** to show a list of all synced Findings\.

1. Choose a Finding to open the record\.

1. The Incident and Problem fields show the Incident and Problem related to the Finding if these exist\.

1. Choose the ⓘ symbol to the right of the field to preview the Incident or Problem\. 

1. Choose **Open Record** on the preview form to open the Incident or Problem\.

1. If the Connector does not automatically create a ServiceNow Incident or Problem when a new Finding syncs, choose the link at the bottom of the form to create one manually\. 

This table shows how fields map from ServiceNow Findings records to ServiceNow as Incident or Problem records\. 


| Finding | Incident | Problem | 
| --- | --- | --- | 
| Created at | Opened at | Opened at | 
| Company Name | Company | Company | 
| Description | Description | Description | 
| Criticality | Impact | Impact | 
| Severity | Urgency | Urgency | 
| Hardcoded to software | Category | Category | 
| Id of record in cmdb\_ci\_service with name AWS Security Hub | Business service | Business service | 
| Description | Short description | Short description | 
| Reference to related Problem if it exists | problem\_id | n/a | 

This table shows how fields synchronize between AWS Security Findings and ServiceNow Incidents or Problems\.


| AWS Security Hub value | ServiceNow Incident | ServiceNow Problem | 
| --- | --- | --- | 
| Severity Label | Urgency | Urgency | 
| Criticality | Impact | Impact | 

**Fields synchronized between AWS Security Findings, Incidents, and Problems in ServiceNow**
+ Finding severity label → Problem/Incident urgency
  + INFORMATIONAL or LOW → LOW
  + MEDIUM → MEDIUM
  + HIGH or CRITICAL → HIGH
+ Finding criticality → Problem/Incident impact
  + 0 \- 29 → LOW
  + 30 \- 69 → MEDIUM
  + 70 \- 100 → HIGH

**Fields synchronized from Findings to AWS Security Hub**
+ Severity \(Label and Normalized\)
+ WorkflowStatus
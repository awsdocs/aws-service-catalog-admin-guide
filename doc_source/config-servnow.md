# Configuring ServiceNow<a name="config-servnow"></a>

After completing the IAM and AWS Service Catalog configurations, the next configuration area to set up is ServiceNow\. Installation tasks in ServiceNow include:
+ Clear the ServiceNow platform cache\.
+ Clear the web browser cache\.
+ Activate two ServiceNow plugins\.
+ Install the ServiceNow Connector scoped application, and upload and commit the ServiceNow Connector Update Set\.
+ Configure ServiceNow platform system admin components\.
+ Configure AWS Service Management Connector scoped application, including accounts, scheduled jobs sync, and permissions\.
+ Validate connectivity to AWS Regions\.
+ Manually sync scheduled jobs\.
+ Configure the AWS Service Catalog Product Widget Components and Assignment Group for Closed Change Records\.
+ Grant access to AWS Service Catalog portfolios\.
+ Configure AWS Tags for provisioned products\.
+ Configure synchronization of AWS Config data using an Aggregator into ServiceNow CMDB\.
+ Configure available ServiceNow tables to sync with AWS Config\.
+ Configure AWS Security Hub integration\.

## Clearing the ServiceNow platform cache<a name="clear-cache"></a>

Before installing the AWS Service Management scoped app, we recommend you clear the ServiceNow platform cache\. To do so, enter this URL: `https://[InsertServiceNowInstanceNameHere]/cache.do`\.

**Note**  
Ensure that you install the update set in a non\-production or sandbox environment\. Consult a ServiceNow system administrator if you need approval to clear the ServiceNow platform cache\.

## Clearing the web browser cache<a name="clear-browser-cache"></a>

Clear the web browser cache to remove previously rendered product forms\. 

## Activating User Criteria Scoped API and Discovery and Service Mappings Patterns plugins<a name="activate-plugins"></a>

**To activate the User Criteria Scoped API plugin**

1.  From your ServiceNow dashboard, enter **plugins** into the navigation panel in the upper left\. 

1.  When the **System Plugins** page populates, next to the **Name** dropdown, search for **Discovery**\. 

1.  Choose **User Criteria Scoped API** and then choose **Activate**\. 

**To activate the Discovery and Service Mappings Patterns plugin**

1. From your ServiceNow dashboard, enter **plugins** into the navigation panel in the upper left\.

1.  When the **System Plugins** page populates, next to the **Name** dropdown, search for **Discovery**\. 

1.  Choose **Discovery and Service Mapping Patterns** and then choose **Activate**\. 

**Note**  
This plugin is free and aligns to the CMDB tables outside of ServiceNow’s family release CMDB updates\. 

## Installing ServiceNow Connector scoped application<a name="install-snow-connector"></a>

The AWS Service Management Connector for ServiceNow release is a conventional ServiceNow scoped application through a [ServiceNow Update Set](https://servicecatalogconnector.s3.amazonaws.com/AWS_SC_update_set_3.5.2.xml.zip)\. 

ServiceNow update sets are code changes to the out\-of\-the\-box platform and enable developers to move code across ServiceNow instance environments\. The Connector for ServiceNow update set is available to download in the [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/f0b117a3db32320093a7d7a0cf961912/)\. 

We provide the code for [Connector for ServiceNow version 3\.7\.1](https://servicecatalogconnector.s3.amazonaws.com/AWS_SC_update_set_3.7.1.xml.zip) for users who install the update set on a ServiceNow Personal Developer Instance \(PDI\)\.

You can apply the [Connector for ServiceNow version 3\.7\.1](https://servicecatalogconnector.s3.amazonaws.com/AWS_SC_update_set_3.7.1.xml.zip) update set to a “Quebec”, "Paris", or “Orlando" platform release of ServiceNow\. 

If you do not already have a ServiceNow instance, start with the first step below\. If you already have a ServiceNow instance, proceed to the instructions below on how to install the update set\. 

**To obtain a ServiceNow instance**

1. Open [ Obtaining a Personal Developer Instance](https://developer.servicenow.com/dev.do#!/guides/quebec/developer-program/pdi-guide/obtaining-a-pdi)\.

1. Create ServiceNow developer program credentials\.

1. Follow the instructions for requesting a ServiceNow instance\.

1. Capture your instance details, including URL, administrative ID, and temporary password credentials\.

**To install the update set**

1.  From your ServiceNow dashboard, enter **update sets** into the navigation panel in the upper left\. 

1.  Choose **Retrieved Update Sets** from the results\. 

1.  Choose **Import Update Set from XML** and upload the release XML file\. 

1.  Choose the **AWS Service Management Connector for ServiceNow** update set\. 

1.  Choose **Preview Update Set**, which makes ServiceNow validate the connector update set\. 

1.  Choose **Update**\. 

1.  Choose **Commit Update Set** to apply the update set and create the application\. This procedure should complete 100%\. 

## Platform system administrator components<a name="configure-snow-connector"></a>

To enable the AWS Service Management Connector for ServiceNow scoped application named **AWS Service Management**, the system admin must create a discovery source, and configure specific platform tables, forms, and views\.

**Create a discovery source AWS Service Management Connector entry**

To allow AWS to report discovered CIs into your CMDB, you must create a new discovery data source, AWS Service Management Connector\. Perform the following steps:

1.  Choose **System Definition**\. Then select **Choice Lists**\.

1.  Choose **New**\. 

1.  Create a new entry with these details: 
   + **Table:** **Configuration Item \[cmdb\_ci\]**
   + **Element:** **discovery\_source**
   + **Label:** **AWS Service Management Connector**
   + **Value:** **AWS Service Management Connector**

**Note**  
Make sure you are in Global mode in ServiceNow System Settings to modify System Definitions\.

**Enable permissions on ServiceNow Platform table \(Catalog Item Category\)**

For AWS products to display under AWS portfolios as sub\-categories in the ServiceNow Service Catalog, you need to modify the Application Access form for Catalog Item Category tables\. This action is necessary because a ServiceNow scoped API is not available for the Catalog Item Category table\. 

1. Enter **Tables** in the Navigator and choose **System Definition**, then choose **Tables**\.

1. In the list of tables, search for a table with label **Catalog Item Category** \(or with the name `sc_cat_item_category`\)\. The list of tables displays\. Choose **Category** to view the form defining the table\.

1. Choose the **Application Access** tab on the form and choose the **Can Create**, **Can Update**, and **Can Delete** checkboxes on the form\. Then choose **Update**\.

## ServiceNow permissions for administrators of the Connector scoped app<a name="admin-permissions-scoped-app"></a>

The AWS Service Management scoped app has two ServiceNow roles that enable access to configure the application\. This feature enables system admins to grant one or more user's privileges to administer the application, without having to open full sysadmin access to them\. System admins can assign these roles to either individual users or to one administrator user\.

**To set up Connector application administrator privileges**

1. Enter *Users* in the navigator and select **System Security – Users**\. 

1. Choose a user to grant one or both previous roles \(such as admin\)\. You can also [create a user](https://docs.servicenow.com/bundle/newyork-platform-administration/page/administer/users-and-groups/task/t_CreateAUser.html)\. 

1.  Choose **Edit** on the Roles tab of the form\. 

1.  Filter the collection of roles by the prefix **x\_**\. 

1. Choose one or both of the following and add them to the user: ** x\_126749\_aws\_sc\_account\_admin**, **x\_126749\_aws\_sc\_portfolio\_manager**, **x\_126749\_ aws\_sc\.automation\_manager**, **x\_126749\_aws\_sc\.finding\_manager** and **x\_126749\_aws\_sc\.opscenter\_manager**\.

1.  Choose **Save**\. 

**To add AWS Service Catalog to ServiceNow Service Catalog categories**

1.  Choose **Self Service \| Service Catalog** and select the **Add content** icon in the upper right\. 

1. Choose the **AWS Service Catalog Product** entry\. To add it to your catalog home page, choose the first **Add Here** link on the second row of the selection panel at the bottom of the page\. 

**To add AWS Systems Manager automation documents \(runbook\) to ServiceNow Service Catalog categories**

1. Choose **Self Service \| Service Catalog** and select the **Add content** icon in the upper right\.

1. Select the **AWS Systems Manager** entry\. To add it to your catalog home page, choose the first **Add Here** link on the second row of the selection panel at the bottom of the page\.

**Note**  
 This Connector release displays all AWS Systems Manager documents in the AWS account that has AWS Systems Manager selected\. 

System administrators can deactivate AWS Systems Manager documents requests\. To deactivate requests, choose **AWS Systems Manager**, **Automation Documents**, and deselect the **Active** button\. After deactivation of the document, end users no longer see the document in the ServiceNow Service Catalog\. 

The Connector creates closed change requests on post provision actions \(such as update, terminate and self\-service\) for AWS Service Catalog products visible in ServiceNow\. 

To achieve a closed change request from post provisioned actions, add a change request type and configure the `sys_id` for the group assigned to the closed change records in the Connector AWS Service Catalog system properties\.

**To add a change request type**

1. If you are upgrading from a previous version of the AWS Service Management scoped app, you must remove the **AWS Product Termination** change request type before you create a new change request type\. 

1.  You must add a new change request type called **AWS Provisioned Product Event** for the scoped application to trigger an automated change request in Change Management\. For instructions, see [Add a new change request type](https://docs.servicenow.com/bundle/newyork-it-service-management/page/product/change-management/task/t_AddNewChangeType.html)\. 

1. Open an existing change request\. 

1. Open \(right\-click\) the context menu for **Type** and then choose **Show Choice List**\. 

1.  Choose **New** and complete these fields: 
   + **Table**: **Change Request**
   + **Label**: **AWS Provisioned Product Event**
   + **Value**: **AWSProvisionedProductEvent**
   + **Sequence**: pick the next unused value

1. Submit the form\.

**Note**  
For more information on how to associate the Change Assignment group, see *Configuring the AWS Service Catalog Product Widget Components* and *Assignment Group for Closed Change Records*\.

## Configuring AWS Service Management Connector scoped application<a name="configure-sc-connector-scoped-app"></a>

After installing and configuring the AWS Service Management Connector for ServiceNow, you must configure the scoped application and applicable roles\.

**To configure the AWS Service Management Connector scoped application permissions**

1. In your ServiceNow instance, create a user group called **Order\_AWS\_Products**\. Members of this group can order AWS Service Catalog products\. For instructions, see [Create a user group\.](https://docs.servicenow.com/bundle/orlando-platform-administration/page/administer/users-and-groups/task/t_CreateAGroup.html)

1. Grant ServiceNow permissions to these users: 
   + **System Administrator \(admin\)**: For simplicity in this example, user **admin** is the administrator of the AWS Service Management scoped application\. Grant this user both of the administrative permissions from the adapter:** x\_126749\_aws\_sc\_account\_admin,** **x\_126749\_aws\_sc\_portfolio\_manager**, **x\_126749\_ aws\_sc\.automation\_manager**, **x\_126749\_aws\_sc\.finding\_manager **and** x\_126749\_aws\_sc\.opscenter\_manager**\. 

     Add System Administrator to the new ServiceNow group **Order\_AWS\_Products**\. In a real scenario, these roles would likely be granted to different users or groups\. In a real scenario, these roles would likely be granted to different users or groups\.
   + **Abel Tuter**: The user **abel\.tuter** is an illustrative end user\. Grant Abel the new role **Order\_AWS\_Products**\. This permission allows Abel to order products from AWS\.


**ServiceNow Permissions Recap**  
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/servicecatalog/latest/adminguide/config-servnow.html)

## Configuring AWS accounts to synchronize in the Connector<a name="configure-accounts"></a>

1. Log in as the system administrator\. 

1. Enter **AWS** in the navigator\. Choose the **AWS Service Management** scoped app\.

1. In the **AWS Service Management** scoped app Accounts menu, create one entry for every AWS account\. You need to use the keys and secret keys from the users you created in AWS\. 

**To create account entry**

1. Enter the name as an account entry identifier, such as **Connector\_Demo** \(for Commercial Region\), or **Connector\_Demo\_GovCloud** \(for GovCloud Region\)\.

1. Enter the AWS access key and secret access key from the AWS account sync user IAM configurations\.

1. Enter the AWS access key and secret access key from the AWS account end user IAM configurations\. 

1. Select the AWS service integrations that you want visible for this AWS account\. The choices include:
   + Integrate with AWS Service Catalog
   + Integrate with AWS Config 
     + Select AWS Config if you plan to integrate AWS Config cloud resources per each AWS account or through the latest AWS Config Aggregator integration feature\. Version 3\.7\.1 of the Connector for ServiceNow includes an AWS Config aggregator feature that enables ServiceNow administrators to align aggregated AWS Config details into one AWS account\. 
     + If you plan to use the Config Aggregator feature, proceed with configuring the AWS account in this section\. For more information on the Config Aggregator steps, see *Configuring synchronization of AWS Config data using an Aggregator into ServiceNow CMDB*\. 
   + Integrate with AWS Systems Manager Automation\.
   +  Integrate with AWS Systems Manager OpsCenter\.
   + Integrate with AWS Security Hub\.
**Note**  
For the AWS Systems Manager OpsCenter integration, you should select AWS Systems Manager Automation if you want to execute automation documents \(runbook\) to remediate incidents from OpsItems\. 

1. Choose **Account Regions**\. Select the **Commercial** or **GovCloud Region**\. To see the AWS account Regions, double\-click **Insert a new row…**\. 

1. Repeat the step above to insert additional Regions\.

1. Save or update the account entries\.

1. Validate AWS account connectivity by following the steps in *Validating Connectivity to AWS Regions*\. Note that in this Connector for ServiceNow version 3\.7\.1, the **Validate Accounts** button only appears once after you submit or update the account entry\. 

## Validating connectivity to AWS Regions<a name="validate-regions"></a>

You can now validate connectivity to AWS accounts between the ServiceNow **Connector\_Demo** account and the AWS IAM SMSyncUser and SMEndUser\.

**To validate connectivity to AWS account**

1.  In the AWS Service Management scoped app, choose **Setup**, then **AWS Accounts**\. 

1. Choose **Connector\_Demo** and select **Validate Account**\. 

1.  A successful connection results in the message, “Successfully validating AWS account in each referenced Region\.” 

 If the AWS IAM access key or secret access key are incorrect, you will receive an error message\. 

## Manually syncing scheduled jobs<a name="manual-sync-scheduled-jobs"></a>

During the initial setup, manually execute the sync instead of waiting for **Scheduled Jobs** to run\. The default sync schedule is every 31 minutes\.

**To sync the accounts manually**

1.  Log in as system administrator\. 

1.  Find **Scheduled Jobs** in the navigator panel\. 

1.  Search for job **Sync all Accounts**, select it, and choose **Execute Now**\. 
**Note**  
If you do not see **Execute Now** in the upper left corner, choose **Configure Job Definition**\. **Execute Now** will be visible\.

Data is visible in the AWS Service Management scoped app menus after the adapter’s scheduled synchronization job has run\.

## Configuring the AWS Service Catalog product widget components and assignment group for closed change records<a name="configure-sc-widget"></a>

 To address the varying personas of end users requesting AWS products, the Connector for ServiceNow includes a scoped app setting to enable or disable components of the AWS product widget\. By default, all AWS product components are active\. 

**To modify the AWS product view**

1.  In the navigator, enter **System Properties** and select **AWS Service Catalog**\. 
**Note**  
Make sure you are in the AWS Service Management Connector scoped application mode\. 

1.  Deselect any AWS product component such as: 
   +  Enable editing of the AWS Service Catalog product name\. 
   +  Enable selection of launch options for AWS Service Catalog Products\. \(This component is only visible if the AWS product has more than one launch path\.\) 
   +  Enable selection of product versions for AWS Service Catalog\. \(This component is only visible if the AWS product has more than one product version\.\) 
   +  Enable tags for AWS Service Catalog products\. 
   +  Enable plans \(ChangeSet\) creation for product\. \(If set to false the plan section is not visible\.\) 

1.  Choose **Save**\. 

The AWS Service Catalog system properties also include a section that identifies an assignment group\. This group associates with closed change records from post provision actions of products \(such as terminate, update, or self\-service actions\)\. 

**To associate the assignment group for change records from AWS Service Catalog post provision actions**

1. In the navigator, enter **System Properties** and select **AWS Service Catalog**\. Make sure you are in the AWS Service Management Connector scoped application mode\.

1. Choose the section **Set the ‘assignment group’ sys\_id or name that the connector will use when creating change requests**\. 

1. Enter the **Assignment group sys\_id**\.

1. If you need to find the `group sys_id`, enter **System Security** in the left navigator\.

1. Select **Groups** module\.

1. Search for the **Group** name\.

1. Choose the group that you want to associate to close changed records and select **Copy sys\_id**\. You are now able to paste the copied `sys_id` into the AWS Service Catalog System Properties for the Connector under **Set the ‘assignment group’ sys\_id or name that the connector will use when creating change requests**\.

   If the `sys_id` is left blank, the change record sends a message that no assignment group exists for the record, which causes change requests created from the Connector to be in an open state\. 

## Granting access to AWS Service Catalog portfolios<a name="grant-access-portfolios"></a>

This release of the Connector does not require you to link AWS identities to ServiceNow roles\. To grant access to AWS Service Catalog products in ServiceNow, you must establish a link between the AWS Service Catalog portfolios and the ServiceNow group \(for example, **Order\_AWS\_Products** from an earlier installation example\)\.

**To grant access to AWS Service Catalog portfolios in ServiceNow**

1.  In the AWS Service Management scoped app, choose **AWS Service Catalog**, then **Portfolios** module\. 

1.  Select the desired Portfolio ARN\. You can double\-click the AWS Service Catalog portfolio name\. 

1. Select the **Allowed Groups** tab\.

1.  Choose **New** and enter the **Group** named **Order\_AWS\_Products**\. 

1.  Choose **Submit**\. 

## Configuring AWS Tags for provisioned products<a name="configure-aws-tags"></a>

The AWS Service Management Connector v3\.7\.1 enables ServiceNow administrators to add tags \(metadata\) to provisioned products globally across the scoped app or granularly at the portfolio level\. These tags are not visible to end users\. 

Three tag types are available in this release:
+ Generic tags in which the administrator can enter the key and value\.
+ ServiceNow Request Item tags in which the admin can enter the syntax for key and value in the table below\. 
+ ServiceNow table\(s\) values that end users can select as tags for provisioned AWS resources\. This release now enables administrators to identify any ServiceNow tables, such as Cost center or Department, and makes values from that table selectable for end users\. 
**Note**  
Generic tags \(from administrators\) and ServiceNow Request Item tags are not viewable by end users\.     
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/servicecatalog/latest/adminguide/config-servnow.html)

**To add generic AWS tags to AWS Service Catalog provisioned products in ServiceNow**

1.  In the AWS Service Management scoped app, choose **Setup**, then the **Automated Tags** module\. 

1.  Choose **New**\. 

1.  For Global tags, enter the Key and Value entries and choose **Submit**\. 

1.  For Portfolio tags, deselect **Global check**\. The **Portfolio** field appears\. 

   Select the AWS Service Catalog portfolio, enter the Key and Value entries, and choose **Submit**\. 

**To add in\-scope ServiceNow request item AWS tags to AWS Service Catalog provisioned products derived from ServiceNow**

1.  In the AWS Service Management scoped app, choose **Setup**, then the **Automated Tags** module\. 

1.  Choose **New**\. 

1.  For Global tags, enter the specific Key and Value entries for either User or Request Item Number, and choose **Submit**\. 

1.  For Portfolio tags, deselect **Global check**\. The Portfolio field appears\. Select the AWS Service Catalog portfolio, enter the Key and Value entries, and choose **Submit**\. 

**To add tags to AWS provisioned products from ServiceNow tables and fields that are selectable by end users**

1. In the AWS Service Management scoped app, choose **Setup**, then the **Automated Tags** module\. 

1. Choose **New**\. 

1. Choose **Selectable by End User**\. 

1. Choose a table from the dropdown list **Table Name**\. 

1. Choose a field from the dropdown list **Table Field**\. 

1. For Global tags, enter the Key and Value entries and choose **Submit**\. 

1. For Portfolio tags, deselect **Global check**\. The **Portfolio** field appears\. 

   Select the AWS Service Catalog portfolio, enter the Key and Value entries, and choose **Submit**\. 

   The ServiceNow Table and field value appear on the AWS Product \(ServiceNow catalog item\)\. It is a required value prior to ordering\. After product provisioning, you can see in the AWS console that these tags associate with the resource\.

### Configuring AWS Security Hub integration<a name="tbd"></a>

**To configure AWS SecurityHub synchronization behavior to the Connector in ServiceNow**

1. In the navigator, enter **AWS Service Management**\.

1. Select **System Properties**, then **AWS Security Hub**\.

1. Set these configuration items:
   + Select the types of AWS Security Hub Findings to sync in ServiceNow: CRITICAL, HIGH, MEDIUM, LOW, and INFORMATIONAL\.
   + Select an action for a newly synced Finding to the Connector in ServiceNow:
     + **Do Nothing**\. This action only imports Security Finding types for the scoped app\. Users with scoped app permissions can view and choose to create incident or problem\. **Do Nothing** is the default value in the Connector\.
     + **Create Incident**\. This action automatically creates incidents from Security Findings and syncs updates in ServiceNow to AWS Security Hub\. 
     + **Create Problem**\. This action automatically creates incidents from Security Findings and syncs updates in ServiceNow to AWS Security Hub\.
     + **Create Incident and Problem**\. This action automatically creates incidents and problems from Security Findings and syncs updates in ServiceNow to AWS Security Hub\.
   + Adjust the maximum number of messages to fetch from the SQS queue per sync, account, or Region \(default 50\)\. By default, the sync process runs every five minutes\.
   + Change the SQS Queue name if you’re not using the default that the Connector created\. The CloudFormation template supplies the Connector\.
**Note**  
We recommend you not change the SQS name in the ServiceNow scoped app \(`AwsServiceManagementConnectorForSecurityHubQueue`\) unless you change the SQS name in the AWS account\. 

1. Select **Save** after any changes\.

   **Fields synchronized from AWS Security Hub Findings to the ServiceNow scoped app AWS Security Hub Findings module in ServiceNow**


|  |  | 
| --- |--- |
| Region | The Region in which the Finding was generated\. | 
| Account Id | The account in which the Finding was generated\. | 
| Company Name | The company which generated the finding \(e\.g\. AWS\)\. | 
| Compliance | Whether a resource passes the configured compliance criteria\. Contains status \(PASSED, WARNING, FAILED, NOT\_AVAILABLE\) and if the resource does not pass will contain some information regarding the reason for this\. | 
| Created At | The creation time of the Finding\. | 
| Description | A description of the Finding\. | 
| Criticality | The level of importance for the resource associated with the Finding\. | 
| First Observed At | First observation of when Findings captured any potential security issues\. | 
| Last Observed at | The most recent time Findings captured any potential security issues\.  | 
| Product Name | The name of the product that generates the Finding \(such as Security Hub\)\. | 
| Product Arn | The ARN of the product that generates the Finding\. | 
| Record State | Either ACTIVE or ARCHIVED\. | 
| Severity \(normalized\) | A value from 0 to 100 that indicates the severity of the problem associated with the Finding\.  | 
| Status | PASSED, WARNING, FAILED, or NOT AVAILABLE\. | 
| Title | The title of the Finding\. | 
| Updated At | When the Finding provider last updated the record\. | 
| Workflow Status | The workflow status can be: NEW, ASSIGNED, IN PROGRESS, RESOLVED, DEFERRED, or DUPLICATE\.  | 
| Remediation Text | A description of suggested action to resolve the discovered issue\.  | 
| Remediation Url | A link to a resource that can resolve the discovered issue\.  | 

## Adding the My AWS Products widget to the Service Portal view<a name="add-aws-product-widget"></a>

 We recommend ServiceNow administrators add the **My AWS Products** widget to the ServiceNow Portal view\. The widget enables users to view their AWS product requests, view outputs, and perform post\-operational actions such as update, terminate, and service actions \(AWS Systems Manager documents\)\. 

**To include the My AWS Products widget on the Service Portal view**

1.  Log in as system administrator in the ServiceNow standard user interface \(Fulfiller view\)\. 

1.  In the navigator panel, find **Service Portal**\. 

1.  Choose **Service Portal Configuration**\. 

1. Choose **Designer**\. 

1. Search for **Service Portal** in the filter\. 

1.  Select the** Service Portal** box with a house image and the word **Index** in the lower right corner\. 

1.  In the left panel in **Widgets**, enter **My AWS Products** in the Filter Widget\. 

1.  Drag the widget to the Service Portal edit view to your desired location\. 

1.  Preview your changes\. 

## Viewing budgets related to AWS Service Catalog portfolios and products<a name="view-budgets"></a>

ServiceNow administrators can view budgets and actual costs related to AWS Service Catalog portfolios and products in the ServiceNow standard user interface\.

**To view portfolio budgets**

1.  Log in as system administrator\. 

1.  In the navigator panel, search for **AWS Service Catalog**\. 

1.  Select the **Portfolios** module\. 

1.  Select the AWS Service Catalog portfolio that contains an associated budget\. 

1.  Choose the **Budget** tab\. 

**To view product budgets**

1.  Log in as system administrator\. 

1.  In the navigator panel, search for **AWS Service Catalog**\. 

1.  Select the **Products** module\. 

1.  Select the AWS Service Catalog product that contains an associated budget\. 

1.  Choose the **Budget** tab\. 

## Syncing updated keys programmatically in ServiceNow<a name="sync-keys"></a>

AWS Service Management Connector for ServiceNow allows synchronization of updated keys by any automation or integration, through a new REST endpoint\. 

You can send requests to sync updated keys for one or more AWS accounts registered in the AWS Service Management Connector, for either the sync or end user\.

For more information about syncing updated keys syntax and instructions, see [Syncing Updated Keys Programmatically in ServiceNow](https://servicecatalogconnector.s3.amazonaws.com/AWS+Service+Management+Connector+for+ServiceNow_3.5.1+-+Syncing+Updated+Keys.pdf)\. 
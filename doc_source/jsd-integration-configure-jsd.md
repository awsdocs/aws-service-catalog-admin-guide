# Configuring Jira Service Management<a name="jsd-integration-configure-jsd"></a>

The AWS Service Management Connector for Jira Service Management is a conventional Jira Service Management add\-on\. Add\-ons are code changes to the Jira software that extend its functionality or extend the functionality of Jira Service Management software\. The Connector for Jira Service Management add\-on is available to download in the [Atlassian Marketplace](https://marketplace.atlassian.com/apps/1221283/aws-service-catalog-connector-for-jsd)\. 

 After completing the IAM and AWS Service Catalog configurations, you must configure Jira Service Management\. Installation tasks within Jira Service Management include: 
+ Clear your web browser cache\.
+ Install the Jira Service Management Connector add\-on\. 
+ Configure AWS Service Management Connector add\-on, including accounts, schedule sync, request and approval permissions, and core operational settings\. 
**Note**  
You'll need to select a dedicated administrator on the Connector settings page to perform operations on Jira tickets, such as status transitions or comments\. If you don't select a dedicated administrator, we list the first administrator in the dropdown by default\. For more details, see the **Core Operation Settings** under the **Configuring Connector Settings** sub\-section\.

## Clear Web Browser Cache<a name="jsd-clear-cache"></a>

 Clear your web browser cache to remove previously rendered Jira Service Management forms\. 

## Installing Jira Service Management Connector Add\-on<a name="install-jsd-connector"></a>

1. Log in to your Jira instance as an admin\.

1.  Open the admin menu and choose **Add\-ons**\. 

1.  On the **Manage add\-ons** screen, choose **Find new apps** or **Find new add\-ons** from the left side of the page\. 

1.  Find **AWS Service Management Connector for JSM**\. The search results should include app versions compatible with your Jira instance\. 

1.  Choose **Install** to download and install your app\. 

1.  Proceed to **Configuring AWS Accounts and Regions**\. 

 Alternatively, you can download the code from the OBR file: [AWS Service Management Connector for Jira Service Management v1\.8\.2 OBR](https://servicecatalogconnector.s3.amazonaws.com/jira-servicedesk-connector-1.8.2-20210524-1403.obr)\. 

1.  Go to **Manage apps**\. 

1.  Select **Upload app** and upload the OBR file\. 

1.  Proceed to **Configuring AWS Accounts and Regions**\. 

You can apply the Connector for Jira Service Management version 1\.8\.2 add\-on to the supported Jira software \(Jira Service Management\) releases noted above\.

## Configuring AWS Accounts and Regions<a name="jsd-configure-accounts-regions"></a>

 Once you install the AWS Service Management Connector, you need to configure it\. To do so, choose the Jira administration icon in the top right, then choose **Add\-ons**\. 

1.  From the AWS Service Catalog section on the left navigation menu, choose **AWS Accounts**\. 

1. Choose **Connect new account**\.

1. Enter the account alias \(used to identify the AWS account in the Connector\)\.

1. Enter the credentials for SC\-sync\-user\. It is the access key identity and credentials for a sync user saved from the AWS configuration\. SC\-sync\-user credentials can retrieve portfolios and products to make them available through Jira Service Management\. You can set the allowed groups that can access them\.

1. Enter the credentials for SC\-end\-user\. It is the access key identity and credentials for the end user saved from the AWS configuration\. The SC\-end\-user credentials provision products on behalf of a Jira user\.

1. Add **AWS Regions**\. It contains AWS Service Catalog products and portfolios you want available in Jira Service Management\.

1. Choose **Test Connectivity**\.

1. Upon successful connection status, choose **Connect**\.

**Note**  
 We recommend the sync user and end user be new users in AWS, used only with AWS Service Management Connectors\. These users should have minimum required priviledges\. An AWS CloudFormation template with the minimal permissions for AWS Service Management Connectors is available\. 

## Configuring AWS Service Catalog portfolios in Jira<a name="jsd-configure-sc-portfolios"></a>

### AWS Product Access<a name="jsd-aws-product-access"></a>

This section describes how to configure AWS Service Catalog portfolios within Jira\. 

 Once your account or accounts are set up and connectivity is successful, use the **AWS Account** page to manage, for each account, which groups can access each portfolio in each Region\. You can expand and collapse each Region and edit and add groups for each portfolio\. Only users in the designated groups have access to those products\. By default, no groups have access\. 

**Note**  
At least one group must be associated to an AWS Service Catalog portfolio for Jira Service Management end users to request AWS products\.

**To provision products and portfolios**

1. Choose **AWS Accounts**\.

1. Choose **Manage** for the AWS account in which you want to configure portfolios\.

1. Under **Portfolios**, expand the Region associated with the account\. Portfolios display under each Region\. 

1. In the **Permission to request** column, choose **Add groups** for the portfolios that you want to make visible in Jira Service Management\. Select the group you want to see and request AWS Service Catalog products\.
**Note**  
Because the AWS Service Management Connector for Jira Service Management allows Jira users to provision AWS products in the portfolios their groups have access to, and to control those provisioned products, users should maintain security in their Jira accounts\.

1.  If products in this portfolio do not require approvals, choose **Save**\. 

### Jira Service Management Approvals for Products in AWS Service Catalog Portfolios<a name="jsd-product-approvals"></a>

 The AWS Service Management Connector for Jira Service Management enables administrators to configure approvals for products at the portfolio level\. All products in a portfolio that contain approval permissions require approval, so AWS and Jira administrators might need to collaborate on the AWS Service Catalog portfolio structure\. 

**To configure the approval process**

1. Choose **AWS Accounts**\.

1. Choose **Manage** on the AWS account for which you want to configure portfolio approvals\.

1. In the **Permission to approve** column, choose **Add groups** for the portfolios that require product approvals\.

1. Select **Require approval for provisioning**\.

1. Under **Permission to approve**, choose **Add group**\.

1. Choose **Save**\.

**Note**  
If a portfolio only has a group associated with **Permissions to request**, products in the portfolio immediately provision when you submit the product request\. 

### Viewing Products and Budgets<a name="jsd-view-budgets"></a>

For reference, two other tabs in the **Admin \-> AWS Accounts \-> Manage** section let you view information on portfolios\. 

The **Available Products** tab lists the products in the portfolio and budgetary information on each\. The **Budgets** tab gives overall budgetary information on the portfolio\. 

**Note**  
Find details about additional configurations for the AWS Service Catalog request form and Automated Tags in the next section Configuring Connector Settings\.

### Configuring Connector Settings \(Jira Project Enablement and Request Type\)<a name="jsd-configure-connector"></a>

 In addition to configuring AWS accounts, the AWS Service Management Connector contains AWS services and UI settings \(AWS Service Catalog\) that enable projects and configure AWS Systems Manager OpsCenter\. 

**Note**  
There are no per\-account settings for AWS Config and AWS Systems Manager Automation through the JSM Connector\.

#### Connector features enabled by default<a name="connector-features-default"></a>

**To configure the default Connector features for specific AWS services**

For a new installation of Connector, we enable the default project configuration for all Connector features \(AWS Service Catalog, AWS Config, AWS Systems Manager Automation, AWS Systems Manager OpsCenter, and AWS Security Hub\)\. If you are upgrading an existing installation, for security reasons, we do not intially enable new features\.
**Note**  
If you are using the AWS Security Hub integration, we recommend you also turn on AWS Config\. If you use the AWS Config integration with JSM, this might add additional resource details in JSM issues created for AWS Security Hub findings\. For example, if the original finding has limited resource details, the Config resource enrichment provides fuller information\. Also, if the resource no longer exists, the Config enrichment provides information about the resource status\. If the resource details changed since the creation of the finding, the Config enrichment provides the latest details, but it does not overwrite the original details\. 

1. In the left navigation menu, under **AWS Service Management**, select **Connector settings\.**

1. At the top, under **Connector features enabled by default**, select each feature depending whether you want projects using the default configuration to be able to use them or not\.

1. Choose **Save**\.

#### UI Settings \(AWS Service Catalog\)<a name="settings-service-catalog"></a>

Configure the AWS Service Catalog product widget components to make them viewable to end users\.

To address the varying personas of end users requesting AWS products, the Connector for Jira Service Management includes an add\-on app setting to enable or disable components of the AWS product widget\. By default, we enable AWS product components\.

**To modify the AWS product view**

1. In the left navigation menu, under **AWS Service Management**, choose **AWS Connector settings**\. 

1. In the **UI settings** \(Service Catalog\) section, deselect any AWS product component such as:

   1. Allow the product name to be edited\. \(If unchecked, we provide an autogenerated name the user cannot edit\.\)

   1. Allow the user to select a launch option\. \(If unchecked, we select the default launch option and hide it\.\)

   1. Allow the user to select a product version\. \(If unchecked, we select the default product version and hide it\.\)

   1. Allow the user to add or edit tags\. \(If unchecked, we select the default values for tag options and hide it\.\)

   1. Allow user to create a plan for creation or update of a provisioned product\. \(If unchecked, we hide the plans section\.\)

1. Choose **Save**\.

#### Projects enabled for the Connector<a name="projects-connector"></a>

The AWS Service Management Connector for Jira Service Management requires the add\-on to be associated to one or more Jira projects and for JSM request types\. You can configure which Connector features are enabled for each Jira project\.

**To configure the Jira projects for AWS Service Catalog, AWS Config, AWS Systems Manager Automation, AWS Systems Manager OpsCenter, and AWS Security Hub**

1. In the left navigation menu, under **AWS Service Management Connector**, choose **Connector settings**\.

1. Under **Projects enabled for Connector**, you must enable at least one Jira project\. You can [create a new Jira Service Management project](https://confluence.atlassian.com/servicedeskserver043/setting-up-your-service-desk-974367545.html) or add an existing one\. Only users with access to the associated project can access the Connector\. When you apply this update, the Connector adds the necessary issue types and other Jira items for AWS Service Catalog products to be available in those projects\. You can return to this screen and add or remove projects at any time\. 

1. Projects initially take the default configuration for which Connector features are enabled\. Choose **Edit** in a project row to change the configuration for individual projects\. We permit projects to use more features than the default\.

1. Choose **Save\.**
**Note**  
For end\-users to be able to request AWS Service Catalog products, one or more projects must be enabled and users must have Jira permissions to create issues in the Jira project and Permission to Request in the Jira settings for the AWS Account for at least one portfolio with products\. 

   **AWS Systems Manager Automation enablement considerations**

    We currently do not support fine\-grained permissions in Jira for which users and groups should be allowed to access which AWS Systems Manager automation documents\. If you enable a project for Systems Manager Automation, then any user with permission to create issues in that project can run any of the automations\. You can restrict access by limiting which users have access to projects with AWS Systems Manager Automation enabled\.

#### AWS Systems Manager OpsCenter Configuration<a name="tbd"></a>

Once you've enabled projects for the Connector, AWS Systems Manager OpsCenter requires Jira admins to associate Jira project\(s\) to this integration, as well as determine the full sync and delta sync intervals\.

**To associate the Jira projects enabled for the Connector to the AWS Systems Manager OpsCenter integration features**

1. In the left navigation menu, under **AWS Service Management Connector**, choose **Connector settings**\. 

1. Create a [new Jira Service Management Project](https://confluence.atlassian.com/servicedeskserver043/setting-up-your-service-desk-974367545.html)\. Under **OpsCenter Configuration**, you must enable at least one Jira project\. You can create a [new Jira Service Management project](https://confluence.atlassian.com/servicedeskserver043/setting-up-your-service-desk-974367545.html) or add an existing one\. Only users with access to the associated project can access the Connector\. When you apply this update, the Connector adds the necessary issue type to associated project\(s\)\. You can return to this screen and add or remove projects at any time\. 

1. Under **AWS Systems Manager OpsCenter Configuration**, in the **Full Sync Interval** and **Delta Sync Interval** fields, you can change the sync interval if you want\. The **Full Sync** and** Delta** interval determines how often Jira Service Management conducts syncs all or changes to OpsItems details with AWS Systems Manager OpsCenter respectively\. Increasing this number reduces the number of API calls to AWS, but increases the time for OpsItems updates to reflect in the Connector\. 

1. Choose **Save**\.

#### Core Operational Settings<a name="core-ops-settings"></a>

**To configure operational settings for the AWS Service Management Connector for Jira Service Management**

1. In the left navigation menu, under **AWS Service Management Connector**, choose **Connector settings**\. 

1. Under **Core operational settings**, in the **Synchronization interval** field, you can change the sync interval if you want\. This interval determines how often Jira Service Management syncs with AWS\. Increasing this number reduces the number of API calls to AWS, but increases the time for updates in AWS portfolios and automation documents to reflect in the Connector\. Information on actively provisioning products and ongoing automation executions updates are more frequent\. 

1. Under **Core operational settings**, in the **JIRA Administrator to run as** field, you can change the admin user assigned to perform automated operations within JIRA\. 
**Important**  
The Connector performs many actions within Jira, and needs to do those actions as a Jira user\. By default, Connector choosees the Jira Admin user with the lowest ID, which works for many environments\.

   However, that approach might be the wrong strategy if the initial admin user has been disabled, or if there is a different admin user\. For clarity within the Connector, it can be a good idea to create a new user called, for example, "AWS Connector Admin", and select that as the default user\.

   We record actions performed automatically by the Connector as being performed by this user, such as synchronizing OpsItems from AWS or adding a comment for changes to an AWS provisioned product\. These actions do not affect actions that end users perform, such as requesting a provisioned product or manually creating an OpsItem in Jira, which we record as the end user performing the action\.

   This user should have global admin permissions, JSM permissions, and admin access to each of the AWS\-enabled projects\.

1. Choose **Save**\.

**Note**  
We recommend no changes to entities that the plugin created, such as the addition of fields, workflows, issue types, screens, and so on\.

#### Configuring Automated Tags \(AWS Service Catalog\)<a name="auto-tags"></a>

The AWS Service Management Connector v1\.8\.2 enables Jira administrators to add tags \(metadata\) to AWS Service Catalog provisioned products globally across the add\-on or granularly at the portfolio level\. These tags are not visible to end users\. 

Two tag types are available in this release:
+ Generic tags in which the admin can enter the key and value\.
+ AWS Service Catalog Request Type tags in which the admin can enter the following syntax for key and value:


**AWS Service Catalog Request Type tags**  

|  |  | 
| --- |--- |
| Key | Value | 
| Project Code | $\{PROJECT\_CODE\} | 
| Project Name | $\{PROJECT\_NAME\} | 
| Project Name | $\{ISSUE\_ID\} | 
| Username | $\{USERNAME\} | 
| Opened By | $\{OPENED\_BY\} | 

**To add generic AWS tags to AWS Service Catalog provisioned products in Jira Service Management**

1. In the left navigation menu, under **AWS Service Management**, select **Automated Tags**\.

1. For Global level tags, enter the Key and Value entries\. Under **Portfolio**, select** Global** \(set by default\)\. Choose the **\+** icon to insert\.

1. For Portfolio level tags, enter the Key and Value entries\. Under **Portfolio**, select the Portfolio dropdown to choose the portfolio associated to associate tag\. Choose the **\+ **icon to insert\. 

**To add in\-scope request type AWS tags to AWS Service Catalog provisioned products derived from Jira Service Management**

1. In the left navigation menu, under **AWS Service Management**, choose **Automated Tags**\.

1. For Global level tags, enter the Key and Value entries\. Under **Portfolio**, select** Global** \(set by default\)\. Select the **\+** icon to insert\.

1. For Portfolio level tags, enter the Key and Value entries\. Under **Portfolio**, select the Portfolio dropdown to choose the portfolio associated to associate tag\. Choose the **\+** icon to insert\. 

   After the product provisions, you can see in the AWS console that these tags are associated to the resource\.

#### Configuring Project Request Type Groups<a name="jsd-configure-request-type"></a>

 The AWS request type must be in a group for users to be able to access it in Jira Service Management\. Enabling Jira projects, as described in [Configuring Connector Settings \(Jira Project Enablement and Request Type\)](#jsd-configure-connector), makes AWS product request types available, but Jira Service Management users won't see the request type until you add it to a **Request Type Group**\. 

**To configure request types**

1. In the AWS Service Management Connector for Jira Service Management , go to the **Connector settings ** page\.

1. In the **Projects** section, choose **add the AWS request type**\.

1. Choose **Add existing request type** in the upper right\-hand corner\.

1. Choose **Request AWS product** from the available request type\.

1. Choose **Edit Groups** for the **Request AWS product** request type\.

1. On the **Edit groups** form, choose **General**, then choose **Save**\.

**Note**  
 When you create a custom **Request AWS Product** request type for the Connector for Jira Service Management, you do not need to edit to the **Request AWS Product** request type\. You can add a request type to an existing group\. If you don't have a group, create a new group and add the request type to it\.
# Validating Configurations<a name="jsd-validate-configurations"></a>

 You can validate the AWS Service Management Connector for Jira Service Management installation procedures\. 

## AWS Service Catalog<a name="validate-sc"></a>

**To order an AWS Service Catalog product**

1. Log in to your Jira Service Management customer portal as the end user\. 

1. In the Jira Service Management customer portal, choose **Request AWS product**\.

1. Enter **Summary** details\.

1. Open the **AWS product request detail** menu and select a product to provision\.

1. Fill in the product request details, including product reference name, parameters, and tags\.

1.  Choose **Create** to submit the Jira Service Management request and provision the AWS Service Catalog product\. 

1. After the request processes, a message appears indicating that your request was created\. When the product is ready to provision, the end user receives a notification that the product is launching\.

**To view provisioned products**

1. In the Jira Service Management customer portal, choose **Requests** in the upper right corner\.

1. Choose **My Requests** in the Jira Service Management customer portal view\.

1. Choose the AWS product you requested\.

1. The AWS product details display, including the status of the product request, product events, and activities\. 

1. If that Connector feature is available, AWS Config information appears\. You can expand **Configuration Items** or **Relationships** to see more information\. Related resources can be loaded by continuing to expand them underneath the** Relationships** section\.

1. Once the product is in the **Available** status, end users can request post\-provision operations actions such as **Request update**, **Request termination**, and **Request self\-service actions**\. These actions render additional product events and activities within the request\. Once the product terminates, the request closes in a resolved state\. 

## AWS Systems Manager Automation<a name="jsd-sys-automation"></a>

**To execute an automation document**

1.  Log in to your Jira Service Management customer portal as the end user\. 

1.  In the Jira Service Management customer portal, choose **Request AWS automation**\. 

1.  Enter **Summary** details\. 

1.  Open the **AWS automation request detail** menu and choose an automation document to execute\. 

1.  Enter the automation request details, parameters, and tags\. 

1.  Choose **Create** to submit the Jira Service Management request and execute the AWS Systems Manager Automation Document\. 

1.  After the request processes, a message indicates the completetion of the request\. As the automation executes, the end user receives a notification of progress\. 

**To view automation executions**

1.  In the Jira Service Management customer portal, choose **Requests** in the upper right corner\. 

1.  Choose **My Requests** in the Jira Service Management customer portal view\. 

1.  Choose the AWS automation execution you requested\. The AWS automation execution details displays and includes the status of the execution, request details, and steps\. 

## AWS Systems Manager OpsCenter<a name="opscenter"></a>

**To view OpsItems in Jira Service Management from AWS Systems Manager**

1.  Log in to your **Jira Agent** view as an end user\. 

1.  In the **Jira Service Management Jira Agent** view, choose the Jira project associated to OpsCenter 

1.  Choose **Open Issues** and select the **OpsItem **from AWS that you want to view\. 

**To create AWS Systems Manager OpsItems in Jira Service Management**

1.  Log in to your **Jira Agent** view as an end user\. 

1.  In the **Jira Service Management Jira Agent** view, choose **Create**\. 

1.  In the **Create Issue** field input the following details: 
   + Project: Auto\-populated\. 
   + Issue Type: Choose **AWS OpsItem **if you have multiple issue types\.
   + Summary: Input Summary Details\.
   + Description: Input Description\.
   + Priority: Choose the appropriate Priority \(default value is Low\)\.
   + Severity: Choose the appropriate Severity \(required for AWS OpsItem\)\.
   + Category: Choose the appropriate Category \(required for AWS OpsItem\)\.
   + Region: Choose the appropriate AWS Region \(required for AWS OpsItem\)\.

1.  Choose **Create**\. 
**Note**  
The newly created OpsItem from Jira Service Management displays in the AWS account view of OpsItem on the next sync between AWS and Jira Service Management\. 

**To update AWS Systems Manager OpsItems in Jira Service Management**

1.  Log in to your** Jira Agent** view as an end user\. 

1. In the **Jira Service Management Jira Agent** view, choose the Jira project associated to OpsCenter\. 

1. Choose **Open Issues** and select the **OpsItem** from AWS that you want to update\. 

1.  Choose **Edit Issue**\. 

1.  Update fields available such as Summary, Description, Priority, Severity, Category\. The **Resolved **button in the OpsItem issue is also available to select upon resolution\.
**Note**  
Updates to OpsItem fields from Jira Service Management displays in the AWS account view of OpsItem on the next sync between AWS and Jira Service Management\.

**To view AWS related resources in AWS Systems Manager OpsItems through Jira Service Management**

1.  Log in to your **Jira Agent** view as an end user\. 

1. In the **Jira Service Management Jira Agent** view, choose the Jira project associated to OpsCenter\. 

1. Choose **Open Issues** and select the **OpsItem** from the OpsItem from AWS\. 

1. Choose the AWS related resource section of the OpsItem selected\. This section displays the related resource details\. 

**To execute runbooks on AWS Systems Manager OpsItems through Jira Service Management**

1.  Log in to your **Jira Agent** view as an end user\. 

1. In the **Jira Service Management Jira Agent** view, choose the Jira project associated to OpsCenter\. 

1.  Choose **Open Issues** and select the **OpsItem**\. 

1. Choose the OpsItem section of AWS Runbooks\. The OpsItem that contains the associated runbooks display a list of automation documents available\. \(See them next to the star shaped symbol\.\) 
   + Choose **Execute** on the desired runbook\. An **Execute Runbook from OpsItem** screen displays\.
   + Enter the workflow parameter details associated to the runbook\. The runbook will not execute successfully without the correct parameter inputs\.
   + Enter metadata tags details if applicable\.
   + **Select Create**\. An **Execute AWS Systems Manager Automation Request** issue generates and provides the execution status\.

   OpsItems without associated runbooks are still able to run automated documents\.

**To run automated documents not associated with runbooks**

1.  In the OpsItem, choose **Show All Runbooks**\. A list on AWS runbooks display\. 

1. To narrow the list of runbooks available, enter details into the search bar above the first listed runbook\.

1.  Choose **Execute** on the desired runbook\. An **Execute Runbook from OpsItem** screen displays\.

1. Enter the workflow parameter details associated to the runbook\. The runbook will not execute successfully without the correct parameter inputs\. 

1. Enter metadata tags details if applicable\. 

1. Choose **Create**\. An **Execute AWS Systems Manager Automation Request** issue displays and provides the execution status\. 
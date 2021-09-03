# Managing AWS Security Hub settings in JSM Integration<a name="security-hub"></a>

This section describes how to view AWS Security Hub Findings, update AWS Systems Manager OpsItems, and view AWS related resources in AWS Systems Manager OpsItems in Jira Service Management\.

**To view AWS Security Hub Findings in Jira Service Management from AWS Systems Manager**

1. Log in to your **Jira Agent **view as an end user\. 

1. In the **Jira Service Management Jira Agent** view, choose the Jira project associated to the AWS Security Hub Finding\.

1. Choose **Open Issues** and select the **AWS Security Hub Finding** from AWS that you want to view\.

**To update AWS Security Hub Finding in Jira Service Management**

1. Log in to your **Jira Agent** view as an end user\. 

1. In the **Jira Service Management Jira Agent** view, choose the Jira project associated to AWS Security Hub Finding\.

1. Choose **Open Issues** and select the AWS Security Hub Finding from AWS that you want to update\.

1. Choose **Edit Issue**\.

1. Update the fields available, such as **Severity**, **Priority**, and **Criticality**\. 

1. Choose **Update** to save the details\.

**Note**  
Updates to Security Hub Finding fields from Jira Service Management displays in the AWS account view of Findings on the next sync between AWS and Jira Service Management\. Only the fields Severity, Priority, and Criticality update in the AWS account from Jira Service Management\. 

**To view AWS related resources in AWS Security Hub Findings through Jira Service Management**

1. Log in to your **Jira Agent** view as an end user\. 

1. In the **Jira Service Management Jira Agent** view, choose the Jira project associated to AWS Security Hub Finding\.

1. Choose **Open Issues** and select the AWS Security Hub Finding\.

1. In the selected AWS resources section of the AWS Security Hub Finding, you see the related resource details\. If the resources relate and the AWS Config integration is active in the Connector, you can drill down on the Config resource details and relationships\. The section remains empty if AWS resources do not relate in AWS Security Hub\. 
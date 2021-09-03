# AWS Security Hub Configuration<a name="secure-hub-config"></a>

After you enable projects for the Connector, AWS Security Hub requires Jira admins to associate Jira projects to this integration, as well as determine the sync interval for polling the SQS queue\. 

**To associate the Jira projects enabled for the Connector to the AWS Systems Manager OpsCenter integration features**

1. In the left navigation menu, under **AWS Service Management Connector**, choose **Connector settings**\. 

1. In **AWS Security Hub Configuration**, you must enable at least one Jira project\. You can create a new Jira Service Management project or add an existing one\. Only users with access to the associated project can access the Connector\. When you apply the update, the Connector adds the necessary issue type to the associated projects\. You can return to this screen and add or remove projects at any time\. 
   + In **AWS Security Hub Configuration**, we set the **SQS Queue Name** to to **AwsSmcJsmSecurityHubQueue** as default\. We recommend this setting as the default\. If you change the SQS queue name, you must access the AWS Console and change the name in AWS too\. 
   + We set **AWS Security Hub Configuration**, the **Sync Interval**, and **Number of messages to pull from SQS** with default values\. You can change these settings\. 

1. In **AWS Security Hub Configuration**, the **Synchronize AWS Security Hub Findings according to their Severity value** section allows Jira admins to filter which Security Hub Findings are visible with Jira Service Management\. The available Severity levels are **Critical**, **High**, **Medium**, **Low**, and **Informational**\. Two Severity values, Critical and High, are set as default\. 

   To add or remove **Findings available for Jira users to view**, deselect the severity and save the change to apply it\. 
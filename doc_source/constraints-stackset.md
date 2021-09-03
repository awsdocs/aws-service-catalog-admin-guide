# AWS Service Catalog Stack Set Constraints<a name="constraints-stackset"></a>

**Note**  
 AutoTags are not currently supported with AWS CloudFormation StackSets\. 

A stack set constraint allows you to configure product deployment options using AWS CloudFormation StackSets\. You can specify multiple accounts and regions for the product launch\. End users can manage those accounts and determine where products deploy and the order of deployment\.

**To apply a stack set constraint to a product**

1. Open the AWS Service Catalog console at [https://console\.aws\.amazon\.com/servicecatalog/](https://console.aws.amazon.com/servicecatalog/)\.

1. Choose the portfolio with the product you want\.

1. Choose the **Constraints** tab and then choose **Create constraints**\.

1. In **Product**, choose the product\. In **Constraint type**, choose **Stack Set**\. 

1. Configure the accounts, regions, and permissions for your stack set constraints\.
   + In **Account settings**, identify the accounts where you want to create products\.
   + In **Region settings**, choose the geographic regions to deploy products and the order you want those products to be deployed in those regions\.
   + In **Permissions**, choose an IAM StackSet Administrator Role to manage your target accounts\. If you don't choose a role, StackSets uses the default ARN\. [Learn more about setting up stack set permissions\.](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs.html)

1. Choose **Create**\.
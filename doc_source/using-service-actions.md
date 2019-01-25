# AWS Service Catalog Self\-Service Actions<a name="using-service-actions"></a>

AWS Service Catalog enables you to reduce administrative maintenance and end\-user training while adhering to compliance and security measures\. With self\-service actions, as the administrator you can enable end users to perform operational tasks, troubleshoot issues, run approved commands, or request permissions in AWS Service Catalog\. You use [AWS Systems Manager documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html) to define self\-service actions\. The [AWS Systems Manager documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html) provide access to pre\-defined actions that implement AWS best practices, such as Amazon EC2 stop and reboot, and you can define custom actions too\.

In this tutorial, you provide end users with the ability to restart an Amazon EC2 instance\. You add the necessary permissions, define the self\-service action, associate the self\-service action with a product, and test the end user experience using the action with a provisioned product\.

## Prerequisites<a name="service-actions-prerequisites"></a>

This tutorial assumes that you have full AWS administrator permissions, you are already familiar with AWS Service Catalog, and that you already have a base set of products, portfolios, and users\. If you are not familiar with AWS Service Catalog, complete the [Setting Up](setup.md) and [Getting Started](getstarted.md) tasks before using this tutorial\.

**Topics**
+ [Prerequisites](#service-actions-prerequisites)
+ [Step 1: Configure End\-User Permissions](#service-actions-configure-end-user-permissions)
+ [Step 2: Create a Self\-Service Action](#service-actions-create-new-service-action)
+ [Step 3: Associate the Self\-Service Action with a Product Version](#service-actions-associate-with-product-version)
+ [Step 4: Test the End\-User Experience](#service-actions-test-end-user-experience)

## Step 1: Configure End\-User Permissions<a name="service-actions-configure-end-user-permissions"></a>

End\-user accounts must have the necessary permissions to view and perform specific service actions\. In this example, the end user needs permission to access the AWS Service Catalog service actions feature and to perform an Amazon EC2 restart\.

**To update permissions**

1. Open the AWS Identity and Access Management \(IAM\) console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. From the menu, choose **Groups**\.

1. On the **Groups** page, select the groups used by end users to access AWS Service Catalog resources\. In this example, we select the end user group\. In your own implementation, choose the group that is used by the relevant end users\.

1. On the **Permissions** tab of your group’s detail page, you either create a new policy or edit an existing policy\. In this example, we add permissions to the existing policy by selecting the custom policy created for the group’s AWS Service Catalog Provision and Terminate permissions\.

1. On the **Policy** page, choose **Edit Policy** to add the necessary permissions\. You can use either the visual editor or the JSON editor to edit the policy\. In this example, we use the JSON editor to add the permissions\. For this tutorial, add the following permissions to the policy:

   ```
   {
   	"Version": "2012-10-17",
   	"Statement": [
   		{
   			"Sid": "Stmt1536341175150",
   			"Action": [
   				"servicecatalog:ListServiceActionsForProvisioningArtifact",
   				"servicecatalog:ExecuteprovisionedProductServiceAction",
   				"ssm:DescribeDocument",
   				"ssm:GetAutomationExecution",
   				"ssm:StartAutomationExecution",
   				"ssm:StopAutomationExecution",
   				"cloudformation:ListStackResources",
   				"ec2:DescribeInstanceStatus",
   				"ec2:StartInstances",
   				"ec2:StopInstances"
   			],
   			"Effect": "Allow",
   			"Resource": "*"
   		}
   	]
   }
   ```

1. After you edit the policy, review and approve the change to the policy\. Users in the end user group now have the necessary permissions to perform the Amazon EC2 restart action in AWS Service Catalog\.

## Step 2: Create a Self\-Service Action<a name="service-actions-create-new-service-action"></a>

Next, you create a self\-service action to restart Amazon EC2 instances\.

1. Open the AWS Service Catalog console at [https://console\.aws\.amazon\.com/sc/](https://console.aws.amazon.com/servicecatalog/)\.

1. From the menu, choose **Service actions**\.

1. On the **self\-service actions** page, choose **Create new action**\.

1. On the **Action creation** page, choose an AWS Systems Manager document to define the self\-service action\. The Amazon EC2 Instance Restart action is defined by an AWS Systems Manager document, so we keep the default option on the drop\-down menu, **Amazon documents**\.

1. Choose the **AWS\-RestartEC2Instance** action, and then choose **Next**\.

1. On the **Configure** page, keep the default configuration values for the purposes of this tutorial\. Note that you can define a name and description for the action that make sense for your environment and team\. The end user will see this description, so choose something that helps them understand what the action does\. We are also using default permissions for the self\-service action\. Other permission configurations are possible and are defined on this page\.

1. After you have reviewed the configuration, choose **Create action**\.

1. On the next page, a confirmation appears when the action has been created and is ready to use\.

## Step 3: Associate the Self\-Service Action with a Product Version<a name="service-actions-associate-with-product-version"></a>

After you define an action, you must associate a product with that action\.

1. On the **self\-service actions** page, choose **AWS\-RestartEC2instance**, and then choose **Associate action**\. 

1. On the **Associate action** page, choose the product that you want your end users to take the self\-service action on\. In this example, we choose **Linux Desktop**\.

1. Select a product version\. Note that you can use the topmost check box to select all versions\.

1. Choose **Associate action**\.

1. On the next page, a confirmation message appears\.

You have now created the self\-service action in AWS Service Catalog\. The next step of this tutorial is to use the service action as an end user\.

## Step 4: Test the End\-User Experience<a name="service-actions-test-end-user-experience"></a>

End users can perform self\-service actions on provisioned products\. For the purposes of this tutorial, the end user must have at least one provisioned product\. The provisioned product should be launched from the product version that you associated with the self\-service action in the previous step\.

**To access the self\-service action as an end user**

1. Log in to the AWS Service Catalog console as an end user\. 

1. On the AWS Service Catalog dashboard, in the navigation pane, choose **Provisioned products list**\. The list shows the products that are provisioned for the end\-user's account\.

1. On the **Provisioned products list** page, choose the instance that is provisioned\.

1. On the **Provisioned product details** page, choose **Actions** in the upper right side, and then choose the **AWS\-RestartEC2instance** action\. 

1. Confirm that you want to execute the custom action\. You receive confirmation that the action has been sent\.
# Step 6: Add a Launch Constraint to Assign an IAM Role<a name="getstarted-launchconstraint"></a>

A launch constraint designates an IAM role that AWS Service Catalog assumes when an end user launches a product\. 

For this step, you add a launch constraint to the Linux Desktop product so that AWS Service Catalog can use the AWS resources that are part of the product's AWS CloudFormation template\. 

The IAM role that you assign to a product as a launch constraint must have permissions to use:

1. AWS CloudFormation

1. Services in the AWS CloudFormation template for the product

1. Read access to the AWS CloudFormation template in Amazon S3

This launch constraint enables the end user to launch the product and, after launch, manage it as a provisioned product\. For more information, see [AWS Service Catalog Launch Constraints](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/constraints-launch.html)\.

Without a launch constraint, you need to grant additional IAM permissions to your end users before they can use the Linux Desktop product\. For example, the `ServiceCatalogEndUserAccess` policy grants the minimum IAM permissions required to access the AWS Service Catalog end user console view\. 

By using a launch constraint, you can keep your end users' IAM permissions to a minimum, which is an IAM best practice\. For more information, see [Grant least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) in the *IAM User Guide*\.

To create an IAM policy, attach it to an IAM role, and add a launch constraint\.

**To add a launch constraint**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam](https://console.aws.amazon.com/iam)\.

1. In the navigation pane, choose **Policies**, **Create policy** and do the following:

   1. On the **Create policy** page, choose the **JSON** tab\.

   1. Copy this example policy and paste it in the **Policy Document** to replace the placeholder JSON in the text field:

      ```
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "cloudformation:CreateStack",
                      "cloudformation:DeleteStack",
                      "cloudformation:DescribeStackEvents",
                      "cloudformation:DescribeStacks",
                      "cloudformation:GetTemplateSummary",
                      "cloudformation:SetStackPolicy",
                      "cloudformation:ValidateTemplate",
                      "cloudformation:UpdateStack",
                      "ec2:*",
                      "s3:GetObject",
                      "servicecatalog:*",
                      "sns:*"
                  ],
                  "Resource": "*"
              }
          ]
      }
      ```

   1. Choose **Next**, **Review policy**\.

   1. For **Policy Name**, type **linuxDesktopPolicy**\.

   1. Choose **Create policy**\.

1. In the navigation pane, choose **Roles**\. Then choose **Create role** and do the following:

   1. For **Select type of trusted entity**, choose **AWS service** and then choose **Service Catalog**\. Select the **Service Catalog** use case and then choose **Next: Permissions**\.

   1. Search for the **linuxDesktopPolicy** policy and then select the checkbox\.

   1. Choose **Next: Tags**, and then **Next: Review**\.

   1. For **Role name**, type **linuxDesktopLaunchRole**\.

   1. Choose **Create role**\.

1. Open the IAM console at [https://console\.aws\.amazon\.com/servicecatalog](https://console.aws.amazon.com/servicecatalog)\.

1. Choose the **Engineering Tools** portfolio\.

1. On the portfolio details page, choose the **Constraints** tab, and then choose **Create constraint**\.

1. For **Product**, choose **Linux Desktop**, and for **Constraint type**, choose **Launch**\.

1. Choose **Select IAM role**\. Next choose **linuxDesktopLaunchRole**, and then choose **Create**\. 
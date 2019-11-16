# Grant Permissions to AWS Service Catalog End Users<a name="getstarted-iamenduser"></a>

Before the end user can use AWS Service Catalog, you must grant access to the AWS Service Catalog end user console view\. To grant access, you attach policies to the IAM user, group, or role that is used by the end user\. In the following procedure, we attach the **AWSServiceCatalogEndUserReadOnlyAccess** policy to an IAM group\. For more information, see [Predefined AWS Managed Policies](controlling_access.md#permissions-managed-policies)\.

To allow an end user to launch a product, you must grant access to the `ProvisionProduct` action\. You can do so using an inline policy, as shown in the following procedure\.

**To grant permissions to an end user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Policies**\.

1. Choose **Create policy** and do the following:

   1. Choose the **JSON** tab\. Copy the following example policy and paste it in **Policy Document**:

      ```
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "servicecatalog:ProvisionProduct"
                  ],
                  "Resource": "*"
              }
          ]
      }
      ```

   1. Choose **Review policy**\.

   1. For **Policy Name**, type **ServiceCatalogEndusers\-AdditionalPermissions**\.

   1. Choose **Create policy**\.

1. In the navigation pane, choose **Groups**\.

1. Choose **Create New Group** and do the following:

   1. For **Group Name**, type **Endusers**, and then choose **Next Step**\.

   1. In the search field, type **ServiceCatalog** to filter the policy list\.

   1. Select the checkboxes for the **AWSServiceCatalogEndUserReadOnlyAccess** and **ServiceCatalogEndusers\-AdditionalPermissions** policies, and then choose **Next Step**\.

   1. On the **Review page**, choose **Create Group**\.

1. In the navigation pane, choose **Users**\.

1. Choose **Add user** and do the following:

   1. For **User name**, type a name for the user\.

   1. Select **AWS Management Console access**\.

   1. Choose **Next: Permissions**\.

   1. Choose **Add user to group**\.

   1. Select the checkbox for the **Endusers** group and choose **Next: Tags** and then **Next: Review**\.

   1. On the **Review** page, choose **Create user**\. Download or copy the credentials and then choose **Close**\.

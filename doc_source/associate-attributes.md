# Associating attribute groups<a name="associate-attributes"></a>

You can associate new or existing attribute groups to your application\. An attribute group is an open JSON object where you define the metadata for a resource\. When you update an attribute group definition, the update applies to every application associated with that attribute group\.

You can associate a new or existing attribute groups from Attribute groups or when you create an AppRegistry application\. 

**Topics**
+ [Creating attribute groups](#create-attr-groups)
+ [Accessing attribute group details](#access-attr-group-details)
+ [Associating attribute groups](#associate-attr-groups)

## Creating attribute groups<a name="create-attr-groups"></a>

**To create attribute groups**

1. In the left navigation menu, choose **AppRegistry**, **Attribute groups**\.

1. In **Attribute groups**, choose **Create attribute group**\.

1. In **New attribute group**, enter a name and description\. Then add an open JSON object schema that captures metadata to filter, sort, and search your applications in AppRegistry\. 

   Here is an example of an open JSON object schema:

   ```
      {
      "ApplicationResilience":"high",
      "DataSecurity":"high",
      "DataSensitivity":"high"
      }
   ```

1. Choose **Next** to assign this attribute groups to an existing application and add tags\. 

   To assign attribute groups to an application, choose one or more applications\. 

   If you want to only assign attribute groups to applications, choose **Finish**\. 

   To add tags to the attribute group, choose **Next**\.

## Accessing attribute group details<a name="access-attr-group-details"></a>

In Attribute group details, you can see the attribute group's:
+ Name
+ Description
+ ID
+ ARN 
+ Metadata as a JSON open object

You can also see your existing tags and create additional tags\. Tags with an *aws* prefix are internal tags\. AppRegistry automatically adds them, and you can’t remove them\. 

On the Attribute group details page, you can delete and edit an attribute group\. You can access Attribute group details from Applications or Attribute groups\.

**To access Attribute group details from Applications**

1. In the left navigation menu, choose **AppRegistry**, **Applications**\.

1. Open an application to show the **Application details**, and choose **Attribute groups**\.

**To access Attribute group details from Attribute groups**

1. In the left navigation menu, choose **AppRegistry**, then **Attribute groups**\.

1. Open an attribute group to show the **Attribute group details**\.

## Associating attribute groups<a name="associate-attr-groups"></a>

You can associate attribute groups from Applications or Application details\.

**To associate attribute groups from Applications**

1. In the left navigation menu, choose **AppRegistry**, **Applications**\.

1. In **Applications**, choose **Create application**\.

1. In **Create an application**, enter a name and description and choose **Next** to add resources\. Choose **Finish** if you do not want to add resources, associate attribute groups, or add tags now\.

1. In **Resources** add one or more provisioned products or CloudFormation stack ARNs as resources\. Choose **Next** to associate to attribute groups, or choose **Finish** if you do not want to add tags now\.

1. You can associate your application to existing attribute groups or create new attribute groups\.

   In **Associate existing attribute groups**, choose one or more attribute groups from your attribute library\.

   In **New attribute group**, enter a name and description\. Then add an open JSON object schema to gather metadata to manage your application in AppRegistry\. 

   Here is an example of an open JSON object schema:

   ```
   {
      "ApplicationResilience":"high",
      "DataSecurity":"high",
      "DataSensitivity":"high"
   }
   ```

1. If you want to only create or add existing attribute groups to your application, choose **Finish**\. To add tags to your application, choose **Next**\.

**To associate new attribute groups from Attributes groups**

1. In the left navigation menu, choose **AppRegistry**, **Attribute groups**\.

1. In **Attribute group**, chose **Create attribute group**\.

1. In **New attribute group**, enter a name and description\.

1. Add an open JSON object schema that gathers the metadata you can use to filter, sort, and search your applications in AppRegistry\. Here is an example of the open JSON object schema:

   ```
   {
      "ApplicationResilience":"high",
      "DataSecurity":"high",
      "DataSensitivity":"high"
   }
   ```

1. To associate the attribute group to one or more existing applications, choose **Next**\.

1. Associate the attribute group to existing applications\. If you want to only associate applications, choose **Finish**\. The Attribute group details appear with information about your new attribute group\. 

1. If you want to add tags, choose **Next**\.

**To associate or disassociate attribute groups from Application details**

1. In the left navigation menu, choose **AppRegistry**, **Applications**\.

1. In **Applications**, open an application to display **Application details**\.

1. Choose **Attribute groups**\.

1. To associate existing attribute groups, choose **Associate attribute group**\. 

1. Select one or more attribute groups from your attribute library and choose **Save changes**\.

   To disassociate existing attribute groups, select an attribute group and choose **Diassociate**\. Confirm your deletion and choose **Ok**\.

**To delete attribute groups from Attribute groups**

1. In the left navigation menu, choose **AppRegistry**, **Attribute groups**\.

1. Choose an attribute group\. Then choose **Actions**, **Delete attribute group**\.

1. In **Delete attribute group**, confirm your deletion and choose **Delete attribute group**\.

**To delete attribute groups from Attribute group details**

1. In the left navigation menu, choose **AppRegistry**, **Attribute groups**\.

1. Open an attribute group to display **Attribute group details**\.

1. Choose **Delete**\. Confirm your deletion and choose **Delete attribute group**,

**To edit attribute groups from Attribute group details**

1. In the left navigation menu, choose **AppRegistry**, **Attribute groups**\.

1. Open an attribute group to display **Attribute group details**\.

1. Choose **Edit**\. In Edit attribute group, enter your changes and choose **Save changes**\.

**To edit attribute groups from Attribute groups**

1. In the left navigation menu, choose **AppRegistry**, **Attribute groups**\.

1. Choose an attribute group\. Then choose **Actions**, **Edit attribute group**\.

1. In **Edit attribute group**, enter your changes and choose **Save changes**\.
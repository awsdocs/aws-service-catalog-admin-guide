# Adding tags<a name="add-tags"></a>

You can use tags to assign metadata to your AppRegistry applications and attribute groups\. You can create a maximum of 50 tags on an application or attribute group to categorize them by purpose, owner, environment, or other criteria\. 

You can access tags from Applications, Application details, Attribute groups, and Attribute key details\.

Tags in AppRegistry with an *aws* prefix indicate internal tags\. AppRegistry automatically adds them, and you can’t remove them\. 

**To add tags from Applications**

1. In the left navigation menu, choose **AppRegistry**, **Applications**\.

1. In **Applications**, choose **Create application**\.

1. In **Create an application**, enter a unique name for your AppRegistry application and a brief description\. If you only want to: 
   + Create an application without resources, attribute groups, or tags, choose **Finish**\. 
   + Add tags and associate resources, choose **Next**\. Associate attribute groups and choose **Next** to add tags\.

1. Choose **Add a tag** and enter information in the **Key** and **Value** fields\. If you want to add more tags, choose **Add another**\. Then choose **Finish**\.

**To add and delete tags from Applications details**

1. In the left navigation menu, choose **AppRegistry**, **Applications**\.

1. In **Applications**, open an application to display **Application details** and choose **Tags**\. You can add, search, or delete tags\.
   + To add tags, enter information in the **Key** and **Value** fields, and choose **Add tag**\.
   + To delete tags, choose a tag in the **Application specific** tags list\. Choose **Delete tag**, confirm your deletion, and then choose **Ok**\.

**To add tags to a new Attribute group**

1. In the left navigation menu, choose **AppRegistry**, **Attribute groups**\.

1. In** Attribute groups**, choose **Create attribute group**\.

1. In **New attribute group**, enter a name and description\. Then add an open JSON object schema to capture metadata to manage your applications\. 

1. In **Assign attribute group to an application**, choose **Next** to skip this step if you don't want to add tags\. If you want to add tags, choose to associate existing applications to this attribute group and proceed to add tags\. 

1. To add tags, choose **Add tag**\. Enter data in the **Key** and **Value** field\. To add more tags, choose **Add another**\. To remove tags, choose **Remove**\. To complete the process, choose **Finish**\.

**To add tags from Attribute group details**

1. In the left navigation menu, choose **AppRegistry**, **Attribute groups**\.

1. Open an attribute group to display **Attribute group details**\. Then choose **Tags**\. You can add, search, or delete tags\.
   + To add tags, enter information in the **Key** and **Value** fields, and choose **Add tag**\.
   + To delete tags, choose a tag in the **Application specific tags** list\. Choose **Delete tag**, confirm your deletion, and choose **Ok**\.
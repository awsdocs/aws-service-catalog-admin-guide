# Using AppRegistry<a name="appregistry"></a>

Use AWS Service Catalog AppRegistry to create a repository of your applications and associated resources\. You can then define and manage your application metadata to understand the context of your applications and resources across your environments\.

An AppRegistry application consists of associated resources and attribute groups\. An application resource can be either an AWS Service Catalog provisioned product or an AWS CloudFormation stack\. You can add or remove resources from your application at any time\. You can associate a resource with only one application\.

You can also associate new or existing attribute groups to your application\. Attribute groups contain the metadata for your application\. When you update an attribute group definition, the update applies to every application associated with that attribute group\. 

You can use tags to assign metadata to your AppRegistry application\. Tags can help you manage, identify, search for, and manage your applications\. 

For every application, AppRegistry creates an application resource group\. An application resource group is a collection of the resources in your application\. It also creates a stack level resource group for every stack associated with the application\.

**Topics**
+ [Creating applications](create-app.md)
+ [Associating application resources](associate-resource.md)
+ [Associating attribute groups](associate-attributes.md)
+ [Adding tags](add-tags.md)
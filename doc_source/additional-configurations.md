# ServiceNow additional features<a name="additional-configurations"></a>

 This section provides information about additional features for the AWS Service Management Connector for ServiceNow\. 

## Viewing products in the Standard User Interface \(Fulfiller View\)<a name="view-products"></a>

**To view provisioned products as an end user**

1.  Choose **My Assets** in the ServiceNow standard user interface\. 

1.  In **My Asset Requests**, view the requests\. 

1.  To view the product, personalize the list view to show the associated configuration item\. To show items, choose the **Settings** icon in the header row of the table of asset requests\. 

1.  Select **Configuration item \(configuration\_item\)** and add it to the view  with the **>** icon\. Move it to below **Stage** in the list\. The configuration item \(the ordered product\) shows in the list of assets\. 

1.  To view the product, choose the configuration item name\. 

1.  View the **Outputs** for the provisioned product in the **Outputs** tab of the form\. 

1.  View the provisioning history of the product in the Product Events tab of the form\. 

**To view provisioned products from the scoped app as an administrator**

1.  Log in to your ServiceNow instance as the end user \(for example, Abel Tuter\)\. 

1.  Enter **AWS Service Catalog** in the navigation filter and choose **Provisioned Products**\. The user interface view displays the provisioned products\. 

1.  Select a provisioned product to view the current status\. You can also select post provisioned actions such as **Request Update**, **Request Termination**, as well as associated service actions\. 

## Ordering AWS Service Catalog products through the ServiceNow Service portal<a name="service-portal"></a>

 The Connector for ServiceNow version 3\.7\.1 supports ordering AWS Service Catalog products through Service Portal by using the Service Catalog and Order Something views\. The release also includes pages and widgets you can add to Service Portal that enable users to view their provisioned products\. 

**Note**  
The audience for the Service Portal Features section is a ServiceNow administrator or equivalent\. The ServiceNow user requires permissions to modify the Service Portal\.

### Service portal widgets<a name="service-portal-widgets"></a>

 The Connector for ServiceNow includes widgets that you can add to your Service Portal\. It also includes two alternative view Portal Pages for the following: 
+ **My AWS Products** – Overview of all provisioned products the user owns\.
+ **AWS Product Details** – Details of a single provisioned product\.

 To access the new widgets, you need to update the Service Portal Designer\.

**To update the Service Portal Designer**

1. Go to [Create and edit a page using the Service Portal Designer](https://docs.servicenow.com/bundle/kingston-servicenow-platform/page/build/service-portal/task/t_ConfigureAPage.html)\.

1.  Following the instructions, choose the **Service Portal Index** page\. 

1.  Under the **Order Something** container, add the **My AWS **widget\. 

1. The new widget appears on your main Service Portal view\.

### Service portal pages<a name="service-portal-pages"></a>

 The following section describes the two new pages available in the Service Portal Beta release of the AWS Service Management Connector, **My AWS Products** and **AWS Product Details**\. You can add links to these pages on the Service Portal home page or other pages by using the usual page configuration mechanism in Service Portal\. 

**My AWS Products**  
An overview of all provisioned products that the user owns\. Terminated products display separately from current products in a collapsed panel on initial page load\. 

 The **My AWS Products** page is available using the following format:

```
http://<insertinstancename>.service-now.com/sp?id=aws_sc_pp
```

**AWS Product Details**  
Details of a single provisioned product\.

 The **AWS Product Details** page is available using the following format:

```
http://<insertinstancename>.service-now.com/sp?id=aws_sc_pp_details&sys_id=<provisioned product id>
```

## Reference: AWS API calls used in the Connector<a name="api-ref"></a>
+  AWSBudgets\.describeBudget
+ AWSCloudFormation\.registerType
+ AWSCloudFormation\.deregisterType
+ AWSCloudFormation\.describeTypeRegistration
+ AmazonConfig\.describeConfigurationRecorders
+ AmazonConfig\.getResourceConfigHistory
+ AmazonConfig\.listDiscoveredResources
+ AmazonConfig\.putResourceConfig 
+ AmazonConfig\.selectResourceConfig
+ AmazonConfig\.selectAggregateResourceConfig
+ AWSSecurityHub\.batchUpdateFindings
+ AWSSecurityTokenService\.getCallerIdentity
+ AWSServiceCatalog\.createProvisionedProductPlan
+ AWSServiceCatalog\.deleteProvisionedProductPlan
+ AWSServiceCatalog\.describePortfolio
+ AWSServiceCatalog\.describeProduct
+ AWSServiceCatalog\.describeProductAsAdmin
+ AWSServiceCatalog\.describeProductView
+ AWSServiceCatalog\.describeProvisionedProduct
+ AWSServiceCatalog\.describeProvisionedProductPlan
+ AWSServiceCatalog\.describeProvisioningParameters
+ AWSServiceCatalog\.describeRecord
+ AWSServiceCatalog\.executeProvisionedProductPlan
+ AWSServiceCatalog\.executeProvisionedProductServiceAction
+ AWSServiceCatalog\.listBudgetsForResource
+ AWSServiceCatalog\.listLaunchPaths
+ AWSServiceCatalog\.listPortfolioAccess
+ AWSServiceCatalog\.listPortfolios
+ AWSServiceCatalog\.listProvisionedProductPlans
+ AWSServiceCatalog\.listServiceActionsForProvisioningArtifact
+ AWSServiceCatalog\.listStackInstancesForProvisionedProduct
+ AWSServiceCatalog\.provisionProduct
+ AWSServiceCatalog\.searchProducts
+ AWSServiceCatalog\.searchProductsAsAdmin
+ AWSServiceCatalog\.terminateProvisionedProduct
+ AWSServiceCatalog\.updateProvisionedProduct
+ AWSSimpleQueueService\.DeleteMessage
+ AWSSimpleQueueService\.DeleteMessageBatch
+ AWSSimpleQueueService\.ReceiveMessage
+ AWSSimpleSystemsManagement\.describeAutomationExecutions
+ AWSSimpleSystemsManagement\.describeDocument
+ AWSSimpleSystemsManagement\.getAutomationExecution
+ AWSSimpleSystemsManagement\.getDocument
+ AWSSimpleSystemsManagement\.listDocuments
+ AWSSimpleSystemsManagement\.startAutomationExecution
+ AWSSimpleSystemsManagement\.describeOpsItems
+ • AWSSimpleSystemsManagement\.getOpsItem
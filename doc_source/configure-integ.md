# Configuring AWS Config integration in ServiceNow<a name="configure-integ"></a>

This version of the Connector enables ServiceNow administrators to configure system properties, Config Aggregators, and AWS Config custom resources from select ServiceNow tables\. 

**To configure the new AWS Config integration System Properties**

1. In the navigator, enter **AWS Service Management**\.

1. Select **System Properties**, then **AWS Config**\. 

1. Review the available settings and recommendations in the table below\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/servicecatalog/latest/adminguide/configure-integ.html)

## Addressing stale AWS Config items in the ServiceNow CMDB<a name="stale-config"></a>

In addition to the AWS Config settings, AWS SMC for ServiceNow now exposes a global API to identify stale config items from the AWS Config integration\. 

**Note**  
This feature requires you to enable the creation relationship to sync the status setting in the AWS Config System Properties in the ServiceNow scoped app\.

## Stale Config items<a name="stale-define"></a>

Stale Config items are the existing AWS Config items that did not update during the most recent sync for the same source \(such as account, Region and aggregator name\)\. 

## Identifying stale Config items<a name="stale-identify"></a>

**Note**  
ServiceNow administrators are the target audience for this section

The script include, `x_126749_aws_sc.AwsSmc`, exposes a public API\. You can use this script to access any application scope, including *global* scope\. As an example, run this script:

```
   x_126749_aws_sc.AwsSmc.asSyncUser().getStaleConfigItems().forAll(function(object)
{
  gs.info(
       object.accountNumber + '/' + object.region + ' '
       + (object.aggregatorName ? 'aggregator: ' + object.aggregatorName + ' ' :
'')
       + 'ci: ' + object.ci.name
       + ' - ' + object.ci.getDisplayValue('install_status')
  );
});
```

As a background script, it would log the following: 

```
Info: 11111111/us-east-1 ci: i-1234567fg6j8 - Installed
Info: 11111111/us-west-1 ci: i-9876541fdgfd - Installed
Info: 22222222/eu-west-1 aggregator: all-dev ci: i-1df5235ftt55 - Installed
```

Each *object* contains the below properties: 


****  

| Property  | Type  | Description  | 
| --- | --- | --- | 
| accountNumber  | String  | The account number from which the stale config item originates\.  | 
| region  | String  | The Region from which the stale config item originates\. | 
| aggregatorName  | String  | The aggregator name \(if applicable\) from which the stale config item originates\. | 
| lastSynced  | GlideDateTime | The GlideDateTime of the when the last synchronization occurred\.  | 
| CI | GlideRecord | The GlideRecord of the stale config item\.  | 

Optionally, you can also pass an `options` object as the second argument to the `forAll` method which allows you to customize the search for stale items\.


| Property  | Type  | Description | 
| --- | --- | --- | 
| lowerTimeLimit | GlideDateTime  | The threshold GlideDateTime from when you should search items\. Any stale item last updated prior to that date does not return\.  | 
| upperTimeLimit | GlideDateTime | The threshold GlideDateTime untilyou should search for items\. Any item last updated after that date does not return\. | 
| excludeStatus  | Number  | The install\_status to filter on\.  | 

Timestamps of sync resources: 
+ `LastSyncTimeField`\(default `checked_in`\): The start of the current sync process\. 
+ `first_discovered` \(for new records\): The current time\. We set the LastDiscoveredField \(default `last_discovered`\) to the `configurationItemCaptureTime` of the resource, if it exists or undefined otherwise\. 

**Additional notes on stale records**

When AWS Service Management Connector reads AWS Config records that refer to other resources, it often creates a relationship to those resources\. 

In some cases, the related resource does not have an entry in the ServiceNow CMDB\. In these cases, the Connector creates a record for that relationship, with an install status of *absent*\. When the Connector reads the AWS Config record for the related resource, that record populates\. 

To see active resources, you should filter ServiceNow records synced from AWS Config by an install status of *not Absent*\.

**Disclaimer**

Because the script compares items linked to state sync records, it is unable to identify stale resources synced before the installation of this SMC version\. When switching to sync with an aggregator or switching from aggregator sync to non\-aggregator sync, the script also fails to detect items that became stale between the last non\-aggregator sync and the first aggregator sync\.

## Configuring synchronization of AWS Config data using an Aggregator in ServiceNow CMDB<a name="config-sync"></a>

**Prerequisite**: You need to opt\-in and configure the AWS account that contains the aggregated AWS Config resources details prior to performing the steps below\. For more information, see the *Configuring AWS Accounts to Synchronize in the Connector*\. 

**To configure the Connector to use an Aggregator to synchronize AWS Config data**

1. In the AWS Service Management scoped app, choose the **Setup** module\.

1. Select **Aggregators for AWS Config**\.

1. Choose **New**\.

1. Enter the name of the new Config Aggregator\.

1. Select the Region where you created the new Config Aggregator\.

1. Choose the AWS account that should use the new Aggregator\. Only AWS accounts opted into the Connector for ServiceNow that have **Integrate with AWS Config** are viewable\. 

1. Select **Submit**\.

   If you define an Aggregator for an AWS account and Region, the Aggregator integration becomes the only AWS Config to ServiceNow CMDB synchronization mechanism for that AWS account\. 

## Configuring available ServiceNow tables to sync as AWS Config custom resources<a name="tbd"></a>

In this Connector for ServiceNow release, you can now sync a set of ServiceNow tables in the CMDB to AWS Config as custom resources\.

The ServiceNow tables and AWS Config custom resource mapping are as follows:


| ServiceNow CMDB table | AWS custom resource  | 
| --- | --- | 
| cmdb\_ci\_apache\_web\_server | Apache Web Server | 
| cmdb\_ci\_app\_server | Application Server | 
| cmdb\_ci\_app\_server\_java | Java Server | 
| cmdb\_ci\_app\_server\_tomcat | Tomcat Server | 
| cmdb\_ci\_app\_server\_tomcat\_war | Tomcat Web Application | 
| cmdb\_ci\_app\_server\_websphere | IBM Websphere Application | 
| cmdb\_ci\_app\_server\_ws\_ear | Websphere Enterprise Archive | 
| cmdb\_ci\_appl | Application | 
| cmdb\_ci\_appl\_dot\_net | A \.Net Application | 
| cmdb\_ci\_appl\_now\_app\_comp | ServiceNow Application Component | 
| cmdb\_ci\_appl\_sap | Sap Application | 
| cmdb\_ci\_appl\_sap\_hana\_db | SAP Hana Database | 
| cmdb\_ci\_appl\_sap\_system | SAP System | 
| cmdb\_ci\_appl\_sharepoint | Microsoft Sharepoint Application | 
| cmdb\_ci\_application\_cluster | Application Cluster | 
| cmdb\_ci\_application\_server\_resource | Application Server Resource | 
| cmdb\_ci\_application\_software | Application Software | 
| cmdb\_ci\_db\_mssql\_database | MySql Database | 
| cmdb\_ci\_db\_mysql\_instance | MySql Instance | 
| cmdb\_ci\_kubernetes\_cluster | Kubernetes Cluster | 

**To configure select ServiceNow tables as AWS Config custom resources**

1. In the navigator, enter **AWS Service Management**\.

1. Choose **Setup**, then **Tables Sync to AWS Config**\.

1. Choose **New**\.

1. Select an in scope ServiceNow table\.

1. Select an account and Region for the new resource type\. You can select any supported Region, in addition to preconfigured Regions for the account\. 

1. Click **Submit**\.

1. Repeat steps above to include additional ServiceNow tables available to sync as AWS Config custom resources\.

   The amount of time to create new AWS Config resources depends on the number of ServiceNow tables you selected\. You can see resources in the **Schema version** field upon successful completion\. The period synchronization of resources automatically includes the new AWS Config custom resource type\. As details in the ServiceNow table update, this information syncs to AWS Config custom resource\. 
# Configuring AWS Config<a name="servicenow-aws-config"></a>

## AWS Config integration to ServiceNow CMDB<a name="config-CMDB"></a>

To allow the connector to synchronize Config data for a given Region, you must enable AWS Config in that Region\. For more information, see [Setting Up AWS Config with the Console](https://docs.aws.amazon.com/config/latest/developerguide/gs-console.html)\.

The Connector can now synchronize Config data from multiple accounts and Regions using an Aggregator\. You must configure the Config Aggregator in AWS before using this feature\. For more information, see [Setting up an Aggregator](https://docs.aws.amazon.com/config/latest/developerguide/setup-aggregator-console.html) in the console\. 

**Note**  
The Config Aggregator view in AWS displays only current config item resources in AWS Config\. Thus, terminated resources are not available in the Config Aggregator view\.   
To minimize stale config item records rendering in the ServiceNow CMDB from the AWS Config Aggregator, we recommend you remove Config rules associated to terminated resources\. For more information, see [ Managing your AWS Config Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_manage-rules.html) 

## Configuring ServiceNow tables as AWS Config custom resources<a name="config-custom"></a>

Version 3\.7\.1 of the Connector for ServiceNow enables ServiceNow administrators to specify select ServiceNow tables as custom resources within AWS Config\.

To set up these resources, use the preconfigured files in the Connector\. These required files include the custom resource schema\. 
# Configuring AWS Security Hub<a name="servicenow-security-hub"></a>

 AWS Security Hub enables users to view security findings from AWS services such as Amazon Guard Duty, Amazon Inspector, as well as AWS Partner solutions\. 

View the following video, *AWS Security Hub \- Bidirectional integration with ServiceNow ITSM*, for an overview of the AWS Security Hub integration to the Connector for ServiceNow\.

**To configure AWS Security Hub integration features**

1. Enable AWS SecurityHub\. For more information, see [Setting up AWS SecurityHub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-get-started.html) with the Console\. 

1. Set up an SQS queue to receive updated Findings\. Name the queue `AwsServiceManagementConnectorForSecurityHubQueue` to align with the default name in the ServiceNow System Properties for the AWS Security Hub integration\. For more information, see [Getting started with Amazon SQS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-getting-started.html)\. 

1. Set up a CloudWatch rule to detect changes to Findings and push these to the queue\. For more information, see [Getting started with Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/GettingStarted.html)\.

1. The CloudWatch rule should have this event pattern and point to the SQS queue created in Step 2\.

```
"EventPattern": {

       "source": [

        "aws.securityhub"

        ],

        "detail-type": [

        "Security Hub Findings - Imported",

        "Security Hub Findings - Custom Action"

  ]

}
```

Note that the [Connector for ServiceNow v3\.7\.1 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForServiceNowv-AWS_Configurations_Commercialv3.7.1.json) and [Connector for ServiceNow v3\.7\.1 \- AWS GovCloud Regions\]](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForServiceNowv-AWS_Configurations_GovCloudv3.7.1.json) templates are available to automate the AWS Config custom resource and AWS Security Hub integration features\.
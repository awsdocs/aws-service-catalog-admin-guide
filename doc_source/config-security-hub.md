# Configuring AWS Security Hub<a name="config-security-hub"></a>

AWS Security Hub enables users to view security findings from AWS services, such as Amazon Guard Duty, Amazon Inspector, as well as AWS Partner solutions\. 

**To configure AWS Security Hub integration features**

1. Enable AWS SecurityHub\. For more information, see [Setting up AWS SecurityHub with the Console](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-get-started.html)\. 

1. Set up an SQS queue to receive updated Findings\. Name the queue **AwsSmcJsmSecurityHubQueue** to align with the default name within the ServiceNow System Properties for the AWS Security Hub integration\. For more information, see [Getting started with Amazon SQS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-getting-started.html)\. 

1. Set up a CloudWatch rule to detect changes to Findings and push these to the queue\. For more information, see [Getting Started with Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/GettingStarted.html)\.

   The CloudWatch rule should have the following event pattern and should point to the SQS queue created in Step 2\.

```
"EventPattern":{
   "source":[
      "aws.securityhub"
   ],
   "detail-type":[
      "Security Hub Findings - Imported",
      "Security Hub Findings - Custom Action"
   ]
}
```

**Note**  
The [Connector for Jira Service Management v1\.8\.2 \- AWS Commercial Regions](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.1-AWS_Configurations_Commercial.json) and[Connector for Jira Service Management v1\.8\.2 \- AWS GovCloud West Region](https://servicecatalogconnector.s3.amazonaws.com/SM_ConnectorForJSDv1.8.1-AWS_Configurations_GovCloud.json) templates are available to automate the AWS Config custom resource and AWS Security Hub integration features\.
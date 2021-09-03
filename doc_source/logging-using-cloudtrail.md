# Logging AWS Service Catalog API calls using AWS CloudTrail<a name="logging-using-cloudtrail"></a>

AWS Service Catalog is integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in AWS Service Catalog\. CloudTrail captures all API calls for AWS Service Catalog as events\. The calls captured include calls from the AWS Service Catalog console and code calls to the AWS Service Catalog API operations\. If you create a trail, you can enable continuous delivery of CloudTrail events to an Amazon S3 bucket, including events for AWS Service Catalog\. If you don't configure a trail, you can still view the most recent events in the CloudTrail console in Event history\. Using the information collected by AWS CloudTrail, you can determine the request that was made to AWS Service Catalog, the IP address from which the request was made, who made the request, when it was made, and additional details\.

To learn more about AWS CloudTrail, see the [ AWS CloudTrail User Guide\.](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/logging-using-cloudtrail.html)

## AWS Service Catalog information in AWS CloudTrail<a name="service-name-info-in-cloudtrail"></a>

AWS CloudTrail is enabled on your AWS account when you create it\. When activity occurs in AWS Service Catalog, that activity is recorded in an AWS CloudTrail event along with other AWS service events in Event history\. You can view, search, and download recent events in your AWS account\. For more information, see [Viewing events with AWS CloudTrail Event history](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)\.

For an ongoing record of events in your AWS account, including events for AWS Service Catalog, create a trail\. A *trail* enables AWS CloudTrail to deliver log files to an Amazon S3 bucket\. By default, when you create a trail in the console, the trail applies to all AWS Regions\. The trail logs events from all Regions in the AWS partition and delivers the log files to the Amazon S3 bucket that you specify\. Additionally, you can configure other AWS services to further analyze and act upon the event data collected in AWS CloudTrail logs\. For more information, see the following:
+ [Overview for creating a trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail.html)
+ [AWS CloudTrail supported services and integrations](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-aws-service-specific-topics.html)
+ [Configuring Amazon SNS notifications for AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/configure-sns-notifications-for-cloudtrail.html)
+ [Receiving AWS CloudTraillog files from multiple regions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving AWS CloudTrail log files from multiple accounts](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)

All AWS Service Catalog actions are logged by CloudTrail and are documented in the https://linkto\.APIref\.topic\. For example, calls to the `[CreatePortfolio](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_CreatePortfolio.html)`, `[CreateProduct](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_CreateProduct.html)` and `[UpdateProvisionedProduct](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_UpdateProvisionedProduct.html)` actions generate entries in the AWS CloudTrail log files\.

Every event or log entry contains information about who generated the request\. The identity information helps you determine the following:
+ Whether the request was made with root or AWS Identity and Access Management \(IAM\) user credentials\.
+ Whether the request was made with temporary security credentials for a role or federated user\.
+ Whether the request was made by another AWS service\.

For more information, see the [AWS CloudTrail userIdentity element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

## Understanding AWS Service Catalog log file entries<a name="understanding-service-name-entries"></a>

A trail is a configuration that enables delivery of events as log files to an Amazon S3 bucket that you specify\. AWS CloudTrail log files contain one or more log entries\. An event represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. AWS CloudTrail log files aren't an ordered stack trace of the public API calls, so they don't appear in any specific order\. The following example shows an AWS CloudTrail log entry that demonstrates the `CreateApplication` API\.

```
{
    "eventVersion": "1.05",
    "userIdentity": {
        "type": "IAMUser",
        "principalId": "account",
        "arn": "arn:aws:iam::12345789012:user/dev-haw",
        "accountId": "12345789012",
        "accessKeyId": "keyId",
        "userName": "dev-haw"
    },
    "eventTime": "2020-09-23T21:07:58Z",
    "eventSource": "servicecatalog-appregistry.amazonaws.com",
    "eventName": "CreateApplication",
    "awsRegion": "us-east-1",
    "sourceIPAddress": "205.251.233.48",
    "userAgent": "aws-cli/1.18.140 Python/3.6.11 Linux/4.9.217-0.1.ac.205.84.332.metal1.x86_64 botocore/1.17.63",
    "requestParameters": {
        "name": "hawTestCT",
        "clientToken": "6f36d650-a086-47cf-810a-fbfab2f8ad33"
    },
    "responseElements": {
        "application": {
            "applicationArn": "arn:aws:servicecatalog:us-east-1:12345789012:application/app-02ocuq2cie2328pv64ya78e22f",
            "applicationId": "app-02ocuq2cie2328pv64ya78e22f",
            "creationTime": 1600895277.775,
            "lastUpdateTime": 1600895277.775,
            "name": "hawTestCT",
            "tags": {}
        }
    },
    "requestID": "1b6ad353-3b06-421b-bcb4-00075a782762",
    "eventID": "0a2ca224-cdfd-4c4b-a4ed-163218ff5e2d",
    "readOnly": false,
    "eventType": "AwsApiCall",
    "recipientAccountId": "12345789012"
}
```
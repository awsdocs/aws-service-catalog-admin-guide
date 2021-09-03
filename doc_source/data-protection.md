# Data Protection in AWS Service Catalog<a name="data-protection"></a>

The AWS [shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model/) applies to data protection in AWS Service Catalog\. As described in this model, AWS is responsible for protecting the global infrastructure that runs all of the AWS Cloud\. You are responsible for maintaining control over your content that is hosted on this infrastructure\. This content includes the security configuration and management tasks for the AWS services that you use\. For more information about data privacy, see the [Data Privacy FAQ](https://aws.amazon.com/compliance/data-privacy-faq/)\. For information about data protection in Europe, see the [AWS Shared Responsibility Model and GDPR](https://aws.amazon.com/blogs/security/the-aws-shared-responsibility-model-and-gdpr/) blog post on the *AWS Security Blog*\.

For data protection purposes, we recommend that you protect AWS account credentials and set up individual user accounts with AWS Identity and Access Management \(IAM\)\. That way each user is given only the permissions necessary to fulfill their job duties\. We also recommend that you secure your data in the following ways:
+ Use multi\-factor authentication \(MFA\) with each account\.
+ Use SSL/TLS to communicate with AWS resources\. We recommend TLS 1\.2 or later\.
+ Set up API and user activity logging with AWS CloudTrail\.
+ Use AWS encryption solutions, along with all default security controls within AWS services\.
+ Use advanced managed security services such as Amazon Macie, which assists in discovering and securing personal data that is stored in Amazon S3\.
+ If you require FIPS 140\-2 validated cryptographic modules when accessing AWS through a command line interface or an API, use a FIPS endpoint\. For more information about the available FIPS endpoints, see [ Federal Information Processing Standard \(FIPS\) 140\-2\.](https://docs.aws.amazon.com/compliance/fips/) 

We strongly recommend that you never put sensitive identifying information, such as your customers' account numbers, into free\-form fields such as a Name field\. This includes when you work with AWS Service Catalog or other AWS services using the console, API, AWS CLI, or AWS SDKs\. Any data that you enter into AWS Service Catalog or other services might get picked up for inclusion in diagnostic logs\. When you provide a URL to an external server, don't include credentials information in the URL to validate your request to that server\.

## Protecting Data with Encryption<a name="encryption"></a>

### Encryption at rest<a name="encryption-at-rest"></a>

 AWS Service Catalog uses Amazon S3 buckets and Amazon DynamoDB databases that are encrypted at rest using Amazon\-managed keys\. To learn more, refer to information about encryption at rest provided by Amazon S3 and Amazon DynamoDB\. 

### Encryption in transit<a name="encryption-in-transit"></a>

AWS Service Catalog uses Transport Layer Security \(TLS\) and client\-side encryption of information in transit between the caller and AWS\.

You can privately access AWS Service Catalog APIs from your Amazon Virtual Private Cloud \(Amazon VPC\) by creating VPC endpoints\. With VPC endpoints, the routing between the VPC and AWS Service Catalog is handled by the AWS network without the need for an internet gateway, NAT gateway, or VPN connection\.

The latest generation of VPC endpoints used by AWS Service Catalog is powered by Amazon PrivateLink, an AWS technology enabling the private connectivity between AWS services using Elastic Network Interfaces with private IPs in your VPCs\.

### <a name="inter-network-traffic-privacy"></a>
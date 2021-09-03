# IT Lifecycle Management Setup and Use Case<a name="jsd-it-lifecycle"></a>

 The AWS Service Management Connector for Jira Service Management allows Jira Service Management end users to provision, manage, and operate AWS resources natively through Atlassian's Jira Service Management\. To enable the IT Lifecycle Management scenario, you need to configure: 
+ AWS Config linked resources 
+ Suggested AWS Systems Manager remediations for an issue
+ Sample Use Case: Automatically Creating Jira Issues for IT Lifecycle Management \- Remediating non\-compliant public S3 buckets

## AWS Config and suggested AWS Systems Manager remediations for any Jira issue<a name="jsd-config-sys-remediations"></a>

The Connector provides two fields to use for any issue\.
+ *AWS Config Linked Resources*: enables any resource with an entry in AWS Config to have its AWS Config information displayed on the issue in Jira\. You can expand and see the information\. You can link multiple AWS resources to an issue\. 
+ *AWS Systems Manager Automation Suggested Remediation*: enables SSM automation documents to be recorded against an issue\. They then display, as suggested, ways to correct the issue\. When a Jira user views the issue, they can see these suggested remediations and choose to apply them\. You can attach multiple suggested remediations to an issue\.

 You can use the two fields individually, but they work very well together\. Upon detecting an incident on an AWS resource or set of resources, setting both allows a Jira user to see the configuration information to confirm or better understand the problem, apply remediations to fix common problems, and then confirm in the AWS Config information that the problem has been fixed\. 

**To add AWS fields to an existing issue**

1.  You must enable the project or projects for the Connector in **Connector Settings** under **Admin \-> Manage Add\-Ons**, as described in the Connector setup guide\. 

1. In **Admin**, **Projects**, open the project you want to use these fields\. 

1.  Choose the issue type you want to use in the menu at left\. 

1. Choose to view **Fields** in the top right \(if not already selected\)\. It should then show a list of fields enabled for the screen\. 

1.  Scroll to the bottom where there should be a textbox where you can enter additional fields\. Enter **AWS**, then choose the AWS field you want to use\. 

1.  Choose **Add** to apply\. 

1.  Repeat the previous step for the other field if you want to use it\. 

1.  Repeat these steps for each issue type you want to use these fields\. Some issue types might share screens so the field might already be added for some\. 

 It is important also to make a note of the field ID for the field or fields you are using\. Choose ** Admin \-> Issues \-> Custom fields** and select **Configure** on each field\. 

Inspect the opened URL to see the numeric field ID\. It should be a 5\-digit number\. 

Alternatively, for any issue in a project where you've added the field \(following the instructions above\), the REST API at `/rest/api/2/issue/PRJ-1/editmeta` \(for example, `http://localhost:2990/jira/rest/api/2/issue/PRJ-1/editmeta`\) will include information on the fields\.

The REST API should contain an entry `customfield_#####: { ..., name: "AWS Config Linked Resources", ... }`, where `#####` is the numeric field ID\. 

 Once these fields are enabled for projects and issue types, use the Jira REST API to create or update issues with values for these fields\. You can use tools such as CloudWatch, AppDynamics, Jenkins, or a Systems Manager Automation Document \(provided in the next section\)\. 

The REST API endpoint to update an issue is `/rest/api/2/issue/issue-key` and the general schema to pass to set a value is as follows:

```
                        { "update": { 
        "customfield_field-ID": [ {
          "set": "value" 
        } ] 
    } }
```

 See the examples below, or for more information on the REST API, see [JIRA Developer Documentation : Updating an Issue through the JIRA REST APIs](https://developer.atlassian.com/server/jira/platform/updating-an-issue-via-the-jira-rest-apis-6848604/)\. 

## AWS Config Linked Resources<a name="jsd-config-linked-resources"></a>

The **AWS Config Linked Resources** field should be set to the JSON string representation of a list of objects \(maps\) corresponding to the linked resources, each with the following keys:
+  *resourceId*: the ID of the resource in AWS Config 
+  *resourceType*: the type of the resource in AWS Config 
+  *accountName*: the name or alias of the AWS account configured in Jira that should be used to access this resource 
+  *region*: the Region where AWS Config should be accessed to get information on this resource 

 For example, the following value would show information on the S3 bucket `my-bucket` in `eu-central-1`, using the account and end user credentials specified in Jira for the AWS account identified in Jira as `MyAccount1`: 

```
                    [ { "resourceId": "my-bucket", 
        "resourceType": "AWS::S3::Bucket", 
        "accountName": "MyAccount1", 
        "region": "eu-central-1" } ]
```

## AWS Systems Manager Automation Suggested Remediation<a name="jsd-sys-remediation"></a>

 The **AWS Systems Manager Automation Suggested Remediation **field should be set to the JSON string that represents a list of objects \(maps\) that correspond to the automation documents as remediations, each with the following keys: 
+  *documentName*: the name of the Systems Manager automation document 
+  *description*: a description of the remediation to display in Jira; this may be different to the document description in AWS and might explain why it is a good remediation for the issue where this is being set 
+  *accountName*: the name or alias of the AWS account configured in Jira that should be used to access this resource 
+  *region*: the Region where AWS Config should be accessed to get information on this resource 

 For example, the following value would suggest the `AWS-DisableS3BucketPublicReadWrite` automation document, with a description to show in Jira, to apply in `eu-central-1`, using the account and end\-user credentials that is specified in Jira for the AWS account identified in Jira as `MyAccount1`: 

```
                               [ { "documentName": "AWS-DisableS3BucketPublicReadWrite", 
        "description": "This will make the bucket private, resolving the issue.", 
        "accountName": "MyAccount1", 
        "region": "eu-central-1" } ]
```

**Scripting Field Creation**  
As an example, the following bash script using curl links the above\-noted resource to an issue and attaches a suggested remediation\. The values used below assume Jira is at *localhost:2990/jira* with login *admin:admin*, the issue is *PRJ\-1*, and the field IDs are 10011 \(AWS Config linked resources\) and 10010 \(suggested remediation\)\. These should be changed to reflect your environment\.

1. Set the following to correspond to your environment and issue:

   JIRA\_BASE\_URL=http://localhost:2990/jira

   JIRA\_USER\_PASS=admin:admin

   ISSUE\_KEY=PRJ\-1

1. Set the field ID and edit the JSON record for an AWS Config resource to link\.

   ```
                             CUSTOM_FIELD_ID=customfield_10011
   cat > value.json  EOF
       [ { "resourceId": "my-bucket", 
           "resourceType": "AWS::S3::Bucket", 
           "accountName": "MyAccount1", 
           "region": "eu-central-1" } ]
   EOF
   ```

1.  Define a helper function to escape the JSON\. 

   ```
                           json_escape () { 
       printf '%s' "$1" | python -c \
         'import json,sys; print(json.dumps(sys.stdin.read()))'
   }
   ```

1.  Make the REST call to set the AWS Config Linked Resource field\. 

   ```
                           curl -v -D- -X PUT  -H "Content-Type: application/json" \
     --data '{ "update": { "'${CUSTOM_FIELD_ID}'": [ {"set": '"$(
        json_escape "$(cat value.json)")"' } ] } }' \
     -u admin:admin ${JIRA_BASE_URL}/rest/api/2/issue/${ISSUE_KEY}
   ```

1. Set the field ID and edit the JSON record for a suggested remediation to attach\.

   ```
                           CUSTOM_FIELD_ID=customfield_10010
   cat > value.json  EOF
       [ { "documentName": "AWS-DisableS3BucketPublicReadWrite", 
           "description": "This will make the bucket private, resolving the issue.", 
           "accountName": "MyAccount1", 
           "region": "eu-central-1" } ]
   EOF
   ```

1.  Make the REST call to set the **AWS Systems Manager Automation Suggested Remediations** field\.

   ```
                           curl -v -D- -X PUT  -H "Content-Type: application/json" \
     --data '{ "update": { "'${CUSTOM_FIELD_ID}'": [ {"set": '"$(
        json_escape "$(cat value.json)")"' } ] } }' \
     -u ${JIRA_USER_PASS} ${JIRA_BASE_URL}/rest/api/2/issue/${ISSUE_KEY}
   ```

The issue should then show AWS Config for the bucket and a suggested remediation to make it private\.

## Creating Issues with Suggestions and a Linked AWS Resource from AWS Systems Manager<a name="jsd-create-issues-linked-resource"></a>

 A Systems Manager Automation Document can automatically create a Jira issue with the fields set to have a linked AWS resource and up to three suggested remediation documents\. 

To install this automation document, download and extract the [JSM Connector Create Remediation Issue Automation and IT Lifecycle Demo\.zip](https://servicecatalogconnector.s3.amazonaws.com/JSDConnector-create-remediation-issue-automation-and-it-lifecycle-demo.zip) that contains two files: 
+ *JSMConnector\-CreateRemediationIssue\.ssmdoc\.yaml*
+ *JSMConnector\-function\.zip*

**Follow these steps**

1. Upload the file *JSMConnector\-function\.zip* to a bucket\. In the following command, replace $\{BUCKET\} with the appropriate bucket:

   ```
   aws s3 cp JSMConnector-function.zip s3://${BUCKET}/function.zip
   ```

1. Create the Systems Manager Automation Document, called **JSMConnector\-CreateRemediationIssue**, with the contents from the file *JSMConnector\-CreateRemediationIssue\.ssmdoc\.yam*l and an attachment *Key=SourceUrl,Values=s3://$\{BUCKET\}/*, using the bucket name from the previous step as $\{BUCKET\}\. The following command replaces $\{BUCKET\}\):

   ```
   aws ssm create-document --name "JSMConnector-CreateRemediationIssue" --content "file://JSMConnector-CreateRemediationIssue.ssmdoc.yaml" --document-type "Automation" --document-format "YAML" --attachments "Key=SourceUrl,Values=s3://${BUCKET}/" 
   ```

Once installed, enter the parameters and run it\. Note that it requires many of the same parameters, as described previously to connect to Jira\. 

 You should then see an issue in Jira with AWS Config information and the suggested remediation shown\. 

## Sample Use Case: Automatically Creating Issues for IT Lifecycle Management \- Remediating non\-compliant public S3 buckets<a name="jsd-sample"></a>

 Once you enable the fields to an issue and create the Systems Manager Automation Document, you can set up rules to automatically create Jira issues for common problem categories in AWS\. You can also include suggested remediations to make it easy for Jira agents and end users to see problems and fix them\. 

This demo creates a Config Rule in AWS, which detects public S3 buckets and makes it possible for Jira agents or end users to disable public access directly from Jira\.

You should set up prerequisites, roles for the automation and lambda to execute, and the Jira password as a secure string in Systems Manager Parameter Store\.

**To store the Jira password securely in Parameter Store**

1. Open the AWS Console and go to **Systems Manager \-> Parameter Store**\.

1. Choose **Create parameter**\.

1. Set the name as **jira\_password**\.

1. Set the type as **SecureString**\.

1. Set the value as the password for the Jira user to create issues\.

1. To save, choose **Create parameter**\.

An AWS CloudFormation template assists setting up the role and configuration rule: ****JSMConnector\-CreateRemediationIssue\-MakePublicBucketsPrivateConfigRule\.cfn\.yaml****

Install the template, setting the following parameters:
+ **JiraURL**: the base URL to your Jira, such that appending* /rest/\.\.*\. after it accesses the REST API
+ **JiraUsername**: the username to log in to Jira \(with the password specified in *jira\_password*\) 
+ **SSMParameterName**: *jira\_password* \(the parameter containing the Jira password\)
+ **ProjectKey**: the key of the project \(the token before the *\-n an issue*\), such as *PRJ*\. 
+ **IssueTypeName**: must exactly match the name of the issue type on the project in Jira
+ **JiraAwsAccountName**: the name of the AWS Account as configured in the Connector in Jira
+ **JiraAwsAccountRegion**: the Region of this violating resource, e\.g\. *us\-east\-1*
+ **JiraAwsResourceFieldId**: the field ID of the AWS Config Linked Resources field in Jira, such as *customfield\_10011*\.
+ **JiraRemediationsFieldId**: the field ID of the **AWS Systems Manager Automation Suggested Remediation** field in Jira, such as *customfield\_10010*\. 

 The Config Rule runs automatically within the period specified\. To see it in action immediately: 

1. Create a public Amazon S3 bucket\. 

1. Open the Config Rule in AWS Config and choose **Re\-evaluate**\. The rule and the automation can take a short while to run, but within a few minutes you should see a new issue in Jira with AWS Config information for the bucket, which is in violation and suggests the **DisableS3BucketPublicReadWrite** automation document as a remediation\.
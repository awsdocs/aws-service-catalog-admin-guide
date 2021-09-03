# Version 2\.3\.4 release transition instructions<a name="transition-instructions"></a>

Previous versions of the AWS Service Catalog Connector for ServiceNow are not fully compatible with major release v3\.7\.1 due to:
+  Streamlining the AWS Account configuration in the ServiceNow scoped app 
+  Removing the dependency of ServiceNow roles mapping to AWS identities\. 

Because of this, customers with previous versions \(v2\.3\.4 and on\) of the AWS Service Catalog Connector in the ServiceNow production environments must plan to transition to version 3\.7\.1 \.

## Major changes in version 3\.7\.1<a name="major-version-changes"></a>

The AWS Service Management Connector for ServiceNow v3\.7\.1 includes:
+  Adding AWS Config and AWS Systems Manager integration features to the Connector\. 
+  Streamlining the Connector Scoped App to six modules \(Getting Started, Setup, AWS Service Catalog, AWS Config, AWS Systems Manager and AWS Security Hub\.\)

The AWS Service Management Connector for ServiceNow v3\.7\.1 no longer includes:
+  Identities and Role Grants modules in the Connector Scoped app\. 
+  Previously provisioned AWS Service Catalog products details in the Connector scoped app\. 
**Note**  
The provisioned products details are still visible within AWS Service Catalog for the customer’s AWS account\. These details are no longer available in the ServiceNow Connector scoped app since we mapped these products based on ServiceNow user role grants as opposed to the new mapping to ServiceNow groups\.

## V2\.3\.4 Version sunset support and transition to 3\.7\.1<a name="sunset-transition"></a>

To provide customers time to plan and transition:
+  AWS will support AWS Service Catalog Connector version 2\.3\.4 until December 31, 2021\. Email aws\-sm\-connector\-issues@amazon\.com if you have any questions\. 
+  [Documentation for v2\.3\.4](https://servicecatalogconnector.s3.amazonaws.com/Connector+for+ServiceNow+v2.3.4.zip) is available\. You must download and extract the zip file\. 

## Transition recommendations<a name="transition-recommendations"></a>

To transition to AWS Service Management Connector version 3\.7\.1 from a ServiceNow Production environment:
+  Install the AWS Service Management Connector in a ServiceNow sandbox instance\. 
+  Follow the AWS Service Management Connector installation instructions starting at [Baseline permissions](baseline-permissions.md)\. 
**Note**  
 There is a known issue with committing update sets that have a previous version of the Connector installed\. Previewing the update set is successful\. However, at the conclusion of the committing update, an error appears that states: “Version loading was stopped by DictionaryUpdateLoader…\.” We consider these errors as false positives after further testing that there is not impact on the update set\. AWS is logging a ServiceNow support case and provides a new release if needed\. 
+  Compare the two versions to plan how you move through your ServiceNow Development\. 
+  Determine how you want to address AWS Service Catalog provisioned products in previous releases\. 
+  Create a check list of all your transition action items that include but are not limited to: 
  + Transition plan
    +  Decision point on AWS Service Catalog provisioned products\. 
    +  Steps to update/install Connector in ServiceNow Development to Production environments\. 
  +  ServiceNow platform admin communications 
  +  End user communications 
# Creating StackSet Constraints<a name="stackset-constraints"></a>

**To apply a stack set constraint to an AWS Service Catalog product**

1. Go to AWS Service Catalog as a catalog admin

1. Choose the portfolio that contains the product\.

1. Expand **Constraints** and choose **Add constraints**\.

1. Choose the product from **Product** and set **Constraint type** to **Stack Set**\. Choose **Continue**\.

1. On the **Stack Set constraint page**, enter a description\.

1. Choose the account\(s\) in which you want to create products\.

1. Choose the region\(s\) in which you want to deploy products\. Products are deployed in these regions in the order that you specify\.

1. Choose the **AWSCloudFormationStackSetAdministrationRole** role that will be used to manage your target accounts\.

1. Choose the **AWSCloudFormationStackSetExecutionRole** role that the Administrator Role will assume\.

1. Choose **Submit**\.

Note that the [Connector for ServiceNow\-AWS Configuration](https://s3.amazonaws.com/servicecatalogconnector/SC_ConnectorForServiceNowv2.0.2-AWS_Configurations.yml) template creates the permissions as well as outputs needed for StackSet constraints\. Example StackSet outputs: 

```
            SCStackSetAdministratorRoleARN 
            arn:aws:iam::123456789123:role/AWSCloudFormationStackSetAdministrationRole SCIAMStackSetExecutionRoleName 
            AWSCloudFormationStackSetExecutionRole  
            SCIAMAdminRoleARN 
            arn:aws:iam::123456789123:role/AWSCloudFormationStackSetAdministrationRole
```

**Note**  
Replace the **123456789123** with your account information\.
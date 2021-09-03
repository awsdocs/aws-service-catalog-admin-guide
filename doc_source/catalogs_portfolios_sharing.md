# Sharing and Importing Portfolios<a name="catalogs_portfolios_sharing"></a>

**Topics**
+ [Relationship Between Shared and Imported Portfolios](#shared-imported-portfolios-relationship)

To make your AWS Service Catalog products available to users who are not in your AWS account, such as users who belong to other organizations or to other AWS accounts in your organization, you share your portfolios with them\. You can share in several ways, including account\-to\-account sharing, organizational sharing, and deploying catalogs using stack sets\.

 Before you share your products and portfolios to other accounts, you must decide whether you want to share a reference of the catalog or to deploy a copy of the catalog into each recipient account\. Note that if you deploy a copy, you must redeploy if there are updates you want to propagate to the recipient accounts\. 

You can use stack sets to deploy your catalog to many accounts at the same time\. If you want to share a reference \(an imported version of your portfolio that stays in sync with the original\), you can use account\-to\-account sharing or you can share using AWS Organizations\. 

If you want to use stack sets to deploy a copy of your catalog, see [How to set up a multi\-region, multi\-account catalog of company standard AWS Service Catalog products](http://aws.amazon.com/blogs/mt/how-to-set-up-a-multi-region-multi-account-catalog-of-company-standard-aws-service-catalog-products/)\.

When you share a portfolio using account\-to\-account sharing or AWS Organizations, you allow an AWS Service Catalog administrator of another AWS account to import your portfolio into his or her account and distribute the products to end users in that account\. 

This *imported portfolio* isn't an independent copy\. The products and constraints in the imported portfolio stay in sync with changes that you make to the *shared portfolio*, the original portfolio that you shared\. The *recipient administrator*, the administrator with whom you share a portfolio, cannot change the products or constraints, but can add AWS Identity and Access Management \(IAM\) access for end users\. For more information, see [Granting Access to Users](catalogs_portfolios_users.md)\.

The recipient administrator can distribute the products to end users who belong to his or her AWS account in the following ways:
+ By adding IAM users, groups, and roles to the imported portfolio\.
+ By adding products from the imported portfolio to a *local portfolio*, a separate portfolio that the recipient administrator creates and that belongs to his or her AWS account\. The recipient administrator then adds IAM users, groups, and roles to the local portfolio\. The constraints that you applied to the products in the shared portfolio are also present in the local portfolio\. The recipient administrator can add additional constraints to the local portfolio, but cannot remove the imported constraints\.

When you add products or constraints to the shared portfolio or remove products or constraints from it, the change propagates to all imported instances of the portfolio\. For example, if you remove a product from the shared portfolio, that product is also removed from the imported portfolio\. It is also removed from all local portfolios that the imported product was added to\. If an end user launched a product before you removed it, the end user's provisioned product continues to run, but the product becomes unavailable for future launches\.

If you apply a launch constraint to a product in a shared portfolio, it propagates to all imported instances of the product\. To override this launch constraint, the recipient administrator adds the product to a local portfolio and then applies a different launch constraint to it\. The launch constraint that is in effect sets a launch role for the product\. 

A *launch role* is an IAM role that AWS Service Catalog uses to provision AWS resources \(such as EC2 instances or RDS databases\) when an end user launches the product\. As an administrator you can choose to designate a specific launch role ARN or a local role name\. If you use the role ARN, the role will be used even if the end user belongs to a different AWS account than the one that owns the launch role\. If you use a local role name, the IAM role with that name in the end user's account will be used\. 

For more information about launch constraints and launch roles, see [AWS Service Catalog Launch Constraints](constraints-launch.md)\. The AWS account that owns the launch role provisions the AWS resources, and this account incurs the usage charges for those resources\. For more information, see [AWS Service Catalog Pricing](https://aws.amazon.com/servicecatalog/pricing/)\.

This video shows you how to share portfolios across accounts in AWS Service Catalog\.

**Note**  
You cannot re\-share products from a portfolio that has been imported or shared\. 

**Note**  
Portfolio imports must occur in the same region between the management and dependent accounts\. 

## Relationship Between Shared and Imported Portfolios<a name="shared-imported-portfolios-relationship"></a>

This table summarizes the relationship between an imported portfolio and a shared portfolio, and the actions that an administrator who imports a portfolio can and can't take with that portfolio and the products in it\.


| Element of Shared Portfolio | Relationship to Imported Portfolio | Recipient Administrator Can | Recipient Administrator Cannot | 
| --- | --- | --- | --- | 
| Products and product versions |  Inherited\. If the portfolio creator adds products to or removes products from the shared portfolio, the change propagates to the imported portfolio\.  |  Add imported products to local portfolios\. Products stay in sync with shared portfolio\.  |  Upload or add products to the imported portfolio or remove products from the imported portfolio\.  | 
| Launch constraints |  Inherited\. If the portfolio creator adds launch constraints to or removes launch constraints from a shared product, the change propagates to all imported instances of the product\. If the recipient administrator adds an imported product to a local portfolio, the imported launch constraint that is applied to that product is present in the local portfolio\.  |   In a local portfolio, the administrator can override the imported launch constraint by applying a different one to the product\.  |  Add launch constraints to or remove launch constraints from the imported portfolio\.  | 
| Template constraints |  Inherited\. If the portfolio creator adds a template constraint to or removes a template constraints from a shared product, the change propagates to all imported instances of the product\. If the recipient administrator adds an imported product to a local portfolio, the imported template constraints that are applied to that product are inherited by the local portfolio\.   |  In a local portfolio, the administrator can add template constraints that take effect in addition to the imported constraints\.  |  Remove the imported template constraints\.  | 
| IAM users, groups, and roles | Not inherited\. | Add IAM users, groups, and roles that are in administrator's AWS account\. | Not applicable\. | 
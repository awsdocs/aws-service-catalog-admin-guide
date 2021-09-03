# Sharing a Portfolio<a name="catalogs_portfolios_sharing_how-to-share"></a>

To enable an AWS Service Catalog administrator for another AWS account to distribute your products to end users, share your AWS Service Catalog portfolio with them using either account\-to\-account sharing or AWS Organizations\.

 When you share a portfolio using account\-to\-account sharing or Organizations, you are sharing a *reference* of that portfolio\. The products and constraints in the imported portfolio stay in sync with changes that you make to the *shared portfolio*, the original portfolio that you shared\. 

The recipient cannot change the products or constraints, but can add AWS Identity and Access Management \(IAM\) access for end users\. 

**Note**  
 You can't share a shared resource\. This includes portfolios that contain a shared product\. 

## Account\-to\-account sharing<a name="portfolio-sharing-account"></a>

To complete these steps, you must obtain the account ID of the target AWS account\. You can find the ID on the **My Account** page in the AWS Management Console of the target account\.

**To share a portfolio with an AWS account**

1. Open the AWS Service Catalog console at [https://console\.aws\.amazon\.com/servicecatalog/](https://console.aws.amazon.com/servicecatalog/)\.

1. In the left navigation menu, choose **Portfolios**, select the portfolio you want to share, then choose **Actions**, and **Share**\.

1. Select the portfolio you want to share\. Then choose **Actions**, then **Share**\.

1. In **Enter AWS account ID**, enter the account ID of the AWS account that you are sharing with\. Then, choose **Share**\. 

1. Send the URL to the AWS Service Catalog administrator of the target account\. The URL opens the **Import Portfolio** page with the ARN of the shared portfolio automatically provided\.

### Importing a Portfolio<a name="catalogs_portfolios_sharing_importing"></a>

If an AWS Service Catalog administrator for another AWS account shares a portfolio with you, import that portfolio into your account so that you can distribute its products to your end users\.

To import the portfolio, you must get a URL to import the portfolio from the administrator\.

Open the URL\. In **Import Portfolio** , choose **Import**\. The **Portfolios** page appears, and the portfolio displays in the **Imported Portfolios** table\.

You don't need to import a portfolio if the portfolio was shared through AWS Organizations\.

## Sharing with AWS Organizations<a name="portfolio-sharing-organizations"></a>

You can share AWS Service Catalog portfolios using AWS Organizations\. 

First, you must decide if you're sharing from the management account or from a delegated administrator account\. If you don't want to share from your management account, register a delegated admin account and use it for sharing\. Next, you must decide who to share to\. You can share to the following entities: 
+ An organization account\.
+ An organizational unit \(OU\)\.
+ The organization itself\. \(This shares with every account in the organization\.\)

### Sharing from a management account<a name="sharing-from-master"></a>

You can share a portfolio with an organization when you use your organizational structure or input the ID of an organizational node\.

****To share a portfolio with an organization by using the organizational structure ****

1. Open the AWS Service Catalog console at [https://console\.aws\.amazon\.com/servicecatalog/](https://console.aws.amazon.com/servicecatalog/)\.

1. On the **Portfolios** page, select the portfolio that you want to share, then choose **Actions**, **Share**\.

1. Select **AWS Organization** and drill down into your organizational structure\. 

   You can select the Root node to share the portfolio with your entire organization, a parent Organizational Unit \(OU\), a child OU, or an AWS account within your organization\. 

   Sharing to a parent OU shares the portfolio to all accounts and child OU's within that parent OU\. 

   You can select **View AWS accounts only** to see a list of all of the AWS accounts in your organization\.

****To share a portfolio with an organization by entering the ID of the organizational node****

1. Open the AWS Service Catalog console at [https://console\.aws\.amazon\.com/servicecatalog/](https://console.aws.amazon.com/servicecatalog/)\.

1. On the **Portfolios** page, select the portfolio that you want to share, then choose **Actions**,** Share**\.

1. Select **Organization Node**\. 

   Select whether you want to share with your entire organization, an OU, or an AWS account within your organization\. 

   Input the ID of the organizational node you selected, which you can find within the AWS Organizations console at[ https://console\.aws\.amazon\.com/organizations/](https://console.aws.amazon.com/organizations/)\.

### Sharing from a delegated administrator account<a name="delegated-admin"></a>

 The management account of an organization can register and de\-register other accounts as delegated administrators for the organization\. 

A delegated administrator can share AWS Service Catalog resources in their organization the same way a management account can\. They are authorized to create, delete, and share portfolios, and more\. 

To register or de\-register a delegated administrator, you must use the API or CLI from the management account\. For more information, see [RegisterDelegatedAdministrator](https://docs.aws.amazon.com/organizations/latest/APIReference/API_RegisterDelegatedAdministrator.html) and [DeregisterDelegatedAdministrator](https://docs.aws.amazon.com/organizations/latest/APIReference/API_DeregisterDelegatedAdministrator.html) in the *AWS Organizations API Reference*\. 

**Note**  
Before you can designate a delegate , the administrator must call [EnableAWSOrganizationsAccess](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_EnableAWSOrganizationsAccess.html)\.

The procedure for sharing a portfolio from a delegated administrator account is the same as sharing from a management account, as seen above in [Sharing from a management account](#sharing-from-master)\.

 If a member is de\-registered as a delegated administrator, the following occurs: 
+ Portfolio shares that were created from that account are removed\.
+ They can no longer create new portfolio shares\.

**Note**  
 If the portfolio and shares created by a delegated administrator do not get removed after the delegated administrator is de\-registered, register and de\-register the delegated administrator again\. This action removes the portfolio and shares created by that account\. 

### Moving accounts within your organization<a name="move-account"></a>

If you move an account within your AWS Organization, the Service Catalog portfolios shared with the account might change\. 

Accounts only have access to portfolios shared with their destination organization or organizational unit\. 

## Sharing TagOptions when sharing portfolios<a name="tagoptions-share"></a>

As an administrator, you can create a share to include TagOptions\. TagOptions are key\-value pairs that enables administrators to:
+ Define and enforce the taxonomy for tags\.
+ Define tag options and associate them to products and portfolios\.
+ Share tag options associated with portfolios and products with other accounts\.

When you add or remove tag options in the main account, the change automatically appears in recipient accounts\. In recipient accounts, when an end user provisions a product with TagOptions, they must choose values for tags that become tags on the provisioned product\. 

In recipient accounts administrators can associate additional local TagOptions to their imported portfolio to enforce tagging rules that are specific to that account\.

**Note**  
To share a portfolio, you need the the consumer's AWS Account ID\. Find the AWS Account ID in **My Account **on the AWS console\.

**Note**  
If a TagOption has a single value, Amazon Service Catalog automatically enforces that value during the provisioning process\.

**To share TagOptions when sharing portfolios**

1. In the left navigation menu, choose **Portfolios**\.

1. In **Local portfolios**, choose and open a portfolio\.

1. Choose **Share** from the list above and then choose the **Share** button\.

1.  "SEA;IAD">Choose to share with another AWS account or AWS organization\.

1. Enter the 12 digit account ID number, select **Enable**, and then choose **Share**\.

   The account you shared displays in the **Accounts shared with** section\. It indicates whether TagOptions were enabled\.

You can also update a portfolio share to include TagOptions\. All TagOptions that belong to the portfolio and product now share to this account\.

**To update a portfolio share to include TagOptions**

1. In the left navigation menu, choose **Portfolios**\.

1. In **Local portfolio**, choose and open a portfolio\.

1. Choose **Share** from the list above\.

1. In **Accounts shared with**, choose an account ID and then choose **Actions**\.

1. Select **Update unshare** or **Unshare**\.

   When you select **Update unshare**, choose **Enable** to initiate sharing TagOptions\. The account you shared displays in the **Accounts shared with** section\.

   When you select **Unshare**, confirm you no longer want to share the account\.
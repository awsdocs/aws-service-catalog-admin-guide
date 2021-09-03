# Updating templates for provisioned products<a name="pp-templates"></a>

You can change the current template of a provisioned product to a different template\. For example if you have an EC2 product in Service Catalog, you can update that EC2 product to retain the same provisioned product ID, but change the template to a S3 bucket\.

**To update a template for a provisioned product**

1. In the left navigation menu, choose **Provisioned products**\.

1. In **Provisioned products**, choose a provisioned product and select **Actions**, **Update**\.

   Note that you can also select **Actions**, **Update** in the **Provisioned product details** page\.

1. In **Product details**, choose **Change product**\.

   In **Change product**, note this warning:

   *Changing the product will update this provisioned product to a different product template\. This may terminate resources and create new resources\.*

1. In **Products**, choose the product you want to update with a different template\. Then choose **Change**\.

   In **Product details**, note this warning:

   *\[Product name\] will be updated from \[current template name\] to \[new template name\]\. However, the name of your provisioned product, \[Product name\], will not change\.*

1. In **Product versions**, choose the version of the product you want\.

1. In **Parameters**, choose the appropriate parameters\.

1. Choose **Update**\.

   In **Provisioned product details**, you can see the details of the update\. The product name does not change, but the product now has a different template\. 
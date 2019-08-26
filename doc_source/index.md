# AWS Service Catalog Administrator Guide

-----
*****Copyright &copy; 2019 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What Is AWS Service Catalog?](introduction.md)
   + [Overview of AWS Service Catalog](what-is_concepts.md)
   + [AWS Service Catalog Default Service Limits](limits.md)
+ [Setting Up for AWS Service Catalog](setup.md)
   + [Grant Permissions to AWS Service Catalog Administrators](getstarted-iamadmin.md)
   + [Grant Permissions to AWS Service Catalog End Users](getstarted-iamenduser.md)
+ [Getting Started](getstarted.md)
   + [Step 1: Download the AWS CloudFormation Template](getstarted-template.md)
   + [Step 2: Create a Key Pair](getstarted-keypair.md)
   + [Step 3: Create an AWS Service Catalog Portfolio](getstarted-portfolio.md)
   + [Step 4: Create an AWS Service Catalog Product](getstarted-product.md)
   + [Step 5: Add a Template Constraint to Limit Instance Size](getstarted-constraint.md)
   + [Step 6: Add a Launch Constraint to Assign an IAM Role](getstarted-launchconstraint.md)
   + [Step 7: Grant End Users Access to the Portfolio](getstarted-deploy.md)
   + [Step 8: Test the End User Experience](getstarted-verify.md)
+ [Authentication and Access Control for AWS Service Catalog](controlling_access.md)
   + [Example Policies for Managing Provisioned Products](permissions-examples.md)
+ [Managing Catalogs](catalogs.md)
   + [Managing Portfolios](catalogs_portfolios.md)
      + [Creating and Deleting Portfolios](portfoliomgmt-create.md)
      + [Adding Products](portfoliomgmt-products.md)
      + [Adding Constraints](portfoliomgmt-constraints.md)
      + [Granting Access to Users](catalogs_portfolios_users.md)
   + [Managing Products](catalogs_products.md)
      + [Creating Products](productmgmt-cloudresource.md)
      + [Adding Products to Portfolios](catalogs_portfolios_adding-products.md)
      + [Updating Products](productmgmt-update.md)
      + [Deleting Products](productmgmt-delete.md)
   + [Using AWS Service Catalog Constraints](constraints.md)
      + [AWS Service Catalog Launch Constraints](constraints-launch.md)
      + [AWS Service Catalog Notification Constraints](constraints-notification.md)
      + [AWS Service Catalog Resource Update Constraints](constraints-resourceupdate.md)
      + [AWS Service Catalog Stack Set Constraints](constraints-stackset.md)
      + [AWS Service Catalog Template Constraints](catalogs_constraints_template-constraints.md)
         + [Template Constraint Rules](reference-template_constraint_rules.md)
         + [AWS Service Catalog Rule Functions](intrinsic-function-reference-rules.md)
   + [AWS Service Catalog Self-Service Actions](using-service-actions.md)
   + [Adding AWS Marketplace Products to Your Portfolio](catalogs_marketplace-products.md)
   + [Portfolio Sharing](catalogs_portfolios_sharing.md)
   + [Using AWS CloudFormation StackSets](using-stacksets.md)
+ [Managing Provisioned Products](provisioned-products.md)
   + [Managing All Provisioned Products as Administrator](provisioned-products-admin.md)
   + [Tutorial: Identifying User Resource Allocation](provisioned-products-tutorial.md)
+ [Managing Tags in AWS Service Catalog](managing-tags.md)
   + [AWS Service Catalog AutoTags](autotags.md)
   + [AWS Service Catalog TagOption Library](tagoptions.md)
      + [Launching a Product with TagOptions](tagoptions-launching.md)
      + [Managing TagOptions](tagoptions-manage.md)
+ [Monitoring AWS Service Catalog](service-catalog-monitoring.md)
   + [Monitoring Tools](monitoring-automated-manual.md)
   + [AWS Service Catalog CloudWatch Metrics](cloudwatch-metrics.md)
      + [Viewing AWS Service Catalog Metrics](viewing-cloudwatch-metrics.md)
+ [Product and Service Integrations with AWS Service Catalog](integrations.md)
   + [Connector for ServiceNow](integrations-servicenow.md)
      + [Baseline Permissions](baseline-permissions.md)
      + [Configure AWS Service Catalog](configure-sc.md)
      + [Creating StackSet Constraints](stackset-constraints.md)
      + [Configure ServiceNow](configure-snow.md)
      + [Validate Configurations](validate-configurations.md)
      + [ServiceNow Additional Administrator Features](additional-configurations.md)
      + [Upgrade Instructions](upgrade-instructions.md)
+ [Document History](history.md)
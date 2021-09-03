# AWSServiceCatalogAppRegistryFullAccess<a name="full"></a>

You can use the `AWSServiceCatalogAppRegistryFullAccess` AWS managed policy to allow your administrators to access AWS Service Catalog AppRegistry\.

This policy adds AWS CloudFormation permissions to update the AWS CloudFormation stack\. AWS Service Catalog AppRegistry needs to perform this action to tag the AWS CloudFormation stacks for SyncResource\.

 AWS Service Catalog AppRegistry adds these actions:
+ [https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_GetAssociatedResource.html](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_GetAssociatedResource.html)
+ [https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_ListTagsForResource.html](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_ListTagsForResource.html)
+ [https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_UntagResource.html](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_UntagResource.html)
+ [https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_TagResource.html](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_TagResource.html)
+ [https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_SyncResource.html](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_SyncResource.html)

This update occurs with the general release of Resource Groups\.

You can link to this policy in the IAM console or include the JSON policy document in your documentation\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "cloudformation:UpdateStack"
            ],
            "Resource": "*",
            "Condition": {
                "ForAnyValue:StringEquals": {
                    "aws:CalledVia": "servicecatalog-appregistry.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": "iam:CreateServiceLinkedRole",
            "Resource": "arn:aws:iam::*:role/aws-service-role/servicecatalog-appregistry.amazonaws.com/AWSServiceRoleForAWSServiceCatalogAppRegistry*",
            "Condition": {
                "StringEquals": {
                    "iam:AWSServiceName": "servicecatalog-appregistry.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "cloudformation:DescribeStacks",
                "servicecatalog:CreateApplication",
                "servicecatalog:GetApplication",
                "servicecatalog:UpdateApplication",
                "servicecatalog:DeleteApplication",
                "servicecatalog:ListApplications",
                "servicecatalog:AssociateResource",
                "servicecatalog:DisassociateResource",
                "servicecatalog:GetAssociatedResource",
                "servicecatalog:ListAssociatedResources",
                "servicecatalog:AssociateAttributeGroup",
                "servicecatalog:DisassociateAttributeGroup",
                "servicecatalog:ListAssociatedAttributeGroups",
                "servicecatalog:CreateAttributeGroup",
                "servicecatalog:UpdateAttributeGroup",
                "servicecatalog:DeleteAttributeGroup",
                "servicecatalog:GetAttributeGroup",
                "servicecatalog:ListAttributeGroups",
                "servicecatalog:SyncResource"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "servicecatalog:ListTagsForResource",
                "servicecatalog:UntagResource",
                "servicecatalog:TagResource"
            ],
            "Resource": "arn:aws:servicecatalog:*:*:*"
        }
    ]
}
```
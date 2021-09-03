# AWSServiceCatalogAppRegistryReadOnlyAccess<a name="read-only"></a>

You can use the `AWSServiceCatalogAppRegistryReadOnlyAccess` AWS managed policy to allow read\-only access to AWS Service Catalog AppRegistry\.

AWS Service Catalog AppRegistry adds these actions:
+ [https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_GetAssociatedResource.html](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_GetAssociatedResource.html) 
+ [https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_ListTagsForResource.html](https://docs.aws.amazon.com/servicecatalog/latest/dg/API_app-registry_ListTagsForResource.html)

This update occurs with the general release of Resource Groups\.

You can link to this policy in the IAM console or include the JSON policy document in your documentation\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "servicecatalog:GetApplication",
                "servicecatalog:ListApplications",
                "servicecatalog:GetAssociatedResource",
                "servicecatalog:ListAssociatedResources",
                "servicecatalog:ListAssociatedAttributeGroups",
                "servicecatalog:GetAttributeGroup",
                "servicecatalog:ListAttributeGroups",
                "servicecatalog:ListTagsForResource"
            ],
            "Resource": "*"
        }
    ]
}
```
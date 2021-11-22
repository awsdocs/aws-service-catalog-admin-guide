# Step 7: Grant End Users Access to the Portfolio<a name="getstarted-deploy"></a>

Now that you have created a portfolio and added a product, you are ready to grant access to end users\.

**Prerequisites**  
If you haven't created an IAM group for the endusers, see [Grant Permissions to AWS Service Catalog End Users](getstarted-iamenduser.md)\.

**To provide access to the portfolio**

1. On the portfolio details page, choose the **Groups, roles, and users** tab\.

1. Choose **Add groups, roles, users**\.

1. On the **Groups** tab, select the checkbox for the IAM group for the end users\.

1. Choose **Add Access**\.

**Working with launch roles and launch constraints**

When you configure a launch role for a launch constraint, you must use this string for `s3:GetObject`:

`"s3:ExistingObjectTag/servicecatalog:provisioning":"true"`.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "s3:ExistingObjectTag/servicecatalog:provisioning": "true"
                }
            }
        }
    ]
}
```




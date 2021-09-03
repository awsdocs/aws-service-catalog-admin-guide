# Step 8: Test the End User Experience<a name="getstarted-verify"></a>

To verify the end user can successfully access the end user console view and launch your product, sign in to AWS as the end user and perform those tasks\.

**To verify that the end user can access the end user console**

1. To sign in as the IAM user, use the account\-specific URL\. To find this URL, open the IAM console, choose **Dashboard** in the navigation pane, and choose **Copy to clipboard\.** Paste the link in your browser, and use the name and password of the IAM user\.

1.  In the menu bar, choose the AWS Region in which you created the `Engineering Tools` portfolio\. For this tutorial, choose **us\-east\-1 region**\.

1. Choose **Service Catalog** from the recently used services to see:
   + **Products** – The products that the user can use\.
   + **Provisioned products** – The provisioned products that the user has launched\.

**To verify the end user can launch the Linux Desktop product**

Note that for this tutorial, choose** us\-east\-1 region**\.

1. In the **Products** section of the console, choose **Linux Desktop**\.

1. Choose **Launch product** to start the wizard that configures your product\.

1. On the **Launch: Linux Desktop** page, enter **Linux\-Desktop** for the provisioned product name\.

1. On the **Parameters** page, enter the following and choose **Next**:
   +  **Server size** – Choose **t2\.micro**\. 
   +  **Key pair** – Select the key pair that you created in [Step 2: Create a Key Pair](getstarted-keypair.md)\.
   +  **CIDR range** – Enter a valid CIDR range for the IP address to connect to the instance\. You can use the default value \(0\.0\.0\.0/0\) to allow access from any IP address, then your IP address, followed by **/32** to restrict access to your IP address only, or something in between\.

1. Choose **Launch** to launch the stack\. The console displays the stack details page for the Linux\-Desktop stack\. The initial status of the product is **Launching**\. It takes several minutes for AWS Service Catalog to launch the product\. To see the current status, refresh your browser\. After the product launches, the status is **Available**\.
# XDM implementation

{% hint style="warning" %}
The Adobe Experience Platform Edge mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more and get access to the materials for this tutorial.
{% endhint %}

## Prerequisites for this tutorial

* Access to Adobe Experience Platform
* Access to AEP Real-time Customer Profile
* Minimal Swift / Android development knowledge 
* Knowledge about the AEP Edge extension
* Completion of [Assignment 1 - AEP Edge extension setup and XDM usage](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/tutorials/tutorial-1-edge-extension-setup).

### Download the sample application

{% tabs %}
{% tab title="Android" %}

#### Java

Clone or download the Android Sample application from [https://github.com/adobe/aepsdk-sample-app-android/tree/beta-assignment-3](https://github.com/adobe/aepsdk-sample-app-android/tree/beta-assignment-3).

To get started, follow the steps described in [AEP SDK Sample App Android - Installation](https://github.com/adobe/aepsdk-sample-app-android/tree/beta-assignment-1#installation).
{% endtab %}

{% tab title="iOS" %}

#### Swift

Clone or download the iOS Swift Sample application from [https://github.com/adobe/aepsdk-sample-app-ios/tree/beta-assignment-3](https://github.com/adobe/aepsdk-sample-app-ios/tree/beta-assignment-3).

To get started, follow the steps described in [AEP SDK Sample App Swift - Installation](https://github.com/adobe/aepsdk-sample-app-ios/tree/beta-assignment-1#installation).
{% endtab %}
{% endtabs %}

### Set up the configuration

In [Adobe Experience Platform Launch](https://experience.adobe.com/launch), go to the **Environments** tab in the mobile property created in Assignment 1 and click on the Development![img](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Lf1Mc1caFdNCK_mBwhe%2F-Lf1N06T8hdv0-r5jPPN%2F-Lf1N3-ofPO9fLFT1edw%2Fscreen-shot-2018-10-18-at-11.22.17-am.png?generation=1558039279051937&alt=media)icon. Find the Environment File ID at the top and copy it.

Set the `LAUNCH_ENVIRONMENT_FILE_ID` to the copied Environment File ID in the `MainApp` \(Android\) / `AppDelegate` \(iOS\) class.

## Create schema and dataset for product reviews

1. In the browser, navigate to [Adobe Experience Platform](https://experience.adobe.com/platform) and login with your credentials.

2. Create an [XDM Schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-ui.html) as follows:

   * From the left panel, select Schemas

   * Click `Create schema`

   * Select `XDM Experience event`

   * Click the `+ Add` button to add mixins

     * Select `ExperienceEvent Environment Details` from the `Use existing mixin` section and click `Add mixin`.

   * Click the `+ Add` button to add mixins

     * Select `Create new mixin` and set the name `Product Review`, click `Add mixin`.

   * In the Schema structure, select the  `Product review` mixin and click on the top level `+`.

   * Start adding fields as follows:

     | Field name | Display name | Type    |
     | :--------- | :----------- | :------ |
     | productSku | Product SKU  | String  |
     | reviewText | Review Text  | String  |
     | rating     | Rating       | Integer |
     | reviewerId | Reviewer ID  | String  |

     * select the `reviewerId` and enable it for `Identity` , enable `Primary Identity` and select Identity namespace `Email`.

   * Set the name for this schema as `Product Reviews` and click `Save`.

![](../../../.gitbook/assets/xdm_product_review.png)

3. This schema is going to be used for Profiles in the next steps in this assigment. 

   - Click on the Schema name, then from the right panel enable the `Profile` toggle.

   - When the `Enable for Profile` pop-up is displayed, click `Enable`.

4. [Create a dataset from this schema](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/user-guide.html#schema).

## Send Product Review 

### Build Product Review XDM objects

For this exercise, implement the Product Review functionality in the sample application. Navigate to `EdgeViewController.swift (iOS)` / `EdgeTab.java (Android)` and implement the `sendProductReviewXdmEvent` function. 

Todo

### Override the default Dataset

Todo

### Implement IdentityMap

Todo

### Run the sample application

Run the sample app on a device or simulator in Xcode / Android Studio. Click on the `Edge` tab and start testing the Product Review implementation. 

1. Select a Product from the list.
2. In the `XDM Product Review Example` section:
   - Fill in the `Reviewer email` with a sample email address.
   - Select a rating for the selected product.
   - Write your comments.
   - Click `Submit Review`.
3. Repeat these steps multiple times to "collect" multiple reviews.

## View the Product reviews in Adobe Experience Platform

After using the sample demo application to send product reviews as XDM Experience Events, query the data in Adobe Experience Platform.

**Note:** It may take up to 15-20mins before the data is showing in Adobe Experience Platform.

Query the dataset which stores the commerce data by doing the following:

1. Log in to [https://experience.adobe.com/platform](https://experience.adobe.com/platform) using your Adobe credentials.

2. Select your Adobe Experience Cloud Organization to the organization ID used to configure the demo application.

3. On the navigation panel, under Data Management, select Datasets and click the dataset you created at the beginning of this tutorial. From the right panel, copy the `Table name` value.

4. From the left panel, select **Queries**.

5. Click the **Overview** tab, then click **Create query**.

6. In the text box, enter a SQL query against your dataset table. Here is an example:

   ```sql
   select * from paste_your_table_name_here 
       where eventType = 'product.review' LIMIT 10
   ```

7. Click the "Play" icon to run the query. The results will appear in the **Results** tab at the bottom.

## View the Real-time Customer Profile


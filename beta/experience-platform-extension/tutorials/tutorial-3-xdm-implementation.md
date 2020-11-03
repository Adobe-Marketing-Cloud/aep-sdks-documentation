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

Download the Android Sample application from [https://github.com/adobe/aepsdk-sample-app-android/tree/beta-assignment-3](https://github.com/adobe/aepsdk-sample-app-android/archive/beta-assignment-3.zip).

To get started, follow the steps described in [AEP SDK Sample App Android - Installation](https://github.com/adobe/aepsdk-sample-app-android/tree/beta-assignment-3#installation).
{% endtab %}

{% tab title="iOS" %}

#### Swift

Download the iOS Swift Sample application from [https://github.com/adobe/aepsdk-sample-app-ios/tree/beta-assignment-3](https://github.com/adobe/aepsdk-sample-app-ios/archive/beta-assignment-3.zip).

To get started, follow the steps described in [AEP SDK Sample App Swift - Installation](https://github.com/adobe/aepsdk-sample-app-ios/tree/beta-assignment-3#installation).
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

     | Field name | Display name | Type    | Required |
     | :--------- | :----------- | :------ | -------- |
     | productSku | Product SKU  | String  | Yes      |
     | reviewText | Review Text  | String  | No       |
     | rating     | Rating       | Integer | Yes      |
     | reviewerId | Reviewer ID  | String  | Yes      |

     * select the `reviewerId` and enable it for `Identity` , enable `Primary Identity` and select Identity namespace `Email`.

   * Set the name for this schema as `Product Reviews` and click `Save`.

![](../../../.gitbook/assets/xdm_product_review.png)

3. This schema is going to be used for Profiles in the next steps in this assigment. 

   - Click on the Schema name, then from the right panel enable the `Profile` toggle.

   - When the `Enable for Profile` pop-up is displayed, click `Enable`.

4. Create a dataset for this schema:

   - Click on `Datasets` from the left panel.
   - Click `Create dataset`.
   - Select `Create dataset from schema`.
   - Search for the `Product Reviews` schema and select it.
   - Click `Next`.
   - Name this dataset `Product Reviews`.
   - Click `Finish`.

5. To include this dataset for Real-time Customer profiles, enable this dataset for Profile:

   - Select the `Product Reviews` dataset created.
   - From the right panel, enable the `Profile` toggle.

## Send Product Review 

### Build XDM objects

For this exercise, implement the Product Review functionality in the sample application. Navigate to `EdgeViewController.swift (iOS)` / `EdgeTab.java (Android)` and implement the `sendProductReviewXdmEvent` function. 

1. Create the XDM Experience Event using the `XDM IdentityMap` containing the reviewer `Email` and the review information.

{% tabs %}
{% tab title="Android" %}

#### Java

```java
// TODO - Assignment 3
Map<String, Object> xdmData = new HashMap<String, Object>();

// 1. Add Email to the IdentityMap.
// Note: this app does not implement a logging system, so authenticatedState ambiguous is used
// in this case. The other authenticatedState values are: authenticated, loggedOut
Map<String, Object> identityMap = new HashMap<String, Object>();
identityMap.put("Email", new ArrayList<Object>() {{
  add(new HashMap<String, Object>() {{
    put("id", reviewerId);
    put("authenticatedState", "ambiguous");
  }});
}});
xdmData.put("identityMap", identityMap);

// 2. Add product review details in the custom mixin
// Note: use your _tenantId here as specified in the Product Reviews Schema in Adobe Experience Platform
xdmData.put("_tenantId", new HashMap<String, Object>() {{
	put("productSku", product.sku);
	put("rating", rating);
	put("reviewText", text);
  put("reviewerId", reviewerId);
}});
```

{% endtab %}

{% tab title="iOS" %}

#### Swift

```swift
// TODO - Assignment 3
var xdmData : [String: Any] = [:]

// 1. Add Email to the IdentityMap.
// Note: this app does not implement a logging system, so authenticatedState ambiguous is used
// in this case. The other authenticatedState values are: authenticated, loggedOut
xdmData["identityMap"] = ["Email": [["id": reviewerEmail,
                                     "authenticatedState": "ambiguous"]]]

// 2. Add product review details in the custom mixin
// Note: use your _tenantId here as specified in the Product Reviews Schema in Adobe Experience Platform
xdmData["_tenantId"] = ["productSku": products[productIndex].sku,
                         "rating": reviewRating,
                         "reviewText": reviewText,
                       	 "reviewerId": reviewerEmail]
```

{% endtab %}
{% endtabs %}

**Note:** when sending XDM data for custom mixins, use your **_tenantId** as shown in the Schema.

{% hint style="info" %}
Use the knowledge from Assignment 1 and connect to an Assurance Session to verify if the XDM data sent from the sample app is in the correct format.
{% endhint %}

### Override the default Dataset

2. Send the Experience Event using the AEP Edge extension and specify the dataset identifier for `Product Reviews`.

{% tabs %}
{% tab title="Android" %}

#### Java

```java
// 3. Send the XDM data using the Edge extension, by specifying Product Reviews Dataset identifiers as
// shown in Adobe Experience Platform
// Note: the Dataset identifier specified at Event level overrises the Experience Event Dataset specified in the
// Edge configuration in Adobe Launch
xdmData.put("eventType", "product.review");
ExperienceEvent event = new ExperienceEvent.Builder()
  .setXdmSchema(xdmData, "yourDatasetIdentifier")
  .build();
Edge.sendEvent(event, new EdgeCallback() {
  @Override
  public void onResponse(Map<String, Object> data) {
    Log.d("Send XDM Event", String.format("Received response for event 'product.review': %s", data));
  }
});
```

{% endtab %}

{% tab title="iOS" %}

#### Swift

```swift
// 3. Send the XDM data using the Edge extension, by specifying Product Reviews Dataset identifiers as
// shown in Adobe Experience Platform
// Note: the Dataset identifier specified at Event level overrises the Experience Event Dataset specified in the
// Edge configuration in Adobe Launch
xdmData["eventType"] = "product.review"
let experienceEvent =
ExperienceEvent(xdm: xdmData,
                data: nil,
                datasetIdentifier: "yourDatasetIdentifier")
Edge.sendEvent(experienceEvent: experienceEvent, responseHandler: nil)
```

{% endtab %}
{% endtabs %}

### Run the sample application

Run the sample app on a device or simulator in Xcode / Android Studio. Click on the `Edge` tab and start testing the Product Review implementation. 

1. Select a Product from the list.
2. In the `XDM Product Review Example` section:
   - Fill in the `Reviewer email` with a sample email address.
   - Add the rating for the selected product.
   - Write your comment.
   - Click `Submit Review`.
3. Repeat these steps multiple times to "collect" product reviews.

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

 The customer profile can be viewed in [Adobe Experience Platform UI](https://experience.adobe.com/platform).

1. Select `Profiles` from the left panel.
2. Click `Browse` and search for the email you sent from the sample app.
   - Select the `merge policy`: _xdm.context.profile Private graph Timestamp ordered
   - Select Email as the `Identity namespace`
   - For the `Identity value`, enter the same Email as you sent from the app.
   - Click on the Profile ID found in the table.
3. Inspect the Customer profile.
   - Notice that the client-side ECID and the Email(s) you sent in XDM format using the Edge extension are now displayed in the `Detail` view, under the `Linked identities` section, as well as in the `Attributes` view.
   - In the `Events` tab you can view the events sent to the dataset(s) enabled for Profile for the selected customer profile.

To learn more about Adobe Customer Profile, see [Identity Service overview](https://docs.adobe.com/content/help/en/experience-platform/identity/home.html) and [Identity namespace overview](https://docs.adobe.com/content/help/en/experience-platform/identity/namespaces.html).

## Extra credit: Create segment based on Identity Authentication State

Create a segment in [Adobe Experience Platform UI](https://experience.adobe.com/platform) for the customer profiles where Authenticated State equal Ambiguous.

1. Select `Segments` from the left panel.
2. Click `Create segment`.
3. Select `Events` -> `XDM Experience Event`-> `Identity Map` and drag the `Authenticated State` element in the `Start building segment section`.
4. Select `Include Identity Map` within `Email` where `Authenticated State` equals `Ambiguous`.
5. Set the name for this segment, for example `Users with email and authenticated state ambiguous`.
6. Click `Save`.
7. Once the segment is computed you can see how many users qualify for this segment.

For more details about Segmentation in Adobe Experience Platform, see the [Segment Builder user guide](https://docs.adobe.com/content/help/en/experience-platform/segmentation/ui/segment-builder.html).
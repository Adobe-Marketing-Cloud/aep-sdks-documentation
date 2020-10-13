# Tutorial 1 - AEP Edge extension setup and XDM usage

{% hint style="warning" %}
The Adobe Experience Platform Edge mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more and get access to the materials for this tutorial.
{% endhint %}

This tutorial illustrates how you may send XDM commerce events to Adobe Experience Platform via Experience Edge using the AEP Edge extension using a sample application. The application is provided in iOS \(Swift\) and Android as part of the beta welcome packet and  - please contact your beta manager for further details.
{% endhint %}

The demo mobile application has multiple tabs. For this exercise, the `AEP` and `Assurance` tabs will be used, demonstrating XDM commerce events in a mobile application.

## Prerequisites for this tutorial

- Access to Adobe Experience Platform
- Access to Adobe Experience Launch dashboard
- Access to Project Griffon
- Minimal Swift / Android development knowledge 
- General knowledge about the Adobe Experience Platform Mobile SDKs

## Setup the schema, dataset and environment identifier

Follow the step by step instructions in the [Generate Environment Identifier](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/experience-platform-setup) page.

## Setup the demo app

### Configure the Launch Mobile property

To configure a mobile property required for this tutorial, follow the steps in [Configure the Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/set-up-the-sdk#configure-the-adobe-experience-platform-mobile-sdk).

### Download the demo application and install the AEP mobile extensions

{% tabs %}
{% tab title="Android" %}

### Java

Follow the steps described in [AEP SDK Sample App Android](https://github.com/adobe/aepsdk-sample-app-android).

{% endtab %}

{% tab title="iOS" %}

### **Swift**

Follow the steps described in [AEP SDK Sample App Swift](https://github.com/adobe/aepsdk-sample-app-ios#swift).
{% endtab %}
{% endtabs %}

### Set up the configuration

In [Adobe Experience Platform Launch](https://experience.adobe.com/launch), go to the **Environments** tab in the mobile property created in the previous step (Configure the Adobe Experience Platform Mobile SDK) and click on the Development![img](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Lf1Mc1caFdNCK_mBwhe%2F-Lf1N06T8hdv0-r5jPPN%2F-Lf1N3-ofPO9fLFT1edw%2Fscreen-shot-2018-10-18-at-11.22.17-am.png?generation=1558039279051937&alt=media)icon. Find the Environment File ID at the top and copy it.

Set the  `LAUNCH_ENVIRONMENT_FILE_ID` to the copied Environment File ID in the `MainApp` (Android) / `AppDelegate` (iOS) class.

## Use the demo app

### AEP Edge extension and XDM objects

This application uses the AEP Edge extension for sending XDM formatted data to the Adobe Experience Edge Network and so to Adobe Experience Platform. The XDM data is modelled based on the XDM Schemas you have configured in Adobe Experience Platform.

The sample app includes automatically generated source classes for the XDM Objects that define the commerce mixin configured in the previous step. To explore these, check the `MobileSDKCommerceSchema`  class and its usages in `ExperiencePlatformViewController.swift (iOS)` / `PlatformTab.java (Android)`.

**Note:** If you would like to use more complex XDM Schemas for your application, the Mobile SDK team can help generating the XDM classes for your Android or Swift implementation similar with the ones used in the commerce example, so please contact your Adobe representative.

### Commerce events

Click on the AEP view/tab that demonstrates the Commerce mixin usage. In the `XDM Commerce Example` section there are two buttons:

- Add to cart
- Purchase

When the `Purchase` button is clicked a new XDM Commerce Purchase Experience event is created and sent to the Adobe Experience Edge Network. 

```json
"events" : [
    {
      "xdm" : {
        "_id" : "F6BB7EE3-C411-4597-A97F-36A49035DCED",
        "eventType" : "commerce.purchases",
        "timestamp" : "2020-10-09T00:18:18Z",
        "productListItems" : [
          {
            "quantity" : 1,
            "currencyCode" : "USD",
            "priceTotal" : 34.76,
            "SKU" : "SHOES123",
            "name" : "Shoes"
          },
          {
            "quantity" : 2,
            "currencyCode" : "USD",
            "priceTotal" : 30.6,
            "SKU" : "HAT567",
            "name" : "Hat"
          }
        ],
        "commerce" : {
          "order" : {
            "priceTotal" : 65.36,
            "currencyCode" : "USD",
            "payments" : [
              {
                "paymentAmount" : 65.36,
                "paymentType" : "Credit card"
              }
            ]
          },
          "purchases" : {
            "value" : 1
          }
        }
      }
    }
  ]
```

### Using AEP Assurance

AEP Assurance (also known as Project Griffon) is a product from Adobe to help you inspect, validate, and debug data collection and experiences for your mobile application. The demo app is already set up to use Adobe's AEP Assurance mobile extension, which allows you to view the events being sent through the AEP Mobile SDK.

1. To use AEP Assurance, follow the [Using Project Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon/using-project-griffon) instructions.

2. When asked for the **Base URL**, enter `sampleapp://` .

3. After starting an Assurance session from [https://experience.adobe.com/griffon](https://experience.adobe.com/griffon), click on the the Session Details button on the right corner of the Project Griffon page and copy the session link.

   **Note:** If you are using a real device, you can also use the `Scan QR Code` functionality. Then jump to step 6.

   ![](../../../.gitbook/assets/Commerce_Session_Details.png)

4. Go to the Sample application that is installed on your Android/iOS device or simulator, and click on the `Assurance` tab.

5. This will take you to the Assurance Connect Page. Paste the Assurance Session URL that you copied from [https://experience.adobe.com/griffon](https://experience.adobe.com/griffon), and click `Connect`.

   ![](../../../.gitbook/assets/Commerce_Griffon_Login.png)

6. Now, this will take you to the Assurance Connect Login Page. Enter the PIN from [https://experience.adobe.com/griffon](https://experience.adobe.com/griffon) and click `Connect`.

   ![](../../../.gitbook/assets/Commerce_Griffon_Connection.png)

7. Once connected to Assurance, you will see an AEP Icon in red color on the top right corner of the Product List Page. The color of this AEP Icon will become gray if the connectivity to Assurance server is lost for any reason. In this case, you want to reconnect to continue to see the session in the UI.

8. In the Assurance session, you should now start seeing events populating the Events List. When clicking the `Purchase` button from the `AEP` tab, you should see the Experience events sent to Experience Edge. For more details, refer to [Event types handled by the AEP Mobile extension](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/experience-platform-debugging).

### Queries in Adobe Experience Platform

After using the sample demo application to view products and checkout items in a cart, the XDM Experience Events containing the commerce data are sent to the Adobe Experience Platform through Experience Edge.

**Note:** It may take up to 15-20mins before the data is ingested in Experience Platform.

You can query the dataset which stores the data for your Schema by doing the following:

1. Log in to [https://experience.adobe.com/platform](https://experience.adobe.com/platform) using your Adobe credentials.

2. Select your Adobe Experience Cloud Organization to the organization ID used to configure the demo application.

3. On the navigation panel, under Data Management, select Datasets and select the Dataset you created at the beginning of this tutorial. From the right panel, copy the `Table name` value.

4. From the left panel, select **Queries**.

5. Click the **Overview** tab, then click **Create query**.

6. In the text box, enter a SQL query against your dataset table. Here is an example:

   ```sql
   select * from paste_your_table_name_here 
       where eventType = 'commerce.purchases' LIMIT 10
   ```

7. Click the "Play" icon in the top-left corner above the query text box to run the query. The results will appear in the **Results** tab in the bottom panel.

**Note:** you can save this query and run it later when needed.

### Implement Add to cart XDM events

For this exercise, implement the Add to cart functionality in the sample application. Navigate to `ExperiencePlatformViewController.swift (iOS)` / `PlatformTab.java (Android)` and implement the `sendAddToCartXDMEvent` function.

**Hint:** Use the `sendPurchaseXDMEvent` as an example and use Project Griffon to validate that the XDM Experience Event is propertly formatted. 

### Next steps

If you would like to explore other XDM Schemas for your mobile use-case, find more details in the [Adobe Experience Platform - Experience Edge](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension) page.


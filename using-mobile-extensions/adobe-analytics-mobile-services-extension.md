# Adobe Analytics - Mobile Services

This extension enables in-app messaging, push notifications, and marketing links functionality from Mobile Services on the Experience Platform SDKs.

{% hint style="info" %}
The following steps assume that you have previously created apps in Mobile Services \([mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)\).
{% endhint %}

To use the Mobile Services extension:

1. Configure and implement Core and Analytics extensions and APIs.
2. Configure the Adobe Analytics – Mobile Services Launch extension.
3. Implement Mobile Services extension and APIs in your app.

## Configure the Adobe Analytics – Mobile Services extension in Launch

1. In Launch, click the Extensions tab.
2. On the **Catalog** tab, locate the **Adobe Analytics – Mobile Services** extension, and click **Install**.
3. Select one of the following options:

    * **Choose a Mobile Services app** and complete the following tasks:
    
       a. In Mobile Services app, select app from the drop-down list.
  
       b. Click Save.
       
    * **Enter Custom settings** and complete the following tasks:
    
      a. Enter an Acquisition time out, recommended time out is 5 seconds.

      b. Provide the Acquisition App ID, for example, `0eb9f2791f0880623f91e41e5309d2ae25066e513054a4cb59168dc886b526da`.
 
      c. Provide the messages URL, for example, `https://assets.adobedtm.com/b213090c5204bf94318f4ef0539a38b487d10368/scripts/satellite-5c7711bc64746d7f5800036e.json`.

4. Click **Save**.
5. Follow the publishing process to update your SDK configuration.

## Configure the Adobe Analytics - Mobile Services extension

You can configure the extension in one of the following ways:

* By selecting your Mobile Services app

  


---
description: >-
  This step outlines the configuration & implementation of the mobile SDK along
  with the Experience Edge extension in your app.
---

# Implement Experience Edge Extension

{% hint style="warning" %}
The Adobe Experience Platform - Experience Edge - Mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more.
{% endhint %}

## Configure the Adobe Experience Platform Mobile SDK

As a pre-requisite, the Experience Edge extension requires the successful implementation of the Adobe Experience Platform Mobile SDK - [Mobile Core](../../using-mobile-extensions/mobile-core/). 

Experience Edge extension relies on the [Mobile Core](../../using-mobile-extensions/mobile-core/) for the transmission of events, managing identity \(ECID\), and triggering client-side rules based on XDM.

1. First, follow these steps to [Set up a mobile property](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) in Adobe Experience Platform Launch.

2. Install the Adobe Experience Platform extension from the Catalog. 

3. In the configuration view, select the `Edge Configuration` you created in the previous step (see [Generate Environment Identifier](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/experience-platform-setup)) and click `Save`.
4. Install the `AEP Assurance` extension from the Catalog. 

5. Go to the Publishing Flow menu, select the development library you created and click `Add All Changed Resources`. 
6. Click `Save & Build for Development` to publish the changes in the Development environment.

## Set up the Experience Edge extension

### Add Experience Platform extension to your app

You should have received the bundle containing the Android and Swift Experience Platform SDKs as part of the BETA welcome packet. In order to get started, reference the SDK in your mobile application as follows:

{% tabs %}
{% tab title="Android" %}
### Java

Follow the steps descried in [AEP SDK Sample App Android](https://github.com/adobe/aepsdk-sample-app-android).

{% endtab %}

{% tab title="iOS" %}
### **Swift**

Follow the steps described in [AEP SDK Sample App Swift](https://github.com/adobe/aepsdk-sample-app-ios#swift).

### Set up the configuration

In Experience Platform Launch, go to the **Environments** tab in the mobile property created in the previous step (Configure the Adobe Experience Platform Mobile SDK) and click on the Development![img](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Lf1Mc1caFdNCK_mBwhe%2F-Lf1N06T8hdv0-r5jPPN%2F-Lf1N3-ofPO9fLFT1edw%2Fscreen-shot-2018-10-18-at-11.22.17-am.png?generation=1558039279051937&alt=media)icon. Find the Environment File ID at the top and copy it.

Set the  `LAUNCH_ENVIRONMENT_FILE_ID` to the copied Environment File ID in the `MainApp` (Android) / `AppDelegate` (iOS) class.

### Register the extension

The `registerExtension` API registers the Experience Edge extension with Mobile Core. This API is required to initialize the Experience Edge extension in order to start sending/receiving events to/from and from the Experience Edge.

{% tabs %}
{% tab title="Android" %}

### Java

In the Application file's `onCreate()` method, initialize the Mobile Core and register the Experience Platform extension.

### Example

```java
public class ExperiencePlatformDemoApplication extends Application {
...
@Override
public void onCreate() {
    super.onCreate();
    MobileCore.setApplication(this);
    MobileCore.configureWithAppID(YOUR_APP_ID);

    try {
        // register Mobile Core extensions
        Identity.registerExtension();
        Signal.registerExtension();
        Lifecycle.registerExtension();

        // register the Experience Platform extension
        ExperiencePlatform.registerExtension();
       } catch (InvalidInitException e) {
         e.printStackTrace();
       }

    MobileCore.start(new AdobeCallback() {
        @Override
        public void call(final Object o) {
            Log.d(LOG_TAG, "Mobile SDK was initialized.");
        }
    });
}
...
}
```
{% endtab %}

{% tab title="iOS" %}
```swift
import UIKit
import ACPCore
import AEPExperiencePlatform

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        ACPCore.configure(withAppId: YOUR_APP_ID)

        // register Mobile Core extensions
        ACPIdentity.registerExtension()
        ACPLifecycle.registerExtension()
        ACPSignal.registerExtension()

        // register the Experience Platform extension
        ExperiencePlatform.registerExtension()
        let filePath = Bundle.main.path(forResource: "ADBMobileConfig", ofType: "json")
        ACPCore.configureWithFile(inPath: filePath)
        ACPCore.start({
            ACPCore.lifecycleStart(nil)
        })
        return true
    }
}
```
{% endtab %}
{% endtabs %}

## Send events to Experience Edge

After you create an [Experience event](experience-platform-events.md), use `sendEvent` to send this event to the Adobe solutions and Adobe Experience Platform. 

{% hint style="info" %}
To generate custom XDM classes for your Android or Swift implementation, please contact your beta manager. 
{% endhint %}

{% hint style="warning" %}
`experiencePlatformEvent (required)`should not be null.`responseCallback (optional)`callback may be invoked when the response handles are received from Experience Edge. It may be called on a different thread and may be invoked multiple times.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### **Java**

### **Syntax**

```java
public static void sendEvent(final ExperiencePlatformEvent experiencePlatformEvent, final ExperiencePlatformCallback responseCallback)
```

You may create an `ExperiencePlatformEvent` with XDM data as Map, by using the `setXdmSchema(final Map<String, Object> xdm, final String datasetIdentifier)` API from the `ExperiencePlatformEvent.Builder`.

### **Example \(commerce event\)**

```java
// Create the ExperiencePlatformEvent for your use case
final String eventType = "commerce.productListAdds";
MobileSDKPlatformEventSchema xdmData = new MobileSDKPlatformEventSchema();
xdmData.setEventType(eventType);
xdmData.setCommerce(commerce);
xdmData.setProductListItems(itemsList);

ExperiencePlatformEvent event = new ExperiencePlatformEvent.Builder()
    .setXdmSchema(xdmData)
    .build();

// Send the event to the Experience Platform extension
ExperiencePlatform.sendEvent(event, null);
```
{% endtab %}

{% tab title="iOS" %}
### **Swift**

### **Syntax**

```java
public static func sendEvent(experiencePlatformEvent: ExperiencePlatformEvent, responseHandler: ExperiencePlatformResponseHandler? = nil)
```

You may create an `ExperiencePlatformEvent` with XDM data as dictionary \(`[String: Any]`\) by using the the following method available in the `ExperiencePlatformEvent` struct.

```text
init(xdm: [String: Any], data: [String: Any]? = nil, datasetIdentifier: String? = nil)
```

### **Example \(commerce event\)**

```swift
// Create the ExperiencePlatformEvent for your use case
var productItem = ProductListItemsItem()
productItem.name = "red ball"
productItem.SKU  = "625-740"
productItem.currencyCode = "USD"
productItem.quantity     = 1
productItem.priceTotal   = 9.95

var itemsList: [ProductListItemsItem]
itemsList.append(productItem)  

var commerce = Commerce()
var productViews = ProductViews()
productViews.value = 1
commerce.productViews = productViews

var xdmData = MobileSDKPlatformEventSchema()
xdmData.eventType = "commerce.productListAdds"
xdmData.commerce = commerce
xdmData.productListItems = itemsList 

// Send the event to the Experience Platform extension
let event = ExperiencePlatformEvent(xdm:xdmData)
let responseHandler = ResponseHandler()
ACPExperiencePlatform.sendEvent(experiencePlatformEvent: event, responseHandler: responseHandler)
```
{% endtab %}
{% endtabs %}

## Retrieving data from Adobe solutions

As described in [Send events to Experience Edge](set-up-the-sdk.md#send-events-to-experience-edge), the server-side event handle comes in chunks to maximize performance.

To be notified when a response is returned, you may register a `responseCallback`\(Android\) or `responseHandler` \(iOS\) that is invoked when new data is available from the server. This callback is invoked for each event handle that is returned by the server and therefore, it may be be called multiple times.

{% hint style="info" %}
In Android, the event handle is represented by a `Map<String, Object>`.
{% endhint %}

Depending on the nature of the event and Adobe solutions you are using, you may receive one, several, or no event handles for an event transmitted.

{% tabs %}
{% tab title="Android" %}
### Java

### Example

```java
// Create the ExperiencePlatformEvent for your use case
...

// Send the event to the Experience Platform extension
ExperiencePlatform.sendEvent(event, new ExperiencePlatformCallback() {
    @Override
    public void onResponse(final Map<String, Object> data) {
        // TODO: handle the data received from the server
        Log.d(LOG_TAG, String.format("Received Data Platform response for event '%s': %s", eventType, data));
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### Swift

### Example

```swift
// Create the ExperiencePlatformEvent for your use case
...
// Send the event to the Experience Platform extension
ACPExperiencePlatform.sendEvent(experiencePlatformEvent: event, responseHandler: ResponseHandler())

// Handle the response from Experience Platform
class ResponseHandler : ExperiencePlatformResponseHandler {
    func onResponse(data: [String : Any]) {
        ACPCore.log(ACPMobileLogLevel.debug, tag:"ResponseHandler", message:"Platform response has been received...")
    }
}
```
{% endtab %}
{% endtabs %}

For more information on response & error response handling, see [Server response handling](response-handling.md).


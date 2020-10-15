---
description: >-
  This step outlines the configuration & implementation of the mobile SDK along
  with the Experience Edge extension in your app.
---

# Implement Adobe Experience Platform Edge Extension

{% hint style="warning" %}
The Adobe Experience Platform Edge mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more.
{% endhint %}

## Configure the Adobe Experience Platform Mobile SDK

As a pre-requisite, the AEP Edge extension requires the successful implementation of the Adobe Experience Platform Mobile SDK - [Mobile Core](../../using-mobile-extensions/mobile-core/). 

Experience Edge extension relies on the [Mobile Core](../../using-mobile-extensions/mobile-core/) for the transmission of events, managing identity \(ECID\), and triggering client-side rules based on XDM.

1. First, follow these steps to [Set up a mobile property](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) in Adobe Experience Platform Launch.

2. Install the `Adobe Experience Platform Edge` extension from the Catalog. 

3. In the configuration view, select the `Edge Configuration` you created in the previous step (see [Generate Environment Identifier](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/experience-platform-setup)) and click `Save`.
4. Install the `AEP Assurance` extension from the Catalog. 

5. Go to the Publishing Flow menu, select the development library you created and click `Add All Changed Resources`. 
6. Click `Save & Build for Development` to publish the changes in the Development environment.

## Set up the AEP Edge extension

### Add AEP Edge extension to your app

You should have received the bundle containing the Android and Swift AEP SDKs as part of the BETA welcome packet. In order to get started, reference the SDK in your mobile application by following the steps below:

{% tabs %}
{% tab title="Android" %}
### Java

Update the dependencies for your Android application in the gradle file.

```
dependencies {
    // Mobile SDK Core Bundle
    implementation 'com.adobe.marketing.mobile:userprofile:1.+'
    implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
    // AEP Edge SDK
    implementation 'com.adobe.marketing.mobile:edge:1.+'
    // Assurance SDK for debugging using Project Griffon
    implementation 'com.adobe.marketing.mobile:assurance:1.+'
    ...
}
```



{% endtab %}

{% tab title="iOS" %}
### **Swift**

Use Cocoapods for integrating with AEP Mobile SDK:

```
platform :ios, '10.0'

use_frameworks!
target 'YourAppTarget' do
  # Mobile SDK Core Bundle
  pod 'AEPServices', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPCore', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPLifecycle', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPIdentity', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPSignal', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPRulesEngine', :git => 'git@github.com:adobe/aepsdk-rulesengine-ios.git', :branch => 'main'
  
  # AEP Edge SDK
  pod 'AEPEdge', :git => 'git@github.com:adobe/aepsdk-edge-ios.git', :branch => 'master'
  
  # Assurance SDK for debugging using Project Griffon
  pod 'ACPCore', :git => 'git@github.com:adobe/aepsdk-compatibility-ios.git', :branch => 'main'
  pod 'AEPAssurance'
  ...
end
```

{% endtab %}

{% endtabs %}

### Set up the configuration

In Experience Platform Launch, go to the **Environments** tab in the mobile property created in the previous step (Configure the Adobe Experience Platform Mobile SDK) and click on the Development![img](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Lf1Mc1caFdNCK_mBwhe%2F-Lf1N06T8hdv0-r5jPPN%2F-Lf1N3-ofPO9fLFT1edw%2Fscreen-shot-2018-10-18-at-11.22.17-am.png?generation=1558039279051937&alt=media)icon. Find the Environment File ID at the top and copy it.

Replace `YOUR_APP_ID` with the copied Environment File ID when calling `configureWithAppID` as in the examples below.

### Register the extension

The `registerExtension` API registers the AEP Edge extension with Mobile Core. This API is required to initialize the AEP Edge extension in order to start sending/receiving events to/from and from the Experience Edge Network.

{% tabs %}
{% tab title="Android" %}

### Java

In the Application file's `onCreate()` method, initialize the Mobile Core and register the AEP Edge extension.

### Example

```java
public class AEPEdgeDemoApplication extends Application {
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

        // register the AEP Edge extension
        Edge.registerExtension();
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

### Swift

```swift
import UIKit
import AEPCore
import AEPEdge
import AEPIdentity
import AEPLifecycle
import AEPSignal

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.configureWith(appId: YOUR_APP_ID)

        // register Mobile Core and AEP Edge extensions
        MobileCore.registerExtensions([Edge.self, Identity.self, Lifecycle.self, Signal.self])
        
        return true
    }
}
```
{% endtab %}
{% endtabs %}

## Send events to Experience Edge

After you create an [Experience event](experience-platform-events.md), use the `sendEvent` API to send this event to the Adobe solutions and Adobe Experience Platform. 

Parameters:

- `experienceEvent (required)`should not be null.

- `responseCallback (optional)`callback is invoked when the response handles are received from Experience Edge. It may be called on a different thread and may be invoked multiple times.

{% tabs %}
{% tab title="Android" %}

### **Java**

### **Syntax**

```java
public static void sendEvent(final ExperienceEvent experienceEvent, final EdgeCallback responseCallback)
```

You may create an `ExperienceEvent` with XDM data as Map, by using the `setXdmSchema(final Map<String, Object> xdm, final String datasetIdentifier)` API from the `ExperienceEvent.Builder`.

### **Example \(commerce event\)**

```java
// Create the ExperienceEvent for your use case
final String eventType = "commerce.productListAdds";
MobileSDKPlatformEventSchema xdmData = new MobileSDKPlatformEventSchema();
xdmData.setEventType(eventType);
xdmData.setCommerce(commerce);
xdmData.setProductListItems(itemsList);

ExperienceEvent event = new ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .build();

// Send the event to the AEP Edge extension
Edge.sendEvent(event, null);
```
{% endtab %}

{% tab title="iOS" %}
### **Swift**

### **Syntax**

```swift
public static func sendEvent(experienceEvent: ExperienceEvent, responseHandler: EdgeResponseHandler? = nil)
```

You may create an `ExperienceEvent` with XDM data as dictionary \(`[String: Any]`\) by using the the following method available in the `ExperienceEvent` struct.

```swift
init(xdm: [String: Any], data: [String: Any]? = nil, datasetIdentifier: String? = nil)
```

### **Example \(commerce event\)**

```swift
// Create the ExperienceEvent for your use case
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

// Send the event to the AEP Edge extension
let event = ExperienceEvent(xdm:xdmData)
let responseHandler = EdgeResponseHandler()
Edge.sendEvent(experienceEvent: event, responseHandler: responseHandler)
```
{% endtab %}
{% endtabs %}

## Retrieving data from Adobe solutions

As described in [Send events to Experience Edge](set-up-the-sdk.md#send-events-to-experience-edge), the server-side event handle comes in chunks to maximize the performance.

To be notified when a response is returned, you may register a `EdgeCallback`\(Android\) or `EdgeResponseHandler` \(iOS\) that is invoked when new data is available from the server. This callback is invoked for each event handle that is returned by the server and therefore, it may be called multiple times.

{% hint style="info" %}
In Android, the event handle is represented by a `Map<String, Object>`.
{% endhint %}

Depending on the nature of the event and the Adobe solutions you are using, you may receive one, several, or no event handles for an event transmitted.

{% tabs %}
{% tab title="Android" %}
### Java

### Example

```java
// Create the ExperienceEvent for your use case
...

// Send the event to the AEP Edge extension
Edge.sendEvent(event, new EdgeCallback() {
    @Override
    public void onResponse(final Map<String, Object> data) {
        // TODO: handle the data received from the server
        Log.d(LOG_TAG, String.format("Received Edge response for event '%s': %s", eventType, data));
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### Swift

### Example

```swift
// Create the ExperienceEvent for your use case
...
// Send the event to the AEPEdge extension
Edge.sendEvent(experienceEvent: event, responseHandler: ResponseHandler())

// Handle the response received from the server
class ResponseHandler : EdgeResponseHandler {
    func onResponse(data: [String : Any]) {
        Log.debug(label:"ResponseHandler", "Received Edge response")
    }
}
```
{% endtab %}
{% endtabs %}

For more information on response & error response handling, see [Server response handling](response-handling.md).


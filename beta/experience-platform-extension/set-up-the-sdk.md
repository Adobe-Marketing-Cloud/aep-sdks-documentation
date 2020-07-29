---
description: >-
  This step outlines the configuration & implementation of the mobile SDK along
  with the Experience Edge extension in your app.
---

# Implement Experience Edge Extension

{% hint style="warning" %}
The Adobe Experience Platform - Experience Edge - Mobile extension is currently in beta. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more.
{% endhint %}

## Configure the Adobe Experience Platform Mobile SDK

As a pre-requisite, the Experience Edge extension requires the successful implementation of the Adobe Experience Platform Mobile SDK - [Mobile Core](../../using-mobile-extensions/mobile-core/). 

Experience Edge extension relies on the [Mobile Core](../../using-mobile-extensions/mobile-core/) for the transmission of events, managing identity \(ECID\), and triggering client-side rules based on XDM.

If your mobile application doesn't use the Adobe Experience Platform Mobile SDK, follow the steps listed in the Getting Started section of this site to [Set up a mobile property](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) and [Get the Experience Platform SDK](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) before you proceed with the steps below.

## Setup the Experience Edge extension

### Add Experience Platform extension to your app

You should have received the bundle containing the Android and Swift Experience Platform SDKs as part of your beta welcome packet. In order to get started, reference the SDK in your mobile application as follows:

{% tabs %}
{% tab title="Android" %}
### Java

1. Create a `libs` folder in your application directory \(ignore this step If you already have this folder\)
2. Copy the `*.aar` file from the bundle path `/Android/lib/` and paste it in the libs folder
3. Add the libs folder to the Gradle dependencies. 

### Example

```text
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.aar'])

    // Mobile SDK Core Bundle
    implementation 'com.adobe.marketing.mobile:userprofile:1.+'
    implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
    // Project Griffon for debugging
    implementation 'com.adobe.marketing.mobile:griffon:1.+'
    ...
}
```
{% endtab %}

{% tab title="iOS" %}
### **Swift**

1. Create a `libs` folder in your application directory. If you already have this folder, you can skip this step.
2. Copy the `*.a` file along with the `*.swiftmodule` folder from the bundle path `/iOS/lib/` and paste it in the libs folder.
3. In Xcode, add the new library to your project dependencies list. 
   * Select the mobile application Target and click on Build Phases.
   * In the Link Binary With Libraries tab, Add new \(+\).
   * Click Add Other -&gt; Add files, navigate to libs/ folder, select the \*.a file and click Open.
{% endtab %}
{% endtabs %}

### Setup configuration

In your application's assets folder, [configure a bundle configuration](../../using-mobile-extensions/mobile-core/configuration/#using-a-bundled-file-configuration) called `ADBMobileConfig.json` with the following content:

```text
{
  "experiencePlatform.configId": "CONFIG_ID"
}
```

{% hint style="warning" %}
Replace the CONFIG\_ID with the Experience Edge environment identifier created in the [Create an Experience Edge environment identifier](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/8bb3c402c0b73759dd5143d60051a20c4eda5d79/beta/experience-platform-setup/README.md#create-an-experience-edge-configuration-id) step. This identifier may be found [Adobe Experience Platform Launch](https://launch.adobe.com) under _Edge Configurations_.
{% endhint %}

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


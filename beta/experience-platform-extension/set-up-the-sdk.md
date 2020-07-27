# Setup Adobe Experience Platform Mobile SDK

In this section, we provide information to help you set up the SDK.

## Configure the Experience Platform extension

Before you can use the SDK, you must first set it up.

### Set up the required configuration

In your application's assets folder, [configure a bundle configuration](../../using-mobile-extensions/mobile-core/configuration#using-a-bundled-file-configuration) called `ADBMobileConfig.json` with the following content:

```text
{
  "global.privacy": "optedin",
  "experienceCloud.org": "COMPANY_ORG_ID@AdobeOrg",
  "experiencePlatform.configId": "CONFIG_ID"
}
```

{% hint style="warning" %}
Replace the COMPANY\_ORG\_ID with your company's Adobe organization ID and CONFIG\_ID with the Experience Edge configuration identifier created in the [Create an Experience Edge configuration ID](../experience-platform-setup#create-an-experience-edge-configuration-id) step. The configuration ID can be found on top of the page in the Edge Configuration page in Experience Platform Launch UI.
{% endhint %}

### Register the extension

The `registerExtension()` API registers the Experience Platform extension with the Mobile Core extension. This API allows you to start sending and receiving events to and from the Experience Platform Mobile SDK.

{% tabs %}
{% tab title="Android" %}
In the Application file's `onCreate()` method, register the Mobile Core and the Experience Platform extensions.

```java
public class ExperiencePlatformDemoApplication extends Application {
...
@Override
public void onCreate() {
    super.onCreate();
    MobileCore.setApplication(this);

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
import ACPExperiencePlatform
import ACPCore
import ACPGriffon
import xdmlib

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        ACPIdentity.registerExtension()
        ACPLifecycle.registerExtension()
        ACPExperiencePlatform.registerExtension()
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

## Sending events

After you create an Experience Platform event, use `sendEvent` to send this event to the Adobe solutions for which you are provisioned and to the Experience Platform. For more information, see [Experience Platform event](experience-platform-events.md).

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void sendEvent(final ExperiencePlatformEvent experiencePlatformEvent, final ExperiencePlatformCallback responseCallback)
```

* _experiencePlatformEvent \(required\)_ event to be sent to Adobe Data Platform. It should not be null.
* _responseCallback \(optional\)_ callback to be invoked when the response handles are received from Adobe Data Platform. It can be called on a different thread and may be invoked multiple times.

{% hint style="info" %}
If you want to use more complex XDM Schemas for Experience Events and you would like help in generating custom XDM classes for your Android implementation, please contact your Adobe Customer Success Manager.

Alternatively, you can create an ExperiencePlatformEvent with XDM data as Map<String, Object>, by using the `setXdmSchema(final Map<String, Object> xdm, final String datasetIdentifier)` API from the `ExperiencePlatformEvent.Builder`. 

{% endhint %}

**Example \(commerce event\)**

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
**Syntax**

```java
public static func sendEvent(experiencePlatformEvent: ExperiencePlatformEvent, responseHandler: ExperiencePlatformResponseHandler? = nil)
```

* _experiencePlatformEvent \(required\)_ event to be sent to Adobe Data Platform. It should not be null.
* _responseHandler \(optional\)_ callback to be invoked when the response handles are received from Adobe Data Platform. It can be called on a different thread and may be invoked multiple times.

{% hint style="info" %}
If you want to use more complex XDM Schemas for Experience Events and you would like help in generating custom XDM classes for your Swift implementation, please contact your Adobe Customer Success Manager.

Alternatively, you can create an ExperiencePlatformEvent with XDM data as dictionary of [String: Any], by using the `init(xdm: [String: Any], data: [String: Any]? = nil, datasetIdentifier: String? = nil)` init from the `ExperiencePlatformEvent` struct.

{% endhint %}

**Example \(commerce event\)**

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

As described in the [Sending events](set-up-the-sdk.md#sending-events) section, the server-side event handle comes in chunks for the best performance. However, to be notified when a response is returned from the Adobe solutions, you can register a responseCallback\(Android\) /responseHandler \(iOS\) that is invoked when new data is available from the server. This callback is invoked for each event handle that is returned by the server and so it can be called multiple times.

**Tip**: In Android, the event handle is represented by a `Map<String, Object>`.

Depending on the nature of the event, and the various Adobe solutions you enabled for your organization, you can receive one, multiple, or no event handles for each Experience Platform event.

{% tabs %}
{% tab title="Android" %}
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

For more information about about response and error response handling, see [Server response handling](response-handling.md).


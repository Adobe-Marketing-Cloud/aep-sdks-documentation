# Set up Adobe Experience Platform Mobile SDK

In this section, we provide information to help you set up the SDK.

## Configure the Mobile Core SDK

As any other mobile extension, the Experience Platform extension relies on the AEP Mobile Core SDK for delivering the events, for managing the unique ECID on the mobile device and, in the future, for triggering client-side rules based on Experience events.

If your mobile application doesn't use the AEP SDK yet, follow the [Set up a mobile property](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) and [Get the Experience Platform SDK](https://aep-sdks.gitbook.io/docs/getting-started/get-the-sdk) pages first and then continue with the steps  below.

## Configure the Experience Platform extension

### Install Experience Platform extension

If you are already enrolled in the beta program, you should have received the bundle containing the Android and Swift Experience Platform SDKs. In order to get started, reference the SDK in your mobile application.

{% tabs %}
{% tab title="Android" %}

1. Create a `libs` folder in your application directory. If you already have this folder, you can skip this step.

2. Copy the `*.aar` file from the bundle path `/Android/lib/` and paste it in the libs folder.

3. Add the libs folder to the gradle dependencies. Example:

   ```
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

**Swift**

1. Create a `libs` folder in your application directory. If you already have this folder, you can skip this step.
2. Copy the `*.a` file along with the `*.swiftmodule` folder from the bundle path `/iOS/lib/` and paste it in the libs folder.
3. In Xcode, add the new library to your project dependencies list. 
   - Select the mobile application Target and click on Build Phases.
   - In the Link Binary With Libraries tab, Add new (+).
   - Click Add Other -> Add files, navigate to libs/ folder, select the *.a file and click Open.

{% endtab %}
{% endtabs %}

### Set up the required configuration

In your application's assets folder, [configure a bundle configuration](../../using-mobile-extensions/mobile-core/configuration#using-a-bundled-file-configuration) called `ADBMobileConfig.json` with the following content:

```text
{
  "experiencePlatform.configId": "CONFIG_ID"
}
```

{% hint style="warning" %}
Replace the CONFIG\_ID with the Experience Edge configuration identifier created in the [Create an Experience Edge configuration ID](../experience-platform-setup#create-an-experience-edge-configuration-id) step. The configuration ID can be found on top of the page in the Edge Configuration page in Experience Platform Launch UI.
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

Alternatively, you can create an ExperiencePlatformEvent with XDM data as dictionary of [String: Any], by using the `init(xdm: [String: Any], data: [String: Any]? = nil, datasetIdentifier: String? = nil)` method available in the `ExperiencePlatformEvent` struct.

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


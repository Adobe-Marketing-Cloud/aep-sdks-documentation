# Mobile Core API reference

## Application reference \(Android only\)

When building Android applications, the `android.app.Application` reference must be passed to Mobile SDK, which allows Mobile SDK to access the `android.app.Context` and monitor the lifecycle of the Android application.

{% hint style="warning" %}
Android applications must call `MobileCore.setApplication()` before calling any other Mobile SDK API.
{% endhint %}

### Set the `Application` instance

You can use the `setApplication` method to pass the Android `Application` instance to Mobile SDK.

{% tabs %}
{% tab title="Android" %}
**Java**

### setApplication

**Syntax**

```java
public static void setApplication(final Application app)
```

**Example**

```java
public class CoreApp extends Application {

   @Override
   public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.start(null);
   }
}
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### setApplication

**Example**

```csharp
public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
{
  protected override void OnCreate(Bundle savedInstanceState)
  {
    base.OnCreate(savedInstanceState);
    ACPCore.Application = this.Application;
    ACPCore.Start(null);
  }
}
```
{% endtab %}
{% endtabs %}

### Get the `Application` instance

You can use the `getApplication` method to get the previously set Android `Application` instance. The `Application` instance is mainly provided for third-party extensions.

{% tabs %}
{% tab title="Android" %}
**Java**

### getApplication

{% hint style="warning" %}
`MobileCore.getApplication` will return `null` if the `Application` object was destroyed or if `MobileCore.setApplication` was not previously called.
{% endhint %}

**Syntax**

```java
public static Application getApplication()
```

**Example**

```java
Application app = MobileCore.getApplication();
if (app != null) {
    ...
}
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### getApplication

{% hint style="warning" %}
`ACPCore.Application` may be `null` if the `Application` object was destroyed or was not set in the Core.
{% endhint %}

**Example**

```csharp
var app = ACPCore.Application;
if (app != null) {
    ...
}
```
{% endtab %}
{% endtabs %}

## Track app actions

Actions are events that occur in your application. You can use the `trackAction` method to track and measure an action. Each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you can use an action to track new subscriptions, every time an article is viewed, or every time a level is completed.

{% hint style="warning" %}
You want to use the `trackAction` method when you want to track an occurring event. In addition to the action name, you can also send context data with each `trackAction` call.
{% endhint %}

{% hint style="info" %}
If you installed and configured the Adobe Analytics extension, this method sends an Adobe Analytics action tracking hit with the provided optional context data.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### trackAction

**Syntax**

```java
public static void trackAction(final String action, final Map<String, String> contextData)
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();
additionalContextData.put("customKey", "value");
MobileCore.trackAction("loginClicked", additionalContextData);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

**Objective-C**

 ### trackAction

 **Syntax**

 ```swift
 @objc(trackAction:data:)
 static func track(action: String?, data: [String: Any]?)
 ```

 * _action_ contains the name of the action to track.
 * _contextData_ contains the context data to attach on this hit.

 **Example**

 ```objectivec
  [AEPMobileCore trackAction:@"action name" data:@{@"key":@"value"}];
 ```

 **Swift**

 ### trackAction

 **Syntax**

 ```swift
 static func track(action: String?, data: [String: Any]?)
 ```

 * _action_ contains the name of the action to track.
 * _contextData_ contains the context data to attach on this hit.

 **Example**

 ```swift
 MobileCore.track(action: "action name", data: ["key": "value"])
 ```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

### trackAction

**Syntax**

```text
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) contextData;
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```text
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```

**Swift**

### trackAction

**Syntax**

```swift
@objc(trackAction:data:)
static func track(action: String?, data: [String: Any]?)
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```swift
ACPCore.track(action: "action name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
**Javascript**

### trackAction

**Syntax**

```jsx
trackAction(action?: String, contextData?: { string: string });
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```jsx
ACPCore.trackAction("action name", {"key": "value"});
```
{% endtab %}

{% tab title="Flutter"}

{% endtab %}

{% tab %}
**Dart**
{% endtab %}

{% tab %}
### trackAction
{% endtab %}

{% tab %}
**Syntax**
{% endtab %}

{% tab %}
```dart
Future<void> trackAction (String action, {Map<String, String> contextData});
```
{% endtab %}

{% tab %}
* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.
{% endtab %}

{% tab %}
**Example**
{% endtab %}

{% tab %}
```dart
FlutterACPCore.trackAction("action name",  data: {"key": "value"});
```
{% endtab %}

{% tab %}
{% tab title="Unity"} **C\#**
{% endtab %}

{% tab %}
### trackAction
{% endtab %}

{% tab %}
**Syntax**
{% endtab %}

{% tab %}
```csharp
public static void TrackAction(string name, Dictionary<string, string> contextDataDict)
```
{% endtab %}

{% tab %}
* _name_ contains the name of the action to track.
* _contextDataDict_ contains the context data to attach on the hit.
{% endtab %}

{% tab %}
**Example**
{% endtab %}

{% tab %}
```csharp
var contextData = new Dictionary<string, string>();
contextData.Add("key", "value");
ACPCore.TrackAction("action", contextData);
```
{% endtab %}

{% tab title="Cordova" %}
**Cordova**

### trackAction

**Syntax**

```jsx
ACPCore.trackAction = function(action, contextData, success, fail);
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.
* _success_ callback is invoked when trackAction executes successfully.
* _fail_ callback is invoked when trackAction fails.

**Example**

```jsx
ACPCore.trackAction("cordovaAction", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### trackAction

**iOS Syntax**

```csharp
public static void TrackAction (string action, NSMutableDictionary<NSString, NSString> data);
```

* _action_ contains the name of the action to track.
* _data_ contains the context data to attach on the hit.

**Android Syntax**

```csharp
public unsafe static void TrackAction (string action, IDictionary<string, string> contextData);
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

**iOS**

```csharp
var data = new NSMutableDictionary<NSString, NSString>
{
  ["key"] = new NSString("value")
};
ACPCore.TrackAction("action", data);
```

**Android**

```csharp
var data = new Dictionary<string, string>();
data.Add("key", "value");
ACPCore.TrackAction("action", data);
```
{% endtab %}
{% endtabs %}

## Track application states and views

States represent screens or views in your application. The `trackState` method needs to be called every time a new state is displayed in your application. For example, this method should be called when a user navigates from the home page to the news feed. This method sends an Adobe Analytics state tracking hit with optional context data.

{% hint style="info" %}
If you installed and configured the Adobe Analytics extension, the `trackState` method increments page views and an Adobe Analytics state tracking hit with the provided optional context data.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

In Android, `trackState` is typically called every time a new `Activity` is loaded.

### trackState

**Syntax**

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();        
additionalContextData.put("customKey", "value");
MobileCore.trackState("homePage", additionalContextData);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

**Objective-C**

### trackState

 **Syntax**

 ```swift
 @objc(trackState:data:)
 static func track(state: String?, data: [String: Any]?)
 ```

 * _state_ contains the name of the state to track.
 * _contextData_ contains the context data to attach on this hit.

 **Example**

 ```objectivec
  [AEPMobileCore trackState:@"state name" data:@{@"key":@"value"}];
 ```

 **Swift**

 ### trackState

 **Syntax**

 ```swift
 static func track(state: String?, data: [String: Any]?)
 ```

 * _state_ contains the name of the state to track.
 * _contextData_ contains the context data to attach on this hit.

 **Example**

 ```swift
 MobileCore.track(state: "state name", data: ["key": "value"])
 ```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

**Objective-C**

### trackState

**Syntax**

```objectivec
(void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```objectivec
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```

**Swift**

### trackState

**Syntax**

```swift
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```swift
ACPCore.trackState("state name", data: ["key": "value"])
```
{% endtab %}

{% tab title="React Native" %}
**Javascript**

### trackState

**Syntax**

```jsx
trackState(state?: String, contextData?: { string: string });
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```jsx
ACPCore.trackState("state name", {"key": "value"});
```
{% endtab %}

{% tab title="Flutter" %}
**Dart**

### trackState

**Syntax**

```dart
Future<void> trackState (String state, {Map<String, String> contextData});
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```dart
FlutterACPCore.trackState("state name",  data: {"key1: "value"})
```
{% endtab %}

{% tab title="Cordova" %}
**Cordova**

### trackState

**Syntax**

```jsx
ACPCore.trackState = function(state, contextData, success, fail);
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.
* _success_ callback is invoked when trackState executes successfully.
* _fail_ callback is invoked when trackState fails.

**Example**

```jsx
ACPCore.trackState("cordovaState", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```
{% endtab %}

{% tab title="Unity" %}
**C\#**

### trackState

**Syntax**

```csharp
public static void TrackState(string name, Dictionary<string, string> contextDataDict)
```

* _state_ contains the name of the state to track.
* _contextDataDict_ contains the context data to attach on the hit.

**Example**

```csharp
var dict = new Dictionary<string, string>();
dict.Add("key", "value");
ACPCore.TrackState("state", dict);
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### trackState

**iOS syntax**

```csharp
public static void TrackState (string state, NSMutableDictionary<NSString, NSString> data);
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Android syntax**

```csharp
public unsafe static void TrackState (string state, IDictionary<string, string> contextData);
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**iOS example**

```csharp
var data = new NSMutableDictionary<NSString, NSString>
{
  ["key"] = new NSString("value")
};
ACPCore.TrackState("state", data);
```

**Android example**

```csharp
var data = new Dictionary<string, string>();
data.Add("key", "value");
ACPCore.TrackState("state", data);
```
{% endtab %}
{% endtabs %}

## Set the advertising ID

The advertising ID is preserved between app upgrades, is saved and restored during the standard application backup process, available via [Signals](signals/), and is removed at uninstall.

For more information about identity in Mobile Core, please read the documentation on the [identity APIs](identity/identity-api-reference.md).

## setPushIdentifier

This API sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

{% hint style="info" %}
It is recommended to call `setPushIdentifier` on each application launch to ensure the most up-to-date device token is set to the SDK. If no device token is available, `null`/`nil` should be passed.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### setPushIdentifier

**Syntax**

```java
public static void setPushIdentifier(final String pushIdentifier);
```

* _pushIdentifier_  is a string that contains the device token for push notifications.

**Example**

```java
//Retrieve the token from either GCM or FCM, and pass it to the SDK
MobileCore.setPushIdentifier(token);
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

### setPushIdentifier

**Syntax**

```text
public static func setPushIdentifier(_ deviceToken: Data?)
```

* _deviceToken_  is a string that contains the device token for push notifications.

**Example**

```objectivec
// Set the deviceToken that the APNS has assigned to the device
[ACPCore setPushIdentifier:deviceToken];
```

**Swift**

### setPushIdentifier

**Syntax**

```swift
@objc(setPushIdentifier:)
public static func setPushIdentifier(_ deviceToken: Data?)
```

* _deviceToken_  is a string that contains the device token for push notifications.

**Example**

```swift
// Set the deviceToken that the APNs has assigned to the device
MobileCore.setPushIdentifier(deviceToken)
```
{% endtab %}
{% endtabs %}

## Collect personally identifiable information

The `collectPii` method lets the SDK to collect sensitive or personally identifiable information \(PII\).

{% hint style="warning" %}
Although this method enables the collection of sensitive data, no data is sent to any Adobe or other third-party endpoints. To send the data to an endpoint, use a PII type postback.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### collectPii

**Syntax**

```java
public static void collectPII(final Map<String, String> piiData);
```

**Example**

```java
Map<String, String> data = new HashMap<String, String>();
data.put("firstname", "customer");
//The rule to trigger a PII needs to be setup for this call
//to result in a network send
MobileCore.collectPII(data);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

**Objective-C**

 ### collectPii

 **Syntax**

 ```swift
 @objc(collectPii:)
 public static func collectPii(_ data: [String: Any])
 ```

 **Example**

 ```objectivec
 [AEPMobileCore collectPii:data:@{@"key1" : @"value1",
                            @"key2" : @"value2"
                            }];
 ```

 **Swift**

 ### collectPii

 **Syntax**

 ```swift
 public static func collectPii(_ data: [String: Any])
 ```

 **Example**

 ```objectivec
 MobileCore.collectPii(["key1" : "value1","key2" : "value2"]);
 ```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

### collectPii

**Syntax**

```swift
(void) collectPii: (nonnull NSDictionary<NSString*, NSString*>*) data;
```

**Example**

```objectivec
[ACPCore collectPii:data:@{@"key1" : "@value1",
                           @"key2" : "@value2"
                           }];
```

**Swift**

### collectPii

**Syntax**

```swift
ACPCore.collectPii(data: [String : String])
```

**Example**

```objectivec
MobileCore.collectPii(["key1" : "value1","key2" : "value2"]);
```
{% endtab %}

{% tab title="React Native" %}
**Javascript**

### collectPii

**Syntax**

```jsx
ACPCore.collectPii(data: [String : String])
```

**Example**

```jsx
ACPCore.collectPii({"myPii": "data"});
```

**Swift**

### collectPii

**Syntax**

```swift
ACPCore.collectPii(data: [String : String])
```

**Example**

```objectivec
MobileCore.collectPii(["key1" : "value1","key2" : "value2"]);
```
{% endtab %}
{% endtabs %}

## Collect launch information

You can provide the user information to the SDK from various launch points in your application.

{% hint style="info" %}
If the Adobe Analytics extension is enabled in your SDK, collecting this launch data results in an Analytics request being sent. Other extensions in the SDK might use the collected data, for example, as a rule condition for an In-App Message.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
The Android SDK automatically registers an `Application.ActivityLifecycleCallbacks`and listens for `onActivityResumed`. When an activity is resumed, SDK collects the data from the activity. Currently, it is being used in the following scenarios:

* Tracking Deep Link click-through.
* Tracking Push Message click-through
* Tracking Local Notification click-through

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

**Objective-C**

 This method should be called to support the following use cases:

 * Tracking Deep Link click-throughs
   * From `application:didFinishLaunchingWithOptions`
   * Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
 * Tracking Push Message click-through
   * From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

 #### collectLaunchInfo

 **Syntax**

 ```text
 @objc(collectLaunchInfo:)
 public static func collectLaunchInfo(_ userInfo: [String: Any])
 ```

 **Example**

 ```text
  [AEPMobileCore collectLaunchInfo:launchOptions];
 ```

 **Swift**

 This method should be called to support the following use cases:

 * Tracking Deep Link click-throughs
   * From `application(_:didFinishLaunchingWithOptions:)`
   * Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
 * Tracking Push Message click-through
   * From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

 #### collectLaunchInfo

 **Syntax**

 ```swift
 public static func collectLaunchInfo(_ userInfo: [String: Any])
 ```

 **Example**

 ```swift
 AEPCore.collectLaunchInfo(userInfo)
 ```

{% endtab %}



{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

The `collectLaunchInfo` method should be used in the following use cases:

* Tracking a Deep Link click-through
  * From `application:didFinishLaunchingWithOptions`
  * Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
* Tracking a Push Message click-through
  * From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

#### collectLaunchInfo

**Syntax**

```objectivec
(void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

**Example**

```text
 [ACPCore collectLaunchInfo:launchOptions];
```

**Swift**

The `collectLaunchInfo` method should be used in the following use cases:

* Tracking a Deep Link click-through
  * From `application(_:didFinishLaunchingWithOptions:)`
  * Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
* Tracking a Push Message click-through
  * From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

#### collectLaunchInfo

**Syntax**

```swift
(void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

**Example**

```swift
AEPCore.collectLaunchInfo(userInfo)
```
{% endtab %}
{% endtabs %}

## Retrieving stored identifiers

The following SDK identities, as applicable, are locally stored:

* Company Context - IMS Org IDs
* Experience Cloud ID \(MID\)
* User IDs
* Integration codes \(ADID, push IDs\)
* Data source IDs \(DPID, DPUUID\)
* Analytics IDs \(AVID, AID, VID, and associated RSIDs\)
* Target legacy IDs \(TNTID, TNT3rdpartyID\)
* Audience Manager ID \(UUID\)

To retrieve data as a JSON string from the SDKs and send this data to your servers, use the `getSdkIdentities` method:

{% hint style="warning" %}
You must call the API below and retrieve identities stored in the SDK, **before** the user opts out.

This API does **not** include the identities stored in the Edge Identity extension. To retrieve the identities from the Edge Identity extension, use [getIdentities](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/09dd71f04d377c356dd24aac9b89ed0fffc1cf63/using-mobile-extensions/adobe-edge-identity/adobe-edge-identity-api-reference.md#getidentities).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### getSdkIdentities

**Syntax**

```java
void getSdkIdentities(AdobeCallback<String> callback);
```

* _callback_ is invoked with the SDK identities as a JSON string.
  * If an instance of  `AdobeCallbackWithError` is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 5000ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate `AdobeError`.

**Example**

```java
MobileCore.getSdkIdentities(new AdobeCallback<String>() {
    @Override
    public void call(String value) {
        // handle the json string
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

#### Objective-C

 ### getSdkIdentities

 #### Syntax

 ```objectivec
 @objc(getSdkIdentities:)
 static func getSdkIdentities(completion: @escaping (String?, Error?) -> Void)
 ```

 * _callback_ is invoked with the SDK identities as a JSON string.
 * _completionHandler_ is invoked with the SDK identities as a JSON string, or _error_ if an unexpected error occurs or the request times out. The default timeout is 1000ms.

 #### Example

 **Objective-C**

 ```objectivec
 [AEPMobileCore getSdkIdentities:^(NSString * _Nullable content, NSError * _Nullable error) {
     if (error) {
       // handle error here
     } else {
       // handle the retrieved identities
     }
 }];
 ```

 **Swift**

 ```swift
 MobileCore.getSdkIdentities { (content, error) in
     // handle completion
 }
 ```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

### getSdkIdentities

**Syntax**

```objectivec
(void) getSdkIdentities: (nullable void (^) (NSString* __nullable content)) callback;
(void) getSdkIdentitiesWithCompletionHandler: (nullable void (^) (NSString* __nullable content, NSError* _Nullable error)) completionHandler;
```

* _callback_ is invoked with the SDK identities as a JSON string.
* _completionHandler_ is invoked with the SDK identities as a JSON string, or _error_ if an unexpected error occurs or the request times out. The default timeout is 1000ms.

**Example**

```objectivec
[ACPCore getSdkIdentities:^(NSString * _Nullable content){
    NSLog(content);

[ACPCore getSdkIdentitiesWithCompletionHandler:^(NSString * _Nullable content, NSError * _Nullable error) {
        if (error) {
            // handle error here
        } else {
            // handle the retrieved identities
            NSLog(content);
        }
    }];
```

**Swift**

```swift
MobileCore.getSdkIdentities { (content, error) in
    // handle completion
}
```
{% endtab %}
{% endtabs %}

## Reset identities

The `resetIdentities` method requests that each extension resets the identities it owns. Each extension responds to this request uniquely.

{% hint style="warning" %}
This API is only handled by the [Edge](mobile-core-api-reference.md) and [Edge Identity](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/de62274f59c14b23acae8992352ec63fbb16411b/foundation-extensions/adobe-edge-identity/README.md) extensions. Calling `resetIdentities` does **not** clear identities in non-edge extensions, such as [Identity](identity/).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### resetIdentities

Note, this method is only available in Mobile Core v.1.8.0 and above.

**Syntax**

```java
void resetIdentities();
```

**Example**

```java
MobileCore.resetIdentities();
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

Note, this method is only available in Mobile Core v.1.8.0 and above.

### resetIdentities

**Syntax**

```swift
@objc(resetIdentities)
static func resetIdentities()
```

**Example**

```objectivec
[ACPCore resetIdentities];
```

**Swift**

Note, this method is only available in Mobile Core v.1.8.0 and above.

### resetIdentities

**Syntax**

```swift
static func resetIdentities()
```

**Example**

```swift
MobileCore.resetIdentities()
```

_since AEPCore v3.1.0_
{% endtab %}
{% endtabs %}

## Set icons for local notification \(Android only\)

You can set the small and large icons that will be used for notifications that are created by the SDK. The small icon appears in the status bar and is the secondary image that is displayed when the user sees the complete notification in the notification center. The large icon is the primary image that is displayed when the user sees the complete notification in the notification center.

{% hint style="warning" %}
The following methods are **only** available in Android and Xamarin Android.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### setSmallIconResourceID

**Syntax**

```java
public static void setSmallIconResourceID(int resourceID)
```

**Example**

```java
 MobileCore.setSmallIconResourceID(R.mipmap.ic_launcher_round);
```

### setLargeIconResourceID

**Syntax**

```java
public static void setLargeIconResourceID(int resourceID)
```

**Example**

```java
 MobileCore.setLargeIconResourceID(R.mipmap.ic_launcher_round);
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### setSmallIconResourceID

**Syntax**

```csharp
public unsafe static void SetSmallIconResourceID (int resourceID);
```

**Example**

```csharp
ACPCore.SetSmallIconResourceID(Resource.Mipmap.icon_round);
```

### setLargeIconResourceID

**Syntax**

```csharp
public unsafe static void SetLargeIconResourceID (int resourceID);
```

**Example**

```csharp
 ACPCore.SetLargeIconResourceID(Resource.Mipmap.icon_round);
```
{% endtab %}
{% endtabs %}

## Logging

The logging APIs allow log messages to be tagged and filtered with the Mobile SDK log messages. This allows application developers to filter the logged messages based on the current logging mode.

Application developers can use the `setLogLevel` method to filter the log messages that are coming from the Mobile SDK.

From least to most verbose, the order of Mobile SDK logging modes is as follows:

* ERROR
* WARNING
* DEBUG
* VERBOSE

When debugging on iOS, you can use `LogLevel.verbose` to enable all the logging messages that are coming from Mobile SDK and partner extensions. Similarly, on Android, you can use `LoggingMode.VERBOSE` to enable all the logging messages that are coming from Mobile SDK and partner extensions.

In a production application, you should use a less verbose logging mode, such as error-level logging.

By default, Mobile SDK logging mode is set to `LoggingMode.ERROR` for Android and `LogLevel.error`on iOS.

{% hint style="info" %}
* On **Android**, Mobile SDK uses the `android.util.Log` class to log messages.
* On **iOS**, Mobile SDK uses `NSLog` to messages to Apple System Log facility.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

### setLogLevel

**Syntax**

```java
public static void setLogLevel(LoggingMode mode)
```

**Example**

```java
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;

MobileCore.setLogLevel(LoggingMode.VERBOSE);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

**Objective C**

 #### setLogLevel

 **Syntax**

 ```swift
 @objc(setLogLevel:)
 public static func setLogLevel(_ level: LogLevel)
 ```

 **Example**

 ```text
 [AEPMobileCore setLogLevel: AEPLogLevelTrace];
 ```

 **Swift**

 #### setLogLevel

 **Syntax**

 ```swift
 public static func setLogLevel(_ level: LogLevel)
 ```

 **Example**

 ```swift
 MobileCore.setLogLevel(.trace)
 ```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

### setLogLevel

**Syntax**

```swift
(void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```text
#import "ACPCore.h"

[ACPCore setLogLevel: AEPLogLevelTrace];
```

**Swift**

### setLogLevel

**Syntax**

```swift
(void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```swift
import ACPCore

ACPCore.setLogLevel(ACPMobileLogLevel.verbose);
```
{% endtab %}

{% tab title="React Native" %}
**Javascript**

### setLogLevel

**Syntax**

```jsx
(void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```jsx
import {ACPMobileLogLevel} from '@adobe/react-native-acpcore';
ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
```
{% endtab %}

{% tab title="Flutter" %}
**Dart**

### setLogLevel

**Syntax**

```dart
(void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```dart
import 'package:flutter_acpcore/src/acpmobile_logging_level.dart';
FlutterACPCore.setLogLevel(ACPLoggingLevel.VERBOSE);
```
{% endtab %}

{% tab title="Cordova" %}
**Cordova**

From least to most verbose, the order of Mobile SDK logging modes is as follows:

* ACPCore.ACPMobileLogLevelError
* ACPCore.ACPMobileLogLevelWarning
* ACPCore.ACPMobileLogLevelDebug
* ACPCore.ACPMobileLogLevelVerbose

### setLogLevel

**Syntax**

```jsx
ACPCore.setLogLevel = function(logLevel, success, fail);
```

**Example**

```jsx
ACPCore.setLogLevel(ACPCore.ACPMobileLogLevelVerbose, successCallback, errorCallback);
 MobileCore.setSmallIconResourceID(R.mipmap.ic_launcher_round);
```
{% endtab %}

{% tab title="Unity" %}
**C\#**

From least to most verbose, the order of Mobile SDK logging modes is as follows:

* ACPCore.ACPMobileLogLevel.ERROR
* ACPCore.ACPMobileLogLevel.WARNING
* ACPCore.ACPMobileLogLevel.DEBUG
* ACPCore.ACPMobileLogLevel.VERBOSE

### setLogLevel

**Syntax**

```csharp
public static void SetLogLevel(ACPMobileLogLevel logLevel)
```

**Example**

```csharp
ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.ERROR);
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

From least to most verbose, the order of Mobile SDK logging modes is as follows for iOS:

* ACPMobileLogLevel.Error;
* ACPMobileLogLevel.Warning;
* ACPMobileLogLevel.Debug;
* ACPMobileLogLevel.Verbose;

From least to most verbose, the order of Mobile SDK logging modes is as follows for Android:

* LoggingMode.Error;
* LoggingMode.Warning;
* LoggingMode.Debug;
* LoggingMode.Verbose;

### setLogLevel

**iOS syntax**

```csharp
public static ACPMobileLogLevel LogLevel { get, set }
```

**Android syntax**

```csharp
public unsafe static LoggingMode LogLevel { get, set }
```

**iOS example**

```csharp
ACPCore.LogLevel = ACPMobileLogLevel.Verbose;
```

**Android example**

```csharp
ACPCore.LogLevel = LoggingMode.Verbose;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Android" %}
**Java**

### getLogLevel

**Syntax**

```java
public static LoggingMode getLogLevel()
```

**Example**

```java
LoggingMode mode = MobileCore.getLogLevel();
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

### getLogLevel

**Syntax**

```objectivec
(ACPMobileLogLevel) logLevel;
```

**Example**

```objectivec
var logLevel:ACPMobileLogLevel = [ACPCore logLevel];
```

**Swift**

### getLogLevel

**Syntax**

```swift
(ACPMobileLogLevel) logLevel;
```

**Example**

```swift
let logLevel:ACPMobileLogLevel = ACPCore.logLevel();
```
{% endtab %}

{% tab title="React Native" %}
**Javascript**

### getLogLevel

**Example**

```jsx
ACPCore.getLogLevel().then(level => console.log("AdobeExperienceSDK: Log Level = " + level));
```
{% endtab %}

{% tab title="Unity" %}
**C\#**

### getLogLevel

**Example**

```csharp
ACPCore.ACPMobileLogLevel logLevel = ACPCore.GetLogLevel();
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### getLogLevel

**Example**

```csharp
var logLevel = ACPCore.LogLevel;
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Android" %}
**Java**

The `MobileCore` logging APIs use the `android.util.Log` APIs to log messages to Android. Based on the `LoggingMode` that is passed to `MobileCore.log()`, the following Android method is called:

* `LoggingMode.VERBOSE` uses `android.util.Log.v`
* `LoggingMode.DEBUG` uses `android.util.Log.d`
* `LoggingMode.WARNING` uses `android.util.Log.w`
* `LoggingMode.ERROR` uses `android.util.Log.e`

All log messages from the Adobe Experience SDK to Android use the same log tag of `AdobeExperienceSDK`. For example, if logging an error message is using `MobileCore.log()`, the call to `android.util.Log.e` looks like `Log.e("AdobeExperienceSDK", tag + " - " + message)`.

### log

**Syntax**

```java
public static void log(final LoggingMode mode, final String tag, final String message)
```

**Example**

```java
MobileCore.log(LoggingMode.DEBUG, "MyClassName", "Provided data was null");
```

**Output**

```text
D/AdobeExperienceSDK: MyClassName - Provided data was null
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

The log messages from the Adobe Experience SDK are printed to the Apple System Log facility and use a common format that contains the tag `AdobeExperienceSDK`. For example, if logging an error message using `ACPCore.log()`, the printed output looks like `[AdobeExperienceSDK ERROR <tag>]: message`.

### log

**Syntax**

```text
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```text
[ACPCore log: ACPMobileLogLevelDebug, tag:@"MyClassName", message:@"Provided data was nil"];
```

**Output example**

```text
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```

**Swift**

### log

**Syntax**

```swift
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```swift
ACPCore.log(ACPMobileLogLevel.debug, tag: "MyClassName", message: "Provided data was nil");
```

**Output example**

```text
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

The log messages from the Adobe Experience SDK are printed to the Log facility and use a common format that contains the tag `ACPMobileLogLevel`.

**Example**

```jsx
ACPCore.log(ACPMobileLogLevel.ERROR, "React Native Tag", "React Native Message");
```

Note: `ACPMobileLogLevel` contains the following getters:

```jsx
const ERROR = "ACP_LOG_LEVEL_ERROR";
const WARNING = "ACP_LOG_LEVEL_WARNING";
const DEBUG = "ACP_LOG_LEVEL_DEBUG";
const VERBOSE = "ACP_LOG_LEVEL_VERBOSE";
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

The log messages from the Adobe Experience SDK are printed to the Log facility and use a common format that contains the tag `AdobeExperienceSDK`.

**iOS syntax**

```csharp
ACPCore.Log(ACPMobileLogLevel.Error, "xamarin tag", "xamarin message");
```

```text
[AdobeExperienceSDK ERROR <xamarin tag>]: xamarin message
```

**Android syntax**

```csharp
ACPCore.Log(LoggingMode.Error, "xamarin tag", "xamarin message");
```

```text
[AdobeExperienceSDK] xamarin tag - xamarin message
```
{% endtab %}
{% endtabs %}

## Handle open URL action

Mobile SDK allows you to add a callback function that is triggered before the [`open url`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-types) action occurs. If the callback function returns **Yes**, the SDK does not complete the `open url` action. If the callback function returns **No**, the SDK completes the `open url` action.

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}
**Objective C**

### registerURLHandler

**Syntax**

```objectivec
+ (void) registerURLHandler: (nonnull BOOL (^) (NSString* __nullable url)) callback;
```

**Example**

```objectivec
[ACPCore registerURLHandler:^BOOL(NSString * _Nullable url) {
    ...
}];
```
{% endtab %}
{% endtabs %}

## Set app group \(iOS only\)

You can use the `setAppGroup` method to set the app group, which is used to share user defaults and files among the containing app and the extension apps.

{% hint style="info" %}
This API _must_ be called in `AppDidFinishLaunching` and before any other interactions with the Adobe Experience SDK have happened. Only the first call to this function will have any effect.
{% endhint %}

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

### setAppGroup

**Syntax**

```swift
public static func setAppGroup(_ group: String?)
```

**Example**

```text
[ACPCore setAppGroup:@"app-group-id"];
```

**Swift**

### setAppGroup

**Syntax**

```swift
public static func setAppGroup(_ group: String?)
```

**Example**

```swift
ACPCore.setAppGroup("app-group-id")
```
{% endtab %}

{% tab title="Xamarin" %}
**C\#**

### setAppGroup

**Syntax**

```csharp
public static void SetAppGroup (string appGroup);
```

**Example**

```csharp
ACPCore.SetAppGroup("app_group");
```
{% endtab %}
{% endtabs %}

## Public classes

{% tabs %}
{% tab title="Android" %}
**Java**

### AdobeCallback

The `AdobeCallback` class provides the interface to receive results when the asynchronous APIs perform the requested action.

```java
public interface AdobeCallback<T> {    
    void call(final T value);
}
```

### AdobeCallbackWithError

The `AdobeCallbackWithError` class provides the interface to receive results or an error when the asynchronous APIs perform the requested action.

When using this class, if the request cannot be completed within the default timeout or an unexpected error occurs, the request is stopped and the fail method is called with the corresponding `AdobeError`.

```java
public interface AdobeCallbackWithError<T> extends AdobeCallback<T> {
    void fail(final AdobeError error);
}
```

### AdobeError

The `AdobeError` class shows the errors that can be passed to an `AdobeCallbackWithError`:

* `UNEXPECTED_ERROR` - An unexpected error occurred.
* `CALLBACK_TIMEOUT` - The timeout was met.
* `CALLBACK_NULL` - The provided callback function is null.
* `EXTENSION_NOT_INITIALIZED` - The extension is not initialized.

**Example**

```java
MobileCore.getPrivacyStatus(new AdobeCallbackWithError<MobilePrivacyStatus>() {
  @Override
  public void fail(final AdobeError error) {
    if (error == AdobeError.UNEXPECTED_ERROR) {
      // handle unexpected error
    } else if (error == AdobeError.CALLBACK_TIMEOUT) {
      // handle timeout error
    } else if (error == AdobeError.CALLBACK_NULL) {
      // handle null callback error
    } else if (error == AdobeError.EXTENSION_NOT_INITIALIZED) {
      // handle extension not initialized error
    }
  }

  @Override
  public void call(final MobilePrivacyStatus value) {
    // use MobilePrivacyStatus value
  }
});
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### ACPError

The `ACPError` class shows the errors that can be passed to a completion handler callback from any API which uses one:

* `ACPErrorUnexpected` - An unexpected error occurred.
* `ACPErrorCallbackTimeout` - The timeout was met.
* `ACPErrorCallbackNil` - The provided callback function is nil.
* `ACPErrorExtensionNotInitialized` - The extension is not initialized.

**Examples**

**Objective-C**

```text
[ACPCore getSdkIdentities:^(NSString * _Nullable content, NSError * _Nullable error) {
  if (error) {
    if (error.code == ACPErrorCallbackTimeout) {
      // handle timeout error
    } else if (error.code == ACPErrorCallbackNil) {
      // handle nil callback error
    } else if (error.code == ACPErrorExtensionNotInitialized) {
      // handle extension not initialized error
    } else if (error.code == ACPErrorUnexpected) {
      // handle unexpected error

    ....

  } else {
    // use privacy status
  }
}];
```

**Swift**

```swift
ACPCore.getPrivacyStatus { (privacyStatus, error) in
  if let error = error {
    let callbackError: NSError = (error as NSError)
    if (callbackError.code == ACPError.callbackTimeout.rawValue) {
      // handle timeout error
    } else if (callbackError.code == ACPError.callbackNil.rawValue) {
      // handle nil callback error
    } else if (callbackError.code == ACPError.extensionNotInitialized.rawValue) {
      // handle extension not initialized error
    } else if (callbackError.code == ACPError.unexpected.rawValue) {
      // handle unexpected error
    }
  } else {
    // use privacyStatus
  }
}
```
{% endtab %}

{% tab title="Xamarin" %}
### Android

**IAdobeCallback**

This class provides the interface to receive results when the async APIs perform the requested action.

```csharp
public interface IAdobeCallback : IJavaObject, IDisposable, IJavaPeerable
{
    void Call (Java.Lang.Object p0);
}
```

**IAdobeCallbackWithError**

This class provides the interface to receive results or an error when the async APIs perform the requested action. When using this class, if the request cannot be completed within the default timeout or an unexpected error occurs, the request is aborted and the _fail_ method is called with the corresponding _AdobeError_.

```csharp
public interface IAdobeCallbackWithError : IAdobeCallback, IJavaObject, IDisposable, IJavaPeerable
{
    void Fail (AdobeError p0);
}
```

**AdobeError**

Errors which may be passed to an AdobeCallbackWithError:

* `UnexpectedError` - An unexpected error occurred.
* `CallbackTimeout` - The timeout was met.
* `CallbackNull` - The provided callback function is null.
* `ExtensionNotInitialized` - The extension is not initialized.

**Example**

```csharp
ACPCore.GetPrivacyStatus(new AdobeCallbackWithError());
class AdobeCallbackWithError : Java.Lang.Object, IAdobeCallbackWithError
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("String callback content: " + stringContent);
    }
    else
    {
      Console.WriteLine("null content in string callback");
    }
  }
  public void Fail(AdobeError error)
  {
    if (error == AdobeError.UnexpectedError)
    {
      // handle unexpected error
    }
    else if (error == AdobeError.CallbackTimeout)
    {
      // handle timeout error
    }
    else if (error == AdobeError.CallbackNull)
    {
      // handle null callback error
    }
    else if (error == AdobeError.ExtensionNotInitialized)
    {
        // handle extension not initialized error
    }
```

### iOS

**ACPError**

Errors which may be passed to a completion handler callback from any API which uses one:

* `ACPError.Unexpected` - An unexpected error occurred.
* `ACPError.CallbackTimeout` - The timeout was met.
* `ACPError.CallbackNil` - The provided callback function is nil.
* `ACPError.ExtensionNotInitialized` - The extension is not initialized.

**Example**

```csharp
ACPCore.GetPrivacyStatusWithCompletionHandler((privacyStatus, error) => {
  if (error != null)
  {
    if ( error.Code == (int)ACPError.CallbackTimeout)
    {
      // handle timeout error
    }
    else if (error.Code == (int)ACPError.CallbackNil) 
    {
      // handle nil callback error
    }
    else if (error.Code == (int)ACPError.ExtensionNotInitialized)
    {
      // handle extension not initialized error
    }
    else if (error.Code == (int)ACPError.Unexpected)
    {
      // handle unexpected error
    }
  }
  else
  {
    Console.WriteLine("privacy status: " + privacyStatus);
  }
});
```
{% endtab %}
{% endtabs %}

## Additional information

To learn what context data is, please read the [documentation on context data](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html).


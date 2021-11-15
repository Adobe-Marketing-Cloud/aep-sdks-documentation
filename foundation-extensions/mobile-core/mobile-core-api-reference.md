# Mobile Core API reference

## collectLaunchInfo

You can provide the user information to the SDK from various launch points in your application.

{% hint style="info" %}
If the Adobe Analytics extension is enabled in your SDK, collecting this launch data results in an Analytics request being sent. Other extensions in the SDK might use the collected data, for example, as a rule condition for an In-App Message.
{% endhint %}

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective-C**

The `collectLaunchInfo` method should be used in the following use cases:

* Tracking a deep link clickthrough
  * From `application:didFinishLaunchingWithOptions`
  * Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
* Tracking a push message clickthrough
  * From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

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

* Tracking a deep link clickthrough
  * From `application(_:didFinishLaunchingWithOptions:)`
  * Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
* Tracking a push message clickthrough
  * From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

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


## collectPii

The `collectPii` method lets the SDK to collect sensitive or personally identifiable information \(PII\).

{% hint style="warning" %}
Although this method enables the collection of sensitive data, no data is sent to any Adobe or other third-party endpoints. To send the data to an endpoint, use a PII type postback.
{% endhint %}

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective-C**

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

**Syntax**

```jsx
ACPCore.collectPii(data: [String : String])
```

**Example**

```jsx
ACPCore.collectPii({"myPii": "data"});
```

**Swift**

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

## getApplication \(Android only\)

You can use the `getApplication` method to get the previously set Android `Application` instance. The `Application` instance is mainly provided for third-party extensions.

{% tabs %}

{% tab title="Xamarin" %}
**C\#**

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

## getLogLevel

This API gets the current log level being used in the SDK.

{% tabs %}

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

## getSdkIdentities

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

{% tab title="iOS \(ACP 2.x\)" %}
**Objective-C**

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

## log

This is the API used to log from the SDK.

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective-C**

The log messages from the Adobe Experience SDK are printed to the Apple System Log facility and use a common format that contains the tag `AdobeExperienceSDK`. For example, if logging an error message using `ACPCore.log()`, the printed output looks like `[AdobeExperienceSDK ERROR <tag>]: message[AEP SDK ERROR - <testLabel>] Test message`.

**Syntax**

```objectivec
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```objectivec
[ACPCore log: ACPMobileLogLevelDebug, tag:@"MyClassName", message:@"Provided data was nil"];
```

**Output example**

```objectivec
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```

**Swift**

**Syntax**

```swift
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```swift
ACPCore.log(ACPMobileLogLevel.debug, tag: "MyClassName", message: "Provided data was nil");
```

**Output example**

```objectivec
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

## registerExtension(s)

Extensions are registered with Mobile Core so that they can dispatch and listen for events.

{% hint style="danger" %}
Extension registration is **mandatory**. Attempting to make extension-specific API calls without registering the extension will lead to undefined behavior.
{% endhint %}

The following code snippets demonstrate how you can import and register the Mobile Core and Profile extensions. You can also see, for reference, how Identity, Lifecycle, Signal, Profile, and other extensions are imported and registered.

{% tabs %}

{% tab title="iOS (ACP 2.x)" %}

The following snippet shows an example of how to add the initialization code. Note that this may need to be adjusted, depending on how your application is structured.

**Objective-C**

```objectivec
#import "AppDelegate.h"
#import "ACPCore.h"
#import "ACPUserProfile.h"
#import "ACPIdentity.h"
#import "ACPLifecycle.h"
#import "ACPSignal.h"
...
@implementation AppDelegate
-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPCore setLogLevel:ACPMobileLogLevelDebug];
  [ACPCore configureWithAppId:@"<your_environment_id_from_Launch>"];
    ...
  [ACPUserProfile registerExtension];
    [ACPIdentity registerExtension];
    [ACPLifecycle registerExtension];
    [ACPSignal registerExtension];
    const UIApplicationState appState = application.applicationState;
    [ACPCore start:^{
      // only start lifecycle if the application is not in the background
      if (appState != UIApplicationStateBackground) {
        [ACPCore lifecycleStart:nil];
      }
    }];
    ...
  return YES;
}

@end
```

**Swift**

```swift
import ACPCore
import ACPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
  func application(_application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool{
    ACPCore.setLogLevel(.debug)
        ACPCore.configure(withAppId: "<your_environment_id_from_Launch>")
    ...
    ACPUserProfile.registerExtension()
        ACPIdentity.registerExtension()
        ACPLifecycle.registerExtension()
        ACPSignal.registerExtension()
        ACPCore.start {
        ACPCore.lifecycleStart(nil)
        }
    ...
    return true
  }
}
```
{% endtab %}

{% tab title="React Native" %}
For React Native apps, initialize the SDK using native code in your `AppDelegate` \(iOS\) and `MainApplication` \(Android\).

### iOS

```objectivec
#import "ACPCore.h"
#import "ACPUserProfile.h"
#import "ACPIdentity.h"
#import "ACPLifecycle.h"
#import "ACPSignal.h"
...
@implementation AppDelegate
-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"<your_environment_id_from_Launch>"];
    [ACPUserProfile registerExtension];
    [ACPIdentity registerExtension];
    [ACPLifecycle registerExtension];
    [ACPSignal registerExtension];

    const UIApplicationState appState = application.applicationState;
    [ACPCore start:^{
      // only start lifecycle if the application is not in the background
      if (appState != UIApplicationStateBackground) {
        [ACPCore lifecycleStart:nil];
      }
    }];
    ...
  return YES;
}

@end
```

### Android

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.InvalidInitException;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
...
import android.app.Application;
...
public class MainApplication extends Application implements ReactApplication {
  ...
  @Override
  public void on Create(){
    super.onCreate();
    ...
    MobileCore.setApplication(this);
    MobileCore.setLogLevel(LoggingMode.DEBUG);
    MobileCore.setWrapperType(WrapperType.REACT_NATIVE);

    try {
      UserProfile.registerExtension();
      Identity.registerExtension();
      Lifecycle.registerExtension();
      Signal.registerExtension();
      MobileCore.start(new AdobeCallback () {
          @Override
          public void call(Object o) {
            MobileCore.configureWithAppID("<your_environment_id_from_Launch>");
         }
      });
    } catch (InvalidInitException e) {
      ...
    }
  }
}
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

For Flutter apps, initialize the SDK using native code in your `AppDelegate` and `MainApplication` in iOS and Android, respectively.

The initialization code is located in the [Flutter ACPCore Github README](https://github.com/adobe/flutter_acpcore).
{% endtab %}

{% tab title="Cordova" %}
For Cordova apps, initialize the SDK using native code in your `AppDelegate` and `MainApplication` in iOS and Android, respectively.

**iOS**

```text
// Import the SDK
#import "ACPCore.h"
#import "ACPLifecycle.h"
#import "ACPIdentity.h"
#import "ACPSignal.h"
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {  
  // make sure to set the wrapper type at the beginning of initialization
  [ACPCore setWrapperType:ACPMobileWrapperTypeCordova];

  //...
  [ACPCore configureWithAppId:@"yourAppId"];
  [ACPIdentity registerExtension];
  [ACPLifecycle registerExtension];
  [ACPSignal registerExtension];
  // Register any additional extensions

  [ACPCore start:nil];
}
```

**Android**

```java
// Import the SDK
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.WrapperType;

@Override
public void onCreate() {
  //...
  MobileCore.setApplication(this);
  MobileCore.configureWithAppID("yourAppId");

  // make sure to set the wrapper type at the beginning of initialization
  MobileCore.setWrapperType(WrapperType.CORDOVA);

  try {
    Identity.registerExtension();
    Lifecycle.registerExtension();
    Signal.registerExtension();

    // Register any additional extensions
  } catch (Exception e) {
    // handle exception
  }

  MobileCore.start(null);
}
```
{% endtab %}

{% tab title="Unity" %}
### C\#

For Unity apps, initialize the SDK using the following code in the start function of the `MainScript`.

```csharp
using com.adobe.marketing.mobile;
using using AOT;

public class MainScript : MonoBehaviour
{
    [MonoPInvokeCallback(typeof(AdobeStartCallback))]
    public static void HandleStartAdobeCallback()
    {   
        ACPCore.ConfigureWithAppID("1423ae38-8385-8963-8693-28375403491d");
    }

    // Start is called before the first frame update
    void Start()
    {   
        if (Application.platform == RuntimePlatform.Android) {
            ACPCore.SetApplication();
        }

        ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.VERBOSE);
        ACPCore.SetWrapperType();
        ACPIdentity.registerExtension();
        ACPLifecycle.registerExtension();
        ACPSignal.registerExtension();
        ACPCore.Start(HandleStartAdobeCallback);
    }
}
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

For Xamarin Forms applications, the SDK initialization differs, depending on the platform being targeted.

**iOS**

```csharp
using Com.Adobe.Marketing.Mobile;

[Register("AppDelegate")]
public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
{
  //
  // This method is invoked when the application has loaded and is ready to run. In this
  // method you should instantiate the window, load the UI into it and then make the window
  // visible.
  //
  // You have 17 seconds to return from this method, or iOS will terminate your application.
  //
  public override bool FinishedLaunching(UIApplication app, NSDictionary options)
  {
    global::Xamarin.Forms.Forms.Init();
    LoadApplication(new App());

    // set the wrapper type
    ACPCore.SetWrapperType(ACPMobileWrapperType.Xamarin);

    // set launch config
    ACPCore.ConfigureWithAppID("your-app-id");

    // register SDK extensions
    ACPIdentity.RegisterExtension();
    ACPLifecycle.RegisterExtension();
    ACPSignal.RegisterExtension();

    // start core
    ACPCore.Start(null);
  }
```

**Android**

```csharp
using Com.Adobe.Marketing.Mobile;

[Activity(Label = "TestApp", Icon = "@mipmap/icon", Theme = "@style/MainTheme", MainLauncher = true, ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation)]
public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
{
  protected override void OnCreate(Bundle savedInstanceState)
  {
    base.OnCreate(savedInstanceState);

    global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
    LoadApplication(new App());

    // set the wrapper type
    ACPCore.SetWrapperType(WrapperType.Xamarin);

    // register SDK extensions
    ACPCore.Application = this.Application;
    ACPIdentity.RegisterExtension();
    ACPLifecycle.RegisterExtension();
    ACPSignal.RegisterExtension();

    // start core
    ACPCore.Start(null);
}
```
{% endtab %}
{% endtabs %}

## registerURLHandler 

Mobile SDK allows you to add a callback function that is triggered before the [`open url`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-types) action occurs. If the callback function returns **Yes**, the SDK does not complete the `open url` action. If the callback function returns **No**, the SDK completes the `open url` action.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Objective C**

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

## setAdvertisingIdentifier

The advertising ID is preserved between app upgrades, is saved and restored during the standard application backup process, available via [Signals](signals/), and is removed at uninstall.

For more information about identity in Mobile Core, please read the documentation on the [identity APIs](identity/identity-api-reference.md#setadvertisingidentifier).

## setAppGroup \(iOS only\)

You can use the `setAppGroup` method to set the app group, which is used to share user defaults and files among the containing app and the extension apps.

{% hint style="info" %}
This API _must_ be called in `AppDidFinishLaunching` and before any other interactions with the Adobe Experience SDK have happened. Only the first call to this function will have any effect.
{% endhint %}

{% tabs %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

**Syntax**

```swift
public static func setAppGroup(_ group: String?)
```

**Example**

```text
[ACPCore setAppGroup:@"app-group-id"];
```

**Swift**

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

## setApplication \(Android only\)

When building Android applications, the `android.app.Application` reference must be passed to Mobile SDK, which allows Mobile SDK to access the `android.app.Context` and monitor the lifecycle of the Android application.

{% hint style="warning" %}
Android applications must call `MobileCore.setApplication()` before calling any other Mobile SDK API.
{% endhint %}

You can use the `setApplication` method to pass the Android `Application` instance to Mobile SDK.

{% tabs %}
{% tab title="Xamarin" %}
**C\#**

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


## setLogLevel

The logging APIs allow log messages to be tagged and filtered with the Mobile SDK log messages. This allows application developers to filter the logged messages based on the current logging mode.

Application developers can use the `setLogLevel` method to filter the log messages that are coming from the Mobile SDK.

From least to most verbose, the order of Mobile SDK logging modes is as follows:

* ERROR
* WARNING
* DEBUG
* VERBOSE / TRACE 

When debugging on iOS, you can use `LogLevel.verbose` to enable all the logging messages that are coming from Mobile SDK and partner extensions. Similarly, on Android, you can use `LoggingMode.VERBOSE` to enable all the logging messages that are coming from Mobile SDK and partner extensions.

In a production application, you should use a less verbose logging mode, such as error-level logging.

By default, Mobile SDK logging mode is set to `LoggingMode.ERROR` for Android and `LogLevel.error`on iOS.

{% hint style="info" %}
* On **Android**, Mobile SDK uses the `android.util.Log` class to log messages.
* On **iOS**, Mobile SDK uses `NSLog` to messages to Apple System Log facility.
{% endhint %}

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective-C**

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

## setPushIdentifier

This API sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

{% hint style="info" %}
It is recommended to call `setPushIdentifier` on each application launch to ensure the most up-to-date device token is set to the SDK. If no device token is available, `null`/`nil` should be passed.
{% endhint %}

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective-C**

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

## setSmallIconResourceID / setLargeIconResourceID \(Android only\)

You can set the small and large icons that will be used for notifications that are created by the SDK. The small icon appears in the status bar and is the secondary image that is displayed when the user sees the complete notification in the notification center. The large icon is the primary image that is displayed when the user sees the complete notification in the notification center.

{% hint style="warning" %}
The following methods are **only** available in Android and Xamarin Android.
{% endhint %}

{% tabs %}

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

## trackAction

Actions are events that occur in your application. You can use the `trackAction` method to track and measure an action. Each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you can use an action to track new subscriptions, every time an article is viewed, or every time a level is completed.

{% hint style="warning" %}
You want to use the `trackAction` method when you want to track an occurring event. In addition to the action name, you can also send context data with each `trackAction` call.
{% endhint %}

{% hint style="info" %}
If you installed and configured the Adobe Analytics extension, this method sends an Adobe Analytics action tracking hit with the provided optional context data.
{% endhint %}

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective-C**

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

{% tab title="Flutter" %}
**Dart**

**Syntax**

```dart
Future<void> trackAction (String action, {Map<String, String> contextData});
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```dart
FlutterACPCore.trackAction("action name",  data: {"key": "value"});
```
{% endtab %}

{% tab title="Unity" %}
**C\#**

**Syntax**

```csharp
public static void TrackAction(string name, Dictionary<string, string> contextDataDict)
```

* * _name_ contains the name of the action to track.
* _contextDataDict_ contains the context data to attach on the hit.

**Example**

```csharp
var contextData = new Dictionary<string, string>();
contextData.Add("key", "value");
ACPCore.TrackAction("action", contextData);
```
{% endtab %}

{% tab title="Cordova" %}
**Cordova**

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

## trackState

States represent screens or views in your application. The `trackState` method needs to be called every time a new state is displayed in your application. For example, this method should be called when a user navigates from the home page to the news feed. This method sends an Adobe Analytics state tracking hit with optional context data.

{% hint style="info" %}
If you installed and configured the Adobe Analytics extension, the `trackState` method increments page views and an Adobe Analytics state tracking hit with the provided optional context data.
{% endhint %}

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective-C**

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

## Public classes

{% tabs %}

{% tab title="iOS \(ACP 2.x\)" %}
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

To learn what context data is, please read the [documentation on context data](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=en).


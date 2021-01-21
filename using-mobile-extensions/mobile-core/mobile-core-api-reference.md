# Mobile Core API reference

## Application reference \(Android only\)

When building Android applications, the `android.app.Application` reference must be passed to the Mobile SDK, which allows the Mobile SDK to access the `android.app.Context` and monitor the lifecycle of the Android application.

{% hint style="warning" %}
Android applications must call `MobileCore.setApplication()` before calling any other Mobile SDK API.
{% endhint %}

### Set Application

You can use this API to pass the Android `Application` instance to the SDK.

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


{% endtabs %}

### Get Application

You can use this API to get the previously set Android `Application` instance, and this instance is mainly provided for the third-party extensions.

{% tabs %}
{% tab title="Android" %}
**Java**

### getApplication

{% hint style="warning" %}
`MobileCore.getApplication` might return `null` if the Application object was destroyed or if `MobileCore.setApplication` was not previously called.
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
{% endtabs %}

## Track app actions

Actions are events that occur in your app. You can use this API to track and measure an action. Each action has one or more corresponding metrics that are incremented each time the event occurs. For example, you might call this API for each new subscription each time an article is viewed, or each time a level is completed.

{% hint style="warning" %}
Call this API when an event that you want to track occurs. In addition to the action name, you can send additional context data with each track action call.
{% endhint %}

{% hint style="info" %}
If you installed and configured the Analytics extension, this method sends an Analytics action tracking hit with the optional context data that you provide.
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
* _contextData_ contains the context data to attach on this hit.

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();
additionalContextData.put("customKey", "value");
MobileCore.trackAction("loginClicked", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
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
{% endtabs %}

## Track app states and views

States represent screens or views in your app. Each time a new state is displayed in your application, for example, when a user navigates from the home page to the news feed, this API can be called. This method sends an Analytics state tracking hit with optional context data.

{% hint style="info" %}
If you installed and configured the Analytics extension, this API increments page views and an Analytics state tracking hit with the optional context data that you provide.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
**Java**

In Android, `trackState` is typically called each time a new Activity is loaded.

### trackState

**Syntax**

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on this hit.

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();        
additionalContextData.put("customKey", "value");
MobileCore.trackState("homePage", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
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
{% endtabs %}

## setAdvertisingIdentifier

The advertising ID is preserved between app upgrades, is saved and restored during the standard application backup process, available via [Signals](identity-api-reference.md), and is removed at uninstall.

{% hint style="info" %}
If the current SDK privacy status is `optedout`, the advertising identifier is not set or stored.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

### setAdvertisingIdentifier

This API sets the provided advertising identifier.

#### Java

**Syntax**

```java
public static void setAdvertisingIdentifier(final String advertisingIdentifier);
```

* _advertisingIdentifier_ is a string that provides developers with a simple, standard system to track the Ads through their apps.     

**Example**

{% hint style="warning" %}
This is just an implementation example. For more information about advertising identifiers and how to handle them correctly in your mobile application, see [Google Play Services documentation about Advertising ID](http://www.androiddocs.com/google/play-services/id.html).
{% endhint %}

This example requires Google Play Services to be configured in your mobile application. For instructions on how to import the Google Mobile Ads SDK and how to configure your ApplicationManifest.xml file, see [Google Mobile Ads SDK setup](https://developers.google.com/admob/android/quick-start#import_the_mobile_ads_sdk).

```java
...
@Override
public void onResume() {
    super.onResume();
    ...
    new Thread(new Runnable() {
        @Override
        public void run() {
            String advertisingIdentifier = null;

            try {
                AdvertisingIdClient.Info adInfo = AdvertisingIdClient.getAdvertisingIdInfo(getApplicationContext());
                if (adInfo != null) {
                    if (!adInfo.isLimitAdTrackingEnabled()) {
                        advertisingIdentifier = adInfo.getId();
                    } else {
                        MobileCore.log(LoggingMode.DEBUG, "ExampleActivity", "Limit Ad Tracking is enabled by the user, cannot process the advertising identifier");
                    }
                }

            } catch (IOException e) {
                // Unrecoverable error connecting to Google Play services (e.g.,
                // the old version of the service doesn't support getting AdvertisingId).
                MobileCore.log(LoggingMode.DEBUG, "ExampleActivity", "IOException while retrieving the advertising identifier " + e.getLocalizedMessage());
            } catch (GooglePlayServicesNotAvailableException e) {
                // Google Play services is not available entirely.
                MobileCore.log(LoggingMode.DEBUG, "ExampleActivity", "GooglePlayServicesNotAvailableException while retrieving the advertising identifier " + e.getLocalizedMessage());
            } catch (GooglePlayServicesRepairableException e) {
                // Google Play services is not installed, up-to-date, or enabled.
                MobileCore.log(LoggingMode.DEBUG, "ExampleActivity", "GooglePlayServicesRepairableException while retrieving the advertising identifier " + e.getLocalizedMessage());
            }

            MobileCore.setAdvertisingIdentifier(advertisingIdentifier);
        }
    }).start();
}
```

{% endtab %}

{% tab title="iOS" %}

### setAdvertisingIdentifier

{% hint style="info" %}
To access IDFA  and handle it correctly in your mobile application, see [Apple developer documentation about IDFA](https://developer.apple.com/documentation/adsupport/asidentifiermanager)
{% endhint %}

{% hint style="warning" %}
Starting iOS 14+, applications must use the [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency) framework to request user authorization before using the Identifier for Advertising \(IDFA\).
{% endhint %}

#### iOS

**Syntax**

```swift
@objc(setAdvertisingIdentifier:)
public static func setAdvertisingIdentifier(_ identifier: String?)
```

* _adId_ is a string that provides developers with a simple, standard system to continue to track the Ads through their apps.    

**Example**

**Objective-C**

```objectivec
#import <AdSupport/ASIdentifierManager.h>
#import <AppTrackingTransparency/ATTrackingManager.h>
...

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
-   ...
-   
    if (@available(iOS 14, *)) {
        [self setAdvertisingIdentitiferUsingTrackingManager];
    } else {
        // fallback to earlier versions
        [self setAdvertisingIdentifierUsingIdentifierManager];
    }

}

- (void) setAdvertisingIdentifierUsingIdentifierManager {
    // setup the advertising identifier
    NSString *idfa = nil;
    if ([[ASIdentifierManager sharedManager] isAdvertisingTrackingEnabled]) {
        idfa = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString];
    } 
    [AEPMobileCore setAdvertisingIdentifier:idfa];
}

- (void) setAdvertisingIdentitiferUsingTrackingManager API_AVAILABLE(ios(14)) {
    [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:
    ^(ATTrackingManagerAuthorizationStatus status){
        NSString *idfa = nil;
        switch(status) {
            case ATTrackingManagerAuthorizationStatusAuthorized:
                idfa = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString];
                break;
            case ATTrackingManagerAuthorizationStatusDenied:        
                //handle error       
                break;
            case ATTrackingManagerAuthorizationStatusNotDetermined:   
                //handle error
                break;
            case ATTrackingManagerAuthorizationStatusRestricted:  
                //handle error
                break;
        }
        [AEPMobileCore setAdvertisingIdentifier:idfa];
    }];
}
```

**Swift**

```swift
import AdSupport
import AppTrackingTransparency
...

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    ...
    if #available(iOS 14, *) {
       setAdvertisingIdentitiferUsingTrackingManager()
    } else {
       // Fallback on earlier versions
       setAdvertisingIdentifierUsingIdentifierManager()
    }

}

func setAdvertisingIdentifierUsingIdentifierManager() {
    var idfa:String = "";
        if (ASIdentifierManager.shared().isAdvertisingTrackingEnabled) {
            idfa = ASIdentifierManager.shared().advertisingIdentifier.uuidString;
        }
        MobileCore.setAdvertisingIdentifier(idfa)
}

@available(iOS 14, *)
func setAdvertisingIdentitiferUsingTrackingManager() {
    ATTrackingManager.requestTrackingAuthorization { (status) in
        var idfa: String = "";

        switch (status) {
        case .authorized:
            idfa = ASIdentifierManager.shared().advertisingIdentifier.uuidString
        case .denied:              
             //handle error
        case .notDetermined:     
             //handle error
        case .restricted:       
             //handle error       
        }

        MobileCore.setAdvertisingIdentifier(idfa)
    }
}
```

{% endtab %}


{% endtabs %}

## setPushIdentifier

This API sets the device token for push notifications in the SDK. If the current SDK privacy status is `optedout`, the push identifier is not set.

{% hint style="info" %}
It is recommended to call `setPushIdentifier` on each application launch to ensure the most up-to-date device token is set to the SDK. If no device token is available, `null`/`nil` should be passed.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

### setPushIdentifier

#### Java

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

{% tab title="iOS" %}

### setPushIdentifier

#### iOS

```swift
@objc(setPushIdentifier:)
public static func setPushIdentifier(_ deviceToken: Data?)
```

* _deviceToken_  is a string that contains the device token for push notifications.

**Example**

**Objective-C**

```objectivec
// Set the deviceToken that the APNS has assigned to the device
[AEPMobileCore setPushIdentifier:deviceToken];
```

**Swift**

```swift
// Set the deviceToken that the APNs has assigned to the device
MobileCore.setPushIdentifier(deviceToken)
```

{% endtab %}
{% endtabs %}



## Collect PII

This API allows the SDK to collect sensitive or personally identifiable information \(PII\) data.

{% hint style="warning" %}
Although this API enables the collection of sensitive data, no data is sent to any Adobe or third-party endpoints. To send the data to an endpoint, use a postback of the PII type.
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

{% tab title="iOS" %}
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
{% endtabs %}

## Retrieving stored identifiers

The following SDK identities \(as applicable\) are locally stored:

* Company Context - IMS Org IDs
* Experience Cloud ID \(MID\)
* User IDs
* Integration codes \(ADID, push IDs\)
* Data source IDs \(DPID, DPUUID\)
* Analytics IDs \(AVID, AID, VID, and associated RSIDs\)
* Target legacy IDs \(TNTID, TNT3rdpartyID\)
* Audience Manager ID \(UUID\)

To retrieve data as a JSON string from the SDKs, and send this data to your servers, use the following:

{% hint style="warning" %}
You must call the API below and retrieve identities stored in the SDK, **before** the user opts out.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### getSdkIdentities

#### Syntax

```java
void getSdkIdentities(AdobeCallback<String> callback);
```

* _callback_ is invoked with the SDK identities as a JSON string.
* If an instance of  `AdobeCallbackWithError` is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 5000ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate `AdobeError`.

#### Example

```java
MobileCore.getSdkIdentities(new AdobeCallback<String>() {
    @Override
    public void call(String value) {
        // handle the json string
    }
});
```
{% endtab %}

{% tab title="iOS" %}
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
{% endtabs %}

## Set Icons for local notification \(Android only\)

You can set the small and large icons that will be used for notifications that are created by the SDK. The small icon appears in the status bar and is the secondary image that is displayed when the user sees the complete notification in the notification center. The large icon is the primary image that is displayed when the user sees the complete notification in the notification center.

{% hint style="warning" %}
Those APIs are **only** available in Android and Xamarin Android.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

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
{% endtabs %}

## Logging

The logging APIs allow log messages to be tagged and filtered with the Mobile SDK log messages and allow application developers to filter the logged messages based on the current logging mode.

Application developers can use the `setLogLevel` API to filter the log messages that are coming from the Mobile SDK. When debugging, use `LoggingMode.VERBOSE` \(Android\) / `LogLevel.verbose` \(iOS\) to enable all the logging messages that are coming from the Mobile SDK and partner extensions. In a production application, we recommend that you use a less verbose logging mode, for example `LoggingMode.ERROR` \(Android\) / `LogLevel.error` \(iOS\).

By default, the Mobile SDK logging mode is set to `LoggingMode.ERROR` \(Android\) / `LogLevel.eror` \(iOS\).

As a Mobile SDK extension developer, you should use the MobileCore \(Android\) / ACPCore \(iOS\) `log` API to include extension log messages with Mobile SDK core log messages.

From least to most verbose, here is the order of the mobile SDK logging modes:

* ERROR
* WARNING
* DEBUG
* VERBOSE

{% hint style="info" %}
* In **Android**, the Mobile SDK uses the `android.util.Log` class to print the messages.
* In **iOS**, the Mobile SDK uses the `NSLog` for logging the message to Apple System Log facility.
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
...

MobileCore.setLogLevel(LoggingMode.VERBOSE);
```
{% endtab %}

{% tab title="iOS" %}
**Objective C**

#### setLogLevel

**Syntax**

```swift
@objc(setLogLevel:)
public static func setLogLevel(_ level: LogLevel)
```

**Example**

```objective-c
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

{% tab title="iOS" %}
TBD
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

#### log

**Syntax**

```java
public static void log(final LoggingMode mode, final String tag, final String message)
```

**Example**

```java
MobileCore.log(LoggingMode.DEBUG, "MyClassName", "Provided data was null");
```

**Output Example**

```text
D/AdobeExperienceSDK: MyClassName - Provided data was null
```
{% endtab %}

{% tab title="iOS" %}
TBD
{% endtab %}


{% endtabs %}



## Set App Group \(iOS only\)

You can use this API to set the app group used to share user defaults and files among the containing app and the extension apps.

Note: This API _must_ be called in AppDidFinishLaunching and before any other interactions with the Adobe Experience SDK have happened. Only the first call to this function will have any effect.

{% tabs %}
{% tab title="iOS" %}
**Objective-C**

### setAppGroup

**Objective-C**

#### setAppGroup

**Syntax**

```swift
public static func setAppGroup(_ group: String?)
```

**Example**

```objc
[AEPMobileCore setAppGroup:@"app-group-id"];
```

**Swift**

#### setAppGroup

**Syntax**

```swift
public static func setAppGroup(_ group: String?)
```

**Example**

```swift
MobileCore.setAppGroup("app-group-id")
```
{% endtab %}
{% endtabs %}

## Public Classes

{% tabs %}
{% tab title="Android" %}
#### Android

**AdobeCallback**

This class provides the interface to receive results when the async APIs perform the requested action.

```java
public interface AdobeCallback<T> {    
    void call(final T value);
}
```

**AdobeCallbackWithError**

This class provides the interface to receive results or an error when the async APIs perform the requested action. When using this class, if the request cannot be completed within the default timeout or an unexpected error occurs, the request is aborted and the _fail_ method is called with the corresponding _AdobeError_.

```java
public interface AdobeCallbackWithError<T> extends AdobeCallback<T> {
    void fail(final AdobeError error);
}
```

**AdobeError**

Errors which may be passed to an AdobeCallbackWithError:

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

{% tab title="iOS" %}
#### iOS

**AEPError**

Errors which may be passed to a completion handler callback from any API which uses one:

* `.unexpected` - An unexpected error occurred.
* `.callbackTimeout`The timeout was met.
* `.callbackNil` - The provided callback function is nil.
* `.errorExtensionNotInitialized` - The extension is not initialized.
* `.serverError` - There was a error on the server side.
* `.networkError` - Network connection failed.
* `.invalidRequest` - Invalid request parameters.
* `.invalidResponse` - Invalid server response.

**Examples**

**Objective C**

```objc
[AEPMobileCore getSdkIdentities:^(NSString * _Nullable content, NSError * _Nullable error) {
  if (error) {
    if (error.code == 1) {
      // handle timeout error
    } else if (error.code == 2) {
      // handle nil callback error
    }
    
    ....
    
  } else {
    // use content
  }
}];
```

**Swift**

```swift
MobileCore.getSdkIdentities { identities, error in
    if let error = error{
        switch (error) {
            case AEPError.unexpected:
                // deal with error if needed
                break;
            default:
                break;
        }
    } else{      
    // use content
    }
}
```
{% endtab %}
{% endtabs %}

### Additional Information

* What is [context data](https://marketing.adobe.com/resources/help/en_US/sc/implement/context_data_variables.html)?


# V4 Mobile SDKs to Experience Platform Analytics migration

## Configuration

The AEP Analytics extension uses [Launch](https://launch.adobe.com/) to configure the AEP SDK's. This replaces the ADBMobileConfig.json which the Mobile Services SDK used for configuration. To get started with the AEP SDK's:

1. Create a mobile property on Launch. See [Set up a mobile property](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/b7706ec53f082a5385a6eb5870418af7c116f0b1/getting-started/create-a-mobile-property/README.md) for more information.
2. Configure your mobile app with the create mobile property. The AEP Mobile Core extension provides general functionality required by all the Adobe AEP extensions. The Configuration extension is built into the Mobile Core and contains the `configureWithAppId` API. This API is used to link the Launch mobile property with your mobile app. The documentation for this API can be seen at the [Configuration API Reference](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/b7706ec53f082a5385a6eb5870418af7c116f0b1/using-mobile-extensions/mobile-core/configuration/configuration-api-reference/README.md#configurewithappid) page. A code sample showing the usage of this API is provided below.
3. Once all the Adobe Experience Platform extensions are imported and configured correctly, remove the v4 Mobile SDK dependency. This step is mandatory and a mix of v4 and AEP API calls is not supported.

{% tabs %}
{% tab title="Android" %}

If using Gradle, remove the v4 Mobile SDK dependency:

```java
dependencies {
  implementation 'com.adobe.mobile:adobeMobileLibrary:4.18.2'
  ...
}
```

Alternatively, if the v4 Mobile SDK library is linked as a jar, search for `adobeMobileLibrary` in your project and remove the jar file. 

{% endtab %}

{% tab title="iOS" %}

If using Cocoapods, remove the v4 Mobile SDK dependency from the Podfile:

```bash
target 'YourTarget' do
	pod 'AdobeMobileSDK'
	...
end
```

Alternatively, if the v4 Mobile SDK library is linked in Xcode, select the application target and go to `Build Phases`, then `Link Binary With Libraries` and remove `AdobeMobileLibrary.a`.

{% endtab %}
{% endtabs %}

## Analytics Migration Overview

For an overview of the API mapping between the Mobile Services SDK and AEP SDK's, see the [API Change Log](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/b7706ec53f082a5385a6eb5870418af7c116f0b1/resources/upgrading-to-aep/api-change-log/README.md). This section will go over the Analytics specific changes made with the AEP Analytics extension.

### Deprecated API

| API | Notes |
| :--- | :--- |
| trackActionFromBackground \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html)\) | Deprecated |
| trackLocation:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/geo_poi.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/geo_poi.html)\) | This functionality is available in the [Places extension](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/b7706ec53f082a5385a6eb5870418af7c116f0b1/using-mobile-extensions/adobe-places/README.md). |
| trackBeacon:Data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ibeacon.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/beacon.html)\) | Support modified, [see guide](https://aep-sdks.gitbook.io/docs/resources/user-guides/track-beacon) |
| trackingClearCurrentBeacon \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/ibeacon.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/beacon.html)\) | Support modified, [see guide](https://aep-sdks.gitbook.io/docs/resources/user-guides/track-beacon) |
| trackLifetimeValueIncrease:data: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/lifetime_value.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/lifetime_value.html)\) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics/) and [User Profile](../../foundation-extensions/profile/) extensions. |
| trackTimedActionStart: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics/) and [User Profile](../../foundation-extensions/profile/) extensions. |
| trackTimedActionUpdate: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics/) and [User Profile](../../foundation-extensions/profile/) extensions. |
| trackTimedActionEnd: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics/) and [User Profile](../../foundation-extensions/profile/) extensions. |
| trackTimedActionExists: \([iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/timed_actions.html), [Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/timed_actions.html)\) | This functionality can be recreated using the [Analytics](../../using-mobile-extensions/adobe-analytics/) and [User Profile](../../foundation-extensions/profile/) extensions. |

## AEP SDK Installation and Setup

### Register the AEP Extensions and link the app to the configuration created on Launch

In your App's Application class add the AEP extension registration and configuration code:

{% tabs %}
{% tab title="Android" %}

```java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Identity;

@Override
public void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setContentView(R.layout.main);

  MobileCore.setApplication(getApplication());
  MobileCore.setLogLevel(LoggingMode.DEBUG);
  try {
    Analytics.registerExtension();
    Identity.registerExtension();
    MobileCore.start(new AdobeCallback() {
      @Override
      public void call(Object o) {
        // add your app id from the "Environments" tab on Launch.
        MobileCore.configureWithAppID("your-app-id");
      }
    });
  } catch (InvalidInitException e) {
    e.printStackTrace();
  }
}
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

```text
#import "ACPCore.h"
#import "ACPAnalytics.h"
#import "ACPIdentity.h"

- (BOOL) application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:^{
      // add your app id from the "Environments" tab on Launch.
          [ACPCore configureWithAppId:@"your-app-id"];
    }];
    return YES;
}
```

**Swift**

```swift
import ACPCore
import ACPAnalytics
import ACPIdentity

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
  ACPCore.setLogLevel(ACPMobileLogLevel.debug)
  ACPAnalytics.registerExtension()
  ACPIdentity.registerExtension()
  ACPCore.start(){
      ACPCore.configureWithAppId("your-app-id") 
  }
  return true
}
```
{% endtab %}
{% endtabs %}

In-depth instructions can be seen at the [Analytics Readme](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/b7706ec53f082a5385a6eb5870418af7c116f0b1/using-mobile-extensions/adobe-analytics/readme.md#add-analytics-to-your-app).

## API changes

### Track App State and Track App Actions

{% tabs %}
{% tab title="Android" %}
#### Mobile Services SDK

The Mobile Services SDK syntax and usage examples for these API are:

```java
// syntax
public static void trackState(final String state, final Map<String, Object> contextData)

// usage
Analytics.trackState("MainPage", new HashMap<String, Object>() {{
  put("firstVisit", true);
}});
```

```java
// syntax
public static void trackAction(final String action, final Map<String, Object> contextData)

// usage
Analytics.trackAction("linkClicked", new HashMap<String, Object>() {{
  put("url", "https://www.adobe.com");
}});
```

#### AEP SDK

The AEP SDK's have moved the `trackAction` and `trackState` APIs to the MobileCore extension. In addition, the context data Map has been changed from `<String, Object>` to `<String, String>`. The syntax is:

```java
// syntax
public static void trackState(final String state, final Map<String, String> contextData)

// usage
MobileCore.trackState("MainPage", new HashMap<String, String>() {{
  put("firstVisit", "true");
}});
```

```java
// syntax
public static void trackAction(final String action, final Map<String, String> contextData)

// usage
MobileCore.trackAction("linkClicked", new HashMap<String, String>() {{
  put("url", "https://www.adobe.com");
}});
```
{% endtab %}

{% tab title="iOS" %}
The Mobile Services SDK syntax and usage examples for these API are:

#### Mobile Services SDK

```text
// syntax
+ (void) trackState:(NSString *)state data:(NSDictionary *)data;

// usage
[ADBMobile trackState:@"MainPage" data:@{@"firstVisit":@true}];
```

```text
// syntax
+ (void) trackAction:(NSString *)action data:(NSDictionary *)data;

// usage
[ADBMobile trackAction:@"linkClicked" data:@{@"url":@"https://www.adobe.com"}];
```

#### AEP SDK

The AEP SDK's have moved the `trackAction` and `trackState` API's to the MobileCore extension. In addition, the NSDictionary has been changed from `<NSString, NSObject>` to `<NSString, NSString>`. The syntax is:

```text
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary<NSString*, NSString*>*) data;
```

```text
+ (void) trackState: (nullable NSString*) action data: (nullable NSDictionary<NSString*, NSString*>*) data;
```

The usage examples are:

**Objective-C**

```text
[ACPCore trackState:@"MainPage" data:@{@"firstVisit":@"true"}];
[ACPCore trackAction:@"linkClicked" data:@{@"url":@"https://www.adobe.com"}];
```

**Swift**

```swift
ACPCore.trackState("MainPage", data: ["firstVisit": "true"])
ACPCore.trackAction("linkClicked", data: ["url": "https://www.adobe.com"])
```
{% endtab %}
{% endtabs %}

## Privacy status changes in the AEP SDK

The privacy status API `setPrivacyStatus` and `getPrivacyStatus` can be found in the MobileCore. Like the Mobile Services SDK, the Analytics extension will follow these behaviors depending on the privacy status set:

**Opted in**: Analytics hits will be sent.

**Unknown**: Analytics hits will be queued.

**Opted out**: Analytics hits will be dropped.

{% tabs %}
{% tab title="Android" %}
#### AEP SDK

The syntax and usage examples for `setPrivacyStatus` are:

```java
// syntax
public static void setPrivacyStatus(final MobilePrivacyStatus privacyStatus);

// usage
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN);
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT);
MobileCore.setPrivacyStatus(MobilePrivacyStatus.UNKNOWN);
```

The syntax and usage examples for `getPrivacyStatus` are:

```java
// syntax
void getPrivacyStatus(AdobeCallback<MobilePrivacyStatus> callback);

// usage
MobileCore.getPrivacyStatus(new AdobeCallback<MobilePrivacyStatus>() {
    @Override
    public void call(MobilePrivacyStatus status) {
          System.out.println("privacy status: " + status);
    }
});
```

The callback is invoked after the privacy status is available. If an instance of AdobeCallbackWithError is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 5000ms. If the operation times out or an unexpected error occurs, the fail method is called with the appropriate AdobeError.
{% endtab %}

{% tab title="iOS" %}
#### AEP SDK

The syntax for `setPrivacyStatus` is:

```text
// syntax
+ (void) setPrivacyStatus: (ACPMobilePrivacyStatus) status;
```

The syntax for `getPrivacyStatus` is:

```text
// syntax
+ (void) getPrivacyStatus: (nonnull void (^) (ACPMobilePrivacyStatus status)) callback;
+ (void) getPrivacyStatusWithCompletionHandler: (nonnull void (^) (ACPMobilePrivacyStatus status, NSError* _Nullable error)) completionHandler;
```

The callback is invoked after the privacy status is available.

If the API with the completion handler is used, the completion handler will be invoked with the current privacy status, or error if an unexpected error occurs or the request times out. The default timeout is 5000ms.

The usage example for `getPrivacyStatus` is:

**Objective-C**

```text
[ACPCore getPrivacyStatus:^(ACPMobilePrivacyStatus status) {
  switch (status) {
    case ACPMobilePrivacyStatusOptIn: NSLog(@"Privacy Status: Opt-In");
    case ACPMobilePrivacyStatusOptOut: NSLog(@"Privacy Status: Opt-Out");
    case ACPMobilePrivacyStatusUnknown: NSLog(@"Privacy Status: Unknown");
    default: break;
  }
}];

[ACPCore getPrivacyStatusWithCompletionHandler:^(ACPMobilePrivacyStatus status, NSError * _Nullable error) {
  if (error) {
    // handle error here
  } else {
    // handle the retrieved privacy status
  }
}];
```

**Swift**

```swift
ACPCore.getPrivacyStatus({ status in
   switch status {
     case ACPMobilePrivacyStatus.optIn: print ("Privacy Status: Opt-In")
     case ACPMobilePrivacyStatus.optOut: print("Privacy Status: Opt-Out")
     case ACPMobilePrivacyStatus.unknown: print("Privacy Status: Unknown")
     default: break
   }
})

ACPCore.getPrivacyStatus(withCompletionHandler: { status, error in
    if error != nil {
      // handle error here
    } else {
      // handle the retrieved privacy status
    }
})
```
{% endtab %}
{% endtabs %}


# Adobe Analytics - Mobile Services

This extension enables in-app messaging, push notifications, and marketing links functionality from [Mobile Services](https://mobilemarketing.adobe.com) on the Experience Platform SDK.

{% hint style="warning" %}
As of **April 1, 2020**, Apple will no longer support UIWebView. To avoid any issues, ensure that you are using the iOS extension versions 1.0.3 or later. For more information, see Apple's documentation on [UIWebView](https://developer.apple.com/documentation/uikit/uiwebview).
{% endhint %}

{% hint style="info" %}
The Adobe Analytics Mobile Marketing Add-on SKU is required to enable Mobile Services access to mobile acquisition, deep linking, geolocation, and mobile messaging capabilities.

For more information, please contact your Adobe Customer Success Manager.
{% endhint %}

Review the following Mobile Services functionality documentation for context and set up before implementation at these links:

* [Getting started with Mobile Services](https://experienceleague.adobe.com/docs/mobile-services/using/get-started-ug/gs.html)
* [Create and managing apps](https://experienceleague.adobe.com/docs/mobile-services/using/manage-apps-ug/manage-apps.html?lang=en)
* [Acquisition and marketing links](https://experienceleague.adobe.com/docs/mobile-services/using/acquisition-main-ug/acquisition-main.html?lang=en)
* [Push and in-app messaging](https://experienceleague.adobe.com/docs/mobile-services/using/messaging-ug/in-app-messaging.html?lang=en)

{% hint style="warning" %}
Postbacks created from the Mobile Services interface are **not** supported. Please use a Launch rule with the Mobile Core extension to create a postback. [Signal extension and Rules Engine integration](../../resources/user-guides/signal-extension-and-rules-engine-integration.md).
{% endhint %}

{% hint style="warning" %}
Before you configure the Mobile Services extension, ensure that you previously created apps in [Mobile Services](https://mobilemarketing.adobe.com). To learn how to create an app in Mobile Services, see the [add a new App](https://experienceleague.adobe.com/docs/mobile-services/using/manage-apps-ug/t-new-app.html?lang=en) tutorial.
{% endhint %}

{% hint style="info" %}
To use location-based functionality for Mobile Services, see the documentation on the [Places Service](https://experienceleague.adobe.com/docs/places/using/home.html?lang=en).
{% endhint %}

To use the Mobile Services extension, complete the following steps:

1. Configure the Mobile Services extension in Launch.
2. If using acquisition and marketing links, update your configuration in the Analytics extension.
3. Add Mobile Services extension to your app.
4. Implement the Mobile Services APIs in your app.

## Configure the Mobile Services extension in Experience Platform Launch

{% hint style="warning" %}
The Mobile Services extension requires the Analytics extension for reporting. It uses the report suite that is specified in the Analytics extension for reporting. However, the Mobile Services extension uses the report suite that is configured for the app in Mobile Services for push and in-app messaging, acquisition, marketing links, and app management. If the report suite in the two locations do not match, a push message from the wrong report suite may be sent.
{% endhint %}

### Automatic configuration \(Recommended\)

1. In Experience Platform Launch, click the **Extensions** tab.
2. Choose **Catalog**, locate the **Adobe Analytics – Mobile Services** extension, and click **Install**.
3. Select a Mobile Services app and complete the following tasks:
   1. In **Mobile Services app**, select app from the drop-down list.
   2. Click **Save**.
   3. Follow the publishing process to update the SDK configuration.

![Mobile Services Extension Configuration](../../.gitbook/assets/screen-shot-2019-04-04-at-10.37.34-pm.png)

### Manual configuration

{% hint style="danger" %}
The following instructions only apply if you **do not** see your app listed or need to manually configure your Mobile Services app.
{% endhint %}

{% hint style="warning" %}
If you are sending data to multiple Analytics report suites, use the Acquisition App ID from the app that is associated with the first report suite in your list of report suite IDs.
{% endhint %}

![](../../.gitbook/assets/screen-shot-2019-04-04-at-10.37.49-pm.png)

To install the Mobile Services extension, complete the following steps:

1. Select **Enter Custom settings**.
2. Enter an Acquisition time out. The recommended time out is 5 seconds. To enable app acquisition, this value must be greater than 0.
3. Provide the **Acquisition App ID** \(sample value: `0eb9f2791f0880623f91e41e5309d2ae25066e513054a4cb59168dc886b526da)`\).

   You can find the Acquisition App ID in Mobile Services.

4. Select your app, navigate to Manage App Settings page, and in the **SDK Acquisition Options** section, copy the hashed string similar to the highlighted value:

   ![](../../.gitbook/assets/screen-shot-2019-04-05-at-1.03.42-pm-1.png)

5. Provide the **Messages URL**. This value would look something similar to: `https://assets.adobedtm.com/b213432c5204bf94318f4ef0539a38b487d10368/scripts/satellite-5c7711bc64746d7f5800036e.json`

   You can find the Messages URL from your `ADBMobileConfig.json` file typically near the bottom of the file.

   ![](../../.gitbook/assets/screen-shot-2019-04-05-at-1.08.29-pm.png)

6. Click **Save**.
7. Follow the publishing process to update your SDK configuration.

## Configure the Adobe Analytics extension

1. To ensure that this extension is correctly configured and implemented, follow the steps in the [configure the Mobile Services extension in Experience Platform Launch](https://app.gitbook.com/@aep-sdks/s/docs/~/drafts/-LzsbnKuIZ7JbOKOD9DC/using-mobile-extensions/adobe-analytics-mobile-services#configure-the-adobe-analytics-extension) tutorial.
2. In **Launch Hit Delay**, type a value of 5s or more to ensure that the acquisition context is sent to Analytics with your Lifecycle information.

![](../../.gitbook/assets/screen-shot-2019-04-05-at-1.50.10-pm.png)

## Add the Mobile Services extension to your app

{% hint style="info" %}
The Mobile Services extension depends on the Core extension, which includes the Identity and Lifecycle frameworks and the Analytics extension.
{% endhint %}

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}
You can add the library to your project through your `Podfile` by adding the `ACPMobileServices` pod.

Import the library into your project:

### Objective-C

```objectivec
#import "ACPCore.h"
#import “ACPIdentity.h”
#import “ACPLifecycle.h”
#import "ACPAnalytics.h"
#import "ACPMobileServices.h"
```
### Swift

```swift
import ACPCore
import ACPIdentity
import ACPLifecycle
import ACPAnalytics
import ACPMobileServices
```


{% endtab %}

{% endtabs %}

## Register Mobile Services with Mobile Core

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}

In your app's `application:didFinishLaunchingWithOptions` function, register the Mobile Services extension with the Mobile Core:

### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   [ACPAnalytics registerExtension];
   [ACPLifecycle registerExtension];
   [ACPIdentity registerExtension];
   [ACPMobileServices registerExtension];
   [ACPCore start:nil]
   // Override point for customization after application launch.
   return YES;
}
```
### Swift

```swift
func application(_application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool{
        ACPAnalytics.registerExtension()
        ACPIdentity.registerExtension()
        ACPLifecycle.registerExtension()
        ACPMobileServices.registerExtension()
        ACPCore.start {
        	ACPCore.lifecycleStart(nil)
        }
    ...
    return true
  }
```

{% endtab %}

{% endtabs %}

## Implement Mobile Services APIs in your app

To use your Android or iOS extension with the Experience Platform SDKs, implement the following APIs:

### Set up push messaging

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}
{% hint style="warning" %}
iOS simulators do not support push messaging.
{% endhint %}

After following Apple's [configure remote notification document](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1), to get your app ready to handle push notifications, set the push token by using the [`setPushIdentifier`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#setpushidentifier) API:

**Syntax**

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

**Example**

### Objective-C

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  [ACPCore setPushIdentifier:deviceToken];
  //...
}
```

### Swift

```swift
func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
    let token = tokenParts.joined()
    print("Device Token: (token)")

    // Send push token to experience platform
    ACPCore.setPushIdentifier(deviceToken)
}
```

{% endtab %}

{% endtabs %}

### Debugging the push messaging set up

If the Mobile Services API is correctly configured, after installing your app on a mobile device, verify that the following SDK debug log is displayed:

To verify, make a request to `demdex.net`, containing the device push token has been sent:

```text
2019-01-31 18:22:35.261676-0800 DemoApp[935:156015] [AMSDK DEBUG <com.adobe.module.identity>]: Sending request (https://dpm.demdex.net/id?d_rtbd=json&d_ver=2&d_orgid=B1F855165B4C9EA50A495E06@AdobeOrg&d_mid=43583282444503123217621782542046274680&d_blob=j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI&dcs_region=9)
```

### Set up push tracking

Use the following API to track a push messaging click in Adobe Analytics.

{% hint style="info" %}
Using the following API does not increment page views.
{% endhint %}

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}
Use the following API to track a push messaging click in Adobe Analytics.

**Syntax**

```objectivec
+ (void) collectLaunchInfo:(NSDictionary *)userInfo;
```

**Example**

### Objective-C

```objectivec
[ACPCore collectLaunchInfo:userInfo];
```
### Swift

```swift
ACPCore.collectLaunchInfo(userInfo)
```

{% endtab %}

{% endtabs %}

## Troubleshooting push messaging

For more information, see the following:

* [iOS troubleshooting guide](https://experienceleague.adobe.com/docs/mobile-services/ios/messaging-ios/push-messaging/c-troubleshooting-push-messaging.html)

## Set up in-app messaging

This feature allows you to deliver in-app messages that are triggered from any analytics data or event. After the implementation, messages are dynamically delivered to the app and do not require a code update. In-app messages are created in Mobile Services. For more information, see the [create an in-app message](https://experienceleague.adobe.com/docs/mobile-services/android/messaging-android/inapp-messaging/messaging.html) tutorial.

To set up your app for in-app messages, implement the following instructions. You can complete these steps even if you have not yet defined any messages in Mobile Services. After you define messages, they are delivered dynamically to your app and displayed without an app store update.

{% tabs %}
{% tab title="iOS" %}
No setup is required for iOS, since Mobile SDK automatically handles in-app message support.
{% endtab %}
{% endtabs %}

## Fallback images

When creating a full-screen message, you can optionally specify a fallback image. If your message cannot retrieve its intended image from the web, the SDK attempts to load the image with the same name from your application’s assets folder. This allows you to show your message in its original form, even if the user is offline or the predetermined image is unreachable.

{% hint style="warning" %}
The fallback image asset name is specified when you configure the message in Mobile Services. You need to ensure that the specified resource is available.
{% endhint %}

## Configuring notification icons

The following methods allow you to configure the small and large icons that appear in the notification area, and the large icon that is displayed when notifications appear in the notification drawer.

{% tabs %}
{% tab title="iOS" %}
No setup is required on iOS, since icons are automatically handled by the SDK.
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="iOS" %}
No setup is required, since icons are automatically handled by the SDK for iOS.
{% endtab %}
{% endtabs %}

### Tracking in-app messages

The SDK automatically tracks metrics for your in-app messages.

For full screen and alert style in-app messages, the following metrics are tracked:

* **Impressions**: when user triggers an in-app message.
* **Click throughs**: when user clicks the **Click through** button.
* **Cancels**: when user clicks the **Cancel** button.

For custom full screen in-app messages, the HTML content in the message needs to include the correct code to notify the SDK tracking about the following buttons:

* **Click-through** \(redirect\) example tracking: `adbinapp://confirm/?url=http://www.yoursite.com`
* **Cancel** \(close\) example tracking: `adbinapp://cancel`

For local \(remote\) notifications, the following metrics are tracked:

* **Impressions**: when user triggers the notification.
* **Opens**: when user opens app from the notification.

The following example shows you how to include open tracking:

{% tabs %}
{% tab title="iOS" %}
```objectivec
- (BOOL) application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

  // handle local notification click-throughs for iOS 10 and older
  NSDictionary *localNotificationDictionary = launchOptions[UIApplicationLaunchOptionsLocalNotificationKey];
  if ([localNotificationDictionary isKindOfClass:[NSDictionary class]]) {
       [ACPCore collectLaunchInfo:localNotificationDictionary];
  }

}
- (void) application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
   [ACPCore collectLaunchInfo:notification.userInfo];
}
```
{% endtab %}
{% endtabs %}

### Troubleshooting in-app messaging

For more information, see the following:

* [iOS Troubleshooting guide](https://experienceleague.adobe.com/docs/mobile-services/ios/messaging-ios/in-app-messaging/in-apps-ts.html)

### Acquisition and marketing links

Acquisition and marketing links must be created in Adobe Mobile Services. For more information, see the documentation on [Acquisition](https://experienceleague.adobe.com/docs/mobile-services/using/acquisition-main-ug/acquisition-main.html) within the Mobile Services.

### Deep link tracking

The SDK can parse key-value pairs of data that are appended to any deep or universal link, provided the link contains a key `a.deeplink.id` and a corresponding non-null and user generated value. All key-value pairs of data that are appended to the URL string are parsed, attached to a lifecycle hit as context data, and sent to Adobe Analytics.

You can also append one or more of the following reserved keys, with user-generated values, to the deep or universal link:

* `a.launch.campaign.trackingcode`
* `a.launch.campaign.source`
* `a.launch.campaign.medium`
* `a.launch.campaign.medium`
* `a.launch.campaign.content`

{% hint style="warning" %}
Ensure that the deep link URL has the `a.deeplink.id` key in the URL string. If `a.deeplink.id` is not found, none of the appended URL parameters are sent to Analytics via context data.
{% endhint %}

{% tabs %}
{% tab title="iOS (ACP 2.x)" %}

### trackAdobeDeepLink

**Syntax**

```objectivec
+ (void) trackAdobeDeepLink: (NSURL* _Nonnull) deeplink;
```

**Example**

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString *, id> *)options {
    [ACPMobileServices trackAdobeDeepLink:url];
    /*
     Handle deep link
     */
    return YES;
}
```

**Swift**

```swift
func application(_ application: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    ACPMobileServices.trackAdobeDeepLink(url)
    /*
     Handle deep link
     */
    return true
}
```

In iOS 13 and later, for a scene-based application, use the `UISceneDelegate`'s `scene(_:openURLContexts:)` method as follows:

**Objective-C**

```objectivec
- (void) scene:(UIScene *)scene openURLContexts:(NSSet<UIOpenURLContext *> *)URLContexts {
    UIOpenURLContext * urlContext = URLContexts.anyObject;
    if (urlContext != nil) {
        [ACPMobileServices trackAdobeDeepLink:url];
        /*
         Handle deep link
         */
    }
}
```

**Swift**

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    guard let urlContexts = URLContexts.first else { return }
    ACPMobileServices.trackAdobeDeepLink(urlContexts.url)
    /*
     Handle deep link
     */
}
```

{% endtab %}

{% endtabs %}

## Integration with Apple Search Ads \(iOS\)

The Adobe Experience Platform SDK leverages [Apple's Search Ads attribution](https://developer.apple.com/documentation/iad/setting_up_apple_search_ads_attribution) to attribute app downloads that originate from Search Ads campaigns in the Apple App Store. For more information about Search Ad campaigns, see [Apple Search Ads](https://searchads.apple.com/). This optional feature helps you easily measure the effectiveness of your Search Ads app download campaigns by adding a few lines of code to your app.

### Implement Search Ads integration

To enable your app for Search Ad attribution, you will need to [add the iAd framework](https://developer.apple.com/documentation/iad/setting_up_apple_search_ads_attribution#overview), in addition to the Mobile Services extension to your app.

### Reporting on Search Ads Attribution

Apple Search Ads attribution data is provided in the acquisition name, the source, and the term values.

If `attribution = true` , all of the `iad-*` fields will be included in a Lifecycle request to Adobe Analytics. In addition, the following values will be mapped from the "iad" dictionary to our typical acquisition context data fields:

* `iad-campaign-id` --&gt; `a.referrer.campaign.trackingcode`
* `iad-campaign-name` --&gt; `a.referrer.campaign.name`
* `iad-adgroup-id` --&gt; `a.referrer.campaign.content`
* `iad-keyword` --&gt; `a.referrer.campaign.term`

This mapping ensures that the values are available in Adobe Analytics standard reporting.

## Migration notes

To prepare for your migration, please note the following information:

* Lifetime value is **not** supported on the Experience Platform SDK, so it should not be used to trigger in-app messages or local notifications.
* `ce` is no longer supported as a trigger for in-app messages or local notifications.
* `a.internalaction` or `action` \(from Lifecycle\) can be used to trigger in-app messages or local notifications. You should, however, use `LaunchEvent` instead.
* Local notifications do **not** support Android 8.0 or higher.

### Configuration keys

| Key | Description |
| :--- | :--- |
| mobile.acquisitionTimeout | Amount of time, in seconds, to wait for acquisition information from the Mobile Services acquisition server. |
| mobile.acquisitionAppId | App ID uniquely identifies the app on the Mobile Services acquisition server. |
| mobile.messagesUrl | Messages URL from your configuration \(`ADBMobileConfig.json`\) file's remotes section. |

## Watch the video

{% embed url="https://youtu.be/VKI2ECZU3bU" caption="Video showing Mobile Services integration with Adobe Experience Platform Mobile SDK" %}

### Additional information

* Visit [Mobile Services documentation](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=en)
* Visit [Mobile Services](https://mobilemarketing.adobe.com)


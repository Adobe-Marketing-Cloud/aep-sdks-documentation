# Adobe Campaign Standard

{% hint style="info" %}
**Before** you install or configure the Campaign Standard extension, read [_Getting Started_](../../getting-started/create-a-mobile-property.md) and [Configuring a mobile application using Adobe Experience Platform SDKs](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html).
{% endhint %}

{% hint style="danger" %}
If you participated in the Campaign Standard beta, to use the new Campaign Standard extension, go to [launch.adobe.com](https://launch.adobe.com), instead of the Experience Platform Launch integration environment, .
{% endhint %}

## Configure the Campaign Standard extension in Experience Platform Launch

1. In Experience Platform Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Campaign Standard** extension, and click **Install**.
3. Provide the extension settings.
4. Click **Save**.
5. Follow the publishing process to update SDK configuration.

### Configure the Campaign Standard extension

![](../../.gitbook/assets/campaign-extension-config-v5.png)

#### Campaign Standard endpoints

Provide endpoint URL\(s\) for your Campaign Standard instances. You can specify up to three unique endpoints for your development, staging, and production environments. In most cases, the server endpoint is the root URL address, for example, `companyname.campaign.adobe.com`.

{% hint style="warning" %}
For this extension, these endpoint URLs should be typed in **without** the `http://` or `https://.`and **cannot** end with a forward slash.
{% endhint %}

#### pKey

A unique, auto-generated identifier for a mobile app that was configured in Adobe Campaign Standard. After you configure this extension in Experience Platform Launch, configure your Launch mobile property in Campaign Standard. For more information, see [Setting up your Adobe Launch application in Adobe Campaign](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html#SettingupyourAdobeExperiencePlatformLaunchapplicationinAdobeCampaign).

After the configuration is successful in Campaign, the pKey is automatically generated and configured in Experience Platform Launch Campaign extension for a successful validation.

#### MCIAS region

Select an MCIAS region based on your customer's location or enter a custom endpoint. The SDK retrieves all in-app messaging rules and definition payloads from this endpoint.

{% hint style="warning" %}
For this extension, the custom MCIAS endpoint URL should be typed in **without** the `http://` or `https://` and **cannot** end with a forward slash.
{% endhint %}

#### Request timeout

Time in seconds to wait for a response from the in-app messaging service before timing out. The default timeout value is 5 seconds, and the minimum timeout value is 1 second.

{% hint style="warning" %}
The **Request Timeout** value must be a non-zero number.
{% endhint %}

## Add the Campaign Standard extension to your app

Remember the following information when you add the Campaign extension to your app:

| Extension | Information |
| :--- | :--- |

| Campaign Standard | This Campaign Standard extension requires the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core), [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile), [Lifecycle](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle), and [Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) extensions. You should always ensure that you get the latest version of the extension. |
| :--- | :--- |


| Profile | The Profile extension is required for In-App trigger frequencies to work accurately. For more information, see [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile). |
| :--- | :--- |

| Signal | The Signal extension is required for all postback rules to work. For more information, see [Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals). |
| :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">Lifecycle</th>
      <th style="text-align:left">
        <p>Lifecycle extension is required for a profile to get registered in Campaign.
          You also need to implement Lifecycle APIs. For more information, see</p>
        <p><a href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-android">Lifecycle extension in Android</a> or
          <a
          href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-ios">Lifecycle extension in iOS</a>.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>{% hint style="info" %}
The instructions to add these extensions to your mobile app are also available in Experience Platform Launch. To access the installation dialog box, open your mobile property, click the **Environments** tab, and click **Install**.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

1. Add the Campaign Standard, [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) and [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile) extensions to your project using the app's Gradle file.

```java
implementation 'com.adobe.marketing.mobile:campaign:1.+'
implementation 'com.adobe.marketing.mobile:userprofile:1.+'
implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
```

1. Import the Campaign Standard, [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core), [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile), [Lifecycle](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle), and [Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) extensions in your application's main activity.

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Campaign;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
```

{% hint style="info" %}
To complete a manual installation, go to the [Adobe Experience Platform SDKs for Android GitHub](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) repo, fetch the Mobile Core, Campaign Standard, Profile, Lifecycle, and Signal artifacts, and complete the steps in the [Manual installation](https://github.com/Adobe-Marketing-Cloud/acp-sdks/blob/master/README.md#manual-installation) section.
{% endhint %}
{% endtab %}

{% tab title="iOS" %}
1. Add the Campaign Standard, [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) and [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile) extensions to your project using Cocoapods.

![](../../.gitbook/assets/acs-pods.png)

{% hint style="info" %}
To complete a manual installation, go to the [Adobe Experience Platform SDKs for iOS GitHub](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS) repo, fetch the Mobile Core, Campaign Standard, Profile, Lifecycle, and Signal artifacts, and complete the steps in the [Manual installation](https://github.com/Adobe-Marketing-Cloud/acp-sdks/blob/master/README.md#manual-installation-1) section.
{% endhint %}

1. In Xcode, import the Mobile Core, Campaign Standard, Profile, Lifecycle, and Signal extensions:

#### Objective-C

```objectivec
#import "ACPCore.h"
#import "ACPCampaign.h"
#import "ACPUserProfile.h"
#import "ACPIdentity.h"
#import "ACPLifecycle.h"
#import "ACPSignal.h"
```

#### Swift

```swift
import ACPCore
import ACPCampaign
import ACPUserProfile
```
{% endtab %}

{% tab title="React Native" %}
You'll need to install the SDK with [npm](https://www.npmjs.com/) and configure the native Android/iOS project in your react native project. Before installing the Campaign Standard extension, you'll need to install the [Core](../mobile-core/) extension. Follow these steps to get started:

#### Create React Native Project

```bash
react-native init MyReactApp
```

#### Install JavaScript packages

Install and link the @adobe/react-native-acpcampaign package:

```bash
npm install @adobe/react-native-acpcampaign
react-native link @adobe/react-native-acpcampaign
```

#### Import the extension

```bash
import {ACPCampaign} from '@adobe/react-native-acpcampaign';
```
{% endtab %}
{% endtabs %}

### Register the Campaign Standard extension with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### **Java**

1. In your app's `OnCreate` method, register the Campaign, Identity, Signal, and Lifecycle extensions:

```java
public class CampaignTestApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);

        try {
            Campaign.registerExtension();
            UserProfile.registerExtension();
            Identity.registerExtension();
            Lifecycle.registerExtension();
            Signal.registerExtension();
            MobileCore.start(new AdobeCallback () {
                @Override
                public void call(Object o) {
                    MobileCore.configureWithAppID("launch-EN2c0ccd3a457a4c47b65a6b085e269c91-staging");
                }
            });
        } catch (InvalidInitException e) {
            Log.e("CampaignTestApp", e.getMessage());
        }

    }
}
```

For more information about starting Lifecycle, see [Lifecycle extension in Android](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-android).
{% endtab %}

{% tab title="iOS" %}
1. In your app's `application:didFinishLaunchingWithOptions:` method, register the Campaign, Identity, Signal, and Lifecycle extensions:

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"launch-EN2c0ccd3a457a4c47b65a6b085e269c91-staging"];

    [ACPCampaign registerExtension];
    [ACPUserProfile registerExtension];
    [ACPIdentity registerExtension];
    [ACPLifecycle registerExtension];
    [ACPSignal registerExtension];
    [ACPCore start:^{
        [ACPCore lifecycleStart:nil];
    }];
  // Override point for customization after application launch.
  return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
       ACPCore.setLogLevel(.debug)
    ACPCore.configure(withAppId: "launch-EN2c0ccd3a457a4c47b65a6b085e269c91-staging")

    ACPCampaign.registerExtension()
    ACPUserProfile.registerExtension()
    ACPIdentity.registerExtension()
    ACPLifecycle.registerExtension()
    ACPSignal.registerExtension()
    ACPCore.start {
        ACPCore.lifecycleStart(nil)
    }

  return true;
}
```

For more information about starting Lifecycle, see [Lifecycle extension in iOS](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-ios).
{% endtab %}

{% tab title="React Native" %}
To register the Campaign Standard with Core, use the following API:

#### JavaScript

```javascript
ACPCampaign.registerExtension();
```
{% endtab %}
{% endtabs %}

### Initialize the SDK and set up tracking

To initialize the SDK and set up tracking, see [Initialize the SDK and set up tracking](https://aep-sdks.gitbook.io/docs/getting-started/initialize-the-sdk).

### Set up in-app messaging

{% hint style="info" %}
Need help creating an in-app message using Adobe Campaign? For more information, see [Preparing and sending an In-App message](https://helpx.adobe.com/campaign/standard/channels/using/preparing-and-sending-an-in-app-message.html).
{% endhint %}

{% hint style="warning" %}
If you are developing an Android application, to correctly display fullscreen in-app messages, add the Campaign Standard extension's `FullscreenMessageActivity` to your AndroidManifest.xml file:

```markup
<activity android:name="com.adobe.marketing.mobile.FullscreenMessageActivity" />
```

In addition to adding the `FullscreenMessageActivity`, a global lifecycle callback must be defined in your app's MainActivity to ensure the proper display of fullscreen in-app messages. To define the global lifecycle callback, see [Implementing Global Lifecycle Callbacks](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-android#implementing-global-lifecycle-callbacks).
{% endhint %}

### Set up local notifications

To set up local notifications in Android, update the AndroidManifest.xml file with `<receiver android:name="com.adobe.marketing.mobile.LocalNotificationHandler"/>`. To configure the notification icons that the local notification will use, see [Configuring notification icons](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#configuring-notification-icons).

### Set up push messaging

To enable push messaging with Adobe Campaign, call `setPushIdentifer` to send the push identifier that is received from the Apple Push Notification Service (APNS) or Firebase Cloud Messaging Platform (FCM) to the Adobe Identity service. For more information about the `setPushIdentifer` API, see [setPushIdentifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#setPushIdentifierTitle).

For more information about setting up your iOS app to connect to APNS and retrieve a device token that will be used as a push identifier, see [Registering Your App with APNs](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns?language=objc). For more information about setting up your Android app to connect to FCM and retrieve a device registration token that will be used as a push identifier, see [Set up a Firebase Cloud Messaging client app on Android](https://firebase.google.com/docs/cloud-messaging/android/client).

{% hint style="info" %}
Need help creating a push notification using Adobe Campaign? For more information, see [Preparing and sending a push notification](https://helpx.adobe.com/campaign/standard/channels/using/preparing-and-sending-a-push-notification.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}

#### Example

```java
FirebaseInstanceId.getInstance().getInstanceId()
        .addOnCompleteListener(new OnCompleteListener<InstanceIdResult>() {
            @Override
            public void onComplete(@NonNull Task<InstanceIdResult> task) {
                if (!task.isSuccessful()) {
                    return;
                }
                // Get new Instance ID token
                String registrationID = task.getResult().getToken();
                // Log and toast
                System.out.println("Received new registration token: " + registrationID);
                // invoke the API to send the push identifier to the Identity Service
                MobileCore.setPushIdentifier(registrationID);
            }
});
```

{% endtab %}

{% tab title="iOS" %}
{% hint style="warning" %}
iOS simulators do not support push messaging.
{% endhint %}

#### Objective-C

#### Example

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  [ACPCore setPushIdentifier:deviceToken];
  //...
}
```

#### Swift

#### Example

```swift
func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
  // Set the deviceToken that the APNS has assigned to the device
  ACPCore.setPushIdentifier(deviceToken)
  //...
}
```

{% endtab %}

{% tab title="React Native" %}

Before you use the following API in your React Native project, complete the steps in the **Android** and **iOS** tabs to set up platform-specific push configuration.

#### Example

```javascript
ACPCore.setPushIdentifier("pushID");
```

{% endtab %}
{% endtabs %}

## Tracking local and push notification message interactions

User interactions with local or push notifications can be tracked by invoking the `collectMessageInfo` API. After the API is invoked, a network request is made to Campaign that contains the message interaction event.

{% hint style="warning" %}
The code samples below are provided as examples on how to correctly invoke the `collectMessageInfo` API. The Campaign documents on local and push notification tracking are the recommended source for the proper implementation of local and push notification message tracking. The Campaign document about local notification tracking is [Implementing local notification tracking](https://helpx.adobe.com/campaign/kb/local-notification-tracking.html#Description) and the Campaign document about push notification tracking is [Push Tracking](https://helpx.adobe.com/campaign/kb/push-tracking.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}

#### Syntax

```java
public static void collectMessageInfo(final Map<String, Object> messageInfo)
```

- *messageInfo* is a map that contains the delivery ID, message ID, and action type for a local or push notification for which there were interactions. The delivery and message IDs are extracted from the notification payload.

#### Java

#### Example

```java
@Override
protected void onResume() {
  super.onResume();
  handleTracking();
}

// handle notification open and click tracking
private void handleTracking() {
  Intent intent = getIntent();
  Bundle data = intent.getExtras();
  HashMap<String, Object> userInfo = null;

  if (data != null) {
    userInfo = (HashMap)data.get("NOTIFICATION_USER_INFO");
  } else {
    return;
  }

  // Check if we have notification user info.
  // If it is present, this view was opened based on a notification.
  if (userInfo != null) {
    String deliveryId = (String)userInfo.get("deliveryId");
    String broadlogId = (String)userInfo.get("broadlogId");

    HashMap<String, Object> contextData = new HashMap<>();

    if (deliveryId != null && broadlogId != null) {
      contextData.put("deliveryId", deliveryId);
      contextData.put("broadlogId", broadlogId);

      // Send Click Tracking since the user did click on the notification
      contextData.put("action", "2");
      MobileCore.collectMessageInfo(contextData);

      // Send Open Tracking since the user opened the app
      contextData.put("action", "1");
      MobileCore.collectMessageInfo(contextData);
    }
  }
}
```

{% endtab %}

{% tab title="iOS" %}

#### Syntax

```objectivec
+ (void) collectMessageInfo: (nonnull NSDictionary*) messageInfo;
```

- *messageInfo* is a dictionary that contains the delivery ID, message ID, and action type for a local or push notification for which there were interactions. The delivery and message IDs are extracted from the notification payload.

#### Objective-C

#### Example

```objectivec
// Handle notification interaction from background or closed
-(void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler{
    dispatch_async(dispatch_get_main_queue(), ^{
    	NSDictionary *userInfo = response.notification.request.content.userInfo;
    	NSString *broadlogId = userInfo[@"_mId"] ?: userInfo[@"broadlogId"];
    	NSString *deliveryId = userInfo[@"_dId"] ?: userInfo[@"deliveryId"];
          
    	if(!broadlogId.length || !deliveryId.length){
      	return;
      }
       // Send Click Tracking since the user did click on the notification
       [ACPCore collectMessageInfo:@{
                                      @"broadlogId" : broadlogId,
                                      @"deliveryId": deliveryId,
                                      @"action": @"2"
                                      }];
       // Send Open Tracking since the user opened the app
       [ACPCore collectMessageInfo:@{
                                      @"broadlogId" : broadlogId,
                                      @"deliveryId": deliveryId,
                                      @"action": @"1"
                                      }];
    });
}
```

#### Swift

#### Example

```swift
// Handle notification interaction from background or closed
func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
       DispatchQueue.main.async(execute: {
       		let userInfo = response.notification.request.content.userInfo
       		var broadlogId:String = (userInfo["_mId"] ?? userInfo["broadlogId"]) as! String
       		var deliveryId:String = (userInfo["_dId"] ?? userInfo["deliveryId"]) as! String

       		if (broadlogId.count == 0 || deliveryId.count == 0) {
          	return
          }
          // Send Click Tracking since the user did click on the notification
					ACPCore.collectMessageInfo([
            "broadlogId": broadlogId,
						"deliveryId": deliveryId,
						"action": "2"
					])
					// Send Open Tracking since the user opened the app
					ACPCore.collectMessageInfo([
            "broadlogId": broadlogId,
						"deliveryId": deliveryId,
						"action": "1"
					])
       })
}
```

{% endtab %}
{% endtabs %}

### Deleting mobile properties in Experience Platform Launch

{% hint style="danger" %}
Deleting your property in Experience Platform Launch might cause disruption to your recurring push and in-app messaging activities.
{% endhint %}

In Experience Platform Launch, if you delete your mobile property, review your mobile property status in the Campaign Standard extension and ensure that the property displays an updated **Deleted in Launch** status. For more information about deleting a property, see [Delete a Property](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#delete-a-property).

To remove the corresponding mobile app in Campaign Standard, click **Remove from ACS**. For more information, see [Deleting your Adobe Launch mobile application](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html#DeletingyourAdobeExperiencePlatformLaunchapplication).

{% hint style="warning" %}
Deleting your mobile property in Experience Platform Launch does not automatically delete your Campaign Standard mobile app.
{% endhint %}

### Handling clickthrough destinations included in Campaign In-App messages

A destination URL can be added to in-app messages that are delivered from Adobe Campaign. The destination can be a website URL such as https://www.adobe.com or a deep link such as `campaigndemoapp://signupactivity?paidaccount=true`, which can be used to direct the user to a specific area of your app.

{% tabs %}
{% tab title="Android" %}

#### Handling in-app message website URLs on Android

Website URL's are handled without any additional action by the app developer. If an in-app message is clicked through and contains a valid URL, the device's default web browser will redirect to the URL contained in the in-app notification payload. The location of the URL differs for each notification type:

- `url` key present in the alert message payload
- `url` present in the query parameters of a fullscreen message button (`data-destination-url`)
- `adb_deeplink` key present in the local notification payload
- `uri` key present in the push notification payload

#### Handling in-app message deep links on Android

To handle deep links in the notification payload, you need to set up URL schemes in the app. For more information about setting URL schemes for Android, see [Create Deep Links to App Content](https://developer.android.com/training/app-links/deep-linking). Once the desired activity is started by the newly added intent filter, the data present in the deep link can be retrieved. Any further actions based on the data present in the deep link can then be made.

#### Java

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);

    Intent intent = getIntent();
    String action = intent.getAction();
    Uri data = intent.getData();
  	// parse any data present in the deep link
}
```

#### Handling in-app message app links on Android

Android app links were introduced with Android OS 6.0. They are similar to deep links in functionality although they have the appearance of a standard website URL. The intent filter setup for deep links is modified to handle ` http` schemes and verification of the app link needs to be setup on [Google Search Console](https://support.google.com/webmasters/answer/9008080). For more information on the additional verification setup needed, see [Verify Android App Links](https://developer.android.com/training/app-links/verify-site-associations.html). The resulting app link can be used to redirect to specific areas of your app if your app is installed or redirect to your app's website if it is not installed. For more information on Android app links, see [Handling Android App Links](https://developer.android.com/training/app-links/index.html#add-app-links).

{% endtab %}

{% tab title="iOS" %}

#### Handling in-app message universal links on iOS



#### Handling alert or fullscreen notification website URLs on iOS

Website URL's included in alert or fullscreen messages are handled without any additional action by the app developer. If an alert of fullscreen message is clicked through and contains a valid URL, the Safari browser will be used to load the URL contained in the notification payload. The location of the URL differs for each notification type:

- `url` key present in the alert message payload
- `url` present in the query parameters of a fullscreen message button (`data-destination-url`)
- `adb_deeplink` key present in the local notification payload
- `uri` key present in the push notification payload

#### Handling alert or fullscreen notfication deep links on iOS

When a deep link is opened in Safari, this does not allow the app to directly handle the link. To provide a better customer experience, the Experience Platform SDK provides a URL handler that you can use with alert or fullscreen notification deep links.

#### Objective-C

```objective-c
[ACPCore registerURLHandler:^BOOL(NSString * _Nullable url) {
	NSLog(@"Inside registerURLHandler callback, clickthrough url is: %@", url);
  if([url containsString:@"campaigndemoapp://"]){
    // handle the deep link (parse any data present in the deep link and/or redirect to a desired area within the app)
    return true;
  }
  // false is returned when the URL should be opened in Safari
  return false;
}];
```

#### Swift

```swift
ACPCore.registerURLHandler({ url in
	print("Inside registerURLHandler callback, clickthrough url is: \(url ?? "")")
	if url?.contains("campaigndemoapp://") ?? false {
        // handle the deep link (parse any data present in the deep link and/or redirect to a desired area within the app)
   	return true
  }
  // false is returned when the URL should be opened in Safari
  return false
})
```

#### Handling local or push notification website URLs on iOS

The website URL in the response can be loaded using the [openURL:options:completionHandler:](https://developer.apple.com/documentation/uikit/uiapplication/1648685-openurl?language=objc) instance method. 

#### Objective-C

```objective-c
-(void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler{
    dispatch_async(dispatch_get_main_queue(), ^{
      NSDictionary *userInfo = response.notification.request.content.userInfo;
      NSString *urlString = userInfo[@"adb_deeplink"];
      if(urlString.length){
      	[[UIApplication sharedApplication] openURL:[NSURL URLWithString: urlString] options:@{} completionHandler:^(BOOL success) {
        	NSLog(@"Open %@: %d",urlString,success);
        }];
			}
    	completionHandler();
		});   
}
```

#### Swift

```swift
func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
    DispatchQueue.main.async(execute: {
        let userInfo = response.notification.request.content.userInfo
        let urlString = userInfo["adb_deeplink"] as? String
        if (urlString?.count ?? 0) != 0 {
            if let url = URL(string: urlString ?? "") {
                UIApplication.shared.open(url, options: [:], completionHandler: { success in
                    print("Open \(urlString ?? ""): \(success)")
                })
            }
        }
        completionHandler()
    })
}
```

#### Handling local or push notification deep links on iOS

When a local or push notification is clicked through, the `didReceiveNotificationResponse` instance method is called with the notification response being passed in as a parameter. For more information, see the Apple developer docs at [userNotificationCenter:didReceiveNotificationResponse:withCompletionHandler:](https://developer.apple.com/documentation/usernotifications/unusernotificationcenterdelegate/1649501-usernotificationcenter?language=objc).

The deep link URL can be retrieved from the response object passed into the handler method. An example for retrieving the deep link URL and loading web links is provided below. For more information about handling deep links and setting URL schemes for iOS, see [Defining a Custom URL Scheme for Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app?language=objc).

{% endtab %}
{% endtabs %}